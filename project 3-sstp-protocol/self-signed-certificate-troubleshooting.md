
# 🔴 Troubleshooting: SSTP VPN Certificate Not Trusted

[ Back to Overview] → [README.md](./README.md)

---

## 📋 Problem Summary

The SSTP VPN connection fails because the Windows client does not trust the server's self-signed certificate.

---

## 💡 Why Does This Happen?

SSTP runs inside an HTTPS (TLS) connection, so the client checks the server's certificate before it builds the tunnel. A self-signed certificate is signed by the server itself, so Windows does not trust it automatically. The client trusts the certificate only if both of these are true:

- The certificate is in the client's **Trusted Root Certification Authorities** store
- The certificate is **valid for the server name** used in the VPN connection (the DNS name in its subject or Subject Alternative Name), and it has not expired

| Setting | Value |
|---------|-------|
| **VPN type** | SSTP, TCP 443 |
| **VPN server name** | `server2021.seemaenterprise.co.in` |
| **Certificate** | Self-signed, friendly name `SSTP`, file `SSTP-Self-Signed.cer` |
| **Required store on the client** | Local Machine → Trusted Root Certification Authorities |

---

## 🔎 Verify the Problem

| Check | What to look for | Meaning |
|-------|------------------|---------|
| **Error message** | A certificate error when you connect, such as **0x800B0109** | The client does not trust the certificate's issuer. The fix is to import the certificate |
| **Other certificate errors** | **0x800B010F**: the name does not match. **0x800B0101**: the certificate has expired | The certificate must be recreated with the right name or dates. Importing it will not help |
| **Certificate store** | Run `certlm.msc` on the client and open **Trusted Root Certification Authorities → Certificates** | The `SSTP` certificate is **not** listed |
| **Name resolution and port** | `nslookup server2021.seemaenterprise.co.in` and `Test-NetConnection server2021.seemaenterprise.co.in -Port 443` | The name resolves and TCP 443 is reachable. This shows the fault is the certificate and not the network |

> Read the exact error code first. Importing the certificate fixes only an untrusted issuer. It does not fix a name mismatch or an expired certificate.

---

## 🔧 Fix - Import the Certificate on the VPN Client

### Step 1 - Get the Public Certificate

1. On the VPN server, export the **public** certificate as a `.cer` file (without the private key).
2. Copy the `.cer` file to the Windows client in a secure way.

> **Important:** Export only the public certificate. Never share the private key.

### Step 2 - Check the Certificate Before You Trust It

Trusting a root certificate gives it a lot of trust, so check that it is really your server's.

1. Double-click the `.cer` file and open the **Details** tab.
2. Note the **Thumbprint**, the **Subject**, and the **Valid to** date.
3. Compare the thumbprint with the one on the server. They must match.

### Step 3 - Install the Certificate

1. Click **Install Certificate...**
2. Select **Local Machine** and click **Next**. Approve the User Account Control prompt.
3. Select **Place all certificates in the following store**.
4. Click **Browse**, select **Trusted Root Certification Authorities**, and click **OK**.
5. Click **Next**, then **Finish**. A message confirms that the import was successful.

> **Use Local Machine, not Current User.** The Windows built-in VPN checks the server certificate in the machine store. A certificate imported for the current user only may not be used, and the same error comes back. Installing into Local Machine needs administrator rights.

### Step 4 - Test the VPN Connection

1. Disconnect any earlier VPN attempt.
2. Open **Settings → Network & internet → VPN**.
3. Select `SSTP_VPN_LAB` and click **Connect**.
4. Enter the VPN user's credentials if asked.

---

## ✅ Verification

| Check | Where | Expected Result |
|-------|-------|-----------------|
| Certificate trusted | `certlm.msc` → Trusted Root Certification Authorities → Certificates | The `SSTP` certificate is listed ✅ |
| Same certificate | Details tab | The thumbprint matches the server's certificate ✅ |
| VPN connects | Settings → Network & internet → VPN | `SSTP_VPN_LAB` shows **Connected** ✅ |
| Address from the pool | `ipconfig /all` | The VPN adapter has a `10.10.10.x` address ✅ |

With PowerShell, as an administrator:

```text
PS C:\> Get-ChildItem Cert:\LocalMachine\Root | Where-Object Subject -like "*server2021*" | Format-List Subject, Thumbprint, NotAfter
```

---

## 🛠️ If the Error Continues

| Symptom | Likely cause | What to check |
|---------|--------------|---------------|
| **0x800B0109 again** | The certificate went into the wrong store, such as Current User or Personal | Import it again into **Local Machine → Trusted Root Certification Authorities** |
| **0x800B010F** | The server name in the VPN profile is not in the certificate | The profile name must match the certificate's DNS name (SAN). Create a new certificate with the right name |
| **0x800B0101** | The certificate has expired | Check the **Valid to** date and create a new certificate |
| **Certificate revocation error (0x80092013)** | The client cannot check the certificate's revocation list | Check whether the certificate has a revocation list address, and use one that does not, for a lab |
| **Connection times out** | TCP 443 blocked, RRAS not running, or the server name does not resolve | Azure NSG rule, Windows Firewall, RRAS status, and `Test-NetConnection -Port 443` |

---

## 🔒 Security Notes

- Trust only certificates whose identity and origin you have checked, by comparing the thumbprint.
- A certificate in **Trusted Root Certification Authorities** gets a lot of trust, so do not import certificates you do not recognise.
- **Current User** affects only one user's store, and **Local Machine** affects the whole computer. The VPN client needs the machine-wide trust.
- For production VPNs, use a certificate from a trusted Certificate Authority (CA), so clients need no manual import.

---

## 📋 Issue Summary

| | Detail |
|---|--------|
| **Issue** | The SSTP VPN connection fails with a certificate error |
| **Cause** | The client does not trust the server's self-signed certificate |
| **Symptom** | A certificate error when connecting, and the certificate is missing from the client's Trusted Root store |
| **Diagnose** | Read the error code, check `certlm.msc`, and confirm that the name resolves and TCP 443 is reachable |
| **Fix** | Imported the public certificate into **Local Machine → Trusted Root Certification Authorities** |
| **Verified** | The certificate is listed, and `SSTP_VPN_LAB` connects with an address from the pool |

---

## 🔑 Key Learning

A successful SSTP connection needs more than an imported certificate. Certificate trust, name match, validity dates, RRAS configuration and network connectivity must all be correct.

---

## 🖼️ Screenshots

**Screenshot: certificate import on the client:**

<img width="2268" height="4032" alt="Certificate Import Wizard on the Windows 11 client with Trusted Root Certification Authorities selected" src="https://github.com/user-attachments/assets/1ff3afcb-f37e-4692-b397-e59cc02a9647" />

**Screenshot: VPN connection result:**

<img width="1398" height="1841" alt="Windows VPN settings showing the SSTP VPN connection after the certificate was imported" src="https://github.com/user-attachments/assets/83253516-df88-4c89-83f0-df90be75b3fc" />

---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)






































OLD--------------------------------


# Troubleshooting: SSTP VPN Certificate Not Trusted

## Problem Summary

The SSTP VPN connection fails because the Windows client does not trust the server's self-signed certificate.

**Cause:** A self-signed certificate is not automatically trusted by Windows. The client must trust the certificate, and the certificate must be valid for the VPN server's hostname.

## Resolution: Import the Certificate on the VPN Client

### Step 1: Transfer the Certificate

1. Export the public certificate from the VPN server as a `.cer` file.
2. Transfer the `.cer` file securely to the Windows client machine.

**Note:** Export only the public certificate. Never share the certificate's private key.

### Step 2: Open the Certificate

1. On the Windows client, locate the `.cer` file.
2. Double-click the certificate file.
3. Click **Install Certificate...**.

### Step 3: Select the Certificate Store

1. Select **Choose Local Machine **.
2. Click **Next**.

This installs the certificate for the current Windows user and usually avoids requiring administrator privileges.

### Step 4: Choose the Trusted Root Store

1. Select **Place all certificates in the following store**.
2. Click **Browse**.
3. Select **Trusted Root Certification Authorities**.
4. Click **OK**, then **Next**.

### Step 5: Complete the Import

1. Review the selected certificate store.
2. Click **Finish**.
3. Review the Windows security warning carefully.
4. Confirm the import only if you have verified that the certificate belongs to your lab's VPN server.

### Step 6: Test the VPN Connection

1. Close the certificate wizard.
2. Disconnect any existing VPN attempt.
3. Open **Settings → Network & internet → VPN**.
4. Select the SSTP VPN profile and click **Connect**.
5. Check whether the connection succeeds.

## Expected Result

The client trusts the imported certificate, provided the certificate is valid and matches the VPN server's hostname. The SSTP VPN connection should then proceed if the other VPN settings are correct.


## Security Notes

* Trust only certificates whose identity and origin you have verified.
* Importing a certificate into **Trusted Root Certification Authorities** grants it significant trust.
* **Current User** affects only the current user's certificate store. For all users or machine-wide trust, the **Local Machine** store may be required and typically needs administrator privileges.
* For production VPN deployments, prefer a certificate issued by a trusted Certificate Authority (CA).

## Key Learning

A successful SSTP connection requires more than importing a certificate. Certificate trust, hostname matching, certificate validity, RRAS configuration, and network connectivity must all be correct.




































































































<img width="2268" height="4032" alt="IMG_0548" src="https://github.com/user-attachments/assets/1ff3afcb-f37e-4692-b397-e59cc02a9647" />



































<img width="1398" height="1841" alt="c76e7bc2-a407-4b01-95bc-8d4baa9e68dc" src="https://github.com/user-attachments/assets/83253516-df88-4c89-83f0-df90be75b3fc" />















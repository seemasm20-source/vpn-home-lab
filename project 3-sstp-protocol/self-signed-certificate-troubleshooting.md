
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















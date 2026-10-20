# SSTP VPN Configuration on Windows Server & Windows 11 Using a Self-Signed Certificate

## Objective

Configure a Secure Socket Tunneling Protocol (SSTP) VPN between an Azure-hosted Windows Server and a Windows 11 client using a self-signed certificate.

## Lab Environment

* **Cloud Platform:** Microsoft Azure
* **VPN Server:** Windows Server 2025 (`server2021`)
* **VPN Client:** Windows 11
* **Domain:** `seemaenterprise.co.in`
* **VPN Protocol:** SSTP
* **VPN Port:** TCP 443
* **Certificate:** Self-signed certificate
* **VPN Address Pool:** `10.10.10.1 – 10.10.10.10`

## Step 1: Create the Windows Server in Azure

1. Sign in to the Azure portal.
2. Create a Windows Server VM or use the existing server from the Windows Server portfolio.
3. Verify that the server is accessible through Remote Desktop Protocol (RDP).
4. Confirm the server hostname and domain configuration.

**Existing lab server:** `server2021`

> Reuse the existing Windows Server VM rather than creating another one, provided it meets the lab requirements.

## Step 2: Install the Remote Access Role

1. Open **Server Manager**.
2. Select **Manage → Add Roles and Features**.
3. Select **Remote Access** as the server role.
4. Under Role Services, select **DirectAccess and VPN (RAS)**.
5. Add the required features and complete the installation.
6. After installation, select **Open the Getting Started Wizard**.
7. Choose **Deploy VPN only**.
8. The **Routing and Remote Access** console opens. Minimise it temporarily.

## Step 3: Create and Export a Self-Signed Certificate

### A. Create the certificate

1. Open **Server Manager → Tools → Internet Information Services (IIS) Manager**.
2. Select the server name in the left panel.
3. Open **Server Certificates**.
4. Select **Create Self-Signed Certificate**.
5. Enter the friendly name `SSTP`.
6. Select the Personal certificate store and click **OK**.

### B. Export the certificate

1. In IIS Manager, open **Server Certificates**.
2. Select the `SSTP` certificate and open its details.
3. Select **Details → Copy to File** to launch the Certificate Export Wizard.
4. Click **Next**.
5. Select **No, do not export the private key**.
6. Select the appropriate certificate export format, such as DER encoded binary X.509 (`.CER`) or Base-64 encoded X.509 (`.CER`).
7. Browse to the `C:\` drive and enter the filename `SSTP-Self-Signed.cer`.
8. Complete the wizard and verify the message confirming that the export was successful.
9. Open File Explorer and confirm that the certificate file exists.

**Important:** Export only the public certificate to the client. Never distribute the server's private key.

## Step 4: Configure Routing and Remote Access (RRAS)

### A. Enable VPN access

1. Return to the **Routing and Remote Access** console.
2. Right-click `server2021` and select **Configure and Enable Routing and Remote Access**.
3. Click **Next**.
4. Select **Custom configuration**.
5. Click **Next** and select **VPN access**.
6. Complete the wizard and start the Routing and Remote Access service when prompted.

### B. Configure SSTP certificate binding

1. Right-click `server2021` and select **Properties**.
2. Open the **Security** tab.
3. Locate the SSL certificate binding settings.
4. Select the `SSTP` certificate from the certificate drop-down list.
5. View the certificate details and verify that the intended certificate is selected.
6. Click **OK** to apply the configuration.

### C. Configure the IPv4 address pool

1. Open the server properties and select the **IPv4** tab.

2. Select **Static address pool**.

3. Click **Add**.

4. Enter the following address range:

   * **Start IP:** `10.10.10.1`
   * **End IP:** `10.10.10.10`

5. Click **OK**, then **Apply**.

6. Restart the RRAS service if required.

> Ensure the VPN address pool does not overlap with existing Azure VNet, subnet, client or server address ranges. Adjust the pool if necessary.

### D. Configure network access

1. Verify that TCP port `443` is allowed in the Azure Network Security Group (NSG).
2. Check the Windows Defender Firewall configuration on the server.
3. Confirm that the VPN server is reachable using the intended DNS name.

## Step 5: Create a VPN User in Active Directory

1. Open **Server Manager → Tools → Active Directory Users and Computers**.
2. Navigate to the appropriate organizational unit.
3. Right-click the OU and select **New → User**. SAM
4. Enter the user's details and create the account.
5. Open the new user's **Properties**.
6. Select the **Dial-in** tab.
7. Under Network Access Permission, select **Allow access**, if this is the permission model used in your lab.
8. Click **Apply → OK**.

Verify that the account is enabled and that the applicable RRAS/NPS network policies permit the connection.

## Step 6: Configure the Windows 11 VPN Client

### A. Create the VPN connection

1. Open **Settings → Network & internet → VPN**.

2. Select **Add VPN**.

3. Configure the connection as follows:

   * **VPN provider:** Windows (built-in)
   * **Connection name:** `SSTP_VPN_LAB`
   * **Server name or address:** `server2021.seemaenterprise.co.in`
   * **VPN type:** Secure Socket Tunneling Protocol (SSTP)
   * **Type of sign-in info:** Username and password

4. Save the VPN connection.

### B. Import the self-signed certificate

1. Transfer `SSTP-Self-Signed.cer` securely from the server to the Windows 11 client.
2. Double-click the certificate file.
3. Select **Install Certificate**.
4. Choose **Local Machine** and click **Next**.
5. Approve the User Account Control prompt if requested.
6. Select **Place all certificates in the following store**.
7. Click **Browse** and select **Trusted Root Certification Authorities**.
8. Click **OK → Next → Finish**.
9. Verify the message confirming that the import was successful.

### C. Connect to the VPN

1. Open **Settings → Network & internet → VPN**.
2. Select the `SSTP VPN LAB` connection.
3. Click **Connect**.
4. Enter the authorised Active Directory username and password when prompted.
5. Wait for the connection status to indicate **Connected**.

**Certificate requirement:** The certificate must be valid for server authentication, and its DNS name must match `server2021.seemaenterprise.co.in`. If the self-signed certificate created through IIS does not contain the required DNS name in its Subject Alternative Name (SAN), create a suitable certificate before testing the connection.

## Step 7: Verify the SSTP VPN Connection

### A. Verify on the Windows 11 client

1. Press `Win + R`.
2. Enter `ncpa.cpl` and press Enter.
3. Locate the newly created VPN connection, such as `SSTP VPN`.
4. Right-click the connection and select **Status**, if available.
5. Open **Details** to inspect the assigned network information.

### B. Verify on the Windows Server

1. Open the **Routing and Remote Access** console.
2. Expand the server node.
3. Select **Remote Access Clients**.
4. Locate the connected VPN user.
5. Right-click the user and select **Status**.
6. Review the connection details, including the assigned VPN client IP address.

### C. Verify the assigned IP address

Confirm that the client has received an address from the configured VPN address pool.

For example, if the client receives `10.10.10.2`, the server's Remote Access Clients view should show `10.10.10.2` as the address assigned to that VPN client.

The client and server views should agree on the assigned VPN address. The client does not necessarily have to use `10.10.10.2`; the address depends on allocation and availability.

### D. Test connectivity

After connecting, run the following command on the client:

```cmd
ipconfig
```

Verify that the VPN adapter has an address from the VPN pool.

If permitted by the network configuration, test connectivity to an authorised internal resource. A successful VPN connection alone does not guarantee that all internal resources are reachable.

## Troubleshooting Checklist

| Issue                                      | What to check                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------ |
| Certificate error                          | Certificate trust, expiry, private key on server, and DNS name/SAN match |
| VPN connection fails                       | RRAS status, TCP 443, Azure NSG and Windows Firewall                     |
| Authentication fails                       | Account status, credentials and RRAS/NPS policies                        |
| No VPN IP address                          | RRAS IPv4 pool configuration and available addresses                     |
| VPN connects but resources are unreachable | Routing, DNS, internal firewall and access permissions                   |

## Security Considerations

* Use a CA-issued certificate for production VPN deployments.
* Never export or distribute the server's private key to the client.
* Restrict access to TCP port 443 to the required sources where appropriate.
* Use authorised accounts and appropriate remote-access policies.
* Do not publish passwords, private keys or sensitive server details in GitHub.





<img width="1920" height="1080" alt="Screenshot (686)" src="https://github.com/user-attachments/assets/e3fb2d28-4936-4259-b7e3-1abf7739291b" />














<img width="1920" height="1080" alt="Screenshot (687)" src="https://github.com/user-attachments/assets/dbe29b1a-2938-4459-9dde-9f295d69a5fd" />







<img width="1920" height="1080" alt="Screenshot (688)" src="https://github.com/user-attachments/assets/07956fb7-324f-4943-b584-f2a7b3629207" />







<img width="1920" height="1080" alt="Screenshot (689)" src="https://github.com/user-attachments/assets/a846ffe4-1709-467c-81dd-d9f2b2f0d4db" />








<img width="1920" height="1080" alt="Screenshot (690)" src="https://github.com/user-attachments/assets/fc452a01-0eeb-4a5d-bcc0-584c18600be6" />











<img width="1920" height="1080" alt="Screenshot (691)" src="https://github.com/user-attachments/assets/1a492035-e2c1-434d-b08e-efad036bc12d" />













<img width="1920" height="1080" alt="Screenshot (692)" src="https://github.com/user-attachments/assets/12bd4449-2585-4179-a382-c9f82280b82b" />










<img width="1920" height="1080" alt="Screenshot (693)" src="https://github.com/user-attachments/assets/b110a11b-93bf-4d3f-baf8-47c31ac62d66" />











<img width="1920" height="1080" alt="Screenshot (694)" src="https://github.com/user-attachments/assets/c04db460-eb5f-496f-9b3f-3044d1489af4" />













<img width="1920" height="1080" alt="Screenshot (695)" src="https://github.com/user-attachments/assets/eb17c5c7-799c-4906-8638-d19d982836aa" />















<img width="1920" height="1080" alt="Screenshot (696)" src="https://github.com/user-attachments/assets/4e653ce3-efd7-4489-bcef-99a9fcd5f711" />














<img width="1920" height="1080" alt="Screenshot (697)" src="https://github.com/user-attachments/assets/cf6655ad-10ea-4928-85ee-0f8f379ece4b" />
















<img width="1920" height="1080" alt="Screenshot (698)" src="https://github.com/user-attachments/assets/0c1098c2-b7c9-48ae-815f-bceab7ad8429" />



















<img width="1920" height="1080" alt="Screenshot (699)" src="https://github.com/user-attachments/assets/d4c4cefc-a100-456c-abc1-5ae4928fc333" />






















<img width="1920" height="1080" alt="Screenshot (700)" src="https://github.com/user-attachments/assets/a3ed2562-0ab0-4cd3-b367-93f373ccaad3" />
















<img width="1920" height="1080" alt="Screenshot (701)" src="https://github.com/user-attachments/assets/cd4aa4af-576e-45b6-ae52-60ba9ca99594" />
















<img width="1920" height="1080" alt="Screenshot (702)" src="https://github.com/user-attachments/assets/77363231-400e-4de0-a0be-86aee82ade88" />



















<img width="1920" height="1080" alt="Screenshot (703)" src="https://github.com/user-attachments/assets/705a56e4-398b-411b-a68c-f6b3360e8098" />
















<img width="1920" height="1080" alt="Screenshot (704)" src="https://github.com/user-attachments/assets/9196de11-39ae-4754-8219-e7457c565fc1" />















<img width="1920" height="1080" alt="Screenshot (705)" src="https://github.com/user-attachments/assets/42efd701-625d-46fe-b8ca-5fdd4666e610" />















<img width="1920" height="1080" alt="Screenshot (706)" src="https://github.com/user-attachments/assets/e654d083-b585-41f2-bf4c-29aec9909ecb" />


























<img width="1920" height="1080" alt="Screenshot (707)" src="https://github.com/user-attachments/assets/762202f5-fd1e-465d-8155-8b67ede8984e" />
















<img width="1920" height="1080" alt="Screenshot (708)" src="https://github.com/user-attachments/assets/613c13a6-2c81-4e39-a010-7b346d640bef" />














<img width="2268" height="2347" alt="IMG_0549" src="https://github.com/user-attachments/assets/ec825fce-d027-401f-b51c-34e72f01b608" />
















































<img width="2268" height="2835" alt="IMG_0552" src="https://github.com/user-attachments/assets/ecf43bd6-b15d-4104-8109-3435672809a4" />






































<img width="2160" height="2766" alt="51406656-ADA4-4696-AA39-2E4AD6D07944" src="https://github.com/user-attachments/assets/c19582f7-5e55-469c-ad61-780599db00b9" />









































<img width="2160" height="2421" alt="05A95E82-70B5-4047-997B-A4B94D5477C6" src="https://github.com/user-attachments/assets/f55605d3-a8dc-4ce4-9011-bdbb41918bd0" />

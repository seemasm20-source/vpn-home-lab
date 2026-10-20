# Troubleshooting: RDP Disconnects Immediately After SSTP VPN Connection

## Problem Summary

**Symptom:** The Remote Desktop Protocol (RDP) session freezes or disconnects immediately after the SSTP VPN status changes to **Connected**.

**Possible Cause:** The VPN connection is configured to use the remote network's default gateway. This can change the client's network routing and interrupt the existing RDP connection.

## Resolution: Enable Split Tunneling

### Step 1: Open Network Connections

1. Press `Windows + R`.
2. Type `ncpa.cpl` and press **Enter**.
3. Locate the SSTP VPN connection.

### Step 2: Open VPN Properties

1. Right-click the SSTP VPN connection.
2. Select **Properties**.
3. Open the **Networking** tab.
4. Select **Internet Protocol Version 4 (TCP/IPv4)**.
5. Click **Properties**.

### Step 3: Change Advanced TCP/IP Settings

1. Click **Advanced**.
2. Under **IP Settings**, locate **Default gateways**.
3. Uncheck **Use default gateway on remote network**.
4. Click **OK** to close each dialog box and save the changes.

### Step 4: Reconnect and Test

1. Disconnect the SSTP VPN.
2. Reconnect to the VPN.
3. Check whether the RDP session remains connected.
4. Verify access to the required remote resources.

## Expected Result

* The VPN connects successfully.
* The client continues using its local default gateway for general internet traffic.
* Traffic for remote networks can use the VPN when the appropriate routes exist.
* The RDP session remains connected, provided its network route is not otherwise interrupted.




<img width="1920" height="1080" alt="Screenshot (710)" src="https://github.com/user-attachments/assets/8872f909-130a-401b-afe0-977f73890999" />







<img width="2268" height="4032" alt="IMG_0552" src="https://github.com/user-attachments/assets/926547f9-e2b9-4103-ab54-29bfaadaba3e" />














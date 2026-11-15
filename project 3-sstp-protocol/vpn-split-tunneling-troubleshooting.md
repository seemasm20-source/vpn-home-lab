

# 🔴 Troubleshooting: RDP Disconnects Immediately After SSTP VPN Connection

[ Back to Overview] → [README.md](./README.md)

---

## 📋 Problem Summary

A Remote Desktop (RDP) session to the Windows 11 client freezes or disconnects as soon as the SSTP VPN status changes to **Connected**.

---

## 💡 Why Does This Happen?

By default, the Windows VPN client has **Use default gateway on remote network** turned on. When the VPN connects, Windows adds a new default route that sends **all** traffic through the VPN, which makes the VPN a **full tunnel**. The replies of the existing RDP session now leave through the VPN instead of the original path, so the RDP connection freezes or drops.

| Setting | Value |
|---------|-------|
| **VPN connection** | `SSTP_VPN_LAB` (SSTP, TCP 443) |
| **Setting involved** | Use default gateway on remote network |
| **Checked** | Full tunnel: all traffic goes through the VPN |
| **Unchecked** | Split tunnel: only traffic for the company network goes through the VPN |

> This is most likely when you are connected to the client through RDP and start the VPN **from inside that RDP session**. See [Split Tunnel vs Full Tunnel](./split-vs-full-tunnel.md).

---

## 🔎 Verify the Problem

Check the routes while the VPN is connected (from the console, or after reconnecting RDP):

```text
C:\> route print
C:\> ipconfig /all
```

| Check | What to look for | Meaning |
|-------|------------------|---------|
| **Default route** (`0.0.0.0` in `route print`) | An entry that points to the **VPN adapter**, with a lower metric than the local gateway | The VPN is a full tunnel, and all traffic goes through it |
| **VPN adapter** (`ipconfig /all`) | A `10.10.10.x` address on `PPP adapter SSTP_VPN_LAB` | The VPN is connected |

You can also read the setting itself in the next step: if **Use default gateway on remote network** is ticked, the VPN is a full tunnel.

---

## 🔧 Fix - Enable Split Tunneling

### Step 1 - Open Network Connections

1. Press **Windows + R**.
2. Type `ncpa.cpl` and press **Enter**.
3. Find the SSTP VPN connection.

### Step 2 - Open the VPN Properties

1. Right-click the SSTP VPN connection and select **Properties**.
2. Open the **Networking** tab.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.

### Step 3 - Turn Off the Default Gateway Setting

1. Click **Advanced**.
2. On the **IP Settings** tab, find **Use default gateway on remote network**.
3. **Untick** it.
4. Click **OK** in each dialog box to save.

### Step 4 - Reconnect and Test

1. Disconnect the SSTP VPN.
2. Connect the VPN again.
3. Check that the RDP session stays connected.
4. Check access to the company resources you need.


`SplitTunneling : True` means the setting is changed.



---

## ✅ Verification

| Check | Where | Expected Result |
|-------|-------|-----------------|
| Setting changed | VPN Properties → IPv4 → Advanced | **Use default gateway on remote network** is unticked ✅ |
| Default route | `route print` | The `0.0.0.0` route still points to the local gateway, not the VPN adapter ✅ |
| VPN connected | `ipconfig /all` | `SSTP_VPN_LAB` has a `10.10.10.x` address ✅ |
| RDP session | The existing Remote Desktop window | The session stays connected after the VPN connects ✅ |
| Company resources | `ping` or a connection to an internal server | The resource is reachable through the VPN ✅ |

---

## ⚠️ Security Note

Split tunneling means internet traffic is **not** sent through the company. A device on the VPN is on the local network and the company network at the same time. If company policy requires a full tunnel, do not change this setting. Use a different way to manage the machine, such as the Azure portal or a different remote path, when you connect the VPN.

---

## 📋 Issue Summary

| | Detail |
|---|--------|
| **Issue** | The RDP session freezes or disconnects when the SSTP VPN connects |
| **Cause** | **Use default gateway on remote network** was ticked, so the VPN became a full tunnel and replaced the default route |
| **Symptom** | The RDP session drops as soon as the VPN shows **Connected** |
| **Diagnose** | `route print` showed the default route through the VPN adapter, or the setting was ticked |
| **Fix** | Unticked **Use default gateway on remote network** to enable split tunneling, then reconnected the VPN |
| **Verified** | The VPN connected and the RDP session stayed connected |

---

## 🖼️ Screenshots

**Screenshot: Advanced TCP/IP Settings with the default gateway option:**

<img width="1920" height="1080" alt="Advanced TCP/IP Settings with Use default gateway on remote network unticked" src="https://github.com/user-attachments/assets/8872f909-130a-401b-afe0-977f73890999" />



<img width="2067" height="2067" alt="05A95E82-70B5-4047-997B-A4B94D5477C6" src="https://github.com/user-attachments/assets/86a47738-cb93-4d61-8b6e-b54d2ef53511" />



**Screenshot: VPN connected while the RDP session stays active:**

<img width="2268" height="4032" alt="VPN connection showing Connected while the Remote Desktop session remains open" src="https://github.com/user-attachments/assets/926547f9-e2b9-4103-ab54-29bfaadaba3e" />

---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)



















































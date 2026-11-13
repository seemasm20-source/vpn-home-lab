# 🔎 VPN Diagnostic - ipconfig

[ Back to Overview] → [README.md](./README.md)

---

## 📋 Summary

`ipconfig /all` is the first command to run after a VPN connects or fails to connect. It shows the state of the VPN adapter, the address it received and the DNS servers it uses. The output shows **what state the connection is in**. It does not show **why** it ended up there, so use it together with the other checks in this portfolio.

---

## 💡 What to Check

```text
C:\> ipconfig /all
```

| Check | What to look for | What it tells you |
|:-----:|------------------|-------------------|
| 1 | **Is the VPN adapter present?** | The VPN is connected and the adapter is active |
| 2 | **Does it have a company IP address?** | The VPN server assigned an address from its pool |
| 3 | **Is DNS pointing to the company server?** | Internal names can resolve through the VPN |

---

## 🔎 Example Output

The names and addresses below are examples from the SSTP lab. The adapter heading is `PPP adapter <connection name>` for the Windows built-in VPN.

```text
PPP adapter SSTP_VPN_LAB:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : SSTP_VPN_LAB
   DHCP Enabled. . . . . . . . . . . : No
   IPv4 Address. . . . . . . . . . . : 10.10.10.2(Preferred)    ← company VPN address
   Subnet Mask . . . . . . . . . . . : 255.255.255.255
   Default Gateway . . . . . . . . . :
   DNS Servers . . . . . . . . . . . : 172.16.0.4               ← company DNS
```

**Screenshot: `ipconfig /all` with the VPN connected:**

<img width="2160" height="2661" alt="ipconfig /all showing the VPN adapter with an address from the VPN pool and the company DNS server" src="https://github.com/user-attachments/assets/8c7a3fb0-ca1d-4938-86ba-df01395351a2" />

---

## 🛠️ Reading the Result

| What you see | Meaning | Next check |
|--------------|---------|------------|
| **No VPN adapter in the output** | The VPN is not connected, or the adapter is missing | Connect the VPN. If it still fails, see the connection phases in [VPN Connection Process](./vpn-connection-process.md) |
| **Adapter shows "Media disconnected"** | The connection dropped | Reconnect, and check the internet connection |
| **Adapter has no IP address, or `169.254.x.x`** | The VPN server did not give an address | Check the server's address pool |
| **Adapter has an IP address from the VPN pool** | The tunnel is up and the address was assigned | Test an internal server by IP |
| **IP address is correct, but the DNS servers are public or missing** | Internal names will not resolve | Check the VPN's DNS settings, then `nslookup` an internal name |
| **No default gateway on the VPN adapter** | Often normal for a **split tunnel** | Check `route print` to see which networks use the VPN |

> The default gateway line can be empty on a working VPN adapter. The routes in `route print` decide where the traffic goes.

---

## ✅ Next Commands

| Command | Why |
|---------|-----|
| `route print` | Shows which networks go through the VPN adapter |
| `nslookup <internal name>` | Tests whether internal names resolve |
| `ping <internal server IP>` | Tests the connection by IP |
| `Test-NetConnection <server> -Port <port>` | Tests whether a specific TCP port is reachable |

---



## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)

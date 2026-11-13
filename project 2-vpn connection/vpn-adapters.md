# 🔌 What is a VPN Adapter?

A **VPN adapter** is a **virtual network interface** that the VPN software creates or activates when a VPN connection is established. It works like a virtual network card, so the computer can send and receive traffic through the VPN tunnel.

```text
Physical network adapter → connects to the home or office network
VPN adapter              → connects to the company network through the VPN tunnel

Both are active at the same time while the VPN is connected.
```

---

## ⚙️ What the VPN Adapter Does

| Function | Meaning |
|----------|---------|
| **Receives an IP address** | The VPN server gives the adapter an address from the company's VPN range |
| **Provides DNS servers** | The adapter often brings the company DNS servers, so internal names resolve |
| **Carries the routes** | Traffic for the company network is sent to this adapter |
| **Sends encrypted traffic** | Data leaves the PC through the tunnel |

---

## 🔎 Finding the VPN Adapter

### With `ipconfig /all`

```text
C:\> ipconfig /all
```

Example output (the names and addresses are examples):

```text
Wireless LAN adapter Wi-Fi:
   IPv4 Address. . . . . . . . . . . : 192.168.1.50      ← home network IP

PPP adapter Company VPN:
   Description . . . . . . . . . . . : Company VPN
   IPv4 Address. . . . . . . . . . . : 10.8.0.45         ← IP given by the VPN server
   DNS Servers . . . . . . . . . . . : 10.0.0.10         ← company DNS
```

The adapter heading depends on the VPN client:

| VPN client | How the adapter appears |
|------------|-------------------------|
| **Windows built-in VPN** | `PPP adapter <connection name>` |
| **Cisco Secure Client** | An Ethernet adapter whose description names the Cisco virtual adapter |
| **OpenVPN** | An Ethernet adapter named like `OpenVPN TAP-Windows` or `OpenVPN Data Channel Offload` |
| **WireGuard** | An adapter named after the tunnel, often listed as `Unknown adapter` |

> The adapter appears in `ipconfig` only while the VPN is **connected**. If you cannot find it, the VPN is not connected or the adapter is disabled.

### With Network Connections

Press **Win + R**, type `ncpa.cpl` and press **Enter**. The VPN adapter is listed next to the physical adapters, with its status (**Enabled**, **Disabled** or **Network cable unplugged**).



---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)



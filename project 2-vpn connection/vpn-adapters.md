

## 🔌 What is a VPN Adapter?

A VPN adapter is a **virtual network interface** created or activated by VPN software when a VPN connection is established.

It works like a virtual network card that allows the computer to send and receive traffic through the VPN tunnel.

```text
Physical Network Adapter → Connects to the home/office network
VPN Adapter               → Connects to the company network through the VPN tunnel

Both can exist simultaneously when the VPN is connected.
```

## 🔎 Finding the VPN Adapter

Run:

```cmd
ipconfig /all
```

Example:

```text
Wireless LAN adapter Wi-Fi:
   IPv4 Address: 192.168.1.50    ← Home network IP

VPN Adapter:
   IPv4 Address: 10.8.0.45       ← Example VPN-assigned IP
   DNS Servers: 10.0.0.10        ← Example company DNS
```

> **Note:** The adapter name and IP addresses depend on the VPN client and company configuration. Examples may appear as Cisco Secure Client, WireGuard, OpenVPN, or Windows VPN adapters.

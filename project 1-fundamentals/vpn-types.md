
# 🔀 VPN Types

VPNs are grouped by what they connect, and by whether the user needs software. Knowing the type tells a technician where to look when a connection fails.

---

## 1. Remote Access VPN

A **remote access VPN** creates a temporary, secure and encrypted tunnel between one remote device, such as a laptop, desktop or phone, and a private company network, across an untrusted network like the internet.

```text
Home laptop
    │
 Internet
    │
VPN tunnel
    │
Company office (LAN)
```

| | Detail |
|---|--------|
| **Used by** | Remote workers and travelling employees |
| **Client software** | Required on each device |
| **Connects** | One device to a network |
| **Azure name** | Point-to-Site (P2S) VPN |

---

## 2. Site-to-Site VPN

A **site-to-site (S2S) VPN** connects two entire networks across the internet, so they work like one private network. Users do not install anything, because the tunnel is built between network devices.

```text
┌──────────────────┐                          ┌──────────────────┐
│ Branch office    │ ◄══ Encrypted tunnel ══► │ Head office      │
│ 192.168.1.0/24   │       over the internet  │ 10.0.0.0/24      │
└──────────────────┘                          └──────────────────┘
```

| | Detail |
|---|--------|
| **Used by** | Branch offices, head offices, an office connected to a cloud network such as an Azure virtual network |
| **Client software** | None on the PCs |
| **Configured on** | Routers, firewalls or VPN gateways, such as Azure VPN Gateway |
| **Connects** | Two networks |

> The two networks must use **different address ranges**. If both offices use `192.168.1.0/24`, traffic cannot be routed between them.

### Remote Access and Site-to-Site Compared

| | Remote access VPN | Site-to-site VPN |
|---|-------------------|------------------|
| **Connects** | One device to a network | Two networks to each other |
| **Client software** | Yes | No |
| **Tunnel is** | Started by the user when needed | Usually always on |
| **Typical ticket** | "I cannot connect from home" | "The branch office cannot reach the head office" |

---

## 3. Client VPN and Clientless VPN

| | Client VPN | Clientless VPN |
|---|-----------|----------------|
| **Software** | Requires a VPN application | No VPN application |
| **How the user connects** | Installs and runs the VPN software | Uses a web browser |
| **Access** | Network access, as allowed by company policy | Limited to specific web applications |
| **Suitable for** | Employees | Vendors, contractors or temporary users |
| **Examples** | Cisco Secure Client, WireGuard, GlobalProtect | An SSL VPN portal opened in a browser |

### Client VPN

```text
Laptop
   │
VPN client (for example Cisco Secure Client)
   │
Encrypted VPN tunnel
   │
Company VPN server
   │
Company network
```

### Clientless VPN

```text
Laptop
   │
Browser (Chrome or Edge)
   │
HTTPS
   │
SSL VPN portal
   │
Internal web applications
```

> A client VPN gives access to whatever the administrator allows, which may be the whole network or only some subnets. A clientless VPN is limited to the web applications listed on its portal.

---

## 🔒 VPN by Protocol

| Protocol | Ports | Notes |
|----------|-------|-------|
| **SSL/TLS VPN** | TCP 443 | Passes most firewalls |
| **IPsec (IKEv2)** | UDP 500 and 4500 | Very secure, and reconnects well |
| **OpenVPN** | UDP 1194 or TCP 443 | Flexible and open source |
| **WireGuard** | UDP 51820 (common, can be changed) | Modern, fast and simple |

For details on each protocol, see [VPN Protocols](./vpn-protocols.md).

---

## 💡 Next Step

→ [VPN Protocols](./vpn-protocols.md)
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 




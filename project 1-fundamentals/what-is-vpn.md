# 🔐 VPN Fundamentals

---

## 💡 What is a VPN?

A **VPN (Virtual Private Network)** creates a secure, encrypted tunnel between a device and a remote network. Through the tunnel, the device can use the remote network as if it were connected to it directly.

---

## 🏢 Why Companies Use a VPN

Remote workers need access to resources such as:

- Internal file servers and databases
- The company intranet and internal applications
- Network printers and email servers

These resources are not exposed directly to the internet. A VPN gives remote users a secure, encrypted way to reach them.

---

## ⚙️ What a VPN Does

| Function | Meaning |
|----------|---------|
| **Encrypts traffic** | Data inside the tunnel is scrambled, so only the two ends can read it |
| **Authenticates the user** | Proves identity with a username and password, often with multi-factor authentication (MFA) or a certificate |
| **Creates a virtual network adapter** | The VPN software adds a virtual network card to the PC |
| **Routes traffic through the tunnel** | Traffic for the company network is sent through the tunnel |

---

## 🔄 Without and With a VPN

| | Without a VPN | With a VPN |
|---|---------------|------------|
| **Path** | PC → Internet → public websites | PC → Encrypted tunnel → VPN server → Company LAN |
| **Internal servers** | Not reachable from the internet | Reachable through the tunnel |
| **Traffic protection** | Depends on the application, for example HTTPS | Everything inside the tunnel is encrypted |

```text
Without VPN:   Your PC ──► Internet ──► Public website

With VPN:      Your PC ══ Encrypted tunnel ══► VPN Server ──► Company LAN
```

---

## 🔑 Key VPN Terms

| Term | Description |
|------|-------------|
| **VPN client** | Software on the PC, such as the built-in Windows VPN client, Cisco Secure Client (AnyConnect) or GlobalProtect |
| **VPN server (gateway)** | The company device that accepts VPN connections |
| **Tunnel** | The encrypted connection between the client and the server |
| **Authentication** | Proving who you are |
| **Encryption** | Scrambling data so only the authorised parties can read it |
| **Split tunnel** | Only traffic for the company network goes through the VPN. Other traffic uses the local internet connection |
| **Full tunnel** | All traffic goes through the VPN |
| **VPN adapter** | The virtual network card created by the VPN software |
| **MFA** | A second proof of identity, such as a code or a phone approval |

---

## 🧩 VPN Components

A VPN connection involves four components. Each one has its own job, and knowing which one failed is the first step in troubleshooting.

```text
User's PC                                         Company network
┌────────────────────────┐                      ┌──────────────────────┐
│ VPN client             │ ══ Encrypted tunnel ══► VPN server / gateway │
│ + VPN adapter          │                      └──────────┬───────────┘
└────────────────────────┘                                 │ checks identity
                                                ┌──────────▼───────────┐
                                                │ Authentication server│
                                                └──────────────────────┘
```

| Component | What it is | Examples | Main responsibilities |
|-----------|------------|----------|-----------------------|
| **VPN client** | Software on the user's device that starts the connection to the company's VPN server | Windows built-in VPN, Cisco Secure Client (AnyConnect), FortiClient, GlobalProtect, WireGuard, OpenVPN | Starts the connection, sends the user's credentials, builds the tunnel, encrypts and decrypts traffic |
| **VPN server (gateway)** | The device or server that accepts VPN connections and gives access to the internal network | Windows Server RRAS, Azure VPN Gateway, Cisco ASA, FortiGate, Palo Alto firewall | Accepts connections, builds the tunnel, passes authentication to the authentication server, grants access to internal resources |
| **Authentication server** | The system that verifies who the user is and whether they may connect | Active Directory (AD DS), Network Policy Server (NPS), RADIUS server, Microsoft Entra ID | Checks the username and password, validates MFA if it is enabled, confirms the user has permission, allows or denies the connection |
| **VPN adapter** | A virtual network card created on the user's computer when the VPN connects | Cisco Secure Client virtual adapter, WireGuard tunnel adapter, OpenVPN TAP/TUN adapter, Windows VPN adapter | Receives an IP address from the VPN server, sends and receives the encrypted traffic, gives the PC access to the internal network |

> **Troubleshooting tip:** Each component fails in its own way. If the client cannot connect at all, check the client, the server and the ports. If the credentials are rejected, check the authentication server and the account in ADUC. If the VPN connects but nothing works, check the VPN adapter, its IP address, its DNS servers and the routes.
## 🔒 Common VPN Protocols



> A VPN that cannot connect from a hotel or public Wi-Fi is often being blocked at the ports above. SSTP on TCP 443 usually gets through.

---

## 🔀 Split Tunnel and Full Tunnel

| | Split tunnel | Full tunnel |
|---|--------------|-------------|
| **Traffic through the VPN** | Only company traffic | All traffic |
| **Internet speed** | Usually faster, because the internet traffic stays local | Often slower, because everything goes through the company |
| **Security** | The company does not inspect the internet traffic | The company can inspect and filter all traffic |

---




---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)

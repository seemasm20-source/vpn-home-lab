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

## 🌐 Types of VPN

| Type | What it connects | Example |
|------|------------------|---------|
| **Remote access VPN** | One user's device to the company network | An employee working from home |
| **Site-to-site VPN** | Two whole networks | A branch office to the head office, or an office to an Azure virtual network |

---

## 🔒 Common VPN Protocols

| Protocol | Notes | Ports used |
|----------|-------|------------|
| **IKEv2/IPsec** | Secure and fast. Reconnects well when the network changes | UDP 500 and 4500 |
| **SSTP** | Windows protocol that runs over HTTPS, so it often passes firewalls | TCP 443 |
| **L2TP/IPsec** | Older but still used | UDP 500, 1701 and 4500 |
| **OpenVPN** | Open-source and widely used | UDP 1194 by default (the port can be changed) |
| **WireGuard** | Modern, fast and simple | UDP 51820 by default (the port can be changed) |
| **PPTP** | Outdated and **insecure**. Should not be used | TCP 1723 and GRE |

> A VPN that cannot connect from a hotel or public Wi-Fi is often being blocked at the ports above. SSTP on TCP 443 usually gets through.

---

## 🔀 Split Tunnel and Full Tunnel

| | Split tunnel | Full tunnel |
|---|--------------|-------------|
| **Traffic through the VPN** | Only company traffic | All traffic |
| **Internet speed** | Usually faster, because the internet traffic stays local | Often slower, because everything goes through the company |
| **Security** | The company does not inspect the internet traffic | The company can inspect and filter all traffic |

---

## 🛠️ Most Common VPN Tickets (Tier 1 & Tier 2)

| Ticket | Likely causes | What to check |
|--------|---------------|---------------|
| **1. Cannot connect to the VPN** | No internet, wrong credentials, locked or disabled account, expired MFA, blocked VPN ports, VPN server down | Test the internet connection, check the account in ADUC, try another network, and check whether other users can connect |
| **2. VPN connected, but cannot reach resources** | Missing route or DNS setting, firewall rule, wrong permissions, split tunnel missing the internal subnet | `ipconfig /all` for the VPN adapter, `route print`, `ping` the internal server by IP, then by name |
| **3. VPN keeps disconnecting** | Unstable internet or Wi-Fi, idle timeout, a firewall closing the connection, VPN client or driver problem | `ping -t` to check for packet loss, check the Wi-Fi signal, update the VPN client |
| **4. Internet slow when the VPN is on** | Full tunnel, a busy VPN server, a weak home connection | Check the tunnel mode, test the speed with and without the VPN |
| **5. Specific apps not working over the VPN** | The app's traffic is not routed through the tunnel, a blocked port, an app that needs internal DNS | Check the routes and DNS, and test the app's port with `Test-NetConnection <server> -Port <port>` |

---

## 🔧 Useful Commands

| Command | What it shows |
|---------|---------------|
| `ipconfig /all` | The VPN adapter, its IP address and DNS servers |
| `route print` | The routes, including which networks go through the VPN |
| `ping <internal server IP>` | Whether the internal network is reachable |
| `nslookup <internal name>` | Whether internal names resolve through the VPN DNS |
| `tracert <server>` | The path the traffic takes |
| `Test-NetConnection <server> -Port <port>` | Whether a specific port is reachable |

---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)

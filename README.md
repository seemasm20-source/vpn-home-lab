# 🔐 VPN Portfolio

**Portfolio:** IT Help Desk Tier 1 & Tier 2 - Networking Labs

**Tool:** Windows Server 2025 (RRAS), Windows 11 built-in VPN client, Microsoft Azure

**Purpose:** Demonstrate VPN knowledge and hands-on VPN configuration and troubleshooting skills for IT Help Desk Tier 1 and Tier 2

**Author:** Seema Soapanahalli Mallikarjunaiah

**Date:** OCTOBER 2026


---

## 📌 Objective

This portfolio explains how VPNs work, from the basic components to protocols, authentication and tunnel modes, and includes a hands-on SSTP VPN lab built on Azure.

The objective of this portfolio is to demonstrate:

- Understanding of what a VPN is, why companies use it, and the parts of a VPN connection
- Knowledge of VPN types, protocols, ports and authentication methods
- The difference between split tunnel and full tunnel, and how it affects tickets
- Reading the VPN adapter, routes and DNS settings on Windows
- Configuring an SSTP VPN server (RRAS) and a Windows 11 client with a self-signed certificate
- A step-by-step approach to the most common VPN tickets

> **Lab Note:** The SSTP VPN is the hands-on lab of this portfolio. The other files are explanations and reference material for the concepts, protocols and troubleshooting method. Troubleshooting scenario files are planned and are listed at the end.

---

## 💡 What is a VPN?

A **VPN (Virtual Private Network)** creates a secure, encrypted tunnel between a device and a remote network. Through the tunnel, a remote user can reach company resources, such as file servers, intranet applications, printers and email servers, that are not exposed directly to the internet.

```text
Without VPN:   Your PC ──► Internet ──► Public website

With VPN:      Your PC ══ Encrypted tunnel ══► VPN server ──► Company LAN
```

A VPN does four things:

| Function | Meaning |
|----------|---------|
| **Encrypts traffic** | Data inside the tunnel can only be read by the two ends |
| **Authenticates the user** | Proves identity with a password, certificate or MFA |
| **Creates a virtual adapter** | The VPN software adds a virtual network card to the PC |
| **Routes company traffic** | Traffic for the company network goes through the tunnel |

---

## 📁 Portfolio Structure

| Topic | What it covers | Key Skills |
|-------|----------------|------------|
| **VPN Fundamentals** | What a VPN is, why it is used, key terms, common tickets | Explaining a VPN, split and full tunnel basics |
| **VPN Components** | VPN client, VPN server, authentication server, VPN adapter | Knowing which component failed |
| **VPN Types** | Remote access, site-to-site, client and clientless VPN | Choosing the right VPN type |
| **VPN Protocols** | IKEv2/IPsec, SSL/TLS, OpenVPN, WireGuard, and others | Protocols, ports and firewall issues |
| **VPN Authentication Methods** | Password, certificate, MFA, SSO, pre-shared key | Authentication faults and fixes |
| **Split Tunnel vs Full Tunnel** | Which traffic uses the VPN | Slow internet and missing resources |
| **VPN Adapter** | The virtual network card and how to read it | `ipconfig /all`, `route print`, DNS |
| **VPN Connection Process** | The phases of a connection and where it can hang | Finding the failing step |
| **SSTP VPN Configuration (hands-on lab)** | RRAS, certificate, address pool, Windows 11 client | Building and testing a working VPN |

---

## 🗂️ Project Files

| Topic | Description | File |
|-------|-------------|------|
| **VPN Fundamentals** | What is a VPN, why companies use it, key terms and common tickets | [VPN Fundamentals](./vpn-fundamentals.md) |
| **VPN Components** | The four components of a VPN connection | [VPN Fundamentals](./vpn-fundamentals.md) |
| **VPN Types** | Remote access, site-to-site, client and clientless | [VPN Types](./vpn-types.md) |
| **VPN Protocols** | IKEv2/IPsec, SSL/TLS, OpenVPN, WireGuard, ports and common issues | [VPN Protocols](./vpn-protocols.md) |
| **VPN Authentication Methods** | Password, certificate, MFA, SSO and pre-shared key | [VPN Authentication Methods](./vpn-authentication.md) |
| **Split Tunnel vs Full Tunnel** | What goes through the VPN and what does not | [Split Tunnel vs Full Tunnel](./split-vs-full-tunnel.md) |
| **VPN Adapter** | Finding and troubleshooting the VPN adapter | [What is a VPN Adapter?](./vpn-adapter.md) |
| **VPN Connection Process** | Phases, connection states and where a connection hangs | [VPN Connection Process](./vpn-connection-process.md) |
| **SSTP VPN Configuration** | Hands-on lab on Azure with a self-signed certificate | [SSTP VPN Configuration](./sstp-vpn-configuration.md) |

---

## 🧪 Hands-On Lab - SSTP VPN

| Setting | Value |
|---------|-------|
| **Platform** | Microsoft Azure |
| **VPN server** | Windows Server 2025 (`server2021`) with Routing and Remote Access (RRAS) |
| **VPN client** | Windows 11, built-in VPN client |
| **Domain** | `seemaenterprise.co.in` |
| **Protocol and port** | SSTP, TCP 443 |
| **Certificate** | Self-signed, friendly name `SSTP` |
| **VPN address pool** | `10.10.10.1 – 10.10.10.10` |
| **VPN user** | `Sam` |

The lab covers: installing the Remote Access role, creating and exporting a self-signed certificate, enabling RRAS and binding the certificate, setting the address pool, opening TCP 443 on the Azure network security group, giving a user dial-in permission, creating the VPN connection on Windows 11, trusting the certificate, and verifying the connection on the client and on the server.

The server is built in the [Windows Server on Azure](https://github.com/seemasm20-source/Windows-Server-Azure-AD/tree/main/Windows%20Server%20Azure) project.

---

## 🔒 VPN Protocols and Ports

| Protocol | Ports | Notes |
|----------|-------|-------|
| **IKEv2/IPsec** | UDP 500 and 4500 | Fast, reconnects well, common in enterprises |
| **SSL/TLS VPN, SSTP** | TCP 443 | Passes most firewalls |
| **OpenVPN** | UDP 1194 (default) or TCP 443 | Open source and flexible |
| **WireGuard** | UDP 51820 (common, configurable) | Modern, fast and simple |
| **L2TP/IPsec** | UDP 500, 1701 and 4500 | Older, but still used |
| **PPTP** | TCP 1723 and GRE | Outdated and insecure, should not be used |

---

## 🎯 VPN Troubleshooting Matrix

| Ticket | Likely causes | What to check | Topic |
|--------|---------------|---------------|-------|
| **Cannot connect to the VPN** | No internet, blocked ports, wrong server name, bad credentials, locked account, expired MFA, certificate error | `ping 8.8.8.8`, `nslookup` the VPN name, `Test-NetConnection -Port 443`, the account in ADUC | [VPN Connection Process](./vpn-connection-process.md) |
| **Hangs at "Connecting"** | The VPN server is unreachable, a firewall blocks the port, the name does not resolve | DNS, the port and another network | [VPN Connection Process](./vpn-connection-process.md) |
| **Hangs at "Authenticating"** | Wrong credentials, locked or disabled account, MFA problem, certificate problem | The account, the MFA status and the time on the device | [VPN Authentication Methods](./vpn-authentication.md) |
| **Certificate error** | The client does not trust the certificate, or the name does not match | Trusted Root store, the certificate's DNS name (SAN) and expiry date | [SSTP VPN Configuration](./sstp-vpn-configuration.md) |
| **VPN connected, but cannot reach resources** | Missing route, wrong DNS, firewall or permissions | `ipconfig /all`, `route print`, `nslookup`, `ping` by IP and then by name | [VPN Adapter](./vpn-adapter.md) |
| **VPN keeps disconnecting** | Unstable internet or Wi-Fi, idle timeout, a firewall closing the connection, client problem | `ping -t` to check for packet loss, update the VPN client | [VPN Connection Process](./vpn-connection-process.md) |
| **Internet slow when the VPN is on** | Full tunnel, a busy VPN server, a weak connection | The tunnel mode, and speed with and without the VPN | [Split Tunnel vs Full Tunnel](./split-vs-full-tunnel.md) |
| **Specific apps not working over the VPN** | The app's traffic is not routed through the tunnel, a blocked port, internal DNS needed | Routes and DNS, `Test-NetConnection -Port <port>` | [Split Tunnel vs Full Tunnel](./split-vs-full-tunnel.md) |
| **Error 691** | Wrong credentials, or the account is not allowed to connect | The account status, the **Dial-in** tab and the RRAS settings | [VPN Connection Process](./vpn-connection-process.md) |

---

## 📋 Key Commands Quick Reference

| Command | What it does |
|---------|--------------|
| `ipconfig /all` | Shows the VPN adapter, its IP address and its DNS servers |
| `route print` | Shows the routes, and which networks go through the VPN |
| `nslookup <name>` | Tests whether a VPN server or internal name resolves |
| `ping <IP>` | Tests the connection to an internal server by IP |
| `tracert <server>` | Shows the path the traffic takes |
| `Test-NetConnection <server> -Port 443` | Tests whether a TCP port is reachable (TCP only) |
| `Get-NetAdapter` | Lists all adapters, including the VPN adapter, and their status |
| `Get-VpnConnection` | Lists the Windows built-in VPN connections |
| `netstat -an \| findstr :443` | Checks that the VPN server listens on port 443 |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| Microsoft Azure | Hosts the VPN server, with a network security group for TCP 443 |
| Windows Server 2025 | VPN server with Routing and Remote Access (RRAS) |
| Windows 11 | VPN client with the built-in VPN |
| IIS Manager and PowerShell | Creating the self-signed certificate |
| Active Directory Users and Computers | VPN user and dial-in permission |
| Command Prompt and PowerShell | Checking the connection, adapter, routes and DNS |

---

## 📚 Skills Demonstrated

- Explaining a VPN, its components, types and protocols
- Choosing a protocol by port and firewall conditions
- Describing authentication methods and their faults
- Explaining split tunnel and full tunnel, and how each affects tickets
- Reading the VPN adapter, routes and DNS settings
- Locating the failing phase of a VPN connection
- Configuring an SSTP VPN with RRAS and a self-signed certificate
- Creating the VPN client connection and trusting the certificate
- Verifying a VPN on the client and on the server
- Technical documentation for a GitHub portfolio

---

## 🎯 Real-World Help Desk Tickets

| Caller Complaint | Root Cause | Fix Applied |
|------------------|------------|-------------|
| "I can't connect to the VPN" | The server name, port, credentials or account | Tested DNS and the port, checked the account in ADUC |
| "The VPN says certificate error" | The certificate is not trusted, or the name does not match | Imported the certificate into Trusted Root, used the matching server name |
| "I'm connected but can't open the file server" | Missing route or DNS, or share permissions | Checked `ipconfig /all`, `route print` and `nslookup` |
| "The internet is slow when I'm on the VPN" | Full tunnel | Checked the tunnel mode, asked whether split tunnel is allowed |
| "My VPN keeps dropping" | Unstable connection | Used `ping -t`, checked the Wi-Fi, updated the client |

---


## 🎓 Learning Outcome

This portfolio provided an understanding of how VPNs work and hands-on experience configuring an SSTP VPN on Windows Server. It built practical skills for the VPN tickets a help desk sees most often: finding which phase of a connection fails, reading the VPN adapter, routes and DNS, and telling a certificate, authentication, port or routing problem apart. These skills are relevant to IT Help Desk Tier 1 and Tier 2 roles.

---

## ✅ Conclusion

The VPN concepts, components, types, protocols, authentication methods and tunnel modes were documented, and an SSTP VPN was configured between a Windows Server on Azure and a Windows 11 client with a self-signed certificate.

Together these show a systematic approach to VPN troubleshooting: confirm the symptom, find the phase that fails, check the name, port, credentials and certificate, and then the adapter, routes and DNS.

**Planned additions:** VPN troubleshooting scenario files (cannot connect, connected but cannot reach resources, keeps disconnecting, slow internet, specific apps failing).

> **Note:** This portfolio is actively being built. Labs and screenshots are added as each section is completed.


# 🔐 VPN Protocols

A VPN protocol sets how the tunnel is built, how it is encrypted and which ports it uses. The protocol decides which firewalls it can pass and what a technician checks when it fails.

---

## 1. 🔐 IKEv2/IPsec (Internet Key Exchange version 2)

| Feature | Details |
|---------|---------|
| **Protocol** | IKEv2 with IPsec |
| **Default ports** | UDP 500 and UDP 4500 |
| **Speed** | Very fast |
| **Security** | Very high |
| **Best for** | Remote workers, mobile devices, corporate VPNs |
| **Key benefit** | Reconnects automatically when the device switches between Wi-Fi and mobile networks |
| **Common usage** | Windows built-in VPN, Azure VPN Gateway, Cisco, Fortinet |

### How it Works

IKEv2/IPsec builds an encrypted tunnel between a remote user's device and the company network. IKEv2 sets up the connection and handles the authentication, and IPsec encrypts the traffic. UDP 500 is used for the key exchange. UDP 4500 is used when a NAT device, such as a home router, is in the path.

### Advantages

- ✅ Fast connection and stable for long sessions
- ✅ Strong encryption with IPsec
- ✅ Reconnects automatically after a network change
- ✅ Common in enterprise environments

### Common IT Support Issues

- Firewall blocking **UDP 500** or **UDP 4500**
- Incorrect VPN server address
- Authentication failure
- Certificate or pre-shared key mismatch
- VPN connected, but the user cannot reach internal resources

---

## 2. 🔐 SSL/TLS VPN (HTTPS)

| Feature | Details |
|---------|---------|
| **Protocol** | TLS (the older name is SSL, Secure Sockets Layer) |
| **Default port** | TCP 443 |
| **Speed** | Good |
| **Security** | High |
| **Best for** | Remote users on hotel, café, airport and public Wi-Fi |
| **Common usage** | Cisco Secure Client (SSL), FortiClient SSL VPN, GlobalProtect, and SSTP on Windows |

### How it Works

An SSL/TLS VPN creates an encrypted tunnel between the user's device and the VPN server on **TCP port 443**, the port used by HTTPS websites. Most networks allow HTTPS, so this type of VPN can usually connect even on restrictive networks.

> The name "SSL VPN" is still common, but the old SSL protocol is obsolete. Current products use **TLS**.

### Advantages

- ✅ Uses TCP port 443 (HTTPS)
- ✅ Passes through most firewalls
- ✅ Encrypted communication
- ✅ Easy for remote workers

### Common IT Support Issues

- VPN authentication failed
- SSL certificate expired
- VPN portal unavailable
- Firewall or proxy blocking the connection
- Slow VPN performance, because TCP carries the traffic

---

## 3. 🔐 SSTP VPN (Secure Socket Tunneling Protocol)

| Feature | Details |
|---------|---------|
| **Protocol** | SSTP (Secure Socket Tunneling Protocol) |
| **Encryption** | TLS (Transport Layer Security) |
| **Default port** | TCP 443 |
| **Speed** | Good, depending on network conditions |
| **Security** | High, when properly configured |
| **Best for** | Windows users requiring secure remote access |
| **Common usage** | Windows Server RRAS and Windows built-in VPN client |

### How it Works

SSTP (Secure Socket Tunneling Protocol) is a VPN protocol developed by Microsoft. It uses **TLS encryption over TCP port 443** to establish a secure connection between a remote user's device and a VPN server.

SSTP encapsulates PPP traffic inside an HTTPS-based TLS connection. Since it uses TCP port 443, it can often connect through networks that allow HTTPS traffic.

During connection establishment, the VPN server presents an SSL/TLS certificate to authenticate its identity. The client validates the certificate before establishing the secure tunnel.

### Advantages

- ✅ Uses TCP port 443, commonly allowed through firewalls.
- ✅ Provides encrypted communication using TLS.
- ✅ Integrated into Windows VPN client.
- ✅ Supports user authentication through PPP.
- ✅ Suitable for Windows-based remote access environments.

### Common IT Support Issues

- SSTP VPN connection error 809.
- SSL/TLS certificate expired or not trusted.
- VPN server name does not match the certificate.
- TCP port 443 blocked by firewall.
- Incorrect VPN username or password.
- RRAS service stopped or incorrectly configured.
- DNS resolution issues after connecting.
- VPN connects, but internal network resources are inaccessible.
- Slow VPN performance due to TCP overhead or network conditions.

---

## 4. 🔐 WireGuard

| Feature | Details |
|---------|---------|
| **Protocol** | WireGuard |
| **Common port** | UDP 51820 (a convention, and it can be changed) |
| **Speed** | Very fast |
| **Security** | Very high |
| **Best for** | Modern VPN deployments, cloud environments, remote users |
| **Common usage** | Home labs, cloud servers, modern VPN services |

### How it Works

- WireGuard builds an encrypted tunnel between the client and the VPN server.
- It usually listens on **UDP port 51820**, but the port is chosen in the configuration.
- It is designed to be lightweight, fast and simple to configure.
- It uses modern cryptography, and each side is identified by a **public and private key pair**.

### Advantages

- ✅ Very fast and lightweight
- ✅ Simple configuration
- ✅ Strong encryption
- ✅ Low CPU usage

### Common IT Support Issues

- Wrong public or private keys
- Firewall blocking UDP 51820 (or the chosen port)
- Incorrect peer configuration
- Routing problems, such as a wrong **AllowedIPs** setting

---

## 🧰 Other Protocols You May See

| Protocol | Ports | Notes |
|----------|-------|-------|
| **SSTP** | TCP 443 | Windows protocol that carries the VPN over HTTPS (TLS). Passes most firewalls |
| **L2TP/IPsec** | UDP 500, 1701 and 4500 | Older, but still used. Needs a pre-shared key or a certificate |
| **PPTP** | TCP 1723 and GRE | Outdated and **insecure**. Should not be used |

---

## 📌 VPN Protocol Port Reference

| VPN Protocol | Ports | Transport |
|--------------|-------|-----------|
| **IKEv2/IPsec** | 500 and 4500 | UDP |
| **SSL/TLS VPN, SSTP** | 443 | TCP |
| **SSTP** |  443 |     |  TCP |
| **WireGuard** | 51820 (common, configurable) | UDP |
| **L2TP/IPsec** | 500, 1701 and 4500 | UDP |
| **PPTP** | 1723, plus GRE | TCP |

> **Testing a port:** `Test-NetConnection <server> -Port 443` works for **TCP** ports only. UDP ports cannot be tested the same way, so for UDP protocols check the firewall rules and the VPN logs.

---

## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)s

f 5f<qfdFc
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 --------------------
 ## 🔐 VPN Protocols 


## 1. 🔐 IKEv2/IPsec - Internet Key Exchange Version 2

| **Feature** | **Details** |
|-------------|-------------|
| **Protocol** | IKEv2 with IPsec |
| **Default Ports** | UDP 500, UDP 4500 |
| **Speed** | ⭐⭐⭐⭐⭐ Very Fast |
| **Security** | ⭐⭐⭐⭐⭐ Very High |
| **Best For** | Remote workers, mobile devices, corporate VPNs |
| **Key Benefit** | Automatically reconnects when switching between Wi-Fi and mobile networks |
| **Common Usage** | Windows Built-in VPN, Azure VPN Gateway, Cisco, Fortinet |



### How it Works

KEv2/IPsec is a secure VPN protocol used to establish an encrypted tunnel between a remote user's device and a company's network. It uses UDP ports 500 and 4500, provides strong encryption through IPsec which is fast and reliable and can automatically reconnect if the network connection changes.



### Advantages

- ✅ Very fast connection
- ✅ Strong encryption using IPsec
- ✅ Stable for long VPN sessions
- ✅ Automatically reconnects after network changes
- ✅ Commonly used in enterprise environments


### Common IT Support Issues

- Firewall blocking **UDP 500** or **UDP 4500**
- Incorrect VPN server address
- Authentication failure
- Certificate or pre-shared key mismatch
- VPN connected but unable to access internal resources





## 2. 🔐 SSL/TLS VPN (HTTPS) Secured Socket Layer/Transport Layer Security

| **Feature** | **Details** |
|-------------|-------------|
| **Protocol** | SSL/TLS |
| **Default Port** | TCP 443 |
| **Speed** | ⭐⭐⭐⭐☆ Good |
| **Security** | ⭐⭐⭐⭐⭐ High |
| **Best For** | Remote users, hotels, cafés, airports, public Wi-Fi |
| **Common Usage** | Cisco Secure Client (SSL), FortiClient SSL VPN, GlobalProtect SSL VPN |

### How it Works

SSL/TLS VPN creates a secure, encrypted tunnel between the user's device and the company's VPN server using **TCP port 443**, which is the same port used by HTTPS websites.

Since most networks allow HTTPS traffic, SSL VPN can usually connect even on restrictive networks such as hotels, cafés, airports and public Wi-Fi.

### Advantages

- ✅ Uses TCP port 443 (HTTPS)
- ✅ Works through most firewalls and proxy servers
- ✅ Secure encrypted communication
- ✅ Easy for remote workers
- ✅ Widely used in enterprise environments

### Common IT Support Issues

- VPN authentication failed
- SSL certificate expired
- VPN portal unavailable
- Firewall or proxy blocking the connection
- Slow VPN performance

  




## 3 🔐 OpenVPN

| **Feature** | **Details** |
|-------------|-------------|
| **Protocol** | OpenVPN |
| **Default Ports** | UDP 1194 (default), TCP 443 (optional) |
| **Speed** | ⭐⭐⭐⭐☆ Good |
| **Security** | ⭐⭐⭐⭐⭐ High |
| **Best For** | Home labs, cloud servers, small businesses |
| **Common Usage** | Open-source VPN deployments |

### How it Works

- OpenVPN creates a secure, encrypted VPN tunnel between the client and the VPN server.
- By default, it uses **UDP port 1194** for better performance.
- It can also use **TCP port 443**, allowing it to work on networks that only permit HTTPS traffic.
- Uses SSL/TLS encryption to protect data during transmission.

### Advantages

- ✅ Open source and free
- ✅ Highly secure
- ✅ Flexible and configurable
- ✅ Works on Windows, Linux, macOS, Android, and iOS

### Common IT Support Issues

- Incorrect configuration file
- Authentication failure
- Firewall blocking UDP 1194
- Certificate issues


## 4 🔐 WireGuard

| **Feature** | **Details** |
|-------------|-------------|
| **Protocol** | WireGuard |
| **Default Port** | UDP 51820 |
| **Speed** | ⭐⭐⭐⭐⭐ Very Fast |
| **Security** | ⭐⭐⭐⭐⭐ Very High |
| **Best For** | Modern VPN deployments, cloud environments, remote users |
| **Common Usage** | Home labs, cloud servers, modern enterprise VPNs |

### How it Works

- WireGuard creates a secure, encrypted VPN tunnel between the client and the VPN server.
- Uses **UDP port 51820** by default.
- Designed to be lightweight, fast, and easy to configure.
- Uses modern cryptographic algorithms for secure communication.

### Advantages

- ✅ Very fast
- ✅ Lightweight
- ✅ Simple configuration
- ✅ Strong encryption
- ✅ Low CPU usage

### Common IT Support Issues

- Incorrect public/private keys
- Firewall blocking UDP 51820
- Incorrect peer configuration
- Routing issues





## 📌 VPN Protocol Port Reference

| **VPN Protocol** | **Default Port(s)** |
|------------------|---------------------|
| **IKEv2/IPsec** | UDP 500, UDP 4500 |
| **SSL/TLS VPN** | TCP 443 |
| **OpenVPN** | UDP 1194 (default) or TCP 443 |
| **WireGuard** | UDP 51820 (default, configurable) |

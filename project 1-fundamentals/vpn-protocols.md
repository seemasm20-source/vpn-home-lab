
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

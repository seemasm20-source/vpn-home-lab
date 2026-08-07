

  ## 🧩 VPN Components


 

## 1. VPN Client

**Definition:**

The VPN client is the software installed on the user's device that establishes a secure connection to the company's VPN server.

**Examples:**

- Windows Built-in VPN
- Cisco Secure Client (AnyConnect)
- FortiClient
- GlobalProtect
- WireGuard Client
- OpenVPN Client

**Responsibilities:**

- Initiates the VPN connection.
- Authenticates the user.
- Creates the encrypted VPN tunnel.
- Encrypts and decrypts VPN traffic.

---

## 2. VPN Server / Gateway

**Definition:**

The VPN server (or VPN gateway) is the device or server that accepts VPN connections from remote users and provides secure access to the company's internal network.

**Examples:**

- Windows Server RRAS
- Azure VPN Gateway
- Cisco ASA
- FortiGate
- Palo Alto Firewall

**Responsibilities:**

- Accepts incoming VPN connections.
- Authenticates users.
- Establishes the encrypted VPN tunnel.
- Grants access to internal company resources.


## 3. Authentication Server

**Definition:**

The Authentication Server verifies the identity of the user before allowing access to the company network.

**Examples:**

- Active Directory (AD DS)
- Network Policy Server (NPS)
- RADIUS Server
- Azure Active Directory (Microsoft Entra ID)

**Responsibilities:**

- Verifies the username and password.
- Validates Multi-Factor Authentication (MFA), if enabled.
- Confirms the user has permission to connect.
- Allows or denies the VPN connection.

---

## 4. VPN Adapter (Virtual Network Adapter)

**Definition:**

A VPN Adapter (Virtual NIC) is a virtual network interface that is created on the user's computer when a VPN connection is established.

**Examples:**

- Cisco Secure Client Virtual Adapter
- WireGuard Tunnel Adapter
- OpenVPN TAP/TUN Adapter
- Windows VPN Adapter

**Responsibilities:**

- Receives an IP address from the VPN server.
- Sends and receives encrypted VPN traffic.
- Acts as the network interface for the VPN connection.
- Allows access to internal company resources through the VPN tunnel.

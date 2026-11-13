# 🔌 VPN Connection Process

The steps below show how a VPN connection is built, from the user clicking **Connect** to a working tunnel. Knowing the order helps a technician find the step where a connection stops.

---

## 🔄 How a VPN Connection is Established

```text
1 Discovery  →  2 Secure connection  →  3 Authentication  →  4 Tunnel  →  5 Network configuration  →  6 Connected
```

### Phase 1 - Discovery

- The client resolves the VPN server name through DNS.
- The client tries to reach the VPN server.

### Phase 2 - Secure Connection

- The client and the VPN server set up a secure channel.
- They agree on the encryption and security settings.
- The VPN server's certificate is checked, when one is used.

### Phase 3 - Authentication

- The user enters the username and password, or a certificate is used.
- The VPN server checks the credentials, often through Active Directory, NPS or a RADIUS server.
- MFA is requested if it is configured.

### Phase 4 - Tunnel Creation

- A secure, encrypted VPN tunnel is established.
- Traffic can now travel securely between the client and the company network.

### Phase 5 - Network Configuration

- The VPN virtual adapter is activated and configured.
- The VPN server assigns an IP address.
- The VPN may provide DNS settings.
- Routes are added so the client can reach company resources.

### Phase 6 - Connected

- The VPN connection is established.
- Authorised internal company resources are accessible.

> **Note:** The exact order differs by protocol. In some protocols, such as IKEv2, authentication happens while the secure channel is being set up, and the VPN software shows only a few of these phases as separate states.

---



## What Changes After VPN Connects

 ```text
BEFORE VPN:

Ethernet: 192.168.1.50    ← Home network IP
Gateway:  192.168.1.1     ← Home router
DNS:      8.8.8.8         ← Public DNS


AFTER VPN:

Ethernet:    192.168.1.50 ← Home network remains connected
VPN Adapter: 10.8.0.45   ← VPN-assigned IP
VPN Gateway: 10.8.0.1    ← Example VPN gateway
DNS:         10.0.0.10   ← Example company DNS

Note: The VPN IP, gateway, and DNS values depend on the organization's VPN configuration. Split-tunnel and full-tunnel VPNs may route traffic differently.

## 🔄 VPN Client Connection States

| State | Meaning |
|-------|---------|
| **Disconnected** | The VPN is not connected |
| **Connecting** | The client is trying to reach the VPN server |
| **Authenticating** | The user's credentials are being verified |
| **Connected** | The tunnel is active and authorised resources are accessible |
| **Reconnecting** | The connection was interrupted and the client is trying again |
| **Failed** | The connection could not be established. Check the error message or code |

---

## 🔧 What to Check When the VPN Connection Hangs

| Where it stops | Phase |
|----------------|-------|
| **Connecting** | Phase 1 and 2: discovery and secure connection |
| **Authenticating** | Phase 3: authentication |
| **Connected, but no access** | Phase 5: network configuration |

### 1. Hangs at "Connecting"

**Possible causes:**

- The VPN server cannot be reached
- A firewall blocks the VPN port
- The VPN hostname does not resolve through DNS
- No internet connection

**Check:**

```text
C:\> ping 8.8.8.8
C:\> nslookup vpn.company.com
PS C:\> Test-NetConnection vpn.company.com -Port 443
```

- `ping 8.8.8.8` confirms the internet connection.
- `nslookup` confirms that the VPN hostname resolves to an IP address.
- `Test-NetConnection` tests a **TCP** port, such as 443 for an SSL/TLS VPN. UDP ports, such as 500 and 4500 for IKEv2, cannot be tested this way, so check the firewall rules and try another network, such as a mobile hotspot.

---

### 2. Hangs at "Authenticating"

**Possible causes:**

- Wrong username or password
- The account is locked or disabled in Active Directory
- The user is not allowed to use the VPN
- MFA is not set up correctly, or the approval fails or times out
- Certificate or authentication problem

**Check:**

- Verify the credentials
- Check the account in ADUC, and unlock or reset it if needed. See [Unlock a User Account](./unlock-user-account.md)
- Check the MFA status and the time on the device
- Review the VPN client and server logs if needed

---

### 3. Shows "Connected" but No Access

**Possible causes:**

- The VPN adapter did not get the expected IP address
- DNS cannot resolve internal names
- The routes were not added
- An internal firewall blocks access

**Check:**

```text
C:\> ipconfig /all
C:\> route print
C:\> nslookup internal-server.company.local
C:\> ping 10.0.0.10
```

- `ipconfig /all`: check the VPN adapter, its IP address and its DNS servers.
- `route print`: check that the company network has a route through the VPN adapter.
- `nslookup`: test whether internal names resolve.
- `ping`: test an internal server by IP.

> A split tunnel VPN adapter often has **no default gateway**. That is normal, and the routes in `route print` decide where the traffic goes.
>
> A failed `ping` does not always mean the server is down. Many servers and firewalls block ping, so also test the actual service, for example with `Test-NetConnection 10.0.0.10 -Port 445`.

---

## 🧾 Common Windows VPN Error Codes

| Error | Usual meaning | What to check |
|-------|---------------|---------------|
| **691** | Access denied: the username or password is wrong, or the account is not allowed | The credentials and the account status in ADUC |
| **809** | The VPN server did not respond | The VPN server address, firewall rules and NAT or port blocking |
| **800** | The VPN connection could not be established | The server address, the VPN type and the VPN server status |

> These codes apply to the **Windows built-in VPN client**. Other clients, such as Cisco Secure Client, show their own messages. Always record the exact message.

---



## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   









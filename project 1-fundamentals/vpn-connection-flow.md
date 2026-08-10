
  ## 🔄 VPN Connection Flow



The VPN connection follows these main steps:

```text

1. DNS
   ↓
Finds the VPN server's IP address

2. Internet / Reachability
   ↓
Checks that the laptop can reach the VPN server

3. TLS / Secure Connection
   ↓
Establishes a secure connection between the laptop and VPN server

4. Authentication
   ↓
Username and password are verified

5. MFA
   ↓
User approves the login on their phone or enters an OTP

6. VPN Tunnel
   ↓
Creates a secure, encrypted tunnel between the laptop and VPN server

7. Routing
   ↓
Windows determines which company traffic should travel through the VPN

8. Connected
   ↓
User can access authorized company resources
```

### 🔎 In Simple Terms

 **DNS** → Finds the VPN server  
 **Reachability** → Checks whether the server can be reached  
 **TLS** → Establishes a secure connection  
 **Authentication** → Verifies username and password  
 **MFA** → Provides a second verification  
 **VPN Tunnel** → Carries encrypted traffic securely  
 **Routing** → Directs company traffic through the VPN  
 **Connected** → Internal company resources become accessible



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

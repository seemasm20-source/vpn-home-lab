
 ## 🔀 VPN Types


  ## 1. Remote Access VPN

   Remote Access Virtual Private Network (VPN)** is a network architecture that establishes a temporary, secure, and encrypted tunnel between an individual remote client device
   
   (such as a laptop, desktop, or mobile device) and a private corporate or home network over an untrusted public network (like the Internet).

                                        Home Laptop
                                           │
                                       Internet
                                          │
                                       VPN Tunnel
                                          │
                                    Company Office (LAN)

  
           Used by: Corporate remote workers, travelling employees  → Client software required on each device



  ## 2. Site-to-Site VPN

     A Site-to-Site (S2S) VPN connects two entire networks across the public Internet, bridging them so they function like a single secure private network.

     Branch Office LAN ←→ VPN Tunnel ←→ Head Office LAN(Configured on routers - no client software on PCs)

    
```text
          Internet
             │
      Encrypted VPN Tunnel
             │
┌──────────────────┐      ┌──────────────────┐
│ Office A         │──────│ Office B         │
│ 192.168.1.0/24   │      │ 10.0.0.0/24      │
└──────────────────┘      └──────────────────┘
```



## 3. Client VPN vs Clientless VPN


| Client VPN                                               | Clientless VPN                                        |
| -------------------------------------------------------- | ----------------------------------------------------- |
| Requires a VPN application                               | No VPN application required                           |
| User installs VPN software                               | User uses a web browser                               |
| Full network access                                      | Limited access to specific web applications           |
| Suitable for employees                                   | Suitable for vendors, contractors, or temporary users |
| Example: Cisco Secure Client, Wireguard, GlobalProtect   | Example: SSL VPN Portal accessed through a browser    |

## Client VPN

```text
Laptop
   │
Cisco Secure Client
   │
Encrypted VPN Tunnel
   │
Company VPN Server
   │
Company Network
```

## Clientless VPN

```text
Laptop
   │
Chrome / Edge
   │
HTTPS
   │
SSL VPN Portal
   │
Internal Web Applications
```



## VPN by Protocol

SSL/TLS VPN  → port 443 - Works through most firewalls

IPSec VPN    → UDP 500/4500 - Very secure

OpenVPN      → UDP 1194 or TCP 443

WireGuard    → modern - Very fast








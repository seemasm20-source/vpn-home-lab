
  🔀 VPN Types


  1. Remote Access VPN

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



  2. Site-to-Site VPN

     A Site-to-Site (S2S) VPN connects two entire networks across the public Internet, bridging them so they function like a single secure private network.

      Branch Office LAN ←→ VPN Tunnel ←→ Head Office LAN

     Configured on routers — no client software on PCs



               Internet
                  │
      Encrypted VPN Tunnel
                  │
┌──────────────────┐      ┌──────────────────┐
│ Office A         │──────│ Office B         │
│ 192.168.1.0/24   │      │ 10.0.0.0/24      │
└──────────────────┘      └──────────────────┘

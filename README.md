  

## Portfolio:  VPN TROUBLESHOOTING PORTFOLIO - IT Help Desk Tier 1 & 2 

 Tool:**       Windows 10/11, Cisco AnyConnect, Windows Built-in VPN, VirtualBox

 Author:**   Seema

 Date:**    2026


















  ## 🔒    What is This Portfolio?

   Hands-on VPN troubleshooting documentation covering the full range of VPN issues faced in real IT Help Desk Tier 1 & 2 remote support roles.

  Every scenario documents the user complaint, root cause, step-by-step diagnosis, fix and verification.






  ## 📁 Portfolio Structure




| Project   | Topic                | Files |
| --------- | -------------------- | ----  |
| Project 1 | VPN Fundamentals     | 5     |
| Project 2 | VPN Connection       | 5     |
| Project 3 | VPN Troubleshooting  | 9     |
| Project 4 | VPN Diagnostics      | 7     |
| Project 5 | Common VPN Errors    | 6     |
| Project 6 | Real-World Scenarios | 6     |







## 🎯 Real-World Tickets Covered




| User Complaint               | Root Cause                              | Project |
| ---------------------------- | --------------------------------------- | ------- |
| Cannot Connect To VPN        | Server Address / Firewall / Credentials | P3 + P5 |
| Authentication Failed        | Wrong Password / Locked Account / MFA   | P3      |
| MFA Not Working              | Clock Sync / New Phone / App Deleted    | P3      |
| VPN Connected - No Internet  | Full Tunnel Routing                     | P3      |
| VPN Connected - No Resources | DNS Not Pushed / Routing                | P3      |
| VPN Keeps Dropping           | Packet Loss / Timeout Policy            | P3      |
| Slow On VPN                  | Full Tunnel / MTU / WiFi                | P3 + P5 |
| Cannot RDP Over VPN          | Port 3389 Blocked                       | P6      |
| Mapped Drives Not Working    | DNS / Port 445 / Credentials            | P6      |
| Outlook Not Working On VPN   | DNS / Autodiscover                      | P6      |
| Teams Drops On VPN           | Full Tunnel Bandwidth                   | P6      |
| Printer Not Available        | VPN Broadcast Limitation                | P6      |








## 📋 Key VPN Commands



| Command                 | Purpose                              |
| ----------------------- | ------------------------------------ |
| ipconfig /all           | Check VPN adapter + company IP + DNS |
| ipconfig /flushdns      | Clear stale DNS after VPN connects   |
| route print             | Confirm traffic routing through VPN  |
| ping vpn.company.com    | Test VPN server reachable            |
| ping 10.0.0.50          | Test internal routing after VPN      |
| ping -t 8.8.8.8         | Check internet stability             |
| nslookup name 10.0.0.10 | Test company DNS directly            |
| netstat -an             | Confirm VPN tunnel active            |
| eventvwr RasClient      | Find VPN error codes                 |



## 🔗 Related Portfolios

| Portfolio              | Relationship                   |
| ---------------------- | ------------------------------ |
| TCP/IP Troubleshooting | Foundation networking concepts |
| DNS Portfolio          | DNS issues over VPN            |
| DHCP Configuration     | IP assignment concepts         |

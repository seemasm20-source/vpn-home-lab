


# 🔀 Split Tunnel vs Full Tunnel

A tunnel mode decides which traffic goes through the VPN. It affects security, internet speed and which resources a user can reach, so it is behind many VPN tickets.

---

## 1. Full Tunnel VPN

In a **full tunnel**, all network traffic goes through the VPN: company traffic and normal internet traffic.

```text
Your PC
   │
VPN tunnel
   │
Company VPN gateway
   │
   ├── Company traffic  → Company network
   └── Internet traffic → Internet (through the company)
```

### Why Companies Use It

- Central security and monitoring of all traffic
- Company security policies, such as web filtering, apply to internet traffic too
- Needed when the organization requires all traffic to pass through its security controls


---

## 2. Split Tunnel VPN

In a **split tunnel**, only traffic for company resources goes through the VPN. Normal internet traffic uses the user's local internet connection.

```text
Your PC
   │
   ├── Company traffic  → VPN tunnel → Company resources
   │
   └── Internet traffic → Home or local network → Internet
```

### Advantages

- ✅ Faster normal internet browsing
- ✅ Less traffic through the VPN gateway
- ✅ Lower VPN bandwidth use


---

## ⚖️ Comparison

| | Full tunnel | Split tunnel |
|---|-------------|--------------|
| **Traffic through the VPN** | All traffic | Only company traffic |
| **Internet speed** | Often slower | Usually faster |
| **Security and monitoring** | The company can inspect all traffic | The company cannot inspect the local internet traffic |
| **VPN gateway load** | Higher | Lower |
| **Local devices** (home printer) | Often unreachable | Usually reachable |
| **Typical ticket** | "Internet is slow when the VPN is on" | "VPN is connected but I cannot reach an internal server" |

---


## 💡 Next Step

→ [Cannot Connect to VPN](./cannot-connect-vpn.md)




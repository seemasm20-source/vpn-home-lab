

# 🔀 Split Tunnel vs Full Tunnel



## Full Tunnel VPN

```text
All network traffic is sent through the VPN.

Your PC
   ↓
VPN Tunnel
   ↓
Company VPN Gateway
   ↓
Internet / Company Resources
```

### Simple Meaning

**Full Tunnel:** Both company traffic and normal internet traffic go through the company's VPN.

```text
Company traffic  → VPN → Company Network
Internet traffic → VPN → Internet
```

### Why Companies Use It

- Centralized security and monitoring
- Company security policies can be applied to internet traffic
- Useful when the organization requires all traffic to pass through corporate security controls




## 🔀 Split Tunnel VPN

```text
Only company traffic goes through the VPN.
Normal internet traffic goes directly through the local network.

Your PC
   │
   ├── Company traffic → VPN Tunnel → Company Resources
   │
   └── Internet traffic → Home/Local Network → Internet
```

### Simple Meaning

**Split Tunnel:** Only traffic destined for company resources uses the VPN. Normal internet traffic continues through the user's local internet connection.

### Example

```text
Company traffic  → VPN → Company Network
Internet traffic → Home Wi-Fi → Internet
```

### Advantages

- ✅ Faster normal internet browsing
- ✅ Reduces traffic through the company VPN
- ✅ Reduces VPN bandwidth usage

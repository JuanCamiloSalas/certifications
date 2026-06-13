[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-alb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-elb-features.md)

# NLB & Gateway Load Balancer

<img src="../../assets/icons/elb.png" width="64">

> **Pitch (1 line):** NLB = Layer 4 ultra-performance with static IPs; GLB = transparent bump-in-the-wire to send traffic through third-party network appliances before reaching your app.

## 🎯 When the exam picks this

- "static IP / Elastic IP for the load balancer" → **NLB**
- "millions of requests per second, ultra-low latency" → **NLB**
- "inspect traffic with a fleet of firewalls / IDS / IPS before reaching the app" → **GLB**
- "TCP/UDP pass-through, preserve client IP at network level" → **NLB**

## 🧠 Core (non-obvious bits)

**NLB:**
- Operates at **Layer 4** (TCP/UDP/TLS). Does not inspect HTTP headers.
- **One static IP per AZ** — you can assign Elastic IPs. This is the only ELB that supports static/fixed IPs.
- Preserves the **client's source IP** natively (no `X-Forwarded-For` needed).
- Supports **TLS termination** at the NLB, or **TCP passthrough** to the backend for end-to-end encryption.
- Health checks support TCP, HTTP, and HTTPS.
- **Zonal DNS** — NLB can be configured to expose per-AZ DNS names for ultra-low-latency routing.

**GLB:**
- Operates at **Layer 3** (IP) using **GENEVE protocol on port 6081**.
- Pattern: traffic enters GLB → forwarded to appliance fleet (firewall, IDS, DPI) → appliance returns traffic to GLB → GLB forwards to your app.
- The appliance is **transparent** — it can inspect, modify, or drop packets.
- Target group = fleet of network appliances (EC2 instances or IPs).

## ⚠️ Common traps

- "assign a fixed IP to the load balancer" → NLB only (ALB and GLB don't support static IPs).
- "GLB is for content delivery" → NO — it's for traffic inspection, not caching.
- NLB does NOT support security group attachment (unlike ALB). Access control must be done at the NACL or instance SG level.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-alb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-elb-features.md)

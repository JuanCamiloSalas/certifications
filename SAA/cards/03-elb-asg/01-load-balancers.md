[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-alb.md)

# Load Balancers — ALB vs NLB vs GLB vs CLB

> **Pitch (1 line):** pick the LB by **what layer and protocol the scenario describes** — ALB (HTTP), NLB (TCP/UDP), GLB (third-party appliances), CLB (legacy, never the right answer).

## 🎯 When the exam picks this

- "HTTP/HTTPS, path-based or host-based routing" → **ALB**
- "TCP/UDP, static IP per AZ, ultra-low latency, millions of req/s" → **NLB**
- "route traffic through a fleet of firewalls / network appliances" → **GLB**
- "legacy app from years ago" → CLB (but exam rarely wants this)

## 🧠 Core (non-obvious bits)

| LB | Protocol | Layer | Key capability |
|---|---|---|---|
| **ALB** | HTTP/HTTPS/gRPC/WebSocket | 7 | Path & host routing, target groups, redirects |
| **NLB** | TCP/UDP/TLS | 4 | Static IP per AZ, preserves client IP, extreme throughput |
| **GLB** | IP (GENEVE on port 6081) | 3 | Bump-in-the-wire for 3rd-party appliances |
| **CLB** | HTTP/HTTPS/TCP | 4+7 | Legacy — no target groups, no SNI |

- All ELBs can distribute across **multiple AZs**.
- All support **health checks** and **SSL/TLS termination** (except NLB at L4 does passthrough unless you terminate TLS on NLB).
- Only **NLB** gives you **Elastic IP / static IP** — useful if clients whitelist IPs.
- **GLB** transparently passes traffic through your inspection fleet; the appliance sees the original traffic and sends it back.

## ⚠️ Common traps

- "preserve client IP at the load balancer" → NLB does this natively at L4; ALB uses `X-Forwarded-For` header.
- "gaming or real-time streaming" → NLB (low latency TCP/UDP, not ALB).
- "HTTPS and redirect HTTP to HTTPS" → ALB (has redirect rules), not NLB.

## 🔄 Easily confused with

- → [ALB deep dive](./02-alb.md)
- → [NLB & GLB](./03-nlb-glb.md)

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-alb.md)

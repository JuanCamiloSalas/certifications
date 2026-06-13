[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-cloudfront-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../08-decoupling/README.md)

# AWS Global Accelerator & CloudFront vs GA

> **Pitch (1 line):** Global Accelerator gives you **2 static Anycast IPs** and routes TCP/UDP traffic over AWS's private backbone from the nearest edge to your regional endpoints — NOT a CDN, no caching.

## 🎯 When the exam picks this

- "static IPs for a global application, traffic goes over AWS backbone" → **Global Accelerator**
- "non-HTTP traffic (TCP/UDP, gaming, IoT, VoIP) that needs global acceleration" → **Global Accelerator**
- "instant failover between regions at the IP level" → **Global Accelerator**
- "cache content at edge, reduce origin load" → **CloudFront** (not GA)

## 🧠 Core (non-obvious bits)

**Global Accelerator:**
- Provides **2 static Anycast IPs** (same IPs globally — Anycast routes to the nearest edge).
- Traffic enters the AWS network at the nearest edge location and travels via private backbone to your endpoint (ALB, NLB, EC2, Elastic IP) in a specific region.
- **Health checks** included — if your endpoint in one region is unhealthy, traffic fails over to another region in seconds (< 30s).
- Supports **traffic dials** (route % of traffic to each endpoint group) and **endpoint weights**.
- No caching — purely a routing and acceleration service.

**CloudFront vs Global Accelerator:**

| | CloudFront | Global Accelerator |
|---|---|---|
| Protocol | HTTP/HTTPS | TCP, UDP (+ HTTP) |
| Caching | ✅ Yes | ❌ No |
| Static IPs | ❌ (dynamic DNS) | ✅ (2 static Anycast IPs) |
| Latency reduction | Cache hit = no origin trip | Always reaches origin, but faster path |
| Use case | Static content, websites, APIs (HTTP) | Gaming, IoT, VoIP, non-HTTP, IP whitelisting |
| Edge compute | CloudFront Functions, Lambda@Edge | ❌ |

## ⚠️ Common traps

- "static IP for a global HTTP app" → if caching is needed → CloudFront. If static IP is the key requirement → Global Accelerator.
- Global Accelerator does NOT cache — every request hits the origin. CloudFront caches.
- Both use the AWS edge network, but for very different purposes.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-cloudfront-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../08-decoupling/README.md)

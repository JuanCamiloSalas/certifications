[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-routing-policies-1.md)

# Route 53 — Records, Alias vs CNAME, TTL & Hosted Zones

> **Pitch (1 line):** AWS-managed authoritative DNS — choose Alias records (not CNAME) for AWS targets, manage TTL trade-offs, and separate public from private hosted zones.

## 🎯 When the exam picks this

- "map a domain to an ALB/CloudFront/S3/API Gateway" → **Alias record** (not CNAME)
- "map the zone apex (example.com, not sub.example.com) to a resource" → **Alias** (CNAME is illegal at zone apex)
- "register a domain and use Route 53 as DNS" → Route 53 supports both
- "DNS only for internal VPC resources" → **Private Hosted Zone**

## 🧠 Core (non-obvious bits)

**Record types:**
- **A:** hostname → IPv4
- **AAAA:** hostname → IPv6
- **CNAME:** hostname → another hostname (cannot point to the zone apex)
- **Alias:** hostname → AWS resource (ALB, NLB, CloudFront, S3 static site, API Gateway, ElasticBeanstalk, etc.) — behaves like an A/AAAA record

**Alias vs CNAME:**

| | CNAME | Alias |
|---|---|---|
| Zone apex (example.com) | ❌ illegal | ✅ |
| AWS resources | ✅ (works but CNAME query costs money per request) | ✅ (free) |
| Non-AWS targets | ✅ | ❌ (AWS resources only) |
| TTL | Set by you | Set by AWS (you can't control it) |

**TTL:**
- High TTL (e.g., 24h): fewer queries, cheaper, but changes propagate slowly — DNS records are cached by resolvers.
- Low TTL (e.g., 60s): more queries (cost), but fast propagation — use before making DNS changes.

**Hosted Zones:**
- **Public:** resolves from the internet.
- **Private:** resolves only from inside associated VPCs. Costs $0.50/month per hosted zone.

## ⚠️ Common traps

- Alias cannot point to an EC2 DNS name (only to specific AWS services).
- You cannot set the TTL of an Alias record — AWS controls it.
- CNAME at zone apex is forbidden in DNS spec; Alias is Route 53's workaround.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-routing-policies-1.md)

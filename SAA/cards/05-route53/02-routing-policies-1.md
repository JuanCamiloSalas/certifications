[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-records-alias-ttl.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-routing-policies-2.md)

# Route 53 Routing Policies — Simple, Weighted, Latency, Failover

> **Pitch (1 line):** each routing policy answers a different question — which one is implied by the scenario keywords.

## 🎯 When the exam picks this

- "single resource, no logic" → **Simple**
- "A/B testing, blue/green, distribute % of traffic" → **Weighted**
- "lowest latency to the user" → **Latency-based**
- "primary/secondary active-passive failover" → **Failover**

## 🧠 Core (non-obvious bits)

**Simple:**
- One record, one or more values. If multiple IPs, Route 53 returns all of them (client picks one randomly).
- No health checks. No logic. Just "here's the address."

**Weighted:**
- Multiple records with the same name but different **weights** (0–255). Route 53 routes traffic proportionally.
- Weight 0 = no traffic to that record (useful for taking a resource offline without deleting the record).
- Can be combined with health checks — unhealthy records are excluded.
- Use case: blue/green deployments, A/B testing, gradual traffic shift.

**Latency-based:**
- Route 53 measures **latency from the user to AWS regions** (not geographic distance) and routes to the region with lowest latency.
- Requires you to create records in each region.
- Can be combined with health checks.

**Failover (active-passive):**
- **Primary** record: serves traffic normally.
- **Secondary** record: receives traffic only if primary is unhealthy.
- **Health check is mandatory** on the primary.
- Common pattern: primary = production region, secondary = static S3 website as fallback.

## ⚠️ Common traps

- Simple policy does NOT do health checks — if the resource is down, Route 53 still returns it.
- Latency ≠ Geolocation: latency picks the lowest RTT, not the physically closest region.
- Failover requires a health check — without one, Route 53 never switches to secondary.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-records-alias-ttl.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-routing-policies-2.md)

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-routing-policies-1.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-health-checks.md)

# Route 53 Routing Policies — Geolocation, Geoproximity, Multi-Value

> **Pitch (1 line):** three policies with easy name-confusion — Geolocation routes by WHERE the user is, Geoproximity biases by distance with a dial, Multi-Value is NOT a replacement for a load balancer.

## 🎯 When the exam picks this

- "serve content based on user's country or continent" → **Geolocation**
- "compliance — users in Germany must hit German servers" → **Geolocation**
- "shift traffic between regions using a bias dial" → **Geoproximity**
- "return multiple healthy IPs for client-side random selection, with health checks" → **Multi-Value**

## 🧠 Core (non-obvious bits)

**Geolocation:**
- Routes based on the **user's geographic location** (continent, country, US state).
- You must create a **default** record for users who don't match any location.
- Use case: content localization, legal/compliance (GDPR, data residency).
- Does NOT pick the closest resource — it picks based on policy rules you define.

**Geoproximity (requires Traffic Flow):**
- Routes based on **distance** to your resources (AWS regions or custom lat/lon).
- You can set a **bias** (+1 to +99 to pull more traffic toward a resource, -1 to -99 to push traffic away).
- Requires **Route 53 Traffic Flow** (visual policy editor, monthly fee).
- Use case: gradually shift traffic from one region to another.

**Multi-Value Answer:**
- Returns up to **8 healthy records** randomly. The client picks one.
- Supports **health checks** — unhealthy records are excluded from the response.
- NOT a substitute for an ELB — ELB does connection-level load balancing; Multi-Value is just DNS.

## ⚠️ Common traps

- Geolocation ≠ Latency: Geolocation is rules-based by location; Latency picks the lowest RTT regardless of location rules.
- Geoproximity ≠ Geolocation: Geoproximity = distance + bias dial; Geolocation = hard geographic rules.
- Multi-Value ≠ Simple with multiple values: Simple doesn't do health checks; Multi-Value does.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-routing-policies-1.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-health-checks.md)

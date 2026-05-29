[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)

# Block 05 — Route 53

> AWS-managed DNS. **Routing policies are the core of this block**: each policy maps to a distinct scenario.

## 🃏 Cards in this block

_No cards yet. Copy [`_TEMPLATE.md`](../_TEMPLATE.md) here to start._

| # | Card | Concept |
|---|---|---|

## 🎯 Suggested concepts to cover

- Record types (A, AAAA, CNAME, Alias)
- **Alias vs CNAME** (Alias = AWS targets only, free, works at the zone apex)
- Routing policies:
  - Simple
  - Weighted
  - Latency-based
  - Failover (active-passive)
  - Geolocation
  - Geoproximity (uses Traffic Flow)
  - Multi-value answer
- Health checks (endpoint, calculated, CloudWatch)
- TTL: behavior and trade-offs
- Hosted zones: public vs private
- Domain registration vs DNS service (can be DNS only)
- Third-party domain on Route 53

## 🔗 Related comparisons

- Alias vs CNAME
- Each routing policy: when to use which
- Failover vs Multi-value answer (NOT the same)

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)

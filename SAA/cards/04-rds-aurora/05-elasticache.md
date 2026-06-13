[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-aurora-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../05-route53/README.md)

# ElastiCache — Redis vs Memcached & Caching Patterns

<img src="../../assets/icons/elasticache.png" width="64">

> **Pitch (1 line):** in-memory cache to offload DB reads and speed up responses; Redis adds persistence, replication, and data structures — Memcached is simpler and purely ephemeral.

## 🎯 When the exam picks this

- "reduce DB load, cache frequent queries" → **ElastiCache**
- "session store, pub/sub, sorted sets, geospatial" → **Redis**
- "simplest cache, multi-threaded, no persistence needed" → **Memcached**
- "sub-millisecond latency for DynamoDB" → **DAX** (not ElastiCache — see block 11)

## 🧠 Core (non-obvious bits)

**Redis vs Memcached:**

| Feature | Redis | Memcached |
|---|---|---|
| Persistence | ✅ (AOF + snapshots) | ❌ |
| Replication / Multi-AZ | ✅ | ❌ |
| Data structures | Strings, hashes, lists, sets, sorted sets, geo | Strings only |
| Pub/Sub | ✅ | ❌ |
| Cluster mode | ✅ (sharding) | ✅ (simple) |
| Multi-threaded | ❌ (single-threaded core) | ✅ |

**Caching Patterns:**
- **Lazy Loading (Cache-Aside):** app checks cache first; on miss, reads from DB and writes to cache. Stale data possible (mitigate with TTL). Most common pattern.
- **Write-Through:** on every DB write, also write to cache. Cache is always fresh, but write latency increases. Risk: cache churn for data that's never read.
- **TTL:** expire keys after a time window to avoid serving indefinitely stale data. Always set a TTL.

**Session Store:**
- Redis is ideal for storing user sessions — data persists across app server restarts, multi-AZ.

## ⚠️ Common traps

- "need the cache to survive restarts" → Redis (persistence) not Memcached.
- "leaderboard / gaming score" → Redis sorted sets.
- "scale horizontally with simple partition" → Memcached (simpler, multi-threaded).
- Lazy loading can serve stale data; write-through can over-populate cache with cold data.

## 🔄 Easily confused with

- → [DAX — DynamoDB Accelerator](../11-bd-data-ml/01-dynamodb.md) — microsecond latency cache, purpose-built for DynamoDB only

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-aurora-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../05-route53/README.md)

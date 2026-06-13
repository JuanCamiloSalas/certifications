[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../05-route53/README.md)

# Block 04 — RDS, Aurora & ElastiCache

> Managed relational databases and in-memory caching. **Aurora is the star** of the block and the highest-frequency topic.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [RDS](./01-rds.md) | Multi-AZ vs read replicas, backups, encryption, subnet groups |
| 02 | [RDS Proxy](./02-rds-proxy.md) | Connection pooling for Lambda/serverless, failover speedup |
| 03 | [Aurora](./03-aurora.md) | Shared storage, endpoints, Serverless, Multi-Master |
| 04 | [Aurora Advanced](./04-aurora-advanced.md) | Global Database, Backtrack, custom endpoints, ML integration |
| 05 | [ElastiCache](./05-elasticache.md) | Redis vs Memcached, caching patterns, session store |

## 🎯 Suggested concepts to cover

- RDS read replicas (up to 15, sync/async, cross-region)
- RDS Multi-AZ (HA, NOT scaling)
- RDS automatic backups vs manual snapshots
- RDS encryption: at rest (KMS) and in transit (SSL)
- RDS Proxy: use case (Lambda + RDS, fast failover)
- Aurora architecture (1 writer + up to 15 readers, shared storage)
- Aurora endpoints: writer / reader / custom
- Aurora Serverless v1 vs v2
- Aurora Global Database (cross-region, < 1s replication, < 1 min DR failover)
- Aurora Machine Learning, Aurora Backtrack
- ElastiCache Redis vs Memcached
- ElastiCache patterns: lazy loading vs write-through, TTL

## 🔗 Related comparisons

- RDS vs Aurora (when each)
- RDS Multi-AZ vs Read Replica
- Aurora endpoints: writer vs reader vs custom
- ElastiCache Redis vs Memcached
- Aurora Serverless v1 vs v2

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../05-route53/README.md)

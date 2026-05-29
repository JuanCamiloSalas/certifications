[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../15-vpc/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)

# Block 16 — Disaster Recovery & Migration

> **DR strategies, DMS, DataSync, Storage Gateway, Snow family.** Closing block of the course. Watch for the RTO/RPO trade-off questions.

## 🃏 Cards in this block

_No cards yet. Copy [`_TEMPLATE.md`](../_TEMPLATE.md) here to start._

| # | Card | Concept |
|---|---|---|

## 🎯 Suggested concepts to cover

### DR strategies (by RTO/RPO)
- Backup & Restore (highest RTO/RPO, lowest cost)
- Pilot Light
- Warm Standby
- Multi-Site / Hot Site (lowest RTO/RPO, highest cost)
- RTO vs RPO definitions (the basic exam trap)

### Migration tools
- AWS DMS: homogeneous and heterogeneous DB migration
- SCT (Schema Conversion Tool): paired with DMS
- AWS DataSync: large-scale data transfer (on-prem ↔ AWS, S3 ↔ EFS ↔ FSx)
- AWS Application Migration Service (MGN) — replaces SMS
- AWS Database Migration: replication continuous + change data capture
- AWS Snow family (Snowcone, Snowball Edge, Snowmobile)
- AWS Storage Gateway: File, Volume, Tape

### Other DR-related
- Aurora Global Database (already in Block 04)
- DynamoDB Global Tables (already in Block 11)
- Cross-region replication: S3 CRR, RDS Read Replicas, EBS snapshot copy

## 🔗 Related comparisons

- DR strategies side-by-side (RTO/RPO/cost)
- DMS vs DataSync vs Storage Gateway (when to use which)
- Snow family devices
- Storage Gateway: File vs Volume vs Tape

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../15-vpc/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)

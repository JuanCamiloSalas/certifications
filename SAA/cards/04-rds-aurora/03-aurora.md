[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-rds-proxy.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-aurora-advanced.md)

# Aurora — Architecture & Endpoints

> **Pitch (1 line):** AWS-proprietary MySQL/PostgreSQL-compatible DB with a shared distributed storage layer across 6 replicas in 3 AZs — up to 5× faster than MySQL, 3× faster than PostgreSQL.

## 🎯 When the exam picks this

- "high performance, high availability MySQL or PostgreSQL compatible" → **Aurora**
- "read scaling with up to 15 replicas, automatic failover" → **Aurora**
- "single writer, many readers sharing storage" → **Aurora**

## 🧠 Core (non-obvious bits)

**Storage:**
- Shared **distributed storage** across **6 copies** in **3 AZs** — 4/6 writes succeed (quorum), 3/6 reads succeed. No single AZ holds all data.
- Auto-scales storage from **10 GB to 128 TiB** in 10 GB increments. You don't manage storage capacity.
- Self-healing: AWS continuously scans for errors and replaces bad blocks in the background.

**Compute:**
- Up to **1 writer + 15 read replicas**. All share the same storage (reads are not lagging).
- Failover to a replica is **automatic and fast** (~30s) — replicas already have the data.
- Writer and replicas can be different instance sizes.

**Endpoints:**
- **Writer endpoint:** DNS that always points to the current primary writer. Clients use this for writes; it flips on failover.
- **Reader endpoint:** load-balanced across all replicas. Clients use this for reads.
- **Custom endpoints:** you define a subset of instances (e.g., larger replicas) to serve specific workloads (analytics).
- **Instance endpoints:** direct to a specific instance. Avoid in production — not failover-safe.

## 🔢 Numbers to memorize

- Storage: **10 GB → 128 TiB** (auto)
- Copies in storage: **6 (3 AZs × 2)**
- Max replicas: **15**
- Failover time: **~30s**
- Replication lag: **< 10ms** (much lower than RDS async replicas)

## ⚠️ Common traps

- "cross-region replication with low lag" → Aurora replicas are in-region; for cross-region → **Aurora Global Database** (next card).
- Reader endpoint balances reads; it does NOT fail over writes.
- Custom endpoints don't include the writer — create a separate writer endpoint usage pattern.

## 🔄 Easily confused with

- → [RDS](./01-rds.md) — standard managed RDS vs Aurora proprietary engine
- → [Aurora advanced](./04-aurora-advanced.md) — Serverless, Global DB, Backtrack

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-rds-proxy.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-aurora-advanced.md)

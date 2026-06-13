[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-aurora.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-elasticache.md)

# Aurora Advanced — Serverless, Global DB & Backtrack

<img src="../../assets/icons/aurora.png" width="64">

> **Pitch (1 line):** three Aurora capabilities that appear frequently in SAA scenario questions — Serverless for intermittent workloads, Global Database for cross-region DR, and Backtrack for point-in-time rewind without a restore.

## 🎯 When the exam picks this

- "database that scales to zero when idle" → **Aurora Serverless**
- "cross-region DR, < 1s replication, < 1 min failover" → **Aurora Global Database**
- "undo an accidental DELETE without a full restore" → **Aurora Backtrack**

## 🧠 Core (non-obvious bits)

**Aurora Serverless v2:**
- Automatically scales compute (ACUs — Aurora Capacity Units) up and down **instantly**, including to near-zero when idle.
- v2 scales continuously in fine-grained increments (unlike v1 which had cold starts). v2 is the current recommendation.
- Pay per ACU-second consumed. Great for: dev/test, infrequent or unpredictable workloads.
- Compatible with all Aurora features (Global DB, Multi-AZ, etc.).

**Aurora Global Database:**
- **1 primary region** (reads + writes) + up to **5 secondary regions** (reads only).
- Replication lag: **< 1 second** (storage-level replication, not logical).
- RTO for cross-region failover (promote secondary): **< 1 minute**.
- Use case: global apps requiring low-latency local reads, or multi-region DR.

**Aurora Backtrack:**
- Rewind the database **in place** to a previous point in time — no restore, no new cluster.
- Available for **Aurora MySQL** only (not PostgreSQL).
- Backtrack window: up to **72 hours**.
- Use case: accidental large-scale DELETE or schema change — rewind in seconds.

## 🔢 Numbers to memorize

- Global DB replication lag: **< 1s**
- Global DB secondary regions: up to **5**
- Global DB DR failover: **< 1 min**
- Backtrack window: up to **72 hours** (Aurora MySQL only)

## ⚠️ Common traps

- Backtrack ≠ restore from snapshot: Backtrack rewinds in place (fast, in seconds), restore creates a new cluster.
- Aurora Serverless v1 had cold start delays; v2 does not — if the exam asks about cold starts or delays, that's v1.
- Global Database secondary regions are **read-only** — writes always go to the primary.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-aurora.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-elasticache.md)

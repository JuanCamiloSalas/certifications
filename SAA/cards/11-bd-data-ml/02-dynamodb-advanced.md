[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-dynamodb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-dynamodb-indexes.md)

# DynamoDB Advanced — Streams, Global Tables, DAX, TTL & Transactions

<img src="../../assets/icons/dynamodb.png" width="64">

> **Pitch (1 line):** five DynamoDB features that each answer a specific scenario question — know the trigger phrase for each.

## 🎯 When the exam picks this

- "react to DynamoDB changes in real-time" → **DynamoDB Streams + Lambda**
- "multi-region active-active database" → **DynamoDB Global Tables**
- "sub-millisecond / microsecond read latency for DynamoDB" → **DAX**
- "automatically expire items after X time" → **TTL**
- "all-or-nothing operations across multiple items/tables" → **DynamoDB Transactions**

## 🧠 Core (non-obvious bits)

**DynamoDB Streams:**
- Ordered stream of item-level changes (INSERT, MODIFY, DELETE). Retained for **24 hours**.
- Consumers: **Lambda** (event source mapping — poll-based), **Kinesis Data Streams** (via Kinesis integration).
- Use cases: replication, auditing, cross-region sync, triggering workflows on data changes.

**Global Tables:**
- Multi-region, **active-active** replication — reads and writes in any region.
- Under the hood uses DynamoDB Streams for replication.
- Requires **DynamoDB Streams** to be enabled.
- Last-write-wins for conflict resolution.

**DAX (DynamoDB Accelerator):**
- In-memory cache **purpose-built for DynamoDB**. Sits between the app and DynamoDB.
- Reduces read latency from single-digit ms to **microseconds**.
- Caches individual items and query results. Write-through cache — writes go to DAX and DynamoDB simultaneously.
- Only for DynamoDB — not a general-purpose cache (use ElastiCache for that).

**TTL (Time To Live):**
- Define a timestamp attribute on items. DynamoDB deletes expired items automatically within **48 hours** (not instant).
- Free — no RCU consumed for TTL deletes.
- Use case: session data, temporary tokens, IoT data with rolling windows.

**Transactions:**
- ACID operations across **multiple items and tables** in a single all-or-nothing call.
- Operations: `TransactGetItems` / `TransactWriteItems`.
- Cost: **2× RCU/WCU**.

## ⚠️ Common traps

- DAX is for **read-heavy** DynamoDB workloads with microsecond requirements. For write-heavy or non-DynamoDB caching → ElastiCache.
- TTL deletes are **not instant** — can take up to 48 hours. Don't rely on it for strict expiry.
- Global Tables require **on-demand mode or provisioned with auto-scaling** in all regions — you can't mix.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-dynamodb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-dynamodb-indexes.md)

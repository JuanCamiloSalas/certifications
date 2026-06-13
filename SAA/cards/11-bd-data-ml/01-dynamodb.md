[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-dynamodb-advanced.md)

# DynamoDB — Fundamentals

<img src="../../assets/icons/dynamodb.png" width="64">

> **Pitch (1 line):** serverless, fully managed key-value / document NoSQL database — single-digit millisecond performance at any scale with no capacity planning in on-demand mode.

## 🎯 When the exam picks this

- "serverless NoSQL, massive scale, single-digit ms latency" → **DynamoDB**
- "session store, gaming leaderboard, IoT data, shopping cart" → **DynamoDB**
- "schema-flexible, key-value access pattern" → **DynamoDB**

## 🧠 Core (non-obvious bits)

**Data model:**
- **Table** → **Items** (rows) → **Attributes** (columns). No fixed schema beyond the key.
- **Primary key** (mandatory, uniquely identifies each item):
  - **Partition key only** (simple PK): uniform key distribution matters.
  - **Partition key + Sort key** (composite PK): items with the same partition key are grouped and sorted by the sort key.

**Capacity modes:**
- **Provisioned:** you set Read Capacity Units (RCU) and Write Capacity Units (WCU). Auto Scaling can manage them. Cheaper at predictable load.
- **On-Demand:** pay per request. No capacity planning. Automatically scales. More expensive per request. Use for spiky or unknown workloads.

**RCU / WCU (provisioned mode):**
- 1 RCU = 1 **strongly consistent** read/s for up to 4 KB, OR 2 **eventually consistent** reads/s for up to 4 KB.
- 1 WCU = 1 write/s for up to 1 KB.
- Transactional reads/writes consume 2× RCU/WCU.

**Consistency:**
- **Eventually consistent** (default): may return stale data (replicated asynchronously across AZs).
- **Strongly consistent**: always returns the most up-to-date data but costs 2× RCU and has higher latency.

## 🔢 Numbers to memorize

- Max item size: **400 KB**
- 1 RCU = strongly consistent read ≤ 4 KB / s (or 2× eventually consistent)
- 1 WCU = 1 write ≤ 1 KB / s

## ⚠️ Common traps

- "ACID transactions across DynamoDB tables" → **DynamoDB Transactions** (next card).
- DynamoDB is NOT relational — no JOINs, no complex queries. If the use case needs joins → RDS/Aurora.
- On-Demand mode is more expensive per request than Provisioned at consistent load.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-dynamodb-advanced.md)

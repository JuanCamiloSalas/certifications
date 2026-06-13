[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-dynamodb-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-other-dbs.md)

# DynamoDB Indexes — LSI vs GSI

<img src="../../assets/icons/dynamodb.png" width="64">

> **Pitch (1 line):** indexes let you query DynamoDB on attributes other than the primary key — LSI adds a sort key alternative at table creation; GSI adds a completely new partition/sort key at any time.

## 🎯 When the exam picks this

- "query by a different attribute within the same partition" → **LSI**
- "query by a completely different attribute (new partition key)" → **GSI**
- "need to add a new access pattern without recreating the table" → **GSI** (can add after creation)

## 🧠 Core (non-obvious bits)

| | LSI (Local Secondary Index) | GSI (Global Secondary Index) |
|---|---|---|
| **Partition key** | Same as base table | Can be any attribute (different from base table) |
| **Sort key** | Different from base table | Any attribute (optional) |
| **Creation** | At table creation ONLY | Anytime |
| **Throughput** | Shares table's RCU/WCU | Has its own RCU/WCU (separate provisioning) |
| **Consistency** | Strongly or eventually consistent | Eventually consistent only |
| **Storage scope** | Same partition as base item (local) | Across all partitions (global) |
| **Max per table** | **5 LSIs** | **20 GSIs** |

**Projected attributes:**
- When creating an index, you choose which attributes are projected (copied) into it: ALL, KEYS_ONLY, or INCLUDE (specific set).
- If you query the index and need a non-projected attribute, DynamoDB fetches it from the base table (extra read cost).

## ⚠️ Common traps

- LSI can only be created **at table creation** — you cannot add one later. GSI can be added anytime.
- GSI reads are **always eventually consistent** — you cannot request strongly consistent reads on a GSI.
- Sparse index: if many items don't have the GSI's partition/sort key, only those that do appear in the index — useful for filtering rare conditions cheaply.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-dynamodb-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-other-dbs.md)

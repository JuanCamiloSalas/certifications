[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-dynamodb-indexes.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-data-analytics.md)

# Other AWS Databases

> **Pitch (1 line):** six purpose-built DBs — pick by the **data model** the question describes: documents, graph, ledger, time-series, Cassandra-compatible, or Redis with durability.

## 🎯 When the exam picks this

- "MongoDB-compatible / JSON documents" → **DocumentDB**
- "graph relationships (social network, fraud detection, recommendation)" → **Neptune**
- "immutable, cryptographically verifiable ledger (blockchain-like audit)" → **QLDB**
- "Cassandra-compatible / wide-column" → **Keyspaces**
- "IoT / time-series data (sensor readings, metrics)" → **Timestream**
- "Redis with full durability + Multi-AZ" → **MemoryDB for Redis**

## 🧠 Core (non-obvious bits)

| Service | Data model | Key trait |
|---|---|---|
| **DocumentDB** | Document (JSON) | MongoDB-compatible; storage auto-scales; 3 AZs, 6 replicas |
| **Neptune** | Graph | Property graph + RDF; highly connected datasets; 3 AZs, up to 15 read replicas |
| **QLDB** | Ledger | Immutable journal; cryptographically verifiable history; serverless |
| **Keyspaces** | Wide-column | Cassandra-compatible; serverless; CQL API |
| **Timestream** | Time-series | Auto data tiering (memory → magnetic); 1,000× faster than relational for TS queries |
| **MemoryDB for Redis** | Key-value / data structures | Redis-compatible with **durable, transactional** writes; Multi-AZ; microsecond reads |

**MemoryDB vs ElastiCache Redis:**
- ElastiCache Redis: in-memory cache (data may be lost on failure; persistence optional but not primary design goal).
- MemoryDB: primary database — all writes are durably persisted to a Multi-AZ transaction log before ACK.

## ⚠️ Common traps

- "MongoDB workload" → DocumentDB (not DynamoDB — different model).
- "fraud detection / recommendation engine with relationships" → Neptune, not DynamoDB.
- QLDB is NOT blockchain — it's a centralized ledger managed by AWS. It's just cryptographically verifiable.
- MemoryDB is NOT a cache — it's a durable primary store that happens to use Redis API.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-dynamodb-indexes.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-data-analytics.md)

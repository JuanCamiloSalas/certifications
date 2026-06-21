[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../05-route53/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-s3-encryption.md)

# S3 Lifecycle Rules & Replication

<img src="../../assets/icons/s3.png" width="64">

> **Pitch (1 line):** Lifecycle rules automate transitioning objects to cheaper storage classes or deleting them on a schedule; replication (CRR/SRR) copies objects across buckets automatically.

## 🎯 When the exam picks this

- "move objects to Glacier after 90 days, delete after 7 years" → **Lifecycle rules**
- "replicate objects to another region for compliance or DR" → **CRR (Cross-Region Replication)**
- "replicate objects within the same region for log aggregation" → **SRR (Same-Region Replication)**

## 🧠 Core (non-obvious bits)

**Lifecycle rules:**
- Two action types: **Transition** (move to another storage class) and **Expiration** (delete objects or delete versions/delete markers).
- Storage class transition must follow the allowed waterfall: Standard → Standard-IA → Intelligent-Tiering → One Zone-IA → Glacier Instant Retrieval → Glacier Flexible → Glacier Deep Archive. You cannot go backwards.
- Can apply to a **prefix** or **object tags** — not just the whole bucket.
- **Minimum days in a class before transitioning**: Standard-IA requires 30 days in Standard; Glacier requires 30 days in Standard-IA (or 90 days directly from Standard if skipping IA).

**Glacier retrieval tiers (how fast you get archived data back):**
- **Glacier Instant Retrieval:** milliseconds (it's a storage class, not a retrieval job).
- **Glacier Flexible Retrieval:** **Expedited 1–5 min** · Standard 3–5 h · Bulk 5–12 h (free).
- **Glacier Deep Archive:** Standard ~12 h · Bulk ~48 h (no Expedited).
- **Provisioned retrieval capacity:** pre-purchase to **guarantee Expedited capacity** is available on demand (high, steady throughput) — the answer when you need sub-15-min retrieval *anytime* at scale.

**Replication (CRR / SRR):**
- **Versioning must be enabled** on both source and destination buckets.
- Replication is **asynchronous** — not instant.
- **CRR (Cross-Region):** compliance, latency reduction, cross-account replication.
- **SRR (Same-Region):** log aggregation, live replication between production and test.
- Only new objects uploaded after enabling replication are replicated. **Existing objects need S3 Batch Replication**.
- **Delete markers** are NOT replicated by default (can be enabled). Permanent deletes (MFA Delete) are never replicated.

## ⚠️ Common traps

- Replication is NOT bidirectional by default — must set up rules in both directions for bi-directional sync.
- Existing objects are NOT automatically replicated when you enable replication.
- "replicate delete markers" must be explicitly enabled — off by default.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../05-route53/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-s3-encryption.md)

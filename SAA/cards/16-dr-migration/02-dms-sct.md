[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-dr-strategies.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-datasync-mgn.md)

# DMS & SCT — Database Migration Service

<img src="../../assets/icons/dms.png" width="64">

> **Pitch (1 line):** DMS migrates databases to AWS with minimal downtime (including live cutover via CDC); SCT converts the schema from one engine to another when the source and target DB engines differ.

## 🎯 When the exam picks this

- "migrate on-prem Oracle/MySQL/PostgreSQL to AWS RDS with minimal downtime" → **DMS**
- "continuous replication from on-prem DB to AWS during migration" → **DMS with CDC**
- "convert Oracle schema to Aurora PostgreSQL schema" → **SCT first, then DMS**
- "homogeneous migration (MySQL → MySQL)" → **DMS only (no SCT needed)**

## 🧠 Core (non-obvious bits)

**DMS (Database Migration Service):**
- Runs on a **replication instance** (EC2) in AWS.
- Supports:
  - **Full load:** copies all existing data once.
  - **Full load + CDC (Change Data Capture):** copies existing data AND continuously replicates ongoing changes → near-zero-downtime migration.
  - **CDC only:** replicate changes only (source already populated in target).
- **Homogeneous:** same engine source → target (MySQL → MySQL, Oracle → Oracle). Only DMS needed.
- **Heterogeneous:** different engine (Oracle → Aurora). Need **SCT** to convert schema first, then DMS to move data.
- Source and target can be on-premises, EC2, or RDS/Aurora.

**SCT (Schema Conversion Tool):**
- Desktop application (download and run locally — not a cloud service).
- Converts stored procedures, views, triggers, and SQL syntax from one engine to another.
- Provides a conversion report showing what was auto-converted vs. what needs manual effort.
- Not needed when source and target are the same engine.

**Common migration patterns:**
| Source | Target | Tool |
|---|---|---|
| Oracle on-prem | Aurora PostgreSQL | SCT + DMS |
| MySQL on-prem | RDS MySQL | DMS only |
| SQL Server | Aurora MySQL | SCT + DMS |
| MongoDB | DynamoDB | DMS (with DocumentDB as intermediate or directly) |

## ⚠️ Common traps

- SCT is a client tool — it runs on your laptop/workstation, not in AWS.
- DMS replication instance must have network access to both source and target databases.
- "Minimal downtime" → DMS with CDC (not full load alone — full load would have a gap during the copy).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-dr-strategies.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-datasync-mgn.md)

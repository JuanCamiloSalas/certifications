[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-other-dbs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-ml-services.md)

# Data & Analytics Services

<img src="../../assets/icons/athena.png" width="64">

> **Pitch (1 line):** eight data services — pick by the keyword: SQL-on-S3 (Athena), data warehouse (Redshift), big data (EMR), serverless ETL (Glue), search (OpenSearch), BI (QuickSight), managed Kafka (MSK).

## 🎯 When the exam picks this

- "query data in S3 with SQL, no infrastructure" → **Athena**
- "petabyte-scale data warehouse, OLAP, columnar" → **Redshift**
- "run Hadoop / Spark / Hive on AWS" → **EMR**
- "serverless ETL, transform and load data" → **Glue**
- "search logs and documents, OpenSearch/Elasticsearch" → **OpenSearch Service**
- "business intelligence dashboards" → **QuickSight**
- "managed Apache Kafka" → **MSK**

## 🧠 Core (non-obvious bits)

**Athena:**
- Serverless SQL queries directly against **S3**. No data loading. Pay per TB scanned.
- Use **Parquet / ORC** columnar formats to reduce cost (scan less data).
- Integrates with **Glue Data Catalog** for table schemas.

**Redshift:**
- Columnar data warehouse. Optimized for **OLAP** (analytical queries), not OLTP.
- **Redshift Spectrum:** query S3 data directly from Redshift without loading it.
- **Cluster-based** (not serverless by default, though Redshift Serverless exists).
- Enhanced VPC routing to force traffic through VPC.

**EMR (Elastic MapReduce):**
- Managed cluster for **Hadoop, Spark, Hive, Presto**, etc.
- Runs on EC2 (On-Demand, Reserved, or Spot). Spot instances common for task nodes to save cost.
- Use case: large-scale batch processing, ML training, ETL.

**Glue:**
- Serverless **ETL** service. Discovers schema (Glue Crawlers), runs Spark-based transformations.
- **Glue Data Catalog:** central metadata repository (used by Athena, Redshift Spectrum, EMR).
- **Glue DataBrew:** visual data preparation (no-code).

**OpenSearch Service:**
- Managed Elasticsearch + Kibana (OpenSearch Dashboards).
- Full-text search, log analytics, anomaly detection.
- Commonly used as the "search" layer behind DynamoDB or S3.

**QuickSight:**
- Serverless BI tool. Connects to RDS, Redshift, Athena, S3, OpenSearch, and more.
- **SPICE:** in-memory engine that accelerates queries.
- Pay per session or per user.

**MSK (Managed Streaming for Kafka):**
- Fully managed Apache Kafka — create, manage, and scale Kafka clusters.
- Use when the app requires Kafka APIs (producers/consumers) and you don't want to manage brokers.

## ⚠️ Common traps

- Athena for ad-hoc queries on S3; Redshift for recurring analytics on a data warehouse.
- EMR vs Glue: EMR gives cluster-level control (any big data framework); Glue is serverless ETL only.
- OpenSearch is NOT a database — it's a search and analytics engine. Don't store primary data there.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-other-dbs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-ml-services.md)

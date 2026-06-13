[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)

# Block 11 — Advanced DB + Data + ML

> **DynamoDB, advanced NoSQL, Athena, Redshift, Glue, EMR, ML services.** Wide block. DynamoDB packs the most trap details.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [DynamoDB Fundamentals](./01-dynamodb.md) | Table/item/attribute, partition + sort key, RCU/WCU, capacity modes |
| 02 | [DynamoDB Advanced](./02-dynamodb-advanced.md) | Streams, Global Tables, DAX, TTL, Transactions |
| 03 | [DynamoDB Indexes](./03-dynamodb-indexes.md) | LSI vs GSI, creation timing, consistency, throughput |
| 04 | [Other AWS Databases](./04-other-dbs.md) | DocumentDB, Neptune, QLDB, Keyspaces, Timestream, MemoryDB |
| 05 | [Data & Analytics](./05-data-analytics.md) | Athena, Redshift, EMR, Glue, OpenSearch, QuickSight, MSK |
| 06 | [ML Services](./06-ml-services.md) | Rekognition, Transcribe, Polly, Comprehend, Lex, Textract, SageMaker |

## 🎯 Suggested concepts to cover

### DynamoDB
- Tables, primary key (partition key, partition + sort key)
- Capacity modes: provisioned vs on-demand
- Read capacity (RCU) and Write capacity (WCU) — how to calculate
- Strongly consistent vs eventually consistent reads
- DynamoDB Streams + Lambda triggers
- Global Tables (multi-region active-active)
- DAX (in-memory caching)
- TTL
- DynamoDB Indexes: LSI vs GSI
- Optimistic locking (conditional writes)
- DynamoDB Transactions

### Other DBs
- DocumentDB (MongoDB-compatible)
- Keyspaces (Cassandra-compatible)
- Neptune (graph)
- Timestream (time-series)
- QLDB (ledger)
- MemoryDB for Redis (Redis with durability)

### Data & Analytics
- Athena: SQL over S3, serverless, Parquet/ORC formats for cost
- Redshift: data warehouse, columnar, OLAP
- Redshift Spectrum (query S3 from Redshift)
- EMR: managed Hadoop/Spark
- Glue: serverless ETL, Glue Data Catalog
- OpenSearch (formerly Elasticsearch)
- QuickSight: BI
- MSK (managed Kafka)

### Machine Learning
- Rekognition (image/video)
- Transcribe (speech → text)
- Polly (text → speech)
- Translate
- Comprehend (NLP)
- Lex (chatbots)
- SageMaker (full ML)
- Forecast, Personalize, Textract, Kendra

## 🔗 Related comparisons

- DynamoDB vs RDS vs DocumentDB
- LSI vs GSI
- DynamoDB provisioned vs on-demand
- Athena vs Redshift vs Redshift Spectrum
- EMR vs Glue (Hadoop ETL vs serverless ETL)
- ML services by task (text, voice, vision)

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)

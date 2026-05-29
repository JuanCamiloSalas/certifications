[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)

# Bloque 11 — BD avanzadas + Data + ML

> **DynamoDB, NoSQL avanzado, Athena, Redshift, Glue, EMR, servicios de ML.** Bloque ancho. DynamoDB es el más cargado de detalles tramperos.

## 🃏 Cards de este bloque

_Sin cards aún. Copia [`_TEMPLATE.md`](../_TEMPLATE.md) aquí para empezar._

| # | Card | Concepto |
|---|---|---|

## 🎯 Conceptos sugeridos a cubrir

### DynamoDB
- Tablas, primary key (partition key, partition + sort key)
- Capacity modes: provisioned vs on-demand
- Read capacity (RCU) y Write capacity (WCU) — cálculo
- Strongly consistent vs eventually consistent reads
- DynamoDB Streams + Lambda triggers
- Global tables (multi-region active-active)
- DAX (caching in-memory)
- TTL
- DynamoDB Indexes: LSI vs GSI
- Optimistic locking (conditional writes)
- DynamoDB transactions

### Otras BD
- DocumentDB (MongoDB-compatible)
- Keyspaces (Cassandra-compatible)
- Neptune (graph)
- Timestream (time-series)
- QLDB (ledger)
- MemoryDB for Redis (Redis con durabilidad)

### Data & Analytics
- Athena: SQL sobre S3, serverless, formato Parquet/ORC para coste
- Redshift: data warehouse, columnar, OLAP
- Redshift Spectrum (query S3 desde Redshift)
- EMR: Hadoop/Spark managed
- Glue: ETL serverless, Glue Data Catalog
- OpenSearch (antes Elasticsearch)
- QuickSight: BI
- MSK (Kafka managed)

### Machine Learning
- Rekognition (imágenes/video)
- Transcribe (voz → texto)
- Polly (texto → voz)
- Translate
- Comprehend (NLP)
- Lex (chatbots)
- SageMaker (ML completo)
- Forecast, Personalize, Textract, Kendra

## 🔗 Comparativas relacionadas

- DynamoDB vs RDS vs DocumentDB
- LSI vs GSI
- DynamoDB provisioned vs on-demand
- Athena vs Redshift vs Redshift Spectrum
- EMR vs Glue (ETL Hadoop vs ETL serverless)
- Servicios ML por tarea (texto, voz, visión)

---

[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../10-serverless/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../12-monitoring/README.md)

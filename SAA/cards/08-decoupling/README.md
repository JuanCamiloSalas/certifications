[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../07-cdn/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../09-containers/README.md)

# Bloque 08 — Decoupling

> **SQS, SNS, Kinesis, Amazon MQ.** El examen ama preguntas del tipo "¿queue, pub-sub o stream?". Aprende a clasificar.

## 🃏 Cards de este bloque

| # | Card | Concepto |
|---|---|---|
| 01 | [SQS Standard](./01-sqs-standard.md) | Cola de mensajes desacoplada, throughput ilimitado, orden best-effort |

_Siguientes a crear: SQS FIFO, SNS, Kinesis Data Streams, Kinesis Firehose, Amazon MQ, patrón Fan-out._

## 🎯 Conceptos sugeridos a cubrir

- SQS Standard: throughput ilimitado, best-effort ordering, at-least-once delivery
- SQS FIFO: orden + dedupe, throughput 300 msg/s (3000 batch, 70k high-throughput)
- SQS: visibility timeout, long polling, DLQ, redrive policy
- SNS: pub/sub, topics, suscripciones (HTTP, email, Lambda, SQS, mobile)
- SNS FIFO topics
- Fan-out pattern: SNS → múltiples SQS
- Kinesis Data Streams: shards, retention, producer/consumer
- Kinesis Data Firehose: hacia S3 / Redshift / OpenSearch (near real-time)
- Kinesis Data Analytics
- Kinesis Video Streams
- Amazon MQ: ActiveMQ y RabbitMQ (lift & shift de apps con JMS/AMQP/MQTT)

## 🔗 Comparativas relacionadas

- **SQS vs SNS vs Kinesis vs Amazon MQ** (la más crítica del bloque)
- SQS Standard vs FIFO
- Kinesis Data Streams vs Firehose vs Data Analytics
- SNS vs SQS (cuándo añadir SQS detrás de SNS)

## 💡 Frases gatillo del bloque

- "decouple components" → **SQS**
- "fan-out / publish-subscribe" → **SNS** (o SNS + SQS)
- "real-time analytics on streaming data" → **Kinesis Data Streams**
- "ordering matters / no duplicates" → **SQS FIFO**
- "lift and shift con JMS/AMQP" → **Amazon MQ**
- "process data and deliver to S3 near real-time" → **Kinesis Firehose**

---

[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../07-cdn/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../09-containers/README.md)

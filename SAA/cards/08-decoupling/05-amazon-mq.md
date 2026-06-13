[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-kinesis.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../09-containers/README.md)

# Amazon MQ

> **Pitch (1 line):** managed message broker for **existing apps using industry-standard protocols** (AMQP, MQTT, STOMP, JMS) — lift-and-shift without rewriting to SQS/SNS.

## 🎯 When the exam picks this

- "existing on-premises app uses JMS / AMQP / MQTT / STOMP and needs to migrate to AWS" → **Amazon MQ**
- "lift-and-shift a message broker (ActiveMQ or RabbitMQ) to the cloud" → **Amazon MQ**
- "building a new app on AWS and need a message queue or pub/sub" → NOT MQ → SQS or SNS

## 🧠 Core (non-obvious bits)

- Runs **ActiveMQ** or **RabbitMQ** as managed services on dedicated instances.
- Supports standard protocols: **AMQP, MQTT, STOMP, OpenWire, WSS** — apps using these don't need code changes.
- NOT serverless — runs on EC2 instances. You pick the instance size.
- For **HA**: deploy with Multi-AZ (active/standby). Failover to standby in case of failure.
- **Throughput is lower** than SQS/SNS — SQS scales virtually unlimited; MQ is bound by instance size.
- Integrated with **VPC** — no public endpoint by default.

## ⚠️ Common traps

- "new cloud-native app that needs pub/sub or queuing" → SQS or SNS, NOT MQ (they scale infinitely and integrate natively with AWS).
- MQ is specifically for **migration scenarios** with legacy protocol dependencies.
- MQ does not auto-scale like SQS — you provision instance size upfront.

## 🔄 Easily confused with

- → [SQS](./01-sqs-standard.md) — native AWS, infinitely scalable, no legacy protocol support needed
- → [SNS](./03-sns-fanout.md) — native AWS pub/sub, not protocol-compatible with JMS/AMQP

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-kinesis.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../09-containers/README.md)

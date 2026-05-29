[![](https://img.shields.io/badge/<_Tips-FF4859?style=for-the-badge)](./README.md)

# Exam Trigger Phrases & Traps

> Add tips here AFTER each Dojo. Format: `> "trigger phrase" → service / answer`. Group by service family.

## 🌐 Networking (VPC, Route 53, CloudFront)

_(empty)_

## 💾 Storage (S3, EBS, EFS, FSx)

_(empty)_

## 🖥️ Compute (EC2, Lambda, ECS, EKS)

_(empty)_

## 🗄️ Databases (RDS, Aurora, DynamoDB, ElastiCache)

_(empty)_

## 📡 Decoupling (SQS, SNS, Kinesis, MQ)

> "decouple components" → **SQS**
> "ordering matters / no duplicates" → **SQS FIFO**
> "fan-out / publish-subscribe" → **SNS** (or SNS + SQS)
> "real-time analytics on streaming data" → **Kinesis Data Streams**
> "lift and shift with JMS/AMQP" → **Amazon MQ**
> "process data and deliver to S3 near real-time" → **Kinesis Firehose**

## 🔐 Security & Identity (IAM, KMS, Cognito, WAF)

_(empty)_

## 📈 Monitoring (CloudWatch, CloudTrail, Config, X-Ray)

_(empty)_

## 🔄 Migration & DR

_(empty)_

## ⚠️ Generic exam traps

- "Security Groups are STATEFUL, NACLs are STATELESS."
- "Lambda max execution: **15 min**. If the workload needs longer → ECS Fargate, not Lambda."
- "RDS Multi-AZ = high availability. RDS Read Replicas = scale reads. They are NOT the same."
- "Aurora Global Database: < 1s replication, < 1 min failover."

---

[![](https://img.shields.io/badge/<_Tips-FF4859?style=for-the-badge)](./README.md)

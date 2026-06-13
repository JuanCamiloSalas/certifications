[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)

# Block 12 — Monitoring & Auditing

> **CloudWatch, CloudTrail, X-Ray, Config, EventBridge.** The exam blends the big three (CloudWatch / CloudTrail / Config) — learn to separate them.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [CloudWatch](./01-cloudwatch.md) | Metrics, Logs, Alarms, Dashboards, CloudWatch Agent |
| 02 | [EventBridge](./02-eventbridge.md) | Event buses, rules, scheduled rules, schema registry |
| 03 | [CloudTrail](./03-cloudtrail.md) | API audit, management vs data events, trails, log integrity |
| 04 | [Config & X-Ray](./04-config-xray.md) | Compliance recorder, Config rules, remediation; distributed tracing |

## 🎯 Suggested concepts to cover

- CloudWatch Metrics: default vs custom, dimensions, statistics
- CloudWatch Alarms: states, actions (SNS, EC2, ASG)
- CloudWatch Logs: log groups, retention, subscription filters → Kinesis/Lambda
- CloudWatch Logs Insights
- CloudWatch Agent (on EC2 / on-prem)
- CloudWatch Synthetics and RUM
- EventBridge (formerly CloudWatch Events): event buses, rules, schedules
- CloudTrail: management events, data events, insights events
- CloudTrail multi-region, integration with S3 + CloudWatch Logs
- AWS Config: rules, conformance packs, remediation
- X-Ray: tracing, segments, subsegments, daemon
- AWS Health Dashboard

## 🔗 Related comparisons

- **CloudWatch vs CloudTrail vs Config** (critical)
- CloudWatch Logs vs CloudWatch Metrics vs CloudWatch Events/EventBridge
- CloudTrail management events vs data events

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)

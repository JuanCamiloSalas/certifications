[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-eventbridge.md)

# CloudWatch — Metrics, Logs, Alarms & Dashboards

> **Pitch (1 line):** AWS's native observability platform — collects metrics and logs from every service, fires alarms, and visualizes everything in dashboards.

## 🎯 When the exam picks this

- "monitor EC2 CPU / memory / disk, alert when threshold exceeded" → **CloudWatch Metrics + Alarm**
- "centralize application logs from EC2, Lambda, containers" → **CloudWatch Logs**
- "trigger an action when a metric crosses a threshold" → **CloudWatch Alarm**
- "custom metric not shown by default (RAM, disk usage)" → **CloudWatch Agent + custom metric**

## 🧠 Core (non-obvious bits)

**Metrics:**
- AWS services publish metrics automatically (CPU, NetworkIn/Out, etc.).
- **Default resolution:** 1-minute granularity. **High-resolution custom metrics:** up to 1-second granularity (extra cost).
- **EC2 default metrics:** CPU, Network, Disk I/O — but **NOT RAM or disk usage** (OS-level stats require the CloudWatch Agent).

**CloudWatch Agent:**
- Installed on EC2 (or on-premises) to collect **RAM, disk usage, processes**, and custom application logs.
- Also needed to send **logs** from EC2 (Logs Insights won't get them otherwise).

**Logs:**
- **Log Group** → **Log Stream** → log events.
- **Log retention:** configurable (1 day to never-expire). Default: never expire.
- **Logs Insights:** interactive query language for logs (like SQL for logs). Serverless, pay per query.
- **Subscription Filters:** stream logs in real-time to Lambda, Kinesis Data Streams, or Kinesis Firehose.
- Cross-account log aggregation: use subscription filters to send logs to a central account.

**Alarms:**
- States: **OK / ALARM / INSUFFICIENT_DATA**.
- Actions: SNS notification, EC2 action (stop/terminate/reboot/recover), Auto Scaling action.
- **Composite Alarms:** combine multiple alarms with AND/OR logic to reduce alarm noise.

**Dashboards:**
- Cross-region, cross-account widgets. Can be shared publicly (read-only URL).

## 🔢 Numbers to memorize

- Default EC2 metric interval: **1 minute** (Detailed Monitoring: **1 minute**, Basic: **5 minutes**)
- High-resolution custom metrics: up to **1 second**

## ⚠️ Common traps

- RAM and disk usage on EC2 are NOT collected by default — need the CloudWatch Agent.
- Alarms can only trigger actions for the **ALARM** state transition (not INSUFFICIENT_DATA, unless explicitly configured).
- CloudWatch is for AWS-native monitoring; for hybrid/multi-cloud, consider 3rd-party tools (but the exam usually stays AWS).

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-eventbridge.md)

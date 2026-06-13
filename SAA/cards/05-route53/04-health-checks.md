[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-routing-policies-2.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)

# Route 53 Health Checks

<img src="../../assets/icons/route53.png" width="64">

> **Pitch (1 line):** Route 53 health checkers continuously probe your endpoints and automatically remove unhealthy records from DNS responses in supported routing policies.

## 🎯 When the exam picks this

- "automatically stop routing to a failed endpoint" → **Health Check** + Failover/Weighted/Latency/Multi-Value
- "monitor a private resource (inside VPC) for health" → **Calculated or CloudWatch health check**

## 🧠 Core (non-obvious bits)

**Types of health checks:**
- **Endpoint health check:** Route 53 checkers (globally distributed) probe a public endpoint (HTTP/HTTPS/TCP). Healthy if ≥18% of checkers report healthy.
- **Calculated health check:** combines results of multiple child health checks using AND/OR/NOT logic. Use to aggregate the health of many endpoints into one status.
- **CloudWatch alarm health check:** health is determined by the state of a CloudWatch alarm — the only way to health-check **private resources** (inside VPCs) because Route 53 checkers cannot reach them directly.

**Private resources:**
- Route 53 health checkers are external — they can't reach private IPs.
- Solution: create a **CloudWatch metric/alarm** for the resource (e.g., EC2 CPU, custom app metric) → create a health check that watches that alarm.

**Health check + routing policies:**
- Failover: health check on primary is **mandatory**.
- Weighted / Latency / Multi-Value: health checks are optional but recommended — unhealthy records are excluded.
- Simple: health checks are **NOT supported**.

## ⚠️ Common traps

- "health check a private EC2" → must go through CloudWatch alarm, not direct endpoint check.
- Simple policy ignores health checks even if you create one — records are always returned.
- Health check failure threshold default: **3 consecutive failures**.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-routing-policies-2.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)

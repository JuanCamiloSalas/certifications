[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./07-direct-connect.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../16-dr-migration/README.md)

# VPC Flow Logs & IPv6

<img src="../../assets/icons/vpc.png" width="64">

> **Pitch (1 line):** Flow Logs capture IP traffic metadata at VPC/subnet/ENI level for troubleshooting and security analysis; IPv6 in VPC uses Egress-Only IGWs for outbound-only private IPv6 access.

## 🎯 When the exam picks this

- "diagnose why traffic is being dropped / allowed in the VPC" → **VPC Flow Logs**
- "security analysis of network traffic patterns" → **VPC Flow Logs → Athena / CloudWatch Logs Insights**
- "EC2 needs outbound IPv6 internet access but no inbound" → **Egress-Only Internet Gateway**

## 🧠 Core — VPC Flow Logs

**What they capture:**
- IP-level metadata: source/destination IP, port, protocol, packets, bytes, action (ACCEPT/REJECT), timestamp.
- Does NOT capture payload content — only metadata.
- **Scope:** can be enabled at VPC, subnet, or individual ENI level.

**Destinations:**
- **CloudWatch Logs:** real-time querying with Logs Insights.
- **S3:** lower cost, long-term storage, queryable with Athena.
- **Kinesis Data Firehose:** for real-time streaming to downstream systems.

**What flow logs don't capture:**
- Traffic to/from 169.254.169.254 (IMDS), 169.254.169.123 (NTP), DHCP, DNS within the VPC.
- Traffic from/to the VPC mirror traffic.

**Troubleshooting:**
- REJECT in flow logs + correct SG rules → check NACL.
- ACCEPT in flow logs but no response → check return traffic (NACL stateless, or ephemeral ports blocked).

## 🧠 Core — IPv6 in VPC

- All IPv6 addresses in AWS are **globally unique and public** — no NAT for IPv6.
- Dual-stack: VPC can have both IPv4 and IPv6 CIDR blocks.
- **Egress-Only Internet Gateway (EIGW):**
  - Allows IPv6 instances in private subnets to initiate outbound traffic to the internet.
  - Does NOT allow inbound connections from the internet.
  - Equivalent of NAT Gateway but for IPv6.
  - A regular IGW allows both inbound and outbound for IPv6 — if you want private outbound-only, use EIGW.

**IPv6 vs IPv4 in VPC:**
| | IPv4 | IPv6 |
|---|---|---|
| **Private outbound only** | NAT Gateway | Egress-Only IGW |
| **Public two-way** | IGW + public IP | IGW + IPv6 address |
| **Address space** | 32-bit, often private RFC1918 | 128-bit, always public in AWS |

## ⚠️ Common traps

- VPC Flow Logs record accepted AND rejected traffic — use the ACCEPT/REJECT field to identify drops.
- Flow Logs don't capture all traffic — IMDS, NTP, and DHCP are excluded.
- Egress-Only IGW is for IPv6 only — for IPv4 private outbound, use NAT Gateway.
- Even with an EIGW, the IPv6 instance must have a route `::0/0 → eigw` in its route table.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./07-direct-connect.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../16-dr-migration/README.md)

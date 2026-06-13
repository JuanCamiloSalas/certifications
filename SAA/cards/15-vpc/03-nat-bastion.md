[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-sg-nacl.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-vpc-endpoints.md)

# NAT Gateway, NAT Instance & Bastion Host

> **Pitch (1 line):** NAT Gateway lets private subnet instances initiate outbound internet traffic (e.g., to download patches) without exposing them inbound; Bastion Host provides SSH jump access into private instances.

## 🎯 When the exam picks this

- "private EC2 instances need to download OS updates from the internet" → **NAT Gateway**
- "SSH into private EC2 instances from the internet" → **Bastion Host (Jump Box)**
- "high-availability NAT, managed by AWS" → **NAT Gateway**
- "cost-conscious, single NAT, can do port forwarding" → **NAT Instance** (old approach)

## 🧠 Core — NAT Gateway

- Managed, highly available (within an AZ). **Deployed in the public subnet** — needs an Elastic IP.
- Private subnet route table: `0.0.0.0/0 → NAT Gateway`.
- **One NAT GW per AZ** for AZ-level redundancy (traffic from a private subnet in AZ-A should go through a NAT GW in AZ-A to avoid cross-AZ charges).
- Traffic flow: Private EC2 → NAT GW (public subnet) → IGW → internet.
- Outbound only — the internet cannot initiate connections to the private instances.
- Supports TCP, UDP, ICMP. Bandwidth: 5–45 Gbps (auto-scales).

**NAT GW vs NAT Instance:**
| | NAT Gateway | NAT Instance |
|---|---|---|
| **Management** | AWS managed | You manage (EC2) |
| **Availability** | Highly available in AZ | Single point of failure (unless you add failover) |
| **Bandwidth** | Up to 45 Gbps | Limited by instance type |
| **Security Groups** | Cannot attach | Can attach SGs |
| **Port forwarding** | No | Yes |
| **Bastion** | No | Can be used as bastion too |

## 🧠 Core — Bastion Host

- An EC2 instance in a **public subnet** used as an SSH/RDP jump server into private instances.
- SG on bastion: allow inbound 22 from your IP only.
- SG on private instances: allow inbound 22 from the bastion's SG (not the public internet).
- Modern alternative: **AWS Systems Manager Session Manager** — SSH into private EC2 with no bastion, no open port 22 needed.

## ⚠️ Common traps

- NAT Gateway is AZ-scoped — deploy one per AZ to avoid single point of failure and cross-AZ data transfer charges.
- NAT Gateway cannot be used as a bastion host — it only does NAT, not port forwarding or SSH.
- NAT Gateway is NOT free — charged per hour + per GB data processed.
- Bastion host with port 22 open to 0.0.0.0/0 is a security risk — restrict source IPs.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-sg-nacl.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-vpc-endpoints.md)

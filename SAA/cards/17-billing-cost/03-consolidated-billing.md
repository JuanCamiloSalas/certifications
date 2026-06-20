[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-cost-management-tools.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Deck_>-FF4859?style=for-the-badge)](../README.md)

# Consolidated Billing & Optimization

> **Pitch (1 line):** one bill for many accounts via Organizations, plus the services that recommend where to cut cost.

## 🎯 When the exam picks this

- "one bill for multiple accounts" → **Consolidated Billing (Organizations)**
- "volume discounts by combining usage across accounts" → **Consolidated Billing**
- "share Reserved Instances / Savings Plans across accounts" → **Consolidated Billing**
- "right-size / rightsizing recommendations" → **Compute Optimizer**
- "checks for underutilized resources / cost optimization" → **Trusted Advisor**

## 🧠 Core (non-obvious bits)

- **Consolidated Billing** (a feature of **AWS Organizations**) — one bill across all accounts; the **management (payer) account pays**. Member accounts stay independent for everything else.
- **Volume discounts** — aggregated usage across all accounts reaches **tiered pricing** thresholds faster (cheaper per unit).
- **RI / Savings Plans sharing** — unused RI/SP benefits are **shared across the organization's accounts** by default (can be turned off per account).
- **Compute Optimizer** — ML-based **rightsizing** recommendations (EC2, ASG, EBS, Lambda).
- **Trusted Advisor** — has a **Cost Optimization** category (idle/underutilized instances, unassociated EIPs, RI coverage).

## ⚠️ Common traps

- "1 bill + volume pricing + share RI/SP" → **Consolidated Billing**.
- **Who pays:** the **management/payer** account — not a member account (a common inverted distractor).
- "Recommend the right instance size" → **Compute Optimizer** (not Trusted Advisor, which flags but doesn't size precisely).

## 🔄 Easily confused with

- → [Organizations & SCPs](../13-iam-advanced/03-organizations-scps.md) — governance/guardrails; Consolidated Billing is the *billing* side of the same Organization.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-cost-management-tools.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Deck_>-FF4859?style=for-the-badge)](../README.md)

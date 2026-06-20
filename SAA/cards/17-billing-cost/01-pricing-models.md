[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../16-dr-migration/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-cost-management-tools.md)

# EC2 Pricing Models

> **Pitch (1 line):** the five ways to pay for compute — On-Demand, Reserved, Savings Plans, Spot, Dedicated — and the trigger phrase that points to each.

## 🎯 When the exam picks this

- "cost-effective" + "steady, predictable, long-term workload" → **Reserved / Savings Plans**
- "interruptible", "fault-tolerant", "batch / big data / CI" → **Spot**
- "short-term", "unpredictable", "uninterruptible but < 1 year" → **On-Demand**
- "BYOL", "per-socket/per-core licensing", "compliance, dedicated hardware" → **Dedicated Host**
- "flexible across instance families / regions / Fargate / Lambda" → **Savings Plans**

## 🧠 Core (non-obvious bits)

- **On-Demand** — pay per second/hour, no commitment. Default for short or spiky workloads.
- **Reserved Instances (RI)** — 1 or 3-year commitment for a discount.
  - **Standard RI**: biggest discount, **cannot** change instance family/OS/tenancy. **Can be sold on the RI Marketplace**.
  - **Convertible RI**: can **change family/OS/tenancy**, smaller discount.
  - Payment: All / Partial / No Upfront.
- **Savings Plans** — commit to a **$/hour** spend for 1/3 years (not to a specific instance).
  - **Compute SP**: most flexible — any family, any region, also **Fargate & Lambda**.
  - **EC2 Instance SP**: locked to a family in one region, bigger discount.
- **Spot** — up to 90% off, AWS can reclaim with a **2-minute warning**. Only for interruption-tolerant work.
- **Dedicated Host** — physical server, socket/core visibility, for **BYOL & compliance**. **Dedicated Instance** = dedicated hardware but no host visibility (can't do per-socket BYOL).

## 🔢 Numbers to memorize

- RI / Savings Plans commitment: **1 or 3 years**
- Spot interruption notice: **2 minutes**; discount up to **~90%**
- RI discount up to **~72%**
- RI Marketplace: **Standard RIs only** (not Convertible)

## ⚠️ Common traps

- "Interruptible / fault-tolerant / cheapest" → **Spot** (never for uninterruptible).
- "Short-term, uninterruptible, ~3 months" → **On-Demand** (RI minimum is 1 year).
- "Change family/OS/tenancy" → **Convertible RI**; "flexible incl. Fargate/Lambda" → **Compute Savings Plan**.
- "BYOL per socket / dedicated physical hardware for compliance" → **Dedicated Host** (not Dedicated Instance).
- **Decommissioned RI, stop charges:** stopping does **not** end RI billing → **terminate + sell on the RI Marketplace**.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../16-dr-migration/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-cost-management-tools.md)

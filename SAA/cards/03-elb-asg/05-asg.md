[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-elb-features.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)

# Auto Scaling Group (ASG)

> **Pitch (1 line):** automatically add or remove EC2 instances to match demand — defined by a launch template, min/desired/max counts, and scaling policies.

## 🎯 When the exam picks this

- "automatically scale EC2 instances based on CPU/request count/custom metric" → **ASG**
- "ensure a minimum number of healthy instances at all times" → **ASG**
- "run logic before an instance joins or leaves the ASG" → **ASG lifecycle hooks**

## 🧠 Core (non-obvious bits)

**Launch Templates (vs Launch Configurations):**
- **Launch Templates** (current): versioned, support mixed instance types (Spot + On-Demand), support T2/T3 unlimited. **Use this.**
- **Launch Configurations** (legacy): no versioning, single instance type. Still appears in older exam questions but AWS recommends migrating to Launch Templates.

**Scaling Policies:**
- **Target Tracking:** keep a CloudWatch metric (e.g., CPU) at a target value. AWS manages the alarms. Simplest to configure.
- **Step Scaling:** step-based rules triggered by CloudWatch alarm thresholds; different scale increments for different alarm severities.
- **Simple Scaling:** one action per alarm trigger; waits for cooldown before acting again. Legacy — prefer Target Tracking.
- **Scheduled Scaling:** predefined scale actions at set times (e.g., scale up every Friday 5PM).
- **Predictive Scaling:** ML-based; analyzes historical patterns and pre-scales before demand hits.

**Lifecycle Hooks:**
- Pause an instance in `Pending:Wait` (launching) or `Terminating:Wait` (terminating) to run custom actions (install agents, drain data, notify).
- Default timeout: 3600s. You complete the hook with `complete-lifecycle-action`.

**Multi-AZ behavior:**
- ASG spans multiple AZs. If an AZ becomes unhealthy, ASG re-launches instances in healthy AZs. This is how ASG provides HA.

## 🔢 Numbers to memorize

- Default cooldown period: **300s** (applies to Simple Scaling; Target Tracking manages its own)
- Default lifecycle hook timeout: **3600s**

## ⚠️ Common traps

- "scale in policies won't terminate instances being drained by the ELB" — ASG respects Connection Draining (Deregistration Delay) before terminating.
- "predictive scaling" ≠ scheduled — predictive uses ML and actual historical data; scheduled is manual cron.
- ASG does NOT auto-balance perfectly if Cross-Zone LB is off on the attached NLB.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-elb-features.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)

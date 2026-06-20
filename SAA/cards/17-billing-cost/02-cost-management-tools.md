[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-pricing-models.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-consolidated-billing.md)

# Cost Management Tools

> **Pitch (1 line):** the toolset to see, track, budget, report and estimate AWS cost — each answers a different verb in the question.

## 🎯 When the exam picks this

- "**track / categorize** cost by department / project / team" → **Cost Allocation Tags**
- "**alert** when a budget / threshold is exceeded" → **AWS Budgets**
- "**visualize / explore / forecast** cost trends" → **Cost Explorer**
- "**programmatically** access and forecast cost" → **Cost Explorer API**
- "**most detailed / granular** billing dataset" → **Cost and Usage Report (CUR)**
- "**estimate** cost before deploying" → **Pricing Calculator**

## 🧠 Core (non-obvious bits)

- **Cost Explorer** — visualize and analyze cost/usage with built-in **forecasting**. Has an **API** for programmatic access (the answer when a report tool must pull cost data with least overhead).
- **AWS Budgets** — **reactive**: alerts (and **budget actions** like applying an SCP/stopping resources) when cost/usage crosses a threshold. Not for analysis.
- **Cost and Usage Report (CUR)** — the **most comprehensive, line-item** billing dataset; delivered to **S3**, queried with Athena/Redshift/QuickSight.
- **Cost Allocation Tags** — tags (AWS-generated or user-defined) activated in the Billing console to **break down and track** cost by dimension. Tagging alone isn't enough — you must **activate** the tags.
- **Pricing Calculator** — estimate a workload's cost **before** building it.

## ⚠️ Common traps

- "Categorize / track cost by department" → **Cost Allocation Tags** (NOT Budgets, NOT Cost Explorer).
- "Alert when budget exceeded" → **Budgets**.
- "Programmatic cost data + forecast, least overhead" → **Cost Explorer API** (not Budgets+SNS, not CSV exports).
- "Most detailed billing data" → **CUR**.

## 🔄 Easily confused with

- **Cost Explorer vs Budgets:** Explorer = *analyze & forecast*; Budgets = *alert & act on thresholds*.
- **Cost Allocation Tags vs CUR:** Tags = *group cost by your own dimensions*; CUR = *raw, full-detail dataset*.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-pricing-models.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-consolidated-billing.md)

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-iac.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-declarative-vs-imperative.md)

# Benefits of IaC / Terraform

> **Pitch (1 line):** codifying infra buys you version control, automation, collaboration, scalability, and consistency.

## 🎯 What the exam tests

- Recognizing the canonical benefits when they're reworded (e.g. "reduce configuration drift" → consistency/repeatability).
- Which benefit solves which pain: audit trail → version control; team review → collaboration; no snowflake servers → consistency.

## 🧠 Core (non-obvious bits)

- **Version control & auditability** — infra changes live in Git: history + ability to revert.
- **Collaboration** — infra reviewed via pull requests, like app code (fewer silos).
- **Automation & efficiency** — less manual work, faster deploys.
- **Scalability & flexibility** — scale up/down by editing code, not touching resources by hand.
- **Consistency & repeatability** — same result across environments → **reduces configuration drift** and human error.

## ⚠️ Common traps

- "Reduce **configuration drift**" is IaC's headline benefit — drift = real infra diverging from the declared state.
- Version control of *infrastructure* (not just app code) is the differentiator vs manual provisioning.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-iac.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-declarative-vs-imperative.md)
</content>

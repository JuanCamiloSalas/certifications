[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-core-components.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-terraform-vs-other-tools.md)

# Desired State vs Current State

> **Pitch (1 line):** your config is the *desired state*; Terraform diffs it against the *current state* and applies only the delta.

## 🎯 What the exam tests

- That the config = **desired state** (the blueprint: resources, properties, relationships).
- That Terraform compares desired vs current (real-world) and makes only the changes needed.
- The vocabulary: desired state, current state, drift, reconcile.

## 🧠 Core (non-obvious bits)

- You declare the outcome; Terraform computes *how* to reach it (declarative → see block 01).
- **Current state** is what actually exists (tracked in the state file / refreshed from the provider).
- If reality already matches desired state → **no changes** (idempotent).
- **Drift** = real infra changed outside Terraform, so current ≠ desired → next plan shows the correction.

## 🔄 Easily confused with

- `plan` vs `refresh` — see [glosario](../../glosario.md) (`refresh` reconciles state with reality; `plan` computes the diff toward desired state).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-core-components.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-terraform-vs-other-tools.md)
</content>

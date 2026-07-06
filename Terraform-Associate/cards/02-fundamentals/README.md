[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../01-iac/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)

# Block 02 — Terraform fundamentals

> **Objetivo 2:** el propósito de Terraform y qué lo distingue de otras herramientas IaC. Conceptual, pero el examen pregunta por los beneficios concretos.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [What is Terraform?](./01-what-is-terraform.md) | Codify / standardize / platform-agnostic; uses HCL |
| 02 | [Core components](./02-core-components.md) | Core · Providers · Resources · State · Modules |
| 03 | [Desired vs current state](./03-desired-state.md) | Config = desired state; Terraform reconciles the diff |
| 04 | [Terraform vs other tools](./04-terraform-vs-other-tools.md) | IaC peers vs config-management (complementary) |
| 05 | [Terraform editions](./05-terraform-editions.md) | CLI (OSS) · HCP (SaaS) · Enterprise (self-hosted) |
| 06 | [HCL basics, style & `fmt`](./06-hcl-basics.md) | Block anatomy + style guide + `terraform fmt` |

> **Nota:** *resource referencing* (S3) vive en el bloque [`04-configuration`](../04-configuration/README.md) — es terreno del objetivo 4. Las cards conceptuales de este bloque **no llevan** `💻 Syntax / Example` (solo la 06, que es práctica, y la 05 con el bloque `cloud {}`).

## 🎯 Suggested concepts to cover

- ✅ Terraform is **cloud-agnostic / multi-cloud** via providers (one workflow, many platforms). → cards 01/04
- ✅ What a **provider** is and the role of the Terraform Registry. → card 02 _(registry deep-dive later in block 03)_
- ✅ Benefits of Terraform **state** (track real resources, plan diffs, metadata, performance). → cards 02/03 _(full state block = 06-state)_
- ✅ Terraform vs other IaC (e.g. provider-specific tools) — when Terraform's multi-cloud, declarative model wins. → card 04
- ✅ The Terraform language is **HCL** (HashiCorp Configuration Language). → card 06
- ✅ Terraform **editions** (CLI / HCP / Enterprise). → card 05

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- Terraform vs other IaC tools (provider-specific vs cloud-agnostic)

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../01-iac/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)

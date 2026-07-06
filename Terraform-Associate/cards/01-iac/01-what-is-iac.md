[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-iac-benefits.md)

# What is Infrastructure as Code (IaC)?

> **Pitch (1 line):** manage infrastructure in versioned config files instead of clicking around a console by hand.

## 🎯 What the exam tests

- The definition: IaC = provision & manage infra through machine-readable files, not manual/console steps.
- That IaC makes infra **repeatable, versioned, and reviewable** — the "why" behind the whole tool.
- Terraform's own tagline: automate **provisioning, management, and versioning** of infrastructure.

## 🧠 Core (non-obvious bits)

- IaC is a *practice*, not a specific tool — Terraform is one implementation of it.
- The config file **is the source of truth**; the real infra is expected to match it (you don't edit infra by hand).
- Terraform is **platform agnostic**: the same HCL workflow provisions any cloud/datacenter via providers.
- Caveat from the course: Terraform isn't magic — you still need to understand the **target platform** (AWS, Azure…) before you can codify it.

## 🔄 Easily confused with

- → [Declarative vs imperative](./03-declarative-vs-imperative.md) — IaC can be either; Terraform is declarative.

---

[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-iac-benefits.md)
</content>

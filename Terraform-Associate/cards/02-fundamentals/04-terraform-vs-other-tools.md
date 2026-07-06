[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-desired-state.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-terraform-editions.md)

# Terraform vs Other Tools

> **Pitch (1 line):** Terraform is an IaC tool — it competes with CloudFormation/Bicep/Pulumi and complements config-management tools like Ansible.

## 🎯 What the exam tests

- Sorting a named tool into **IaC (similar)** vs **configuration management (complementary)**.
- Terraform's differentiators: cloud-agnostic, declarative, **immutable infrastructure**, modular.

## 🧠 Core (non-obvious bits)

- **Similar (IaC, competitors):** AWS CloudFormation, Azure Bicep, Pulumi — provision & manage infra.
- **Different but complementary (config mgmt):** Ansible, Chef, Puppet — install packages, manage files/config *inside* hosts.
- IaC ≠ config management: Terraform builds the machine; config mgmt configures what runs on it (often used **together**).
- Terraform's edge over CloudFormation/Bicep: those are **vendor-locked**; Terraform is platform-agnostic.
- Terraform leans on **immutable infrastructure** (replace rather than mutate in place).

## 🔄 Easily confused with

- → [Terraform vs other tools (full table)](../../comparativas/terraform-vs-other-tools.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-desired-state.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-terraform-editions.md)
</content>

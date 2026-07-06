[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-terraform-vs-other-tools.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-hcl-basics.md)

# Terraform Editions

> **Pitch (1 line):** three ways to run Terraform — the open-source CLI, HCP Terraform (SaaS), and Terraform Enterprise (self-hosted).

## 🎯 What the exam tests

- Matching an edition to a description: "command-line, free, open source" vs "SaaS, hosted by HashiCorp" vs "self-hosted/managed in your own environment".
- That remote state, runs, private registry, and Sentinel policy come with HCP/Enterprise, not the bare CLI.

## 🧠 Core (non-obvious bits)

- **Command-Line Based** — Terraform CLI, open source, free; you manage state/backends yourself.
- **SaaS Platform** — **HCP Terraform** (formerly Terraform Cloud): remote runs, remote state, private module registry, VCS integration, Sentinel.
- **Self-Hosted & Managed** — **Terraform Enterprise**: the HCP feature set installed in your own infrastructure (air-gapped/compliance).
- HCP and Enterprise are the *same platform*, differing in where it runs (hosted vs self-hosted).

## 💻 Syntax / Example

```hcl
# The CLOUD block ties the CLI to HCP Terraform (SaaS) for remote state + runs.
terraform {
  cloud {
    organization = "my-org"
    workspaces { name = "prod" }
  }
}
# The bare CLI without this block just runs locally with a local/remote backend.
```

## 🔄 Easily confused with

- `terraform` (CLI) vs **HCP Terraform** (SaaS platform) — see [glosario](../../glosario.md).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-terraform-vs-other-tools.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-hcl-basics.md)
</content>

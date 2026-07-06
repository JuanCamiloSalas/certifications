[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-terraform.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-desired-state.md)

# Terraform Core Components

> **Pitch (1 line):** the five moving parts — Core, Providers, Resources, State, Modules.

## 🎯 What the exam tests

- Naming the five components and what each one does.
- Which piece talks to cloud APIs (**providers**) vs which tracks reality (**state**).

## 🧠 Core (non-obvious bits)

- **Terraform Core** — the engine (the `terraform` binary): reads config + state, builds the dependency graph, computes the plan.
- **Providers** — plugins that translate HCL into API calls for a platform (AWS, Azure, random, local…). Installed on `init`.
- **Resources** — the infra objects Terraform manages (a `resource` block = one managed object).
- **State** — the map between your config and real-world resources; how Terraform knows what already exists.
- **Modules** — reusable bundles of `.tf` files, invoked to avoid repetition and standardize patterns.

## ⚠️ Common traps

- **Providers ≠ resources.** Provider = the plugin/API client; resource = the thing it creates.
- **State is a core component**, not an optional extra — no state, no idea what exists.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-terraform.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-desired-state.md)
</content>

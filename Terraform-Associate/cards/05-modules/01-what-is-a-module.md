[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-module-block.md)

# What is a Module (root · parent · child)

> **Pitch (1 line):** a module is a **container of related resources** — a folder of `.tf` files — and the primary way to package and reuse configuration.

## 🎯 What the exam tests

- That **every** Terraform config has a **root module** = the directory where you run `terraform`.
- **Parent (calling) vs child**: the parent references/configures other modules; the **child** is the reusable component being called.
- That a module is just a **folder of `.tf` files** (conventionally `main.tf`, `variables.tf`, `outputs.tf`) — nothing more magical.
- Where children come from: **registry**, **Git repo**, or a **local path**.

## 🧠 Core (non-obvious bits)

- **Root module** = the working directory Terraform runs from. It becomes the **parent** as soon as it calls a child via a `module` block.
- **Child module** = the package being reused; it can itself call further children (nesting).
- A module groups resources into a **logical unit** (a "network" module, a "database" module) to reuse the same pattern repeatedly.
- Conventional files: **`main.tf`** (resources), **`variables.tf`** (inputs), **`outputs.tf`** (exposed values) — the filenames are convention, not requirements (all `.tf` merge).
- Value on the exam: modules enforce **consistent patterns** (naming, security) and enable **collaboration** (shared/approved building blocks).

## 💻 Syntax / Example

```
my-project/            # ROOT module (where you run terraform)
├── main.tf            #   calls the child via a module block
├── variables.tf
├── outputs.tf
└── modules/
    └── network/       # CHILD module (reusable)
        ├── main.tf
        ├── variables.tf   # its inputs
        └── outputs.tf     # values it exposes back
```

## ⚠️ Common traps

- The **root module always exists** — even a single `main.tf` with no `module` blocks is the root module.
- Conventional filenames (`main`/`variables`/`outputs`.tf) are **not enforced** — Terraform merges every `.tf` in the folder.

## 🔄 Easily confused with

- **Root vs child module** → [glosario](../../glosario.md) · sources in [module sources & versioning](./03-module-sources-and-versioning.md)

---

[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-module-block.md)

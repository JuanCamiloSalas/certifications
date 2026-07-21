[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-module-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-module-inputs-outputs-scope.md)

# Module Sources & Versioning

> **Pitch (1 line):** `source` picks where a module comes from — **registry**, **Git**, or **local path** — and `version` pins it, but **`version` only works for registry** modules.

## 🎯 What the exam tests

- The three main **source** types: **registry**, **Git repo**, **local path** — and how each `source` string looks.
- That **`version` applies only to registry** modules. Git pins with **`?ref=`**; local paths aren't versioned.
- The **registry address format**: `[<HOST>/]<NAMESPACE>/<NAME>/<PROVIDER>` (e.g. `terraform-aws-modules/vpc/aws`).
- Why you **pin** a version: modules evolve (new features, provider-API breaks) — pinning keeps runs reproducible.

## 🧠 Core (non-obvious bits)

- **Registry:** `source = "terraform-aws-modules/vpc/aws"` + `version = "~> 4.0"`. Public (`registry.terraform.io`) or private (HCP/Terraform Cloud, prefixed with a host).
- **Git:** `source = "github.com/org/repo//subdir?ref=v1.2.0"` — the **`?ref=`** picks a tag/branch/commit (there is **no `version` arg** for Git). `//` separates repo from a subdirectory.
- **Local:** `source = "./modules/network"` — a relative path, **no versioning** (it's the same repo), **not re-downloaded** on `init`.
- **Version constraints** reuse the provider operators: `= 4.0.1` (exact), `>= 4.0`, **`~> 4.0`** (pessimistic). → [terraform-block operators](../04-configuration/08-terraform-block.md)
- Registry/Git modules are downloaded on **`terraform init`**; local ones are read in place.

## 💻 Syntax / Example

```hcl
# Registry (version allowed):
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"   # NAMESPACE/NAME/PROVIDER
  version = "~> 4.0"
}

# Git (pin with ?ref=, NOT version):
module "app" {
  source = "github.com/my-org/modules//app?ref=v1.2.0"
}

# Local path (no version, not downloaded):
module "network" {
  source = "./modules/network"
}
```

## 🚩 Flags & values to memorize

- **`version` → registry only.** Git → `?ref=<tag/branch/commit>` · local → none.
- Registry `source` = `[HOST/]NAMESPACE/NAME/PROVIDER`.
- Git `source` uses `//` to point at a **subdirectory**.
- Operators: `=` exact · `>=` at-least · `~>` pessimistic.

## ⚠️ Common traps

- Putting **`version`** on a **Git or local** source → invalid; version is a **registry** feature.
- Local modules are **not re-downloaded** — editing them takes effect directly (but adding a new one still needs `init`).

## 🔄 Easily confused with

- → [module source types (registry vs Git vs local)](../../comparativas/module-source-types.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-module-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-module-inputs-outputs-scope.md)

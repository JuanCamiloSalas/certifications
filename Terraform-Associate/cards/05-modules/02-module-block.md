[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-a-module.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-module-sources-and-versioning.md)

# Calling Modules — the `module` Block

> **Pitch (1 line):** `module "name" { source = … }` calls a child module; `source` says where to get it and the other arguments are the **inputs** you pass in.

## 🎯 What the exam tests

- The required argument: **`source`** (every `module` block needs it). `version` is optional (registry only).
- That module arguments other than `source`/`version`/meta-args are the child's **input variables**.
- That you must run **`terraform init`** (or `terraform get`) to **download** modules before `plan`/`apply`.
- Meta-arguments (`count`, `for_each`, `depends_on`, `providers`) work on a `module` block too.

## 🧠 Core (non-obvious bits)

- **`source`** = where to download the module (registry address, Git URL, or local path). → [module sources & versioning](./03-module-sources-and-versioning.md)
- **Inputs**: any other argument (`name = var.vpc_name`) is passed to the child as an input variable. → [inputs, outputs & scope](./04-module-inputs-outputs-scope.md)
- **Download step:** `terraform init` fetches modules into `.terraform/modules/`. Add or change a module `source` → **re-run `init`** (or `terraform get`). A bare `plan` won't pull a newly-added module.
- **`count` / `for_each` on the module** instantiate it multiple times: `module.web["a"]`. → [count](../04-configuration/12-count-meta-argument.md) · [for_each](../04-configuration/13-for_each-meta-argument.md)
- Reference a module's outputs with **`module.<name>.<output>`**.

## 💻 Syntax / Example

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"   # where to download from
  version = "4.0.1"                            # registry only

  # everything below = inputs passed into the child module:
  name            = var.vpc_name
  cidr            = var.vpc_cidr_block
  azs             = ["us-west-2a", "us-west-2b"]
  private_subnets = ["10.0.1.0/24"]
  public_subnets  = ["10.0.101.0/24"]
}

# then: terraform init   (downloads the module)
# use an output: module.vpc.vpc_id
```

## 🚩 Flags & values to memorize

- **`source`** = required · **`version`** = optional (registry only).
- **`terraform init`** / `terraform get` downloads modules → into `.terraform/modules/`.
- Reference outputs: `module.<name>.<output>`.

## ⚠️ Common traps

- **Adding a `module` block then running `plan` fails** until you `terraform init`/`get` to download it.
- Arguments in the block are the child's **inputs** — they must match the child's declared `variable`s.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-what-is-a-module.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-module-sources-and-versioning.md)

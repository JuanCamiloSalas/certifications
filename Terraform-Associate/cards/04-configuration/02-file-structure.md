[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-resource-referencing.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-provider-block.md)

# File Structure & Organization

> **Pitch (1 line):** Terraform merges **all** `.tf` files in the working directory into one configuration; the common file names are **convention, not requirement**.

## 🎯 What the exam tests

- That Terraform loads **every** `.tf` file in the current working directory and treats them as one merged config (file split is for humans; order doesn't matter).
- That names like `main.tf` / `variables.tf` are **conventional only** — not required.
- Which files Terraform **generates/manages** (state, backup, lock) and which to git-ignore.

## 🧠 Core (non-obvious bits)

- **All `.tf` in the working dir = one config.** Terraform concatenates them. Only the **current** directory is processed — **subdirectories are not**, unless referenced as a `module`.
- **Conventional files:** `main.tf` (primary resources) · `variables.tf` (declarations) · `outputs.tf` · `providers.tf` (provider config/requirements) · `terraform.tfvars` (variable **values**).
- **Terraform-managed files:** `terraform.tfstate` (state) · `terraform.tfstate.backup` (previous state) · `.terraform.lock.hcl` (dependency lock — pins provider versions) · `.terraform/` (downloaded providers/modules).
- **`.gitignore`** typically excludes `*.tfstate*`, `.terraform/`, and `*.tfvars` (secrets) — but **keep `.terraform.lock.hcl`** (commit it).
- **Subdirectories** (`dev/`, `test/`, `prod/`) split environments into separate states → smaller **blast radius**.

## 💻 Syntax / Example

```text
aws_deploy/
├── .terraform.lock.hcl        # commit — pins provider versions
├── main.tf            ┐
├── variables.tf       │  all merged into ONE configuration
├── outputs.tf         │  (names are convention, not required)
├── providers.tf       ┘
├── terraform.tfvars           # variable values (usually git-ignored)
├── terraform.tfstate          # state (git-ignored; use a remote backend)
└── terraform.tfstate.backup
```

## ⚠️ Common traps

- Terraform reads **only the current working dir**, not nested folders — those need an explicit `module` reference.
- Putting everything in a single `main.tf` works **identically** to splitting files.
- **Do commit `.terraform.lock.hcl`**; do **not** commit `*.tfstate` (plaintext secrets) or `*.tfvars`.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-resource-referencing.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-provider-block.md)

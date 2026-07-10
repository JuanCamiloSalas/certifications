[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-variable-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-output-block.md)

# Assigning Variable Values & Precedence

> **Pitch (1 line):** a variable's value can come from several sources; when more than one sets it, Terraform applies a **fixed order of precedence** — CLI `-var` always wins.

## 🎯 What the exam tests

- The **order of precedence** (a favorite exam question — memorize it cold).
- That **`-var` / `-var-file` override everything**, and block defaults are the lowest.
- That `terraform.tfvars` / `*.auto.tfvars` are **auto-loaded**; other `*.tfvars` need `-var-file`.

## 🧠 Core — precedence (LOW → HIGH)

1. **Variable block `default`** — lowest
2. **Environment variables** `TF_VAR_<name>`
3. **`terraform.tfvars`** (and `terraform.tfvars.json`)
4. **`*.auto.tfvars`** / `*.auto.tfvars.json` — loaded in **alphabetical** order
5. **`-var` / `-var-file`** on the CLI — **highest, always wins**

- **Auto-loaded files:** `terraform.tfvars` and any `*.auto.tfvars`. A differently-named file (e.g. `prod.tfvars`) must be passed with **`-var-file=prod.tfvars`**.
- Within the same tier, later sources override earlier (`*.auto.tfvars` alphabetical; multiple `-var` = last one wins).
- `-var` is ideal for **quick, temporary** overrides without editing files.

## 💻 Syntax / Example

```bash
export TF_VAR_region="us-east-1"          # tier 2 (env var)
# terraform.tfvars contains:  region = "us-west-1"   → tier 3 (auto-loaded)
terraform apply -var="region=eu-west-1"    # tier 5 → THIS value wins
```

## 🚩 Flags & values to memorize

- Precedence low→high: **default < `TF_VAR_*` < `terraform.tfvars` < `*.auto.tfvars` < `-var`/`-var-file`**.
- `terraform.tfvars` & `*.auto.tfvars` **auto-load**; custom names need `-var-file`.
- `*.auto.tfvars` load in **alphabetical** order.

## ⚠️ Common traps

- **CLI `-var` beats a `.tfvars` file** — don't assume the file wins.
- A file named `prod.tfvars` is **not** auto-loaded (only `terraform.tfvars` / `*.auto.tfvars` are).

## 🔄 Easily confused with

- The `TF_VAR_*` env-var mechanism itself → [environment variables](../03-core-workflow/09-environment-variables.md).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-variable-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-output-block.md)

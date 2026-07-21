[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./15-securing-secrets.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./17-secrets-env-vars-and-external-sources.md)

# Sensitive Variables & Outputs

> **Pitch (1 line):** `sensitive = true` **masks** a value in plan/apply output and logs — it is *hide from logs*, **not** *encrypt*.

## 🎯 What the exam tests

- That `sensitive = true` works on both **`variable`** and **`output`** blocks.
- **What it DOES:** hides the value in `plan`/`apply` output (`(sensitive value)` / `<sensitive>`), logs, and error messages.
- **What it DOESN'T:** the value is **still in state as plaintext**, **still sent to the provider**, and it's **not encryption**.
- That an `output` consuming a sensitive value must itself be marked `sensitive` (or Terraform errors).

## 🧠 Core (non-obvious bits)

- **Output masking only.** Think "keep it out of the logs", never "the data is protected".
- **Still in state:** anyone who can read `terraform.tfstate` sees it in cleartext → you still need [state security](../06-state/08-securing-state-files.md) and/or [ephemeral values](./18-ephemeral-values-and-write-only-arguments.md).
- **Propagation:** if you feed a sensitive value into an `output`, that output must be `sensitive = true` too — Terraform refuses to silently expose it.
- **Still transmitted** to the provider (it has to be, to create the resource).
- Combine with **env vars** (keep out of files) — `sensitive` and `TF_VAR_*` are complementary. → [env vars & external sources](./17-secrets-env-vars-and-external-sources.md)

## 💻 Syntax / Example

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}

output "db_password" {
  value     = var.db_password
  sensitive = true          # required, or Terraform errors on a sensitive value
}
```

```text
# plan / apply output:
+ password = (sensitive value)
db_password = <sensitive>
```

## ⚠️ Common traps

- **`sensitive` ≠ encryption.** It does **not** remove the value from **state** (plaintext).
- The value **is still sent to the provider** and stored — masking is cosmetic (logs/output).
- Forgetting `sensitive` on a downstream `output` → plan **error** ("Output refers to sensitive values").

## 🔄 Easily confused with

- → [secret protection techniques](../../comparativas/secret-protection-techniques.md) (sensitive vs env vars vs external vs ephemeral)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./15-securing-secrets.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./17-secrets-env-vars-and-external-sources.md)

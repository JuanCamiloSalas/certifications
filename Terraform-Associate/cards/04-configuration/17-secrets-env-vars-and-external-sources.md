[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./16-sensitive-variables-and-outputs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./18-ephemeral-values-and-write-only-arguments.md)

# Secrets via Environment Variables & External Sources

> **Pitch (1 line):** keep secrets **out of files/git** by injecting them as `TF_VAR_*` env vars or reading them from an external secret manager — but note both **still land in state**.

## 🎯 What the exam tests

- **`TF_VAR_<name>`** injects a variable's value from the environment — no `default`, nothing committed.
- That env vars are great for **CI/CD** (GitHub Secrets injected at runtime) and work with `sensitive = true`.
- **External sources** (AWS Secrets Manager, Azure Key Vault, GCP Secret Manager, **HashiCorp Vault**) read the secret at runtime via a provider/data source — not in `.tf`.
- The shared caveat: env vars and external sources **still write the value into state** (fix that with [ephemeral/write-only](./18-ephemeral-values-and-write-only-arguments.md)).

## 🧠 Core (non-obvious bits)

- **Env vars:** `export TF_VAR_db_password=…` → Terraform reads it automatically. Never in files, never in git, ideal for pipelines. → [environment variables](../03-core-workflow/09-environment-variables.md)
- **External secret managers:** a `data` source pulls the secret at apply time → single source of truth, centralized rotation & access control. Same pattern across Secrets Manager / Key Vault / Vault.
- **Both still hit state:** reading a secret into a normal resource argument persists it in `terraform.tfstate`. Only **ephemeral values / write-only arguments** avoid that.
- **Vault dynamic credentials** (the strongest pattern): instead of long-lived static creds, Vault mints **short-lived** credentials on demand (TTL of minutes), auto-revoked at expiry, limited scope. Devs never hold cloud creds; the attack surface shrinks. With **ephemeral resources**, those creds aren't written to state.

## 💻 Syntax / Example

```bash
# Env var — no default in the variable block, nothing committed:
export TF_VAR_db_password="MyP@ssw0rd!"
terraform apply
```

```hcl
# External source — read at runtime (still lands in state):
data "aws_secretsmanager_secret_version" "db" {
  secret_id = "prod/db/password"
}

resource "aws_db_instance" "main" {
  password = data.aws_secretsmanager_secret_version.db.secret_string
}
```

## 🚩 Flags & values to memorize

- `TF_VAR_<name>` — env-var form of a variable; **low precedence** (`-var`/`.tfvars` beat it).
- Static creds = long-lived/risky · Vault **dynamic creds** = short-lived (minutes), auto-revoked.

## ⚠️ Common traps

- Env vars and external sources keep secrets out of **git**, **not** out of **state**.
- A secret read via a `data` source is **still stored in state** in cleartext.

## 🔄 Easily confused with

- → [secret protection techniques](../../comparativas/secret-protection-techniques.md) · state-avoidance → [ephemeral & write-only](./18-ephemeral-values-and-write-only-arguments.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./16-sensitive-variables-and-outputs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./18-ephemeral-values-and-write-only-arguments.md)

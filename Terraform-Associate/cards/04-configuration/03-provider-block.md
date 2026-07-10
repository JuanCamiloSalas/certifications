[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-file-structure.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-resource-and-data-blocks.md)

# Provider Block (`provider`)

> **Pitch (1 line):** the `provider` block configures a plugin that lets Terraform talk to an API-driven platform (AWS, Azure, GitHub…); `alias` runs several configs of the same provider.

## 🎯 What the exam tests

- That authentication (keys/tokens) should come from **environment variables**, not be hardcoded in the block.
- That **one** provider block can manage **many** resources on that platform.
- The **`alias`** + `provider = <name>.<alias>` pattern for multi-region / multi-account.

## 🧠 Core (non-obvious bits)

- **`provider "<name>" { ... }`** — name is set by the provider's maintainer (`aws`, `azurerm`). Arguments (region, profile…) come from the provider docs on **registry.terraform.io**.
- **Auth via env vars, not HCL:** put `AWS_ACCESS_KEY_ID` etc. in the environment; hardcoding creds in the block is a security anti-pattern.
- A **single** provider block enables all that platform's resources (one `aws` provider → EC2 + S3 + EKS…).
- Providers are **downloaded on `terraform init`** to the machine running Terraform (plugin code lives on GitHub; docs on the Registry).
- **`alias`** defines an additional configuration of the same provider; a resource opts in with **`provider = aws.<alias>`**. Used for multi-region or multi-account (dev vs prod).
- Provider **version** is pinned in `required_providers` (inside the `terraform` block), **not here** → [terraform-block](./08-terraform-block.md).

## 💻 Syntax / Example

```hcl
provider "aws" {
  region = "us-east-1"          # default provider (no alias)
}

provider "aws" {
  alias  = "prod"               # a second configuration of the same provider
  region = "us-west-1"
}

resource "aws_s3_bucket" "dev" {
  bucket = "my-dev-bucket"      # uses the default provider
}

resource "aws_s3_bucket" "prod" {
  provider = aws.prod           # explicitly opt into the aliased provider
  bucket   = "my-prod-bucket"
}
```

## ⚠️ Common traps

- Don't hardcode credentials in the provider block — use **env vars**.
- **Version constraints live in `required_providers`** (terraform block), not the provider block.
- Without `provider = aws.<alias>`, a resource uses the **default** (unaliased) provider.

## 🔄 Easily confused with

- **`provider` block** (config: region/auth/alias) vs **`required_providers`** (source + version pin, inside the `terraform` block) → [terraform-block](./08-terraform-block.md).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-file-structure.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-resource-and-data-blocks.md)

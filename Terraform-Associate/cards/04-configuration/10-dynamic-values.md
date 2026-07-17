[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./09-built-in-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./11-locals.md)

# Dynamic Values (interpolation & data sources)

> **Pitch (1 line):** replace hardcoded values with expressions — **interpolation `${…}`**, variables, `local`s, functions, and **data sources** — so one config adapts instead of repeating itself.

## 🎯 What the exam tests

- What **interpolation** is: `${…}` evaluates the expression, converts the result, and inserts it **into a string**.
- That `${…}` is **only needed inside a string** — a bare reference uses no `${}` in modern HCL.
- That a **data source** (`data` block) **only reads** — it never creates or changes infrastructure.
- Recognizing "dynamic code" = interpolation + variables + locals + functions + data sources + meta-arguments (vs hardcoded static values).

## 🧠 Core (non-obvious bits)

- **Interpolation** = string templating: `"server-${var.env}"`. Outside a string you reference directly: `instance_type = var.size` (no `${}`). → [resource-referencing](./01-resource-referencing.md)
- **Data sources are read-only.** They query provider info about **existing** things (region, AMI, account id) so you can use it without hardcoding — no infra is created. Address: `data.<type>.<name>.<attr>`.
- Dynamic value = compose sources: `"${var.app}-${local.env}-${data.aws_region.current.name}"` beats three separate hardcoded strings.
- Common "avoid hardcoding" wins: current **region**/**account id** via data sources, environment/prefix via `var`/`local`.
- You can nest functions inside interpolation: `"${upper(var.env)}-app"`.

## 💻 Syntax / Example

```hcl
variable "environment" { type = string, default = "dev" }

data "aws_region" "current" {}                 # read-only lookup
data "aws_caller_identity" "current" {}         # read-only lookup

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id                       # bare ref, no ${}
  instance_type = var.instance_type
  tags = {
    Name = "server-${data.aws_region.current.name}-${var.environment}"
    # => "server-us-east-1-dev"
  }
}

# bucket_name = "s3-${data.aws_caller_identity.current.account_id}-backups"
#            => "s3-9876543210-backups"
```

## ⚠️ Common traps

- `${…}` is **only for inside strings**. `x = "${var.y}"` where you could write `x = var.y` is redundant (older style).
- A **`data` source does not create anything** — if a question says a data block provisions a resource, it's wrong.
- Values from a data source may only be **known after apply** if they depend on something not yet created — plan shows them as computed.

## 🔄 Easily confused with

- **Input variable vs local value** (both feed dynamic values) → [locals](./11-locals.md) · [glosario](../../glosario.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./09-built-in-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./11-locals.md)

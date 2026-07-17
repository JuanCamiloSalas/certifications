[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./10-dynamic-values.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./12-count-meta-argument.md)

# Local Values (`locals`)

> **Pitch (1 line):** named values computed **inside** the config, defined once in a `locals` block and reused with `local.<name>` — the fix for a repeated value or expression.

## 🎯 What the exam tests

- The **plural/singular split**: you **define** in a **`locals {}`** block but **reference** with **`local.<name>`** (singular).
- That locals are **computed inside** the config and **cannot be set from outside** (no CLI/`.tfvars`/env) — unlike variables.
- When to use a local: a value/expression repeated across resources, or a derived value built from vars + data.

## 🧠 Core (non-obvious bits)

- **Define plural, use singular:** `locals { env = "dev" }` → reference `local.env`. Mixing them up is a classic exam trap.
- **Not an input.** A local can't be overridden at runtime — it's internal. Use a **variable** for outside input, a **local** for computed/derived values. → [glosario](../../glosario.md)
- A local can reference **variables, data sources, functions, and other locals** — great for a single source of truth (prefix, `common_tags`).
- Change it **once** in the `locals` block and every reference updates → less risk than editing N hardcoded copies.
- You can have **multiple `locals` blocks** in a config; all names share one namespace.

## 💻 Syntax / Example

```hcl
locals {
  env    = "dev"
  prefix = "${var.app}-${local.env}"        # a local referencing another local
  common_tags = {
    Environment = local.env
    ManagedBy   = "terraform"
  }
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type
  tags = merge(local.common_tags, {
    Name = "${local.prefix}-server"          # => "myapp-dev-server"
  })
}
```

## ⚠️ Common traps

- **`locals`** (block, plural) vs **`local.`** (reference, singular) — know which is which.
- A local is **not settable** via `-var` / `.tfvars` / `TF_VAR_*` — that's only for `variable`s.
- Don't over-local: a value used once, straight from a variable, doesn't need a local.

## 🔄 Easily confused with

- **Input variable vs local value** → [glosario](../../glosario.md) (variable = from outside · local = computed inside)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./10-dynamic-values.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./12-count-meta-argument.md)

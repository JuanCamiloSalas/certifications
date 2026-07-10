[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-provider-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-variable-block.md)

# Resource & Data Blocks

> **Pitch (1 line):** `resource` **creates/manages** infrastructure; `data` **reads** existing infrastructure without managing it — both are addressed as `"<type>" "<name>"`.

## 🎯 What the exam tests

- The distinction: **resource = create/update/delete**; **data = read-only lookup** (creates nothing).
- That the resource **type** is provider-defined and the **name** is yours, **unique per config**.
- Resource **name rules** and how a `data` block queries (constraints/filters).

## 🧠 Core (non-obvious bits)

- **`resource "<type>" "<name>" { args }`** — type from the provider (e.g. `aws_instance`), name is a user string **unique per configuration**. Arguments come from provider docs. Address = `<type>.<name>`.
- **`data "<type>" "<name>" { query }`** — retrieves attributes of something that **already exists** (a VPC, an AMI, a cluster) **without creating it**. Reference with `data.<type>.<name>.<attr>`.
- **Resource name rules:** must start with a **letter or underscore**; may contain only **letters, digits, underscores, and dashes**.
- A data block's body holds **query constraints** (e.g. a `filter { name / values }`) that pick which existing object to read.
- Data blocks **avoid hardcoding** — pull a real ID at plan time instead of pasting a literal.

## 💻 Syntax / Example

```hcl
# READ an existing VPC (creates nothing)
data "aws_vpc" "prd" {
  filter {
    name   = "tag:Name"
    values = ["prd-vpc"]
  }
}

# CREATE a subnet inside that VPC
resource "aws_subnet" "pub" {
  vpc_id     = data.aws_vpc.prd.id     # data.<type>.<name>.<attr>
  cidr_block = "10.0.6.0/24"
}
```

## ⚠️ Common traps

- **`data` never creates or destroys** anything — it only reads. "Reference an existing resource not managed by this config" → **data source**.
- Resource **name** must be unique per config; the **type** is fixed by the provider (you can't invent it).

## 🔄 Easily confused with

- → [Resource referencing](./01-resource-referencing.md) (how attributes wire blocks into implicit dependencies) · [glosario](../../glosario.md) (resource vs data source).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-provider-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-variable-block.md)

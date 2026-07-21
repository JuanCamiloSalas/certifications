[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-depends-on.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)

# `lifecycle` Meta-Argument

> **Pitch (1 line):** a nested block inside a resource that changes **how Terraform creates, replaces, and destroys** it — `create_before_destroy`, `prevent_destroy`, `ignore_changes`, `replace_triggered_by`.

## 🎯 What the exam tests

- What each option does — especially **`create_before_destroy`** (zero-downtime) and **`prevent_destroy`** (block deletion).
- **`ignore_changes`** — ignore drift on listed attributes (or `all`).
- **`replace_triggered_by`** — force replacement when another resource/attribute changes.
- That `lifecycle` can also hold **`precondition`/`postcondition`** (a validation concern → separate card).

## 🧠 Core (non-obvious bits)

- **`create_before_destroy = true`** → build the replacement **first**, then destroy the old one (zero-downtime replaces). Default is the reverse (destroy-then-create).
- **`prevent_destroy = true`** → any plan that would destroy the resource **errors out**. Guardrail for critical infra (databases). Must be a **literal** — it can't reference a variable.
- **`ignore_changes = [tags, ...]`** → stop Terraform reverting attributes changed **outside** Terraform. Use `all` to ignore every attribute.
- **`replace_triggered_by = [aws_security_group.web]`** → recreate this resource when the referenced resource/attribute changes, even without an attribute dependency.
- **`precondition` / `postcondition`** live here too, but they're **validation**, not behavior → [custom conditions & validation](../04-configuration/14-custom-conditions-and-validation.md).

## 💻 Syntax / Example

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345"
  instance_type = "t3.micro"
  tags          = { Name = "app-server" }

  lifecycle {
    create_before_destroy = true
    prevent_destroy       = false        # true would block any destroy
    ignore_changes        = [tags]       # or: all
    replace_triggered_by  = [aws_security_group.web.id]
  }
}
```

## 🚩 Flags & values to memorize

- `create_before_destroy` default = **false** (destroy-then-create).
- `prevent_destroy = true` → destroy plans **error**; value must be a **literal**.
- `ignore_changes = [attrs]` or `all`.
- `replace_triggered_by = [refs]` → force recreate on referenced change.

## ⚠️ Common traps

- **`prevent_destroy` can't take a variable** — literal only. And it blocks `terraform destroy` for that resource too.
- `ignore_changes` only stops Terraform from **reverting** the drift; it doesn't push your config value either.

## 🔄 Easily confused with

- **`prevent_destroy` vs `create_before_destroy`** → [glosario](../../glosario.md)
- `precondition`/`postcondition` (validation) → [custom conditions & validation](../04-configuration/14-custom-conditions-and-validation.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-depends-on.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)

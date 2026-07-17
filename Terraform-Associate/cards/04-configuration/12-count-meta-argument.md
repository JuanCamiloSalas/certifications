[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./11-locals.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./13-for_each-meta-argument.md)

# `count` Meta-Argument

> **Pitch (1 line):** `count = N` on a resource (or module) creates N instances addressed by a **numeric index** — `resource.name[0]`, `[1]`, …

## 🎯 What the exam tests

- That `count` makes **N copies**, addressed by **index** starting at **0** — and `count.index` gives the current index.
- The **reindex gotcha**: because `count` is **list-backed**, removing or reordering a middle element shifts every later index → Terraform **destroys and recreates** them.
- The **conditional-create idiom**: `count = var.enabled ? 1 : 0` (0 = resource not created).
- That a resource **can't use `count` and `for_each` together**.

## 🧠 Core (non-obvious bits)

- **Index-based identity.** Instances are `aws_instance.web[0]`, `web[1]`… tracked by **position**, not by a stable key.
- **Reordering/removing from the middle reindexes** everything after it → those get **recreated**, not just the one you touched. When identity must be stable, use **`for_each`** instead. → [count vs for_each](../../comparativas/count-vs-for-each.md)
- **`count.index`** (0-based) inside the block builds per-instance names: `name = "web-${count.index}"`.
- **Conditional creation:** `count = condition ? 1 : 0` — the standard way to toggle a resource on/off.
- **Splat** grabs an attribute across all instances: `aws_instance.web[*].id`.
- Best fit: several **identical/interchangeable** copies where position doesn't matter.

## 💻 Syntax / Example

```hcl
resource "aws_instance" "web" {
  count         = 3
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
  tags = { Name = "web-${count.index}" }   # web-0, web-1, web-2
}

# Reference one:  aws_instance.web[0].id
# Reference all:  aws_instance.web[*].id

# Conditional creation:
resource "aws_eip" "maybe" {
  count = var.assign_eip ? 1 : 0            # 0 => not created
}
```

## 🚩 Flags & values to memorize

- `count.index` is **0-based**.
- Address one → `name[0]` · all → `name[*]` (splat).
- Toggle idiom → `count = cond ? 1 : 0`.
- `count` and `for_each` are **mutually exclusive** on one resource.

## ⚠️ Common traps

- Deleting a **middle** item (or reordering) **reindexes** → later instances recreated. Stable identity → **`for_each`**.
- `count = 0` **removes** the resource (destroys it), it doesn't "pause" it.

## 🔄 Easily confused with

- → [count vs for_each](../../comparativas/count-vs-for-each.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./11-locals.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./13-for_each-meta-argument.md)

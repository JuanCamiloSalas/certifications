[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./12-count-meta-argument.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./14-custom-conditions-and-validation.md)

# `for_each` Meta-Argument

> **Pitch (1 line):** `for_each` over a **map or set** creates one instance per **key** — addressed by that key (`resource.name["k"]`), so instances stay stable when the collection changes.

## 🎯 What the exam tests

- That `for_each` takes a **map** or a **set of strings** (not a plain list) → one instance per **key**.
- The addressing: **`resource.name["key"]`**, and inside the block **`each.key`** / **`each.value`**.
- The advantage over `count`: **stable keys** → adding/removing one item **doesn't recreate the others** (no reindex).
- That you must **`toset()`** a list before using it with `for_each`.

## 🧠 Core (non-obvious bits)

- **Key-based identity.** Instances are `aws_instance.web["dev"]`, `web["prod"]` — tracked by **key**, so removing `"dev"` leaves `"prod"` untouched. This is the reason to prefer `for_each` over `count`. → [count vs for_each](../../comparativas/count-vs-for-each.md)
- **List not allowed directly** → wrap it: `for_each = toset(var.names)`. With a **set**, `each.key == each.value`.
- **`each.key` / `each.value`**: with a map, key = the map key, value = the map value (often an object).
- **Keys must be known at plan time** — `for_each` can't depend on values only known after apply (computed IDs). If it does, `terraform plan` errors.
- `count` and `for_each` are **mutually exclusive** on one resource.

## 💻 Syntax / Example

```hcl
# set of strings -> each.key == each.value
resource "aws_iam_user" "team" {
  for_each = toset(["dev", "prod"])
  name     = "user-${each.key}"                 # user-dev, user-prod
}

# map(object) -> each.value is the object
resource "aws_instance" "web" {
  for_each      = var.instances                 # { app = {ami=..,type=..}, db = {...} }
  ami           = each.value.ami
  instance_type = each.value.type
  tags          = { Name = each.key }           # "app", "db"
}

# Reference one:  aws_instance.web["app"].id
```

## 🚩 Flags & values to memorize

- Accepts **map** or **set of strings** — **not a list** (use `toset(list)`).
- Set → **`each.key == each.value`**; map → `each.key` (key), `each.value` (value/object).
- Address one → `name["key"]`.
- Keys must be **known at plan time** (no computed/unknown values).

## ⚠️ Common traps

- Passing a **list** to `for_each` → error; wrap with **`toset()`**.
- `for_each` on **unknown values** (attributes only set after apply) → plan-time error; use `count` or restructure.
- Changing an item's **key** recreates that instance (identity = key).

## 🔄 Easily confused with

- → [count vs for_each](../../comparativas/count-vs-for-each.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./12-count-meta-argument.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./14-custom-conditions-and-validation.md)

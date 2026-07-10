[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-resource-and-data-blocks.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-variable-precedence.md)

# Variable Block (input variables) & types

> **Pitch (1 line):** `variable` blocks parameterize a config so one codebase serves many environments; each has an optional `type`, `default`, and `description`.

## 🎯 What the exam tests

- The common arguments: `description`, `type`, `default` — and that a `default` makes the variable **optional**.
- The variable **types**: primitives (string/number/bool) and collections (list/map/set).
- Referencing: **`var.<name>`**, `var.<name>[0]` for a list — and that **sets have no index**.

## 🧠 Core (non-obvious bits)

- **`variable "<name>" { type, default, description }`.** Reference anywhere with **`var.<name>`**.
- **Primitives:** `string`, `number`, `bool`.
- **Collections:**
  - **`list(...)`** — ordered, **index from 0** → `var.x[0]`.
  - **`map(...)`** — named keys → `var.x["key"]` or `var.x.key`.
  - **`set(...)`** — **unordered + unique**, **no index access** (convert to a list first).
- **`default`** present → variable is **optional**; absent → **required** (Terraform prompts interactively, or errors in automation).
- Variables kill hardcoding: the same config produces dev/test/prod by swapping values.

## 💻 Syntax / Example

```hcl
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-2"
}

variable "permitted_size" {
  type    = list(string)
  default = ["t3.small", "t4g.micro"]      # var.permitted_size[0] == "t3.small"
}

variable "course_details" {
  type    = map(string)
  default = { instructor = "bryan", course = "terraform" }  # var.course_details.instructor
}
```

## 🚩 Flags & values to memorize

- **list** = ordered (index 0) · **map** = named keys · **set** = unordered + unique, **no index** (convert to list).
- `default` present → optional; absent → required (prompted).

## 🔄 Easily confused with

- **Input variable vs local value** → [glosario](../../glosario.md) (locals are computed **inside** the config; variables come from **outside**).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-resource-and-data-blocks.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-variable-precedence.md)

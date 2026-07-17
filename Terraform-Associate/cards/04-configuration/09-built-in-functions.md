[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./08-terraform-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./10-dynamic-values.md)

# Built-In Functions

> **Pitch (1 line):** Terraform ships ~100+ built-in functions to transform strings, numbers, and collections — call them as `name(arg, …)` to keep config DRY and consistent.

## 🎯 What the exam tests

- The **call syntax**: `function_name(arg1, arg2, …)` — functions are called, never defined.
- That **you cannot write your own functions** — Terraform has **no user-defined functions**. Only the built-ins exist.
- Which category solves a task: **type conversion** (`toset`/`tolist`/`tomap`), **numeric** (`min`/`max`), **string** (`join`/`split`), **collection** (`length`/`lookup`/`merge`), **network/CIDR** (`cidrsubnet`).
- That you validate a function's output in **`terraform console`**.

## 🧠 Core (non-obvious bits)

- **No custom functions.** If an option says "define a custom function", it's wrong — extend logic with `locals` + built-ins instead.
- **Type conversion feeds meta-args:** `toset(list)` de-dupes and unorders → the usual way to hand a **list** to `for_each` (which won't take a list directly). → [for_each](./13-for_each-meta-argument.md)
- **Categories worth recognizing:** string (`upper`, `lower`, `replace`, `format`, `trimspace`), numeric (`min`, `max`, `abs`, `ceil`), collection (`length`, `element`, `lookup`, `contains`, `keys`, `merge`, `concat`, `flatten`, `distinct`), encoding (`jsonencode`, `base64encode`), network (`cidrsubnet`, `cidrhost`), filesystem (`file`, `templatefile`).
- **`terraform console`** is the golden way to try one live (`> upper("hi")`) before wiring it into a resource.
- **`lookup(map, key, default)`** returns the default when the key is missing — handy to avoid errors on optional keys.

## 💻 Syntax / Example

```hcl
# General form: function_name(arg1, arg2, ...)
upper("hello")                 # => "HELLO"
min(4, 7, 2, 9, 5)             # => 2
join("-", ["hello", "world"])  # => "hello-world"
toset(["a", "a", "b"])         # => ["a", "b"]  (deduped, unordered)
lookup({ a = 1 }, "z", 0)      # => 0           (key missing -> default)

# In config: build a subnet CIDR from the VPC CIDR
resource "aws_subnet" "app" {
  cidr_block = cidrsubnet("10.0.0.0/16", 8, 2)   # => "10.0.2.0/24"
}
```

```bash
terraform console          # then type: min(4,7,2)  ->  2
```

## 🚩 Flags & values to memorize

- Syntax `name(args)` — **no user-defined functions** exist.
- `toset()` = de-dupe + drop order · `tolist()` / `tomap()` / `tostring()` = coerce type.
- `lookup(map, key, default)` — default when key absent.
- `cidrsubnet(prefix, newbits, netnum)` — carve a subnet out of a prefix.

## ⚠️ Common traps

- "Create a **custom/user-defined** function" → **not possible**; only built-ins.
- `toset()` **loses ordering** — fine for `for_each`, but don't rely on order afterwards.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./08-terraform-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./10-dynamic-values.md)

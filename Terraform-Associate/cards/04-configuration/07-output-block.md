[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-variable-precedence.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./08-terraform-block.md)

# Output Block (`output`)

> **Pitch (1 line):** `output` blocks surface values after apply (IPs, DNS, IDs) and are how a **parent module reads a child's** values.

## 🎯 What the exam tests

- What outputs are for: display key values after `apply` **and** pass data **between modules**.
- The required **`value`** argument (plus optional `description`, `sensitive`).
- That an output `value` can be an **expression/interpolation**, not just a bare reference.

## 🧠 Core (non-obvious bits)

- **`output "<name>" { value = <expr> }`** — name is yours; **`value` is required**.
- Outputs print after `apply` and are readable any time with **`terraform output [name]`**.
- **Module integration:** a child module's outputs are how a parent reads its values → `module.<name>.<output>`.
- **`sensitive = true`** masks the value in CLI output — but it is **still stored in state in plaintext**.
- `value` can be a full **interpolation**: `"https://${aws_alb.web.dns_name}"`.

## 💻 Syntax / Example

```hcl
output "instance_public_ip" {
  description = "Public IP of the web server"
  value       = aws_instance.web.public_ip
}

output "website_url" {
  value = "https://${aws_alb.web.dns_name}"   # interpolated expression
}
```

## ⚠️ Common traps

- **`sensitive = true`** only hides the CLI display — the value is **still in state in plaintext**.
- Outputs are the **only** way a parent module reads a child module's values.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-variable-precedence.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./08-terraform-block.md)

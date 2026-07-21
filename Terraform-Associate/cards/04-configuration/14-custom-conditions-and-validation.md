[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./13-for_each-meta-argument.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./15-securing-secrets.md)

# Custom Conditions & Validation

> **Pitch (1 line):** four ways to assert your assumptions — **variable validation**, **precondition**, **postcondition**, and **check blocks** — each firing at a different stage of the workflow.

## 🎯 What the exam tests

- The **four mechanisms** and where each is written.
- The big split: **variable validation / precondition / postcondition BLOCK** the operation on failure; a **`check` block only WARNS** (non-blocking).
- **When** each runs: input → before create → after create → last step of plan/apply.
- That a **`check` block is top-level** — not nested inside a resource/data/variable.

## 🧠 Core (non-obvious bits)

- **Variable validation** — inside a `variable` block: enforce format/range on **input**; fails **before** planning and stops the run.
- **Precondition** — inside a resource/data `lifecycle`: verify assumptions **BEFORE** create/update (e.g. the AMI has the right architecture). Blocking.
- **Postcondition** — same place: verify results **AFTER** create/update (e.g. the instance got a private DNS name). Blocking.
- **`check` block** — standalone **top-level** block: validates infra **as a whole**; runs as the **last step** of plan/apply; on failure Terraform prints a **warning and continues** (does **not** block). → [validation mechanisms](../../comparativas/validation-mechanisms.md)
- All use the same pair: **`condition`** (must be `true`) + **`error_message`**.
- `precondition`/`postcondition` are written in the `lifecycle` block covered by [lifecycle](../07-maintain/03-lifecycle.md), but they're a **validation** concern.

## 💻 Syntax / Example

```hcl
# 1) Variable validation
variable "vm_size" {
  type = string
  validation {
    condition     = var.vm_size != "Basic_A0"
    error_message = "Basic_A0 is deprecated."
  }
}

# 2) + 3) Pre / postcondition (inside a resource's lifecycle)
resource "aws_instance" "web" {
  ami = data.aws_ami.ubuntu.id
  lifecycle {
    precondition {
      condition     = data.aws_ami.ubuntu.architecture == "x86_64"
      error_message = "AMI must be x86_64."
    }
    postcondition {
      condition     = self.private_dns != ""
      error_message = "Instance did not get a private DNS name."
    }
  }
}

# 4) check block — top-level, non-blocking
check "health" {
  assert {
    condition     = aws_instance.web.instance_state == "running"
    error_message = "Web instance is not running."
  }
}
```

## 🚩 Flags & values to memorize

- Blocking: **variable validation**, **precondition**, **postcondition**. Non-blocking (warning): **`check`**.
- `check` runs **last** (after plan/apply) and is **top-level** (never nested).
- Every mechanism = `condition` (bool) + `error_message`.

## ⚠️ Common traps

- A **`check` failure does NOT stop** the apply — it's a warning. The other three **do** stop it.
- `check` blocks are **top-level**, not inside a resource/variable.
- Don't confuse this with **`terraform validate`** (syntax/consistency check, no provider calls) → [validate](../03-core-workflow/07-terraform-validate.md).

## 🔄 Easily confused with

- → [validation mechanisms (which one, when)](../../comparativas/validation-mechanisms.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./13-for_each-meta-argument.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./15-securing-secrets.md)

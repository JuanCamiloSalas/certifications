[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-terraform-validate.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./09-environment-variables.md)

# The Terraform CLI — structure, help & autocomplete

> **Pitch (1 line):** everything runs through `terraform <subcommand> [options]`; built-in `-help` and `-install-autocomplete` make the CLI faster and less error-prone.

## 🎯 What the exam tests

- The command anatomy: `terraform [global options] <subcommand> [args/flags]`.
- How to enable tab completion (`terraform -install-autocomplete`) and where per-command help lives.
- That global options (like `-chdir`) go **before** the subcommand, and Terraform flags use a **single dash**.

## 🧠 Core (non-obvious bits)

- **Structure:** base `terraform` + subcommand + optional flags — the same pattern on every platform, which is what gives the workflow its consistency/repeatability.
- **`-install-autocomplete`** sets up Tab completion for **Bash/Zsh** (it edits your shell rc file). It only offers valid subcommands/flags, so it also prevents typos.
- **Help:** `terraform -help` lists all commands; `terraform <subcommand> -help` (e.g. `terraform plan -help`) shows that command's options. `--help` is accepted too.
- **Single-dash flags** by convention: `-out=planfile`, `-auto-approve` — **not** `--out`, unlike many CLIs.
- **`tofu <subcommand> [options]`** — OpenTofu (the open-source fork) mirrors the exact CLI shape. Exam is Terraform, but the pattern is 1:1.

## 💻 Syntax / Example

```bash
terraform <subcommand> [options]       # e.g. terraform plan -out=planfile
terraform -install-autocomplete        # enable Tab completion (Bash/Zsh)
terraform -help                        # list every command
terraform plan -help                   # options for one subcommand
terraform -chdir=envs/prod apply       # global option BEFORE the subcommand
```

## 🚩 Flags & values to memorize

- **`-install-autocomplete`** / `-uninstall-autocomplete` — toggle Tab completion.
- **`-help`** (or `--help`) — global command list; `<cmd> -help` — per-command options.
- **`-chdir=DIR`** — global option (before the subcommand): run as if in `DIR`, without `cd`.

## ⚠️ Common traps

- `-chdir` is a **global** option → it goes **before** the subcommand (`terraform -chdir=DIR plan`), never after.
- Autocomplete works only **after** `-install-autocomplete` **and** a shell reload; Bash/Zsh only.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-terraform-validate.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./09-environment-variables.md)

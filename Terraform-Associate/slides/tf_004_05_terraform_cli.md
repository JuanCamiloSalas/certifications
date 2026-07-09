# S5 — Using the Terraform CLI (resumen de slides)

> Outline de la sección 5 del curso (Bryan Krausen).
> **No es transcripción** del PDF (`tf_004_05_terraform_cli.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `03-core-workflow` (objetivo 3).

## Lecture — Using the Terraform CLI

- **What is the Terraform CLI?** la forma principal de interactuar con Terraform y ejecutar el workflow. Patrón consistente `terraform <command> [options]` (y `tofu <command> [options]`). Tres ideas: *Unified Workflow* · *Command Interface* · *Consistent Pattern* (consistencia/repetibilidad sin importar la plataforma).
- **Getting to know the CLI:** estructura `terraform <subcommand> [options or flags]` → base command + subcommand + optional flag. Ejemplo: `terraform plan -out=planfile`.
- **Mapping the workflow to commands:** Write → `fmt` · Initialize → `init` · Plan → `plan` · Apply → `apply` · Destroy → `destroy`. _(ya cubierto por card 01)_
- **Using environment variables with the CLI:** pasan config y credenciales sin hardcodear en `.tf`; aumentan seguridad (API keys fuera de los ficheros). Ejemplos: `TF_LOG=DEBUG`, `TF_VAR_svr_name`, `AWS_ACCESS_KEY_ID`. Multi-shell: `export` (bash/zsh) · `$Env:` (PowerShell) · `setx` (cmd).
- **Making the most of the CLI:**
  - *Auto-complete:* `terraform -install-autocomplete` habilita Tab completion (Bash/Zsh); reduce errores y solo ofrece opciones válidas.
  - *help feature:* `terraform --help` (lista de comandos) y `terraform <cmd> --help` (opciones de ese comando).
  - *`terraform fmt`:* formatea al estilo canónico; `-recursive` para subdirectorios. _(ya cubierto en 02/06 HCL basics)_
  - *`terraform validate`:* comprueba sintaxis y validez estructural; **no** verifica que despliegue; atrapa errores antes de plan/apply. _(ya cubierto por card 07)_
- **Summary:** subcommand por paso · `-install-autocomplete` · personalizar con options/flags · `validate` temprano · `fmt` para formato · datos sensibles vía `TF_VAR_*` y otras env vars.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `03-core-workflow` | 08 terraform-cli (structure · `-help` · `-install-autocomplete` · `-chdir` · single-dash flags) · 09 environment-variables (`TF_VAR_*` · `TF_LOG`/`TF_LOG_PATH` · provider creds) |

> Reconciliación: `fmt`, `validate` y el mapping del workflow ya estaban carded (02/06, 07, 01) → no se duplican, se referencian. Providers **no** aparecen en estas slides (el README del bloque los esperaba en S5); quedan pendientes para más adelante.

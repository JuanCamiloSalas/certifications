# S7 — Understanding the Terraform Blocks (resumen de slides)

> Outline de la sección 7 del curso (Bryan Krausen). Sección **densa** (los bloques del lenguaje).
> **No es transcripción** del PDF (`tf_004_07_terraform_config_fundamentals.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `04-configuration` (objetivo 4).

## Lectures — por bloque del lenguaje

- **Terraform Block Types (overview):** `provider` · `resource` · `data` · `variable` · `output` · `terraform` · `module` · `import` (lista no exhaustiva).
- **Provider block:** conecta Terraform a una plataforma API-driven; nombre definido por el maintainer; argumentos en la doc del Registry; **auth vía env vars** (no hardcodear); un provider habilita muchos recursos; se descarga en `init`; docs en `registry.terraform.io`. **provider meta-argument:** `alias` + `provider = aws.prod` para multi-region/multi-cuenta.
- **Resource block:** `resource "<type>" "<name>" {}`; type definido por el provider, name único por config; argumentos de la doc del provider; **reglas de nombre** (empieza con letra o `_`; solo letras, dígitos, `_`, `-`).
- **Data block:** lee info de recursos **existentes** sin crearlos; query constraints (`filter`); referencia `data.<type>.<name>.<attr>`; evita hardcodear.
- **Variable block:** define inputs (`description`, `type`, `default`); tipos primitivos (string/number/bool) y complejos (**list** ordenada index 0, **map** key=value, **set** único sin index → convertir a list); referencia `var.<name>` / `var.<name>[0]`.
- **Assigning values / Order of precedence** (menor→mayor): Variable Block Defaults → Environment Variables (`TF_VAR_`) → `*.tfvars` → `*.auto.tfvars` → **Command Line Flags** (`-var`/`-var-file` ganan). `terraform.tfvars` y `*.auto.tfvars` se auto-cargan; nombres custom con `-var-file`.
- **Output block:** muestra info tras el deploy (IPs, DNS, IDs); `value` (obligatorio), `description`, `sensitive`; pasa datos entre módulos; admite interpolación `"${...}"`.
- **Terraform block:** config global — `required_version`, `required_providers` (`source` + `version`), `backend`. Escenario del "mismatched provider/TF version" motiva pinnear. **Version constraints:** `=`/bare (exacta), `>=` (o mayor), `~>` (pesimista: el componente más a la derecha incrementa).

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `04-configuration` | 03 provider-block · 04 resource-and-data-blocks · 05 variable-block (+ types) · 06 variable-precedence · 07 output-block · 08 terraform-block (+ version constraints) |

> Reconciliación: la **anatomía HCL** del `resource` ya estaba en `02/06 hcl-basics`; el **referencing** en `04/01`; `TF_VAR_*` en `03/09`. No se duplican, se referencian. No hubo card de "overview de block types" (se cubre repartido + `02/02 core-components`). Providers en `required_providers` → tratado en la card 08, cruzado con la 03.

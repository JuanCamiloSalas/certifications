# S9 — Understanding and Managing Terraform State (resumen de slides)

> Outline de la sección 9 del curso (Bryan Krausen). Sección **crítica** (el state es donde más cae la gente).
> **No es transcripción** del PDF (`tf_004_09_understanding_terraform_state.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `06-state` (objetivo 6).

## Lectures — por tema

- **Intro a Terraform State:** `.tfstate` = archivo JSON que **mapea la config a los recursos reales** (por ID) y guarda **metadata** (dependencias, orden de operaciones, provider). Es la **única fuente de verdad**; Terraform **no funciona sin state**. Hace un **refresh antes de cada operación**. Nombre por defecto `terraform.tfstate` en el working dir. **Guarda secretos en texto plano.**
- **Where can I store my state? / Remote State (63-67):** backend **local** (por defecto, en disco) vs **remoto**. El **backend va en el bloque `terraform {}`** (no en `provider`); hay que correr **`terraform init`** al añadir/cambiar backend (ofrece **migrar** el state). Opciones remotas: **S3**, **Azure Blob (`azurerm`)**, **GCS**, **HCP Terraform**. **State locking**: automático en la mayoría; en **S3 → `use_lockfile = true`** — ⚠️ **DynamoDB locking está DEPRECATED** (cambio del 004). **Nunca** poner credenciales en el bloque backend (roles/env vars). Best practice: local solo para aprender; remoto con locking para equipo/prod.
- **Inspecting State (68-69):** `terraform state list` (solo **direcciones**) · `terraform show` (dump completo humano de todo el state o de un plan) · `terraform state show <addr>` (atributos de **un** recurso). Flujo: `list` → coger la address → `state show`. Comandos legacy de escritura: `state mv`, `state rm` (no destruye), `state pull/push` (raro). El 004 empuja hacia bloques declarativos.
- **State Drift + Refresh-Only (70-73):** drift = cambio fuera de Terraform. Dos salidas: **revertir** con `terraform apply` (la config manda → infra vuelve a la config) o **aceptar** con `terraform apply -refresh-only` (la realidad manda → actualiza el **state**, no la infra). `terraform plan -refresh-only` = preview seguro, no escribe. **Si pierdes el state:** la infra sigue viva pero Terraform la deja de reconocer → un plan quiere recrear todo; recuperación vía versioning del backend remoto o `import`.
- **Managing Multiple Environments with Workspaces (74):** **CLI workspaces** = varios states para **una misma config** (evita duplicar directorios). `default` siempre existe (state en la raíz); los demás en **`terraform.tfstate.d/<name>/`**. Comandos: `terraform workspace list/new/select/show/delete`. Referencia en config con **`terraform.workspace`**. ⚠️ **CLI workspaces ≠ HCP workspaces**. No es aislamiento fuerte (mismo backend/credenciales).

## Preview no carbonizado aquí (se ve en el PDF pero es de otra sección)

- **State Refactoring — bloques `moved` / `removed` / `import`** (pages 22-25): "the old way" (comandos CLI `state mv/rm`, `import`) vs "the new way" (bloques declarativos, versionados, revisables en PR, dentro del workflow plan/apply). El curso lo trata a fondo en **S11 (Refactoring Terraform State)** con demos → **se cardea al cursar S11** (bloque `06`/`07`). No se duplica aquí para no adelantar S11.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `06-state` | 01 terraform-state · 02 backends-and-state-storage (local/remoto, locking, `use_lockfile`) · 03 inspecting-state (`state list`/`show`/`state show` + legacy) · 04 state-drift-refresh-only · 05 workspaces (CLI) |

**Comparativas creadas:** `local-vs-remote-backend` · `cli-workspaces-vs-hcp-workspaces`.

> Reconciliación: el `backend` ya se mencionaba en `04/08 terraform-block` ("detalle en bloque 06") → aquí se desarrolla y se cruza. `terraform init -migrate-state`/`-reconfigure` ya estaba en `03/02 init` → se referencia, no se repite. **Corregido dato desactualizado**: `planning.md` y `glosario.md` decían "S3 + DynamoDB (locking)" → actualizado a `use_lockfile` (DynamoDB deprecated en 004). Los bloques `moved`/`removed`/`import` se dejan para S11.

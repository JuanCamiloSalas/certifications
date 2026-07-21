# S11 — Refactoring Terraform State (resumen de slides)

> Outline de la sección 11 del curso (Bryan Krausen). Tema: **refactorizar el state de forma declarativa** con los bloques `moved` / `removed` / `import`. 6 clases (85-90), **2 labs**.
> **No es transcripción** del PDF (`tf_004_11_refactoring_state.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta dos bloques:** `moved`/`removed` (refactor del state) → **`06-state`** (objetivo 6); `import` (adoptar infra existente) → **`07-maintain`** (objetivo 7). El curso ya lo anticipaba en la nota de S9 ("the old way vs the new way").

## Lectures — por tema

- **85 · State Refactoring (intro):** reorganizar **cómo Terraform rastrea** la infra **sin cambiar la infra**. Escenarios: renombraste un recurso, reorganizas módulos, adoptas infra existente, o dejas de gestionar algo pero quieres que siga vivo. **Sin herramientas de refactor, Terraform cree que destruyes lo viejo y creas lo nuevo.**
  - **The Old Way vs The New Way:** CLI (`terraform state mv`/`state rm`/`import`) = fuera de la config, **no versionado**, difícil de revisar en PR, **arriesgado** (un comando mal → state modificado permanentemente) · Bloques (`moved`/`removed`/`import`) = en los `.tf`, **versionados**, revisables en PR, parte del **plan/apply**, testeables antes de aplicar.
  - **Workflow de refactor:** Write (añadir bloques) → `plan` (validar) → `apply` (actualiza state) → **borrar los bloques** después.
- **86 · Moved Block:** dice a Terraform que **renombraste/reubicaste** un recurso → actualiza la **dirección en el state** sin destruir/recrear. `moved { from = <addr_viejo>  to = <addr_nuevo> }`. Sirve para: renombrar, mover un recurso **dentro de un módulo** (`to = module.storage.aws_s3_bucket.data`), o **renombrar un módulo entero** (`module.old_app → module.new_app`). Evita downtime y pérdida de datos. Sin él, renombrar = `Plan: 1 to add, 1 to destroy`.
- **87 · Removed Block:** deja de **gestionar** un recurso **sin borrarlo** (lo saca del state, la infra sigue viva). `removed { from = <addr>  lifecycle { destroy = false } }`. **Debes también borrar el `resource` block** de la config. Uso: entregar la propiedad a otro equipo, control manual. Reemplazo declarativo de `terraform state rm`.
  - **Key Differences moved vs removed:** `moved` = reubica dentro del state (sigue gestionado) · `removed` = lo saca del state (deja de gestionarse).
  - **Decision tree:** renombrar / reorganizar en módulos → **moved** · parar gestión / handoff a otro equipo / dividir configs → **removed**.
- **88 · Lab — Refactoring Terraform State:** aplicar `moved`/`removed` en un config real.
- **89 · Import Block:** trae infra **existente** (creada a mano) bajo gestión de Terraform mapeando el ID real a una dirección de config. `import { to = <addr>  id = "<id_del_provider>" }`. El `id` es **específico del provider** (`"my-org/production"`, `"/subscriptions/1234/rg/my-rg"`, `i-123…`). **Requisito: escribir primero el `resource` block** (a mano o con `terraform plan -generate-config-out=PATH`). Parte de plan/apply → previsualizable.
  - **`terraform import` (CLI):** la vía original — `terraform import <addr> <id>`; añade al state **de inmediato**, **sin paso de plan**, y **también** exige escribir la config a mano. **Para el examen:** saber que existe, pero **enfocarse en el `import` block** como enfoque moderno.
- **90 · Lab — Importing Resources into Terraform State:** importar recursos con el `import` block.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `06-state` | 06 moved-block · 07 removed-block |
| `07-maintain` | 01 import-block (+ contraste con `terraform import` CLI) |

**Comparativas creadas:** `refactoring-moved-removed-import` (los 3 bloques + CLI vieja-vía vs bloques declarativos + árbol de decisión).

> Reconciliación: `03-inspecting-state` (bloque 06) ya mencionaba los comandos legacy `state mv`/`state rm` y anticipaba "config-driven blocks en S11" → ahora se cruza con las cards nuevas. El **`import`** se ubica en `07-maintain` (objetivo 7 = mantener infra) siguiendo el mapeo; `moved`/`removed` en `06-state` (objetivo 6). Glosario: añadidos `moved`/`removed` blocks y el par confuso **CLI (`state mv/rm/import`) vs bloques declarativos**; la entrada "Import" se matizó (bloque + CLI). Los meta-args `lifecycle`/`depends_on` no son el foco de S11 (solo aparece `lifecycle { destroy }` dentro del `removed`) → se cardean en **S13** (bloque 07).

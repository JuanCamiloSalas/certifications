# S13 — Managing Resource Behavior and Dependencies (resumen de slides)

> Outline de la sección 13 del curso (Bryan Krausen). Tema: **controlar orden, comportamiento y validación** de recursos. Clases 100-103 (+demo/lab).
> **No es transcripción** del PDF (`tf_004_13_manage_resource_behavior.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta dos bloques:** `depends_on` + `lifecycle` (comportamiento/dependencias) → **`07-maintain`** (objetivo 7); **Validación de configuración** (variable validation, pre/postconditions, checks) → **`04-configuration`** (objetivo 4, es *escribir* config, no mantener infra).

## Lectures — por tema

- **100 · Explicit Dependencies (`depends_on`):** **implícita** = una referencia de atributo (`aws_instance.web.id`) → Terraform infiere el orden solo · **explícita** = `depends_on` cuando el orden importa **pero no hay referencia** que lo exprese. `depends_on = [<recurso/módulo>]` (una **lista de recursos**, no atributos). Último recurso: preferir referencias implícitas.
- **101 · Managing Resource Behavior (`lifecycle`):** meta-argumento que controla cómo Terraform gestiona el recurso:
  - **`create_before_destroy = true`** → crea el reemplazo **antes** de destruir el viejo (cero downtime). Por defecto es destroy-then-create.
  - **`prevent_destroy = true`** → **bloquea** cualquier destroy del recurso (el plan da error). Protege infra crítica (DBs).
  - **`ignore_changes = [attr]`** → ignora drift en atributos concretos (cuando algo externo los modifica). `all` para todos.
  - **`replace_triggered_by = [refs]`** → fuerza el reemplazo cuando cambian recursos/atributos referenciados.
  - **`precondition` / `postcondition`** también viven dentro de `lifecycle` → pero son un mecanismo de **validación** (ver card de validación).
- **102 · Demo — lifecycle:** demo de las opciones de `lifecycle`.
- **103 · Validating Your Configuration:** **cuatro** mecanismos de validación como "capas defensivas" en distintas etapas:
  1. **Variable validation** — `variable { validation { condition, error_message } }`: valida formato/rango del **input** antes de plan; **detiene** la operación si falla.
  2. **Precondition** — `lifecycle { precondition {…} }`: verifica supuestos **ANTES** de crear (p.ej. arquitectura del AMI). Bloqueante.
  3. **Postcondition** — `lifecycle { postcondition {…} }`: verifica resultados **DESPUÉS** de crear (p.ej. que la instancia obtuvo DNS). Bloqueante.
  4. **Check blocks** — bloque **top-level** `check "name" { assert {…} }`: valida la infra **como un todo**; se ejecuta como **último paso** de plan/apply; al fallar **avisa (warning) y continúa** — **NO bloquea**. No se anida dentro de otros bloques.
  - **Order of operations:** variable validation (input) → precondition (antes) → [crear] → postcondition (después) → check (último, no bloqueante).
  - **Decision tree:** input del usuario antes de plan → *variable validation* · supuestos antes de crear → *precondition* · resultados tras crear → *postcondition* · salud de la infra sin bloquear → *check*.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `07-maintain` | 02 depends-on (implícita vs explícita) · 03 lifecycle (CBD/prevent_destroy/ignore_changes/replace_triggered_by) |
| `04-configuration` | 14 custom-conditions-and-validation (los 4 mecanismos) |

**Comparativas creadas:** `validation-mechanisms` (variable validation vs pre/postcondition vs check — qué bloquea, cuándo corre).

> Reconciliación: `depends_on` ya se mencionaba en `04/01 resource-referencing` (implícita vs explícita) → ahora se cardea a fondo y se cruza. `create_before_destroy`/`prevent_destroy` ya estaban en el glosario (par confuso) → se desarrollan en la card de `lifecycle`. La **variable validation** se anticipaba en `04/05 variable-block` ("deepened in S14") → **corregido**: se profundiza aquí en **S13** (card 04/14), no en S14. `precondition`/`postcondition` viven en `lifecycle` pero se tratan como validación (card 04/14), no en la card de comportamiento (07/03). Los meta-args `count`/`for_each` (que el README del 07 listaba) ya viven en `04/12-13` desde S10 → se aclara en el README del 07.

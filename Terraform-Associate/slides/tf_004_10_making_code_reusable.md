# S10 — Making Code Reusable (resumen de slides)

> Outline de la sección 10 del curso (Bryan Krausen). Tema: **primitivas de reutilización** (functions, dynamic values, locals, `count`, `for_each`). 10 clases (75-84), **3 labs**.
> **No es transcripción** del PDF (`tf_004_10_making_code_reusable.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `04-configuration` (objetivo **4**, no 5). ⚠️ El título "Making Code Reusable" sugiere módulos, pero **la sección no toca módulos**: todo es lenguaje de configuración (functions/interpolación/locals/meta-args = objetivo 4). Remapeada de 05→04. Los módulos reales llegan en **S12**.

## Lectures — por tema

- **75 · Built-In Functions to Standardize Code:** funciones nativas para manipular strings, números, listas, etc. Sintaxis `nombre(arg1, arg2, ...)`. Categorías vistas: **string** (`join`, `split`, `upper`), **numeric** (`min`, `max`), **type conversion** (`toset`/`tolist`/`tomap`/`tostring`), **network** (CIDR: subnets/hosts). Ejemplos: `upper("hello")→"HELLO"`, `min(4,7,2,9,5)→2`, `join("-","hello","terraform")→"hello-terraform"`. ⚠️ **No existen funciones definidas por el usuario** — solo las built-in. Probarlas en **`terraform console`**.
- **76 · Enhancing Code with Dynamic Values:** código dinámico = NO valores estáticos → usa **interpolación `${...}`**, meta-args, funciones, locals, variables y **data sources**. Static vs dynamic (mismos recursos, uno hardcodeado y otro parametrizado). **Interpolación**: evalúa la expresión entre `${ }`, la convierte y la inserta en el string (`"server-${data.aws_region.current.name}-${var.environment}"` → `server-us-east-1-dev`). **Data sources** = solo lectura, no crean/modifican infra; consultan info del provider (`data.aws_caller_identity.current.account_id`). Combinar var + data + local = código flexible y DRY.
- **77 · Lab — Refactor Code with Dynamic Values:** refactor de config hardcodeada a dinámica (variables + data + interpolación).
- **78 · Using Locals to Avoid Code Duplication:** locals = "memoria a corto plazo" del config; valores con nombre calculados **dentro** de la config, referenciables en otras partes. Centralizan valores repetidos (prefijos, env, tags comunes). Bloque **`locals {}`** (plural) / referencia **`local.<name>`** (singular). Beneficios: lógica centralizada (cambias en un sitio), código más claro, menos riesgo que editar N valores hardcodeados.
- **79 · Demo — locals:** demo de `locals` para dejar de duplicar valores.
- **80 · Lab — Using Locals:** aplicar `locals` (tags/prefijos comunes) en un config.
- **81 · count Meta-Argument:** `count = N` → N instancias, direccionadas por **índice** → `azurerm_virtual_machine.example[0]`. `count.index` (0-based). Respaldo tipo **lista** → reordenar/borrar del medio **reindexa** y recrea. Útil para copias idénticas o creación condicional (`count = cond ? 1 : 0`).
- **82 · for_each Meta-Argument:** `for_each` sobre **map o set** → una instancia por clave, direccionada por **clave** → `azurerm_virtual_machine.example["vm1"]`. `each.key` / `each.value`. Claves **estables** → añadir/quitar uno no afecta a los demás (no recrea). Preferido cuando la identidad importa.
- **83 · Demo — for_each:** crear múltiples recursos con `for_each`.
- **84 · Lab — Deploying Multiple Resources with for_each:** desplegar N recursos con `for_each` (map/set).

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `04-configuration` | 09 built-in-functions · 10 dynamic-values (interpolación + data sources) · 11 locals · 12 count-meta-argument · 13 for_each-meta-argument |

**Comparativas creadas:** `count-vs-for-each`.

> Reconciliación: `count`/`for_each`/interpolation/meta-argument/local ya estaban en `glosario.md` (par confuso + términos HCL) → aquí se desarrollan en cards y se cruzan; el glosario se dejó, añadiendo el matiz `locals` (plural, define) vs `local.` (singular, referencia). La interpolación se apoya en `04/01 resource-referencing` (referencia "pelada" sin `${}`) y en `04/05 variable-block` (tipos de colección que alimentan `for_each`) — se referencian, no se repiten. **Los meta-args `depends_on`/`lifecycle` no salen en S10** → se cardean en S13 (bloque `07-maintain`).

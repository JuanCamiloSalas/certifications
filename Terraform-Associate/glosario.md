[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](./README.md)

# Glosario — términos y distinciones de examen

> Referencia única de Terraform. A diferencia del SAA (EN→ES + siglas), aquí pesan los **pares que se confunden** y la **terminología precisa** del lenguaje y la CLI. Búscalo con Ctrl+F durante el repaso.

## ⚠️ Pares que más se confunden

| A | B | Diferencia en una línea |
|---|---|---|
| **`count`** | **`for_each`** | `count` = índice numérico (lista, recrea al reordenar) · `for_each` = mapa/set con **claves estables** (no recrea al reordenar) |
| **`plan`** | **`apply`** | `plan` = previsualiza cambios, no toca infra · `apply` = ejecuta los cambios |
| **`validate`** | **`plan`** | `validate` = sintaxis/consistencia, **no** contacta providers · `plan` = sí consulta el estado real y los providers |
| **`refresh`** | **`plan`** | `refresh` = reconcilia state con la infra real (drift) · `plan` = calcula el diff hacia el estado deseado |
| **Backend local** | **Backend remoto** | local = `.tfstate` en disco (solo tú) · remoto (S3 con `use_lockfile` / HCP) = compartido + **locking** + cifrado. ⚠️ DynamoDB locking **deprecated** |
| **CLI workspaces** | **HCP workspaces** | CLI = varios states de **una misma config** (`terraform workspace`) · HCP = unidad de trabajo en la nube (state + variables + runs propios) |
| **Root module** | **Child module** | root = el directorio actual donde corres Terraform · child = el que invocas con un bloque `module` |
| **Input variable** | **Local value** | variable = entrada parametrizable (desde fuera) · local = valor calculado **dentro** de la config, no se pasa desde fuera |
| **`local-exec`** | **`remote-exec`** | `local-exec` = comando en **tu** máquina · `remote-exec` = comando **en el recurso** creado (vía SSH/WinRM) |
| **`terraform`** | **HCP Terraform** | `terraform` = la CLI/binario open source · HCP Terraform = plataforma SaaS (remote runs, state, registry, Sentinel) |
| **`prevent_destroy`** | **`create_before_destroy`** | `prevent_destroy` = bloquea el destroy del recurso · `create_before_destroy` = crea el nuevo antes de borrar el viejo |

## 🧱 Términos del lenguaje (HCL)

| Término | Qué es |
|---|---|
| **HCL** | HashiCorp Configuration Language — el lenguaje declarativo de Terraform |
| **Provider** | Plugin que habla con una API (AWS, Azure, random, local…) |
| **Resource** | Un objeto de infra gestionado por Terraform (bloque `resource`) |
| **Data source** | Lee info existente/externa sin gestionarla (bloque `data`) |
| **Module** | Conjunto reutilizable de archivos `.tf` invocable con `module` |
| **Variable** | Entrada parametrizable (`variable` block) |
| **Output** | Valor expuesto por una config/módulo (`output` block) |
| **Local** | Valor calculado dentro de la config. Se **define** en `locals {}` (plural) y se **referencia** con `local.<name>` (singular) |
| **Built-in function** | Función nativa `nombre(args)` (string/numeric/collection/type-conversion/CIDR). ⚠️ **No hay funciones definidas por el usuario**; probar en `terraform console` |
| **Meta-argument** | Argumento especial en cualquier recurso: `count` (`count.index`), `for_each` (`each.key`/`each.value`), `depends_on`, `lifecycle`, `provider` |
| **Expression** | Referencias, condicionales `? :`, `for`, splat `[*]`, funciones |
| **Interpolation** | `${...}` para insertar expresiones en strings (fuera de un string, la referencia va "pelada", sin `${}`) |

## ⚙️ Términos de la CLI / estado

| Término | Qué es |
|---|---|
| **State (`.tfstate`)** | Mapa entre tu config y la infra real; guarda **secretos en texto plano** |
| **Backend** | Dónde vive el state y cómo se opera (local / remoto) |
| **State locking** | Bloqueo que impide ejecuciones concurrentes sobre el mismo state |
| **Drift** | Diferencia entre el state y la infra real (cambios fuera de Terraform) |
| **Refresh-only mode** | `plan -refresh-only` (preview) / `apply -refresh-only` (actualiza **state**, no infra) — para **aceptar** drift |
| **Workspace (CLI)** | Contenedor con nombre para un state aislado dentro de una misma config (`terraform workspace`) |
| **`terraform.tfstate.d/`** | Directorio donde viven los states de los workspaces no-`default` (`<name>/terraform.tfstate`) |
| **`use_lockfile`** | State locking nativo de S3 (`= true`); reemplaza el locking por DynamoDB (deprecated) |
| **Lock file (`.terraform.lock.hcl`)** | Fija versiones de providers; se commitea |
| **Plan file (`-out`)** | Plan guardado para aplicar exactamente lo previsto |
| **Provisioner** | Ejecuta scripts al crear/destruir un recurso (**último recurso**) |
| **Taint / `-replace`** | Marca un recurso para recrearlo (`-replace=ADDR` es lo moderno) |
| **Import** | Trae un recurso existente bajo gestión de Terraform |
| **Sentinel** | Policy as code en HCP Terraform |

## 🔢 Operadores de versión

| Operador | Significado |
|---|---|
| `= 1.2.0` | Exactamente esa versión |
| `>= 1.2.0` | Esa o superior |
| `~> 1.2.0` | ≥1.2.0 y <1.3.0 (permite el último dígito) — "pessimistic constraint" |
| `~> 1.2` | ≥1.2 y <2.0 |
| `>= 1.1, < 2.0` | Rango compuesto |

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](./README.md)

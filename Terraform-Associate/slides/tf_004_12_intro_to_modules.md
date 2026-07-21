# S12 — Terraform Modules (resumen de slides)

> Outline de la sección 12 del curso (Bryan Krausen). Tema: **módulos** — empaquetar y reutilizar configuración. 9 clases (91-99), **2 labs**.
> **No es transcripción** del PDF (`tf_004_12_intro_to_modules.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `05-modules` (objetivo **5**). Encaja perfecto — este bloque estaba reservado justo para módulos reales.

## Lectures — por tema

- **91 · Intro to Modules:** un módulo es un **contenedor de recursos relacionados** usados juntos; la forma primaria de **empaquetar y reutilizar** config. Beneficios: patrones consistentes (naming/seguridad/best practices), colaboración (building blocks compartidos), organización (dividir configs grandes en unidades lógicas). Un módulo = una **carpeta con `.tf`** (por convención `main.tf` / `variables.tf` / `outputs.tf`).
- **92 · Parent and Child Modules:** **parent (calling)** = el que referencia/configura otros módulos · **child** = el componente reutilizable que se invoca. El **root module** = el directorio donde corres Terraform (y es el parent cuando llama hijos). Los módulos se obtienen de un **registry**, un **repo (git)** o **localmente**.
- **93 · Module Versioning & Version Constraints:** los módulos evolucionan (v5.10→v5.14: baseline, nueva funcionalidad, cambio de API del provider). **Fijar (`pin`) una versión** para estabilidad → `version = "4.0.1"` o restricciones (`~>`). ⚠️ **`version` solo aplica a módulos del registry** (git usa `?ref=`, local no versiona).
- **94 · Calling Modules with the Module Block:** `module "name" { source = ...  version = ...  <inputs> }`. `source` = **dónde** está para descargarlo · `version` = qué versión · el resto = **variables de entrada** que se pasan al módulo. Hay que correr **`terraform init`** (o `terraform get`) para **descargar** los módulos antes de plan/apply. Ejemplo real: `terraform-aws-modules/vpc/aws` (formato registry `NAMESPACE/NAME/PROVIDER`).
- **95 · Variable Scope in Modules:** **cada módulo tiene su propio scope aislado** (hay un BOUNDARY). Parent y child pueden tener variables con el mismo nombre sin colisionar. **Por defecto el root NO tiene acceso** a datos/variables del child. Paso de datos:
  - **Entrada (in):** en el `module` block, `env = var.environment` → dentro del child se lee como `var.env`.
  - **Salida (out):** el child declara `output`s; el root los lee con **`module.<name>.<output>`** (p.ej. `module.network.subnet_1`).
- **96 · Demo — Modules from the Terraform Registry:** usar módulos del registry público.
- **97 · Lab — Using Terraform Registry Modules:** invocar un módulo del registry (VPC AWS).
- **98 · Demo — Writing and Using Your Own Modules:** escribir un módulo propio (child local) con sus `variables.tf`/`outputs.tf` y llamarlo desde el root.
- **99 · Lab — Writing and Using Your Own Modules:** crear y consumir un módulo local propio.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `05-modules` | 01 what-is-a-module (root/parent/child) · 02 module-block (llamar, `source`, init/get) · 03 module-sources-and-versioning (registry/git/local; `version` solo registry) · 04 module-inputs-outputs-scope (aislamiento; args→`var`; `module.<name>.<output>`) |

**Comparativas creadas:** `module-source-types` (registry vs git vs local).

> Reconciliación: los `output` (bloque `04/07`) y `variable` (bloque `04/05`) ya existían → aquí se cruzan como el mecanismo de **inputs/outputs** entre módulos. Los meta-args `count`/`for_each` (bloque `04/12-13`) **también aplican al `module` block** → se referencian desde la card del module block, no se repiten. `version`/`~>` ya estaban en `04/08 terraform-block` (para providers) → se reutiliza el operador, matizando que aquí es la **versión del módulo** y solo para registry. Glosario: Root/Child module ya estaban → añadidos `module` block, source y `module.<name>.<output>`.

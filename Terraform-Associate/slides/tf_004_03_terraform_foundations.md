# S3 — Terraform Foundations (resumen de slides)

> Outline de los temas cubiertos en la sección 3 del curso (Bryan Krausen).
> **No es transcripción** del PDF (`tf_004_03_terraform_foundations.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `01-iac` (objetivo 1) + bloque `02-fundamentals` (objetivo 2).

## Lecture 1 — Introduction to HashiCorp Terraform

- **What is Terraform?** IaC estándar de la industria que automatiza *provisioning*, *management* y *versioning* de infraestructura. Tres pilares:
  - **Codify your infrastructure** — flujo repetible y versionado en vez de clicar en la consola.
  - **Standardize workflows** — una sola herramienta para desplegar/gestionar recursos.
  - **Platform agnostic** — HCL para provisionar en cualquier cloud/datacenter.
- **Benefits of Terraform:** version control & auditability · collaboration · scalability & flexibility · automation & efficiency · consistency & repeatability (reduce *configuration drift* y errores humanos).
- **Platform agnostic:** cloud platforms + otros servicios vía *providers*.
- **Aviso:** antes de usar Terraform hay que dominar la plataforma destino (Terraform no es magia).
- **Traditional provisioning vs provisioning con Terraform** (VM/Container/Network → application workload).
- **Reusing code:** input variables (mismo config, distintos valores → Web app vs Data app).
- **IaC = tratar la infra como código de aplicación:** ramas, pull requests, equipos (network, k8s, cloud ops).
- **Speed & consistency:** spin up/decommission rápido para dev/test/QA/prod; componentes estandarizados.
- **Core components:** Terraform Core · Providers · Resources · State · Modules.
- **Terraform editions:** Command-Line Based (CLI OSS) · SaaS Platform (HCP Terraform) · Self-Hosted & Managed (Terraform Enterprise).
- **Compare con otras herramientas:**
  - *Similar (IaC):* AWS CloudFormation, Azure Bicep, Pulumi.
  - *Different but complementary (Configuration Management):* Ansible/Chef/Puppet.
  - IaC = infra provisioning & management, declarative, immutable infrastructure, modular design.
  - Config mgmt = instalar paquetes, gestionar ficheros, config de sistemas, tareas rutinarias/multi-step.
- **Declarative vs imperative:** declarativo = *qué* quieres (el resultado); imperativo = *cómo* (paso a paso).
- **Desired state:** lo que escribes en la config es el *desired state*; Terraform compara *current state* (real) vs *desired* y aplica solo los cambios necesarios.
- Resumen de la lecture.

## Lecture 2 — Learn the Basics of HCL

- **HCL (HashiCorp Configuration Language):** lenguaje declarativo, fácil de leer/escribir, la interfaz principal de Terraform.
- **HCL example (`main.tf`):** bloques `data`, bloque `resource`, *arguments*, comentario de una línea.
- **Anatomía de un bloque:** tipo de bloque + tipo de recurso + nombre de recurso + `{ ... }` (p.ej. `resource "aws_vpc" "vpc" {}`).
- **HCL style guide:**
  - `#` para comentarios de una línea y de bloque.
  - `_` (underscores) para separar palabras en nombres.
  - Indentar **2 espacios** por nivel de anidamiento.
  - Alinear los `=` en líneas consecutivas.
  - Líneas en blanco para separar grupos de argumentos.
- **Resource referencing:** conectar recursos entre sí para compartir datos y construir *dependencies* (resource ↔ resource ↔ data/variable/output).
- **DEMO:** basics of HCL.
- **Best practices for HCL:** file extensions (`.tf`) · formatting · organization · commenting & documentation · **avoid hardcoding values**.
- **Enhancing code quality:** linters & extensiones (VSCode, autocompletado) + herramientas built-in → `terraform fmt` (formatea automáticamente para consistencia).
- Resumen de la lecture.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `01-iac` | 01 what-is-iac · 02 iac-benefits · 03 declarative-vs-imperative |
| `02-fundamentals` | 01 what-is-terraform · 02 core-components · 03 desired-state · 04 terraform-vs-other-tools · 05 terraform-editions · 06 hcl-basics (blocks + style + fmt) |
| `04-configuration` | 01 resource-referencing _(introducido en S3; objetivo 4)_ |

> Consolidado tras revisión: HCL blocks/style/fmt en una sola card; resource-referencing movido al bloque 04; cards conceptuales sin `Syntax/Example` de relleno.
</content>
</invoke>

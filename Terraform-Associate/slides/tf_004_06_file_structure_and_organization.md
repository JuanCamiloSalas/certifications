# S6 — File Structure and Organization (resumen de slides)

> Outline de la sección 6 del curso (Bryan Krausen).
> **No es transcripción** del PDF (`tf_004_06_file_structure_and_organization.pdf`, no versionado) — es el índice de lo que vi, para dar contexto a futuras sesiones y saber qué está convertido en cards.
> **Alimenta:** bloque `04-configuration` (objetivo 4).

## Lecture — File Structure and Organization

- **Organizing code:** un requerimiento de infra (S3, VM, subnet, firewall, DNS, LB, k8s) puede vivir en un solo `customer-app.tf` o repartirse en varios `.tf` (`network.tf`, `firewall.tf`, `dns.tf`, `variables.tf`, `outputs.tf`…).
- **Executing code:** Terraform **procesa todos los archivos del working directory juntos** — los concatena como una sola config (el split es para humanos).
- **Common Terraform files:** `main.tf` (recursos primarios) · `variables.tf` (declaraciones) · `outputs.tf` (valores de salida) · `providers.tf` (config/requisitos de providers) · `terraform.tfvars` (valores de variables, normalmente git-ignored).
- **Additional files (gestionados por Terraform):** `terraform.tfstate` (estado) · `terraform.tfstate.backup` (estado previo) · `.terraform.lock.hcl` (lock de versiones de providers) · `.gitignore` (qué ignora Git).
- **Working directory & subdirectorios:** dividir en `prod/`, `test/`, `dev/`, `projectX/` → states separados → **reducir el blast radius**. Push/pull vía Git repo.
- **Summary:** organizar en varios `.tf` · Terraform solo procesa el working dir actual salvo que referencies otros (módulos) · Terraform crea/gestiona ficheros de state y config · los nombres comunes son convención, no obligatorios · combina todos los archivos al ejecutar.

## Cards generadas desde esta sección

| Bloque | Cards |
|---|---|
| `04-configuration` | 02 file-structure (all `.tf` merged · conventional filenames · state/backup/lock/`.gitignore` · subdirs & blast radius) |

> Nota: la idea "Terraform funde todos los `.tf`" ya aparecía en `02/06 hcl-basics`; aquí se consolida el **inventario de archivos** (state/lock/gitignore) y el **blast radius**.

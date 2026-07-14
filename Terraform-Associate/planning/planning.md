[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

# Plan de estudio — Terraform Associate (004)

> **🎯 EXAMEN: viernes 31 de julio de 2026.** Online proctored, opción múltiple, 1 hora. Versión **004** (evalúa Terraform 1.12).
> **Punto de partida:** estudio arranca el **miércoles 1 de julio de 2026**. ~4,5 semanas → ritmo ágil pero alcanzable (recién aprobado el SAA con 845, vienes en forma).

## 🧭 Filosofía para ESTE examen

A diferencia del SAA (escenarios), el Terraform Associate es **práctico y preciso**: sintaxis HCL, el workflow de CLI, y cómo se comporta el state. **La regla de oro: por cada concepto, escríbelo y ejecútalo.** Leer la doc sin `terraform apply` no fija nada. Monta un proyecto sandbox (un provider gratis como `random`, `local`, `null`, o AWS free tier) y toca todo.

> El método que te funcionó en el SAA (flashcards de lo no obvio + simulacros + repaso dirigido) se mantiene; solo le sumamos **labs prácticos** como pilar.

## ⏱️ Disponibilidad y ritmo

> **Eje = el orden real del curso (secciones), no el orden de objetivos.** El curso interleava los temas con criterio pedagógico; seguirlo en orden es lo más eficiente. La columna "Objetivos" indica qué objetivo del examen cubre cada tramo, para que sepas dónde estás respecto al blueprint. Carga total: ~20 h de vídeo (S3-S17) + 9 labs → ~5 h/semana.

| Semana | Fechas | Secciones del curso | Objetivos | Vídeo |
|---|---|---|---|---|
| **1** | Mié 1 – dom 5 jul | Setup (S1-2: instalar Terraform + sandbox) · **S3** Foundations · **S4** Core Workflow · **S5** CLI · **S6** File Structure | 1, 2, 3 | ~3,4 h |
| **2** | Lun 6 – dom 12 jul | **S7** Configuration Fundamentals · **S8** Hands-On Labs · **S9** Managing State | 4, 6 | ~5,3 h |
| **3** | Lun 13 – dom 19 jul | **S10** Making Code Reusable · **S11** Refactoring State · **S12** Modules · **S13** Resource Behavior & Dependencies | 5, 6, 7 | ~5,2 h |
| **4** | Lun 20 – dom 26 jul | **S14** Securing Configs · **S15** Troubleshooting · **S16** HCP Terraform + **Simulacro #1** | 4, 7, 8 | ~4,5 h |
| **5** | Lun 27 – jue 30 jul | **S17** Exam Prep (repaso por objetivo) + **Simulacro #2** + cheat-sheet. Cerrar temas flojos. Jue 30: cierre temprano. | todos | ~1,8 h |
| **🎯** | **Vie 31 jul** | **EXAMEN.** | — | — |

> ⚠️ **Time-box en S16 (HCP Terraform):** es la sección más larga del curso (3 h 7 min / 18 clases) pero HCP es solo 1 de 8 objetivos y pesa modesto. No te claves; cubre lo esencial (remote runs, remote state, private registry, Sentinel, workspaces HCP vs CLI) y sigue.

## 🔑 Temas clave / gotchas del examen (donde caen las preguntas)

Estos son los puntos que el examen 004 explota con preguntas precisas — fíjalos especialmente:

**Workflow & CLI**
- `terraform init` → descarga providers/módulos e inicializa el backend. Obligatorio antes de plan/apply.
- `plan` (previsualiza) · `apply` · `destroy` · flags: `-auto-approve`, `-target`, `-var`, `-var-file`.
- `fmt` (formatea), `validate` (sintaxis/consistencia, **no** contacta providers), `console` (probar expresiones).

**Variables — precedencia (de menor a mayor):**
1. valores por defecto → 2. variables de entorno `TF_VAR_*` → 3. `terraform.tfvars` → 4. `*.auto.tfvars` (orden alfabético) → 5. `-var` / `-var-file` en CLI (gana).

**State**
- El `.tfstate` guarda **secretos en texto plano** → nunca al control de versiones; usa backend remoto.
- Backend remoto típico: **S3** (locking nativo con `use_lockfile = true` — ⚠️ **DynamoDB deprecated** en 004) o **HCP Terraform**. El **state locking** evita ejecuciones concurrentes.
- Comandos: `state list`, `terraform show`, `state show`, `state mv`, `state rm`; drift con `plan/apply -refresh-only`. Workspaces (CLI) con `terraform workspace`.
- `terraform_remote_state` (data source) = leer outputs de otro state.

**Módulos**
- `source` (registry público, Git, ruta local) + `version` (solo aplica al registry).
- Input variables (entradas) y outputs (salidas) para componer módulos. El módulo raíz es el del directorio actual.

**Meta-argumentos**
- `count` (índice numérico) vs `for_each` (mapa/set, claves estables) — saber cuándo usar cada uno.
- `depends_on` (dependencia explícita), `lifecycle` (`create_before_destroy`, `prevent_destroy`, `ignore_changes`).

**Providers**
- `required_providers` + restricciones de versión (`~>`, `>=`, `=`). `alias` para múltiples configuraciones del mismo provider.

**Provisioners (último recurso)**
- `local-exec` / `remote-exec`; creation-time vs destroy-time (`when = destroy`). El examen pregunta que son el **último recurso**, no la práctica recomendada.

**HCP Terraform / Terraform Cloud**
- Remote runs, integración VCS, **private module registry**, remote state, teams, y **Sentinel** (policy as code). Diferencia entre **CLI workspaces** y **Terraform Cloud workspaces**.

## 📚 Recursos

- Ruta oficial de tutoriales (004) y guía de objetivos — ver [README](../README.md).
- Doc oficial de Terraform (registry, CLI, language).
- Simulacros: busca bancos de preguntas estilo examen (similar a lo que hiciste con Dojo en el SAA).

## ✅ Checklist final (jueves 30 jul)

- [ ] Los 8 dominios cubiertos con al menos un lab práctico cada uno.
- [ ] 2 simulacros hechos y revisados; temas flojos cerrados.
- [ ] Cheat-sheet de gotchas (precedencia de variables, comandos de state, meta-argumentos) repasada.
- [ ] Logística del examen confirmada (proctoring, ID, conexión, espacio despejado).
- [ ] Sandbox: `terraform destroy` de todo lo creado (no dejar recursos AWS encendidos 💸).
- [ ] Cierre temprano. Llegar fresco.

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

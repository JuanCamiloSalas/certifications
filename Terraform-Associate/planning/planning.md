[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

# Plan de estudio — Terraform Associate (003)

> **🎯 EXAMEN: viernes 31 de julio de 2026.** Online proctored, ~57 preguntas, 60 min.
> **Punto de partida:** estudio arranca el **miércoles 24 de junio de 2026** (recién aprobado el SAA con 845; lun 22 – mar 23 de descanso). ~5 semanas → ritmo cómodo.

## 🧭 Filosofía para ESTE examen

A diferencia del SAA (escenarios), el Terraform Associate es **práctico y preciso**: sintaxis HCL, el workflow de CLI, y cómo se comporta el state. **La regla de oro: por cada concepto, escríbelo y ejecútalo.** Leer la doc sin `terraform apply` no fija nada. Monta un proyecto sandbox (un provider gratis como `random`, `local`, `null`, o AWS free tier) y toca todo.

> El método que te funcionó en el SAA (flashcards de lo no obvio + simulacros + repaso dirigido) se mantiene; solo le sumamos **labs prácticos** como pilar.

## ⏱️ Disponibilidad y ritmo

| Semana | Fechas | Foco |
|---|---|---|
| **0** | Lun 22 – mar 23 jun | 🛌 Descanso post-SAA. Opcional: instalar Terraform + montar el sandbox. |
| **1** | Mié 24 – dom 28 jun | Dominios **1, 2, 3**: IaC, propósito de Terraform, basics (providers, `init/plan/apply/destroy`). |
| **2** | Lun 29 jun – dom 5 jul | Dominio **6** (core workflow a fondo) + Dominio **8** (configuración: variables, outputs, data sources, expresiones, funciones). |
| **3** | Lun 6 – dom 12 jul | Dominio **7** (state: backends remotos, locking, comandos de state, datos sensibles) + Dominio **5** (módulos). |
| **4** | Lun 13 – dom 19 jul | Dominio **4** (fuera del core workflow: import, `-replace`, console, fmt, validate, provisioners, workspaces) + Dominio **9** (HCP Terraform / Terraform Cloud). |
| **5** | Lun 20 – dom 26 jul | **Repaso dirigido + Simulacro #1**. Cerrar los temas flojos que salgan. |
| **6** | Lun 27 – jue 30 jul | **Simulacro #2** + cheat-sheet + repaso final ligero. Jue 30: cierre temprano. |
| **🎯** | **Vie 31 jul** | **EXAMEN.** |

## 🔑 Temas clave / gotchas del examen (donde caen las preguntas)

Estos son los puntos que el examen 003 explota con preguntas precisas — fíjalos especialmente:

**Workflow & CLI**
- `terraform init` → descarga providers/módulos e inicializa el backend. Obligatorio antes de plan/apply.
- `plan` (previsualiza) · `apply` · `destroy` · flags: `-auto-approve`, `-target`, `-var`, `-var-file`.
- `fmt` (formatea), `validate` (sintaxis/consistencia, **no** contacta providers), `console` (probar expresiones).

**Variables — precedencia (de menor a mayor):**
1. valores por defecto → 2. variables de entorno `TF_VAR_*` → 3. `terraform.tfvars` → 4. `*.auto.tfvars` (orden alfabético) → 5. `-var` / `-var-file` en CLI (gana).

**State**
- El `.tfstate` guarda **secretos en texto plano** → nunca al control de versiones; usa backend remoto.
- Backend remoto típico: **S3 + DynamoDB** (locking) o **Terraform Cloud**. El **state locking** evita ejecuciones concurrentes.
- Comandos: `state list`, `state show`, `state mv`, `state rm`, `terraform refresh`.
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

- Ruta oficial de tutoriales (003) y guía de objetivos — ver [README](../README.md).
- Doc oficial de Terraform (registry, CLI, language).
- Simulacros: busca bancos de preguntas estilo examen (similar a lo que hiciste con Dojo en el SAA).

## ✅ Checklist final (jueves 30 jul)

- [ ] Los 9 dominios cubiertos con al menos un lab práctico cada uno.
- [ ] 2 simulacros hechos y revisados; temas flojos cerrados.
- [ ] Cheat-sheet de gotchas (precedencia de variables, comandos de state, meta-argumentos) repasada.
- [ ] Logística del examen confirmada (proctoring, ID, conexión, espacio despejado).
- [ ] Sandbox: `terraform destroy` de todo lo creado (no dejar recursos AWS encendidos 💸).
- [ ] Cierre temprano. Llegar fresco.

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

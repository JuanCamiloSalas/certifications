[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

# 🧾 Cheat-sheet final — Terraform Associate (004)

> La hoja de la recta final. Todo lo memorizable de golpe: comandos, flags, precedencias y gotchas. Repásala el día antes. Se llena durante el estudio — arranca con el esqueleto y lo afinas según lo que se te resista.

## ⌨️ CLI esencial

| Comando | Qué hace |
|---|---|
| `terraform init` | Descarga providers/módulos, inicializa el backend. **Obligatorio** antes de plan/apply. |
| `terraform init -migrate-state` | Migra el state al cambiar de backend. |
| `terraform plan` | Previsualiza cambios (no toca infra). |
| `terraform plan -out=tfplan` | Guarda el plan para aplicarlo exacto. |
| `terraform apply` | Aplica cambios (pide confirmación). |
| `terraform apply -auto-approve` | Aplica sin confirmar. |
| `terraform apply tfplan` | Aplica un plan guardado (no repregunta). |
| `terraform destroy` | Destruye todo lo gestionado. |
| `terraform fmt` | Formatea el código. |
| `terraform validate` | Valida sintaxis/consistencia (**no** contacta providers). |
| `terraform console` | REPL para probar expresiones y funciones. |
| `terraform show` | Muestra state o un plan en formato legible. |
| `terraform output` | Imprime los outputs. |
| `terraform graph` | Genera el grafo de dependencias. |

## 🚩 Flags que caen

- `-target=ADDR` — limita la operación a un recurso (uso excepcional).
- `-var 'k=v'` / `-var-file=archivo.tfvars` — pasar variables.
- `-replace=ADDR` — fuerza recrear un recurso (sustituye a `taint`).
- `-auto-approve` — sin confirmación.
- `-out=archivo` — guarda el plan.

## 🥇 Precedencia de variables (menor → mayor; gana la última)

1. `default` en el bloque `variable`
2. Variables de entorno `TF_VAR_<nombre>`
3. `terraform.tfvars`
4. `terraform.tfvars.json`
5. `*.auto.tfvars` / `*.auto.tfvars.json` (orden **alfabético**)
6. `-var` / `-var-file` en la CLI ← **gana**

## 🗃️ State

- `.tfstate` guarda **secretos en texto plano** → nunca al control de versiones; usa backend remoto.
- Backend remoto típico: **S3 + DynamoDB** (locking) o **HCP Terraform**.
- **State locking** evita ejecuciones concurrentes.
- Comandos: `state list`, `state show`, `state mv`, `state rm`, `state pull`, `state push`.
- `terraform_remote_state` (data source) = leer outputs de otro state.
- `terraform refresh` / refresh-only = reconciliar con la infra real (drift).

## 🔁 Meta-argumentos

- `count` (índice numérico) vs `for_each` (mapa/set, claves estables).
- `depends_on` (dependencia explícita).
- `lifecycle`: `create_before_destroy`, `prevent_destroy`, `ignore_changes`.
- `provider` (elegir alias).

## 📦 Módulos

- `source`: registry (público/privado), Git, ruta local.
- `version`: **solo** aplica al registry.
- Root module = directorio actual; child = invocado con `module`.

## 🔢 Operadores de versión

`=` exacta · `>=` esa o superior · `~>` pessimistic (`~> 1.2.0` → <1.3.0; `~> 1.2` → <2.0) · rango compuesto `>= 1.1, < 2.0`.

## 🧰 Provisioners (último recurso)

- `local-exec` (tu máquina) / `remote-exec` (en el recurso).
- creation-time (default) vs destroy-time (`when = destroy`).
- El examen pregunta que son el **último recurso**, no la práctica recomendada.

## ☁️ HCP Terraform

- Remote runs, remote state, **private module registry**, **Sentinel** (policy as code), cost estimation, teams.
- Workflows: **CLI-driven · VCS-driven · API-driven**.
- **HCP workspaces ≠ CLI workspaces.**

## ⚠️ Gotchas frecuentes

- `validate` **no** contacta providers; `plan` sí.
- Reordenar una lista con `count` **recrea** recursos; `for_each` con claves estables, no.
- `version` se ignora en módulos con `source` Git o local.
- Cambiar de backend requiere `init` (con `-migrate-state` si quieres conservar el state).
- `.terraform.lock.hcl` se **commitea** (fija versiones de providers).

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

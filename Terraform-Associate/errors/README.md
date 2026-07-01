[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

# Error Reviews — Practice tests

> Un archivo por simulacro (`test-review-N.md`) en formato *weak points*: scorecard por objetivo + errores agrupados por prioridad + tabla resumen. Tras cada simulacro: registrar errores y actualizar el **progreso por objetivo** y el **consolidado de cards** de abajo. (Mismo método que funcionó en el SAA.)

## Reviews por simulacro

| Test | Fecha | Score | Review |
|---|---|---|---|
| _(none yet)_ | — | — | — |

---

## Progreso por objetivo

> Actualiza esta tabla tras cada simulacro. Lectura = tendencia, no medida exacta.

| # | Objetivo | #1 | #2 | Lectura |
|---|---|---|---|---|
| 1 | Infrastructure as Code (IaC) | — | — | — |
| 2 | Terraform fundamentals | — | — | — |
| 3 | Core workflow & CLI | — | — | — |
| 4 | Read & write configuration | — | — | — |
| 5 | Modules | — | — | — |
| 6 | State management | — | — | — |
| 7 | Maintain infrastructure | — | — | — |
| 8 | HCP Terraform | — | — | — |

---

## Cards a repasar — consolidado

> Orden de prioridad: lo que **repites entre simulacros** o pesa más, primero. "Fallos" = veces que el tema cayó.

### 🔴 Crítico — crónico (≥2 tests) o ≥3 fallos

| Card | Tema | Objetivo | Fallos |
|---|---|---|---|
| _(none yet)_ | — | — | — |

### 🟡 Importante — 1–2 fallos

| Card | Tema | Objetivo | Fallos |
|---|---|---|---|
| _(none yet)_ | — | — | — |

### ⚠️ Sin card — candidatos a crear

| Tema | Objetivo | Nota |
|---|---|---|
| _(none yet)_ | — | — |

---

## Cómo registrar un nuevo simulacro

1. Sube los screenshots de las preguntas a `errors/test-N/`.
2. Crea `errors/test-review-N.md` copiando el formato de un review existente (scorecard → secciones por objetivo → summary). Mientras no exista uno, usa el esqueleto de abajo.
3. Actualiza la tabla **Reviews por simulacro**, el **Progreso por objetivo** y el **consolidado de cards** (suma los `Fallos` de los temas que reaparezcan; sube a 🔴 lo que caiga en ≥2 tests).

### Esqueleto de `test-review-N.md`

```markdown
# Terraform Practice Test N — Weak Points

**Result:** XX% (NN/MM). YYYY-MM-DD.

| Objetivo | Score | Priority |
|---|---|---|
| ... | ... | 🔴/🟡/🟢 |

# 🔴 1. <Objetivo> 

## 1.1 <Tema fallado>
**Sample question:** *"..."*
- ✅ correcto — por qué.
- ❌ distractor — por qué no.
> [!TIP]
> Regla de examen: ...
> 📇 [Card: ...](../cards/NN-block/...)
```

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

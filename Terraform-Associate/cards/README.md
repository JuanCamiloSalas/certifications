[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

# 🃏 Terraform Associate Deck

> Flashcards for the Terraform Associate (004) exam. Each file is a self-contained card. Use the **Prev / Next** buttons inside every card to navigate.

> **Golden rule of this exam:** for every concept, **write it and run it**. A card should capture what you confirmed with `terraform apply`, not what you skimmed in the docs.

## 📚 Blocks (= the 8 exam objectives)

| # | Block | Objetivo 004 |
|---|---|---|
| 01 | [Infrastructure as Code (IaC)](./01-iac/README.md) | 1 — Learn about IaC |
| 02 | [Terraform fundamentals](./02-fundamentals/README.md) | 2 — Review Terraform fundamentals |
| 03 | [Core workflow & CLI](./03-core-workflow/README.md) | 3 — Use the core Terraform workflow |
| 04 | [Read & write configuration](./04-configuration/README.md) | 4 — Variables, outputs, data, functions |
| 05 | [Modules](./05-modules/README.md) | 5 — Use and create modules |
| 06 | [State management](./06-state/README.md) | 6 — Backends, locking, state commands |
| 07 | [Maintain infrastructure](./07-maintain/README.md) | 7 — import, replace, workspaces, provisioners |
| 08 | [HCP Terraform](./08-hcp-terraform/README.md) | 8 — Use HCP Terraform |

## 🧭 How to navigate

- **Mobile (GitHub app):** open a block, pick any card, and use the `Prev` / `Next` buttons to walk through the whole block.
- **Desktop:** open the block's README to see all its cards listed, or use the file finder (`t`) and type the concept.

## 🔄 Flujo: generar cards al terminar una sección del curso

> Convención con Claude. Cuando termines una sección del curso, Claude genera las cards correspondientes.

**Disparador:** escribe `cards S7` (o "terminé la sección 7").

**Dos modos:**

- ⚡ **Rápido** — solo `cards S7`. Claude genera las cards de los temas estándar de esa sección.
- 🎯 **Fiel (recomendado)** — `cards S7` + la **lista de clases** de la sección y/o **lo que se te hizo no-obvio**. Cards calcadas a tu curso, sin inventar cobertura. Encaja con la regla de "solo lo no obvio".

**Qué hace Claude:** mapea la sección → bloque correcto (tabla abajo) · redacta con el template · numera · cablea prev/next · actualiza la tabla del block README. Tú solo revisas.

**Mapeo sección del curso → bloque de cards** (el curso interleava, así que el nº no siempre coincide):

| Sección curso | Bloque(s) |
|---|---|
| S3 Foundations | `01-iac` + `02-fundamentals` |
| S4 Core Workflow · S5 CLI | `03-core-workflow` |
| S6 File Structure · S7 Config · S14 Securing | `04-configuration` |
| S8 Hands-On Labs | refuerzan 03/04 (gotchas de lab si surgen) |
| S9 Managing State · S11 Refactoring State | `06-state` |
| S10 Making Code Reusable · S12 Modules | `05-modules` |
| S11 (import) · S13 Dependencies · S15 Troubleshooting | `07-maintain` |
| S16 HCP Terraform | `08-hcp-terraform` |
| S17 Exam Prep | repaso global — rellenar huecos, no cards nuevas |

## ➕ How to add a new card

1. Copy [`_TEMPLATE.md`](./_TEMPLATE.md) into the matching block folder.
2. Rename: `NN-short-name.md` (NN = next number in the block).
3. Update the prev/next buttons at the top and bottom of the new card.
4. Add the new card to the block's `README.md` table.
5. If inserted in the middle, also fix the `next` of the previous card and the `prev` of the following card.

## 📏 Quality rules

- **Language: English only** (the exam is English-only — cards mirror it).
- **Show the code.** Unlike SAA (scenario → service), this exam is syntax/CLI/state. Every card carries a real HCL snippet or the CLI command + the flags that matter. A card with no `💻 Syntax / Example` is usually incomplete.
- One topic = one card. Keep a topic together even if the card runs long.
- No transcribing docs. Only non-obvious facts, precise flags/precedences, or things that already tricked you in a practice test.
- **Required sections:** Pitch, "What the exam tests", "Core", "Syntax / Example" — always. "Flags & values to memorize" and "Easily confused with" only if applicable. Traps and Diagram are optional.
- **Images:** Mermaid for conceptual flows (workflow, state locking, dependency graph). For a real diagram, download it into [`../assets/`](../assets/) and link locally (no fragile external URLs).
- Long versus comparisons live in [`../comparativas/`](../comparativas/), not here.

---

[![](https://img.shields.io/badge/<_Terraform-7B42BC?style=for-the-badge)](../README.md)

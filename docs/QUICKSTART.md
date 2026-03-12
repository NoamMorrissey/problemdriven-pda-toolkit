# Quick Start Guide / Guía de inicio rápido

## Before You Begin / Antes de empezar

**EN:** This toolkit assumes you've already done the hard human work: talked to real people who live the problem, collected evidence, and aligned your team. If you haven't, the templates will feel empty. That's by design — the toolkit doesn't replace thinking, it structures it.

**ES:** Este toolkit asume que ya has hecho el trabajo humano difícil: hablar con personas reales que viven el problema, recopilar evidencia y alinear a tu equipo. Si no lo has hecho, las plantillas se sentirán vacías. Es intencional: el toolkit no reemplaza el pensamiento, lo estructura.

---

## Step 1: Setup / Paso 1: Configuración (5 min)

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project

# Choose your AI agent / Elige tu agente IA
specify init --here --ai claude      # Claude Code
specify init --here --ai copilot     # GitHub Copilot
specify init --here --ai cursor      # Cursor

git init && git add -A && git commit -m "Initial PDA + Spec Kit setup"
```

---

## Step 2: Phase 1 — Problem / Fase 1 — Problema

1. The repo includes a complete example. To start fresh:
   `cp docs/templates/pda-problem.template.md docs/pda-problem.md`
2. Fill all 9 elements with your research / Rellena los 9 elementos con tu investigación
3. Reference evidence for every claim / Referencia evidencia para cada afirmación
4. Run: `/pda.validate-problem`
5. Fix flagged issues / Corrige los problemas señalados
6. Get stakeholder approval → **Gate 1** / Obtener aprobación de stakeholders → **Gate 1**

---

## Step 3: Phase 2 — Solution / Fase 2 — Solución

1. Start fresh: `cp docs/templates/pda-solution-brief.template.md docs/pda-solution-brief.md`
2. Explore solutions freely (no agents yet) / Explorar soluciones libremente (sin agentes aún)
3. Fill all 8 sections / Rellena las 8 secciones
4. Every component needs `gap_ref` + `success_ref`
5. Complete translatability map / Completar mapa de traducibilidad
6. Run: `/pda.validate-solution`
7. Get team consensus → **Gate 2** / Obtener consenso del equipo → **Gate 2**

---

## Step 4: Phase 3 — Context / Fase 3 — Contexto

```
/pda.adapt-constitution     → Generates constitution.md
                              Review output / Revisar output

/pda.adapt-specify          → Prepares specification inputs
/speckit.specify            → Spec Kit generates the spec
/pda.verify-specify         → Traceability check / Verificación de trazabilidad

/speckit.plan               → Technical plan
/pda.verify-plan            → Traceability + coverage / Trazabilidad + cobertura

/speckit.tasks              → Task breakdown
/pda.verify-tasks           → Traceability check / Verificación de trazabilidad
```

---

## Step 5: Phase 4 — Build / Fase 4 — Construcción

```
/speckit.implement           → Code generation / Generación de código
/pda.verify-build            → Fidelity check / Verificación de fidelidad
```

---

## What Each Command Catches / Qué detecta cada comando

| Command | Catches / Detecta |
|---|---|
| `/pda.validate-problem` | Missing evidence, incomplete elements, contradictions, stale data |
| `/pda.validate-solution` | Orphan components, missing traceability, vague dimensions |
| `/pda.verify-specify` | Scope creep, missing PS connections, inconsistent criteria |
| `/pda.verify-plan` | Unrequired plan elements, missing SB components |
| `/pda.verify-tasks` | Orphan tasks, uncovered requirements |
| `/pda.verify-build` | Output not addressing the gap, unverifiable criteria |

---

## Tips / Consejos

- **Don't skip Phase 1.** A bad Problem Statement means everything downstream is wrong.
  **No te saltes la Fase 1.** Un mal Problem Statement significa que todo lo demás está mal.

- **Evidence matters.** Claims without evidence are assumptions. Label them honestly.
  **La evidencia importa.** Afirmaciones sin evidencia son supuestos. Etiquétalos honestamente.

- **The adapter translates, not replaces.** Vague Solution Brief → vague spec.
  **El adaptador traduce, no reemplaza.** Solution Brief vaga → spec vaga.

- **Verify after every step.** Fixing a spec is cheaper than fixing code.
  **Verifica tras cada paso.** Corregir una spec es más barato que corregir código.

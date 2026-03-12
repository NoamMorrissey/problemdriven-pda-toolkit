# Quick Start Guide / Guía de inicio rápido

## Before You Begin / Antes de empezar

**EN:** This toolkit assumes you've already done the hard human work: talked to real people who live the problem, collected evidence, and aligned your team. If you haven't, the templates will feel empty. That's by design — the toolkit doesn't replace thinking, it structures it.

**ES:** Este toolkit asume que ya has hecho el trabajo humano difícil: hablar con personas reales que viven el problema, recopilar evidencia y alinear a tu equipo. Si no lo has hecho, las plantillas se sentirán vacías. Es intencional: el toolkit no reemplaza el pensamiento, lo estructura.

---

## Step 1: Setup / Paso 1: Configuración (5 min)

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project
```

---

## Step 2: Phase 1 — Problem / Fase 1 — Problema

1. Gather your research evidence (interviews, surveys, analytics, competitor analysis).
   Reúne tu evidencia de investigación (entrevistas, encuestas, analítica, análisis competitivo).

2. Run the problem agent with your evidence:
   ```
   /pda-problem
   ```
   Provide your evidence files when prompted. The agent reads them, generates a Problem Statement with 9 elements, and validates every claim against the evidence.

3. Review the generated PS. The agent will ask: **"Do you approve this Problem Statement?"**

4. If something needs changing, tell the agent what to fix. It will regenerate and present again.

5. Once approved → the agent writes `docs/pda-problem.md` → **Gate 1 passed**.

---

## Step 3: Phase 2 — Solution / Fase 2 — Solución

1. Run the solution agent:
   ```
   /pda-solution
   ```
   It reads your approved PS and generates a Solution Brief with business decisions only: components, success criteria, constraints, actor map.

2. **Important:** The SB contains NO technical decisions. No stack, no architecture, no data model. Those come in Phase 3.

3. Review the generated SB. Every component must have `gap_ref` + `success_ref` tracing to the PS.

4. Once approved → the agent writes `docs/pda-solution-brief.md` → **Gate 2 passed**.

---

## Step 4: Phase 3 — Context / Fase 3 — Contexto

1. Run the context agent:
   ```
   /pda-context
   ```
   It reads your PS + SB and generates a Context Specification with all technical decisions: stack, architecture, data model, interaction patterns, visual design, accessibility, error handling.

2. The agent will ask you when the SB is ambiguous on a technical point — it never invents.

3. Review the generated Context Spec. Every technical decision must justify against a SB constraint or component.

4. Once approved → the agent writes `docs/pda-context-spec.md` → **Gate 3 passed**.

---

## Step 5: Phase 4 — Build / Fase 4 — Construcción

1. Run the build agent:
   ```
   /pda-ai-build
   ```
   It reads all three documents and executes the full pipeline:
   - Generates constitution, spec, plan, tasks
   - Verifies traceability at each step
   - Builds the code
   - Verifies fidelity to the Problem Statement

2. If any verification fails, the agent **stops** and tells you what went wrong.

3. If everything passes, it presents the result and asks: **"Do you approve this build?"**

4. Once approved → **Gate 4 passed**. Ready for users.

---

## What Each Agent Catches / Qué detecta cada agente

| Agent | Catches / Detecta |
|---|---|
| `/pda-problem` | Missing evidence, incomplete elements, contradictions, stale data, unlabeled assumptions |
| `/pda-solution` | Orphan components, missing traceability, vague dimensions, technical decisions that don't belong |
| `/pda-context` | Unjustified technical decisions, SB ambiguity, missing accessibility/error handling |
| `/pda-ai-build` | Scope creep, unrequired components, uncovered requirements, orphan tasks, fidelity gaps |

---

## Tips / Consejos

- **Don't skip Phase 1.** A bad Problem Statement means everything downstream is wrong.
  **No te saltes la Fase 1.** Un mal Problem Statement significa que todo lo demás está mal.

- **Evidence matters.** Claims without evidence are assumptions. Label them honestly.
  **La evidencia importa.** Afirmaciones sin evidencia son supuestos. Etiquétalos honestamente.

- **The SB defines what, the Context Spec defines how.** Keep them separate.
  **La SB define qué, la Context Spec define cómo.** Mantenlos separados.

- **The AI never decides for you.** Every agent asks for human approval before writing.
  **La IA nunca decide por ti.** Cada agente pide aprobación humana antes de escribir.

- **If a verification fails, fix the source.** Don't patch downstream — fix the document that caused the issue.
  **Si una verificación falla, corrige la fuente.** No parchees aguas abajo — corrige el documento que causó el problema.

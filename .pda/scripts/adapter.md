# PDA → Spec Kit Adapter / Adaptador PDA → Spec Kit

## What This Solves / Qué resuelve

**EN:** The Solution Brief (8 sections, Gate 2 approved) contains all human thinking. Spec Kit needs specific inputs for each command. This adapter defines what travels, what gets lost, and how PDA agents compensate.

**ES:** La Solution Brief (8 secciones, Gate 2 aprobado) contiene todo el pensamiento humano. Spec Kit necesita inputs específicos para cada comando. Este adaptador define qué viaja, qué se pierde y cómo compensan los agentes PDA.

---

## Step 1: Solution Brief → /speckit.constitution

### Extract from SB / Extraer de la SB

| SB Section / Sección SB | Target in constitution.md |
|---|---|
| Section 7: Constraints | Non-negotiable constraints / Restricciones innegociables |
| Section 4: Architecture dimension | Technical decisions / Decisiones técnicas |
| Section 4: Data dimension | Data principles / Principios de datos |
| Section 6: Success criteria | Quality criteria / Criterios de calidad |
| Section 5: High-risk assumptions | Risk-derived constraints / Restricciones derivadas de riesgo |

### Add PDA traceability block / Añadir bloque de trazabilidad PDA

```markdown
## PDA Traceability
- Problem Statement: docs/pda-problem.md
- Solution Brief: docs/pda-solution-brief.md
- Every decision must be justified against these documents.
- Requirements without trace to SB components = scope creep → escalate.
```

---

## Step 2: PS + Solution Brief → /speckit.specify

### Mapping

| Source / Fuente | Extract / Extraer | Role in specify / Rol |
|---|---|---|
| PS element 1 (gap) | Current vs. desired state | "Why" context |
| PS element 3 (success criteria) | Solved-state definition | Acceptance criteria |
| PS element 7 (cost of inaction) | Impact of not solving | Urgency |
| SB section 2 (proposed solution) | Functional description | Central "what" |
| SB section 3 (key decisions) | Why this solution | Prevents reinvention |
| SB section 4 (business dimension) | Components, relationships | Structure |
| SB section 4 (model dimension) | AI type, metrics | AI requirements |
| SB actor map | Who lives problem, who decides | User context |
| SB section 6 (success criteria) | KPIs per component | Acceptance |
| SB section 8 (translatability map) | Vagueness risk areas | Zones: do NOT invent |

### Lost and compensated / Perdido y compensado

| Lost / Perdido | Compensation / Compensación |
|---|---|
| gap_ref + success_ref per component | pda-problem-validator verifies post-generation |
| Actor map as structured model | Injected as context in prompt |
| Assumptions as constraints | Already in constitution (step 1) |

### Post-generation verification / Verificación post-generación

`pda-problem-validator` → `skill-traceability-qa`:
1. Each user story traces to SB component?
2. Acceptance criteria consistent with PS?
3. Scope outside PS element 8 boundaries?
4. Failures → correct before advancing.

---

## Step 3: Solution Brief → /speckit.plan

**Input:** SB section 4 (Architecture, Data, Model) + SB section 7 (technical constraints).

**Critical:** Architecture decisions are already made. The plan implements, does not question. Incompatibilities → document and escalate.

**Double verification / Verificación doble:**
- `pda-problem-validator` → traceability: plan introduces no unrequired components?
- `pda-solution-brief` → coverage: every SB component in the plan?

---

## Step 4: /speckit.tasks

No additional SB input. Spec Kit decomposes from its own artifacts.

**Verification:** `pda-problem-validator` → each task traces to a user story? Tasks without requirements?

---

## Step 5: /speckit.implement

Spec Kit executes. PDA agents do not intervene during execution in V1.

**Post-build verification:** Does output address PS gap? Are success criteria verifiable?

---

## Summary / Resumen

| Step | Command | PS Input | SB Input | PDA Verification |
|---|---|---|---|---|
| 1 | /speckit.constitution | — | Sections 4,5,6,7 | — |
| 2 | /speckit.specify | Elements 1,3,7 | Sections 1,2,3,4,6,8 | problem-validator |
| 3 | /speckit.plan | — | Sections 4,7 | problem-validator + solution-brief |
| 4 | /speckit.tasks | — | — | problem-validator |
| 5 | /speckit.implement | — | — | problem-validator (post-build) |

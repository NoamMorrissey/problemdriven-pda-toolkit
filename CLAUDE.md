# Problem-Driven AI × Spec Kit — Project Instructions

## What This Project Is / Qué es este proyecto

This is a Problem-Driven AI (PDA) project using Spec Kit for spec-driven development. PDA adds a verification layer ensuring everything built traces back to a validated problem.

Este es un proyecto Problem-Driven AI (PDA) que usa Spec Kit para desarrollo dirigido por especificaciones. PDA añade una capa de verificación que garantiza que todo lo construido tiene trazabilidad a un problema validado.

## Core Principle / Principio central

The AI builds. Humans think. When the AI starts building, it should not need to make any important decision. Only execute.

La IA construye. Los humanos piensan. Cuando la IA empieza a construir, no debería necesitar tomar ninguna decisión importante. Solo ejecutar.

## Architecture / Arquitectura

- **Phases 1–2:** Humans investigate and decide. PDA agents verify.
- **Phase 3:** PDA adapter translates human artifacts into Spec Kit inputs. PDA agents verify each output.
- **Phase 4:** Spec Kit implements. PDA agents verify fidelity post-build.

## Key Files / Archivos clave

- `docs/pda-problem.md` — Problem Statement (9 elements). Source of truth for the problem.
- `docs/pda-solution-brief.md` — Solution Brief (8 sections). Source of truth for the solution.
- `.pda/agents/pda-problem-validator.md` — Verification agent: traceability, evidence, consistency.
- `.pda/agents/pda-solution-brief.md` — Verification agent: coverage, translatability.
- `.pda/scripts/adapter.md` — How to translate PDA artifacts into Spec Kit inputs.

## Rules / Reglas

1. **Never invent.** If information is insufficient, flag it. Do not fill gaps with assumptions.
2. **Traceability is mandatory.** Every spec, plan, and task must trace to Solution Brief → Problem Statement.
3. **Only humans modify PDA artifacts.** Agents verify but never edit the PS or SB.
4. **Constitution reflects PDA decisions.** `.specify/memory/constitution.md` is generated from the Solution Brief.
5. **Verify after every Spec Kit step.** Run PDA verification after `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`.

## Workflow

```
1. Fill docs/pda-problem.md       → /pda.validate-problem    → Gate 1
2. Fill docs/pda-solution-brief.md → /pda.validate-solution   → Gate 2
3. /pda.adapt-constitution → /speckit.specify → /pda.verify-specify
4. /speckit.plan → /pda.verify-plan
5. /speckit.tasks → /pda.verify-tasks
6. /speckit.implement → /pda.verify-build
```

## Evidence Weighting / Ponderación de evidencia

When evidence conflicts, apply this hierarchy:
1. Behavioral > declared
2. First-hand > secondary
3. Quantitative with sample > individual qualitative
4. More recent > older
5. Real user validation > internal validation

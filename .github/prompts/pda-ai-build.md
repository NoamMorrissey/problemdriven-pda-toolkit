# PDA AI Build Agent (Phase 4)

Execute the complete build pipeline from approved documents to working code.

## Prerequisites

All three must exist: `docs/pda-problem.md`, `docs/pda-solution-brief.md`, `docs/pda-context-spec.md`. If any is missing, stop and tell the user.

## Behavior

Execute the full pipeline without stopping unless a verification fails:

1. **Constitution** — extract from Context Spec → `.specify/memory/constitution.md`
2. **Spec** — generate functional spec from PS + SB + Context Spec → `.specify/specs/001-feature/spec.md` → verify traceability
3. **Plan** — generate technical plan → `.specify/specs/001-feature/plan.md` → verify coverage + no orphan components
4. **Tasks** — decompose into self-contained tasks → `.specify/specs/001-feature/tasks.md` → verify traceability + self-containment
5. **Implement** — build the code following tasks in dependency order → verify fidelity to PS
6. **Present** — show summary table of all verifications, present code, ask user to approve

## Rules

- Never invent requirements. Everything traces to PS, SB, or Context Spec.
- Technical decisions from Context Spec are implemented as written — do not substitute.
- If any verification fails, STOP. Show what failed. Ask the user.
- Constitution comes from Context Spec, not from SB directly.
- Never approve the build yourself. Only the human approves.

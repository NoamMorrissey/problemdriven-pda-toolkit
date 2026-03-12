# PDA AI Build Agent (Phase 4)

If a path argument is provided (e.g. `/pda-ai-build example/`), use that as the base directory for all file reads and writes. Default base directory is the project root.

Execute the complete build pipeline from approved documents to working code.

## Prerequisites

All three must exist: `{base}/docs/pda-problem.md`, `{base}/docs/pda-solution-brief.md`, `{base}/docs/pda-context-spec.md`. If any is missing, stop and tell the user.

## Behavior

Execute the full pipeline without stopping unless a verification fails:

1. **Constitution** — extract from Context Spec → `{base}/.specify/memory/constitution.md`
2. **Spec** — generate functional spec from PS + SB + Context Spec → `{base}/.specify/specs/001-feature/spec.md` → verify traceability
3. **Plan** — generate technical plan → `{base}/.specify/specs/001-feature/plan.md` → verify coverage + no orphan components
4. **Tasks** — decompose into self-contained tasks → `{base}/.specify/specs/001-feature/tasks.md` → verify traceability + self-containment
5. **Implement** — build the code following tasks in dependency order → verify fidelity to PS
6. **Present** — show summary table of all verifications, present code, ask user to approve

## Rules

- Never invent requirements. Everything traces to PS, SB, or Context Spec.
- Technical decisions from Context Spec are implemented as written — do not substitute.
- If any verification fails, STOP. Show what failed. Ask the user.
- Constitution comes from Context Spec, not from SB directly.
- Never approve the build yourself. Only the human approves.

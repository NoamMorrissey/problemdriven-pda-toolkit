# PDA Context Specification Agent (Phase 3)

If a path argument is provided (e.g. `/pda-context example/`), use that as the base directory for all file reads and writes. Default base directory is the project root.

Generate the Context Specification that translates product decisions into technical specs.

## Prerequisites

Both `{base}/docs/pda-problem.md` and `{base}/docs/pda-solution-brief.md` must exist. If either is missing, stop and tell the user.

## Behavior

1. Read the PS and SB.
2. Generate a Context Specification with 8 sections: Stack (with justification), Architecture (files, state, rendering, navigation), Data Model (complete schemas with types and limits), Interaction Decisions (UI patterns + mobile fallbacks), Visual Design (CSS architecture, responsive, states), Accessibility (semantic HTML, ARIA, focus, WCAG AA), Error Handling (storage, validation, empty states, corruption), What Is NOT Decided Here (SB prevails on conflict).
3. Every technical decision must justify against a SB constraint or component.
4. Do not question SB decisions — translate them to technical specs.
5. If the SB is ambiguous on a technical point, ask the user — do not invent.
6. Present the result with a clear header FIRST: `✅ CONTEXT APPROVED — Context Specification complete` (or `❌ CONTEXT ISSUES` with numbered gaps/conflicts). Include one-sentence summary, key stats, and approval question. Then `---` separator, then the full Context Spec content.
7. If approved, write to `{base}/docs/pda-context-spec.md`.
8. Never approve the Context Spec yourself. Only the human approves.

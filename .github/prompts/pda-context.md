# PDA Context Specification Agent (Phase 3)

Generate the Context Specification that translates product decisions into technical specs.

## Prerequisites

Both `docs/pda-problem.md` and `docs/pda-solution-brief.md` must exist. If either is missing, stop and tell the user.

## Behavior

1. Read the PS and SB.
2. Generate a Context Specification with 8 sections: Stack (with justification), Architecture (files, state, rendering, navigation), Data Model (complete schemas with types and limits), Interaction Decisions (UI patterns + mobile fallbacks), Visual Design (CSS architecture, responsive, states), Accessibility (semantic HTML, ARIA, focus, WCAG AA), Error Handling (storage, validation, empty states, corruption), What Is NOT Decided Here (SB prevails on conflict).
3. Every technical decision must justify against a SB constraint or component.
4. Do not question SB decisions — translate them to technical specs.
5. If the SB is ambiguous on a technical point, ask the user — do not invent.
6. Present the Context Spec and ask the user to approve. If approved, write to `docs/pda-context-spec.md`.
7. Never approve the Context Spec yourself. Only the human approves.

# PDA Solution Brief Agent (Phase 2)

If a path argument is provided (e.g. `/pda-solution example/`), use that as the base directory for all file reads and writes. Default base directory is the project root.

Generate and validate a Solution Brief from the approved Problem Statement.

## Prerequisites

`{base}/docs/pda-problem.md` must exist. If missing, stop and tell the user.

## Behavior

1. Read the approved Problem Statement.
2. Generate a Solution Brief with: Summary, Proposed Solution, Key Decisions, Business Components (with gap_ref + success_ref), Assumptions, Success Criteria, Constraints (business/org only), Translatability Map, Actor Map.
3. CRITICAL: The SB contains NO technical decisions. No stack, no architecture, no data model, no libraries. Those go in the Context Specification (Phase 3).
4. Validate: every component traces to PS, success criteria cover all PS criteria, no scope creep.
5. If you detect technical decisions, flag them: "This should be in the Context Specification."
6. Present the result with a clear header FIRST: `✅ GATE 2: PASS — Solution Brief validated` (or `❌ GATE 2: FAIL` with numbered issues). Include one-sentence summary, key stats, and approval question. Then `---` separator, then the full SB content.
7. If approved, write to `{base}/docs/pda-solution-brief.md`.
8. Add a note at the end: "Technical decisions are defined in the Context Specification (Phase 3)."
9. Never approve the SB yourself. Only the human approves.

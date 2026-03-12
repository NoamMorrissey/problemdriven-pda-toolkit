# PDA Solution Brief Agent (Phase 2)

If a path argument is provided (e.g. `/pda-solution example/`), use that as the base directory for all file reads. Default base directory is the project root.

Validate a Solution Brief that the human already wrote.

## Prerequisites

`{base}/docs/pda-problem.md` must exist. If missing, stop and tell the user.

## Behavior

1. Read the Solution Brief from `{base}/docs/pda-solution-brief.md`.
2. If the file does not exist, stop and tell the user: "No Solution Brief found. Write your Solution Brief in `docs/pda-solution-brief.md` and run this command again to validate it."
3. Read the approved Problem Statement from `{base}/docs/pda-problem.md`.
4. Validate: all 8 sections present, every component traces to PS (gap_ref + success_ref), no orphan components, success criteria cover all PS criteria, no scope creep.
5. CRITICAL: The SB must contain NO technical decisions. No stack, no architecture, no data model, no libraries. If found, flag them: "This should be in the Context Specification."
6. Present the result with a clear header FIRST: `✅ GATE 2: PASS — Solution Brief validated` (or `❌ GATE 2: FAIL` with numbered issues). Include one-sentence summary, key stats. Then `---` separator, then details.
7. The agent NEVER writes or modifies `pda-solution-brief.md`. Only the human does.
8. Never generate content or propose solutions. Only verify.
9. Never approve the SB yourself. Only the human approves.

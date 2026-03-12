# PDA Problem Statement Agent (Phase 1)

If a path argument is provided (e.g. `/pda-problem example/`), use that as the base directory for all file reads. Default base directory is the project root.

Validate a Problem Statement that the human already wrote.

## Behavior

1. Read the Problem Statement from `{base}/docs/pda-problem.md`.
2. If the file does not exist, stop and tell the user: "No Problem Statement found. Write your Problem Statement in `docs/pda-problem.md` and run this command again to validate it."
3. Read the research evidence from `{base}/research/`.
4. Validate against these criteria:
   - All 9 PS elements present and complete: Gap, Who Is Affected, Success Criteria, Root Causes, Current Alternatives, Constraints, Cost of Inaction, Scope Boundaries, Assumptions.
   - Every element cites specific evidence from the research.
   - No unresolved contradictions between evidence sources.
   - Assumptions are clearly identified (what has NO evidence).
   - Behavioral evidence weighted above declared evidence where they conflict.
   - Evidence older than 6 months flagged for review.
5. Present the result with a clear header FIRST: `✅ GATE 1: PASS — Problem Statement validated` (or `❌ GATE 1: FAIL` with numbered issues). Include one-sentence summary, key stats. Then `---` separator, then details.
6. The agent NEVER writes or modifies `pda-problem.md`. Only the human does.
7. Never generate content, propose insights, or fill gaps. Only verify.
8. Never approve the PS yourself. Only the human approves.

Activate as pda-problem-validator (Phase 3 mode).

Read: `docs/pda-problem.md`, `docs/pda-solution-brief.md`, the most recent `spec.md` and `tasks.md` in `.specify/specs/`.

Execute skill-traceability-qa:
1. Each task traces to a user story in spec.md?
2. Tasks without associated requirements?
3. Spec requirements with no tasks?

Write report to `pda-verification/verify-tasks.md`:

```
## Tasks Verification Report
Date: [today]

### Task Traceability
| Task | User Story | Status |
|---|---|---|

### Orphan Tasks
- [list or "None"]

### Uncovered Requirements
- [list or "None"]

### Verdict: PASS / FAIL
### Blocking issues: [list]
```

Read `.pda/scripts/adapter.md`, section "Step 1".

Read `docs/pda-solution-brief.md` and generate `.specify/memory/constitution.md` by extracting:

1. SB Section 7 (Constraints) → "Non-negotiable Constraints"
2. SB Section 4 (Architecture dimension) → "Technical Decisions"
3. SB Section 4 (Data dimension) → "Data Principles"
4. SB Section 6 (Success criteria) → "Quality Criteria"
5. SB Section 5 (High-risk assumptions) → "Risk-Derived Constraints"

Add the PDA traceability block at the end:

```markdown
## PDA Traceability
- Problem Statement: docs/pda-problem.md
- Solution Brief: docs/pda-solution-brief.md
- Every decision must be justified against these documents.
- Requirements without trace to SB components = scope creep → escalate.
```

Write result to `.specify/memory/constitution.md`. Display a summary of what was extracted and from which section. Ask the human to review before proceeding.

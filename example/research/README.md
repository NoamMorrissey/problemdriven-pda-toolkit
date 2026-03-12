# Research Evidence Index

This folder contains all primary research conducted during Phase 1 (Problem Discovery).

## How Evidence Works in This Project

There are two ways to access the research evidence:

### For AI agents: `evidence.jsonl`

The file `evidence.jsonl` is the structured evidence base that PDA agents query directly. Each line is a JSON object representing one piece of evidence with the full PDA metadata taxonomy:

| Field | Description |
|---|---|
| `id` | Evidence ID (E-001, E-002, etc.) referenced in the Problem Statement |
| `claim` | The specific finding this evidence supports |
| `source` | Human-readable source description |
| `source_file` | Path to the full research document |
| `type` | Primary evidence type (PDA taxonomy) |
| `type_secondary` | Secondary type if applicable |
| `date` | Date of data collection |
| `confidence` | High / Medium / Low |
| `phase` | PDA phase where evidence was collected |
| `tags` | Searchable tags for thematic lookup |
| `methodology_note` | Limitations or caveats (when applicable) |

**PDA Evidence Taxonomy (Phase 1):**
- `1st-hand-declared` — What people say (interviews, surveys)
- `1st-hand-behavioral` — What people do (observation, analytics)
- `1st-hand-quantitative` — Numbers from direct measurement
- `1st-hand-qualitative` — Coded open-ended responses
- `secondary-analytical` — Third-party analysis (reports, studies)
- `secondary-competitive` — Competitor information
- `secondary-quantitative` — Third-party numbers

When `/pda-problem` runs, it reads this file and verifies that evidence IDs cited in the Problem Statement exist, have sufficient metadata, and support the claims they're attached to.

### For humans: Research documents + NotebookLM

The full research documents are in this folder as readable markdown:

| File | Type | Date | Description |
|---|---|---|---|
| `interviews/user-interview-01.md` | 1st-hand declared + behavioral | 2026-02-10 | Maria, team lead at 6-person design agency |
| `interviews/user-interview-02.md` | 1st-hand declared + behavioral | 2026-02-12 | James, freelance developer managing subcontractors |
| `interviews/user-interview-03.md` | 1st-hand declared + behavioral | 2026-02-14 | Priya, co-founder of 4-person startup |
| `analytics/usage-data-summary.md` | 1st-hand quantitative | 2026-02-05 | Survey of 127 respondents on task management |
| `benchmarks/competitor-analysis.md` | Secondary competitive | 2026-02-08 | Analysis of 5 existing solutions |

These same documents are also available in a NotebookLM for conversational exploration:

**NotebookLM link:** https://notebooklm.google.com/notebook/b4da2d9c-5f80-49f4-ba1f-123977952dd6

Use NotebookLM when you want to ask questions about the research in natural language, explore connections between interviews, or verify specific claims interactively.

## Evidence Weighting

When evidence conflicts, PDA agents apply this hierarchy:
1. Behavioral > declared
2. First-hand > secondary
3. Quantitative with sample > individual qualitative
4. More recent > older
5. Real user validation > internal validation

## Adding New Evidence

To add evidence to this project:
1. Create the research document in the appropriate subfolder
2. Add a new line to `evidence.jsonl` with full metadata
3. Reference the new evidence ID in the Problem Statement
4. Run `/pda-problem` to regenerate and verify the Problem Statement

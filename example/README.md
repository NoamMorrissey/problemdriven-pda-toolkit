# Example: TeamTasks — Shared Task List for Small Teams

This is a complete example of the Problem-Driven AI methodology. It includes the research evidence, the three approved documents (Problem Statement, Solution Brief, Context Specification), and everything needed to run the build phase.

## What's Inside

```
example/
├── research/                        ← The evidence base (Phase 1 input)
│   ├── interviews/                  ← 3 user interviews
│   ├── analytics/                   ← Survey data (N=127)
│   ├── benchmarks/                  ← Competitor analysis (5 tools)
│   └── evidence.jsonl               ← Evidence index (12 pieces)
│
├── docs/                            ← Approved PDA documents (Phases 1-3 output)
│   ├── pda-problem.md               ← Problem Statement — Gate 1 PASS
│   ├── pda-solution-brief.md        ← Solution Brief — Gate 2 PASS
│   └── pda-context-spec.md          ← Context Specification — Gate 3 PASS
│
└── README.md
```

## How to Use This Example

Phases 1-3 are already complete. The three documents in `docs/` represent the output of each phase. You can:

### Option A: Run the build (recommended)

Skip straight to Phase 4 and see the AI build the app from the approved documents:

```
/pda-ai-build example/
```

This reads the Problem Statement, Solution Brief, and Context Specification, then generates the constitution, spec, plan, tasks, and working code — all verified against the source documents.

### Option B: Browse the documents

Read the three documents to understand what each phase produces:

1. **[Problem Statement](docs/pda-problem.md)** — 9 elements extracted from research evidence. Every claim cites a specific evidence ID.
2. **[Solution Brief](docs/pda-solution-brief.md)** — Business and product decisions only. No technical stack, no architecture. Defines what to build and why.
3. **[Context Specification](docs/pda-context-spec.md)** — Technical decisions that translate the Solution Brief into buildable specs. Three files only, localStorage only, zero dependencies.

### Option C: Re-run from scratch

Delete the `docs/` folder and regenerate everything from the research evidence:

```
1. /pda-problem example/       → Generates example/docs/pda-problem.md        → Gate 1
2. /pda-solution example/      → Generates example/docs/pda-solution-brief.md  → Gate 2
3. /pda-context example/       → Generates example/docs/pda-context-spec.md    → Gate 3
4. /pda-ai-build example/      → Builds working code in example/src/           → Gate 4
```

Each agent validates its output and asks for your approval before proceeding to the next phase.

## The Point

The app itself is simple. That's intentional. The value is not the app — it's the process that got there. Every line of code traces back through tasks → spec → Solution Brief → Problem Statement → evidence from real (fictional) people.

That's what Problem-Driven AI does: it ensures the AI builds the right thing, not just builds things right.

## Reference Documents (Google Docs)

The same PDA documents are also available as Google Docs for easier reading and sharing:

- **Problem Statement:** https://docs.google.com/document/d/1H1z7gSJiWOhQwOr7u6XmoFFtSbS_wZm8/edit
- **Solution Brief:** https://docs.google.com/document/d/1Y7aiZH-INSYB-vPSAF_KD3Cjq3mdUXCj/edit
- **Context Specification:** https://docs.google.com/document/d/1vbWxN2RH76BBW8hQsB2JmLEHAYpvPRa-/edit?rtpof=true

## RAG Access

The research documents are also available in a NotebookLM for AI agent verification:

**NotebookLM link:** https://notebooklm.google.com/notebook/b4da2d9c-5f80-49f4-ba1f-123977952dd6

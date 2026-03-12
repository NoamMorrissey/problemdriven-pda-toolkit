# Example: TeamTasks — Shared Task List for Small Teams

This is a complete example of the Problem-Driven AI methodology. It includes the research evidence needed to run the full PDA process from scratch.

## What's Inside

```
example/
├── research/                    ← The evidence base
│   ├── interviews/              ← 3 user interviews
│   ├── analytics/               ← Survey data (N=127)
│   ├── benchmarks/              ← Competitor analysis (5 tools)
│   └── evidence.jsonl           ← Evidence index (12 pieces)
│
└── README.md
```

## How to Use This Example

Run the 4 PDA agents in order, using `example/` as the base path:

```
1. /pda-problem example/       → Generates example/docs/pda-problem.md        → Gate 1
2. /pda-solution example/      → Generates example/docs/pda-solution-brief.md  → Gate 2
3. /pda-context example/       → Generates example/docs/pda-context-spec.md    → Gate 3
4. /pda-ai-build example/      → Builds working code in example/src/           → Gate 4
```

Each agent reads the research evidence, generates an artifact, validates it, and asks for your approval before proceeding.

## The Point

The app itself is simple. That's intentional. The value is not the app — it's the process that got there. Every line of code traces back through tasks → spec → Solution Brief → Problem Statement → evidence from real (fictional) people.

That's what Problem-Driven AI does: it ensures the AI builds the right thing, not just builds things right.

## Reference Documents (Google Docs)

Pre-built versions of the PDA artifacts are available as Google Docs for reference. These show what the agents will generate when you run the process:

- **Problem Statement:** https://docs.google.com/document/d/1H1z7gSJiWOhQwOr7u6XmoFFtSbS_wZm8/edit
- **Solution Brief:** https://docs.google.com/document/d/1Y7aiZH-INSYB-vPSAF_KD3Cjq3mdUXCj/edit
- **Context Specification:** https://docs.google.com/document/d/1Z0Kvot2_LQTr4U02lZslJJHHnGQ0oyGQ/edit

## RAG Access

The research documents are also available in a NotebookLM for AI agent verification:

**NotebookLM link:** https://notebooklm.google.com/notebook/b4da2d9c-5f80-49f4-ba1f-123977952dd6

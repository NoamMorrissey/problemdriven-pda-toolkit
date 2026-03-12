# Quick Start Guide

Get from zero to running PDA in 10 minutes.

---

## Prerequisites

You need one of these AI coding agents:

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (recommended)
- [GitHub Copilot](https://github.com/features/copilot)
- [Cursor](https://cursor.sh)

That's it. You do **not** need Spec Kit CLI installed — the `/pda-ai-build` agent handles that internally.

---

## Setup

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project
```

---

## Option A: Start Your Own Project

1. **Add your research.** Put your evidence files (interviews, surveys, analytics, competitor analysis) in a `research/` folder at the project root.

2. **Write your Problem Statement.** Use the template in `templates/pda-problem.template.md` as a guide. Write your PS in `docs/pda-problem.md` with all 9 elements, citing your research evidence.

3. **Run Phase 1 — Validate your Problem Statement:**
   ```
   /pda-problem
   ```
   The agent reads your PS and your research, validates every claim against evidence, and reports PASS or FAIL with specific issues to fix.

4. **Write your Solution Brief.** Use the template in `templates/pda-solution-brief.template.md`. Write your SB in `docs/pda-solution-brief.md` with business decisions only — no technical decisions.

5. **Run Phase 2 — Validate your Solution Brief:**
   ```
   /pda-solution
   ```
   The agent reads your SB and checks traceability to the Problem Statement, reports PASS or FAIL.

6. **Write your Context Specification.** Use the template in `templates/pda-context-spec.template.md`. Write your Context Spec in `docs/pda-context-spec.md` with all technical decisions (stack, architecture, data model, etc.).

7. **Run Phase 3 — Validate your Context Specification:**
   ```
   /pda-context
   ```
   The agent reads your Context Spec and checks technical coherence against the Solution Brief, reports PASS or FAIL.

8. **Run Phase 4 — Build:**
   ```
   /pda-ai-build
   ```
   The agent reads all three validated documents, generates the full spec chain, builds the code, verifies everything, and asks for your approval. This is the only phase where the AI generates content.

Each command validates (or builds from) one artifact. Each artifact requires your approval before the next phase begins.

---

## Option B: Run the Included Example

Don't have your own research yet? Run the included **TeamTasks** example to see the full process:

```
/pda-problem example/
```

This uses the pre-built research evidence in `example/research/` (3 user interviews, survey N=127, competitor analysis). Follow the 4 phases in order — each agent will read from `example/docs/`.

See [EXAMPLE.md](EXAMPLE.md) for a detailed walkthrough.

---

## The 4 Commands

| Command | What It Does | Output |
|---|---|---|
| `/pda-problem` | **Validates** human-written Problem Statement against research evidence | PASS/FAIL report |
| `/pda-solution` | **Validates** human-written Solution Brief against Problem Statement | PASS/FAIL report |
| `/pda-context` | **Validates** human-written Context Specification against Solution Brief | PASS/FAIL report |
| `/pda-ai-build` | **Generates** and builds code from all 3 validated docs: constitution → spec → plan → tasks → code → verify | `src/`, `.specify/`, `pda-verification/` |

All commands accept an optional path argument (e.g., `/pda-problem example/`) to use a subdirectory as the base.

---

## Something Went Wrong?

**Agent can't find my files**
Make sure your documents are in `docs/` (or `[path]/docs/` if using a base path). The agents look for `pda-problem.md`, `pda-solution-brief.md`, and `pda-context-spec.md` there.

**"No Problem Statement found" error**
You need to write the document first, then run the agent to validate it. Use the templates in `templates/` as a starting point.

**Validation failed**
This is working as intended. The agent found issues in your document. Read the numbered list of issues, fix them in your document, and run the agent again.

**Verification failed in /pda-ai-build**
This is working as intended. The agent stops when it finds a problem. Read the verification report in `pda-verification/` to understand what failed, fix the source document, and run again.

**Agent asks questions I don't know how to answer**
The agent asks when the Solution Brief is ambiguous about something it needs to decide. Go back to the SB, clarify the point, and re-run the context or build agent.

**I changed a document and now things don't match**
Always fix upstream. If you change the Problem Statement, re-run `/pda-solution`. If you change the Solution Brief, re-run `/pda-context`. Traceability flows in one direction.

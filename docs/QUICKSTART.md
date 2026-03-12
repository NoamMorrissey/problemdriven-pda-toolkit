# 🚀 Quick Start Guide

Get from zero to running PDA in 10 minutes.

---

## 📋 Prerequisites

You need one of these AI coding agents:

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (recommended)
- [GitHub Copilot](https://github.com/features/copilot)
- [Cursor](https://cursor.sh)

That's it. You do **not** need Spec Kit CLI installed — the `/pda-ai-build` agent handles that internally.

---

## 🚀 Setup

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project
```

---

## 📝 Option A: Start Your Own Project

1. **Add your research.** Put your evidence files (interviews, surveys, analytics, competitor analysis) in a `research/` folder at the project root.

2. **Run Phase 1 — Problem:**
   ```
   /pda-problem
   ```
   The agent reads your research, generates a Problem Statement with 9 elements, validates every claim against evidence, and asks for your approval.

3. **Run Phase 2 — Solution:**
   ```
   /pda-solution
   ```
   The agent reads your approved Problem Statement, generates a Solution Brief with business decisions only, and asks for your approval.

4. **Run Phase 3 — Context:**
   ```
   /pda-context
   ```
   The agent reads your PS + SB, generates a Context Specification with all technical decisions (stack, architecture, data model, etc.), and asks for your approval.

5. **Run Phase 4 — Build:**
   ```
   /pda-ai-build
   ```
   The agent reads all three documents, generates the full spec chain, builds the code, verifies everything, and asks for your approval.

Each command produces one artifact. Each artifact requires your approval before the next phase begins.

---

## 👀 Option B: Run the Included Example

Don't have your own research yet? Run the included **TeamTasks** example to see the full process:

```
/pda-problem example/
```

This uses the pre-built research evidence in `example/research/` (3 user interviews, survey N=127, competitor analysis). Follow the 4 phases in order — each agent will read from and write to `example/docs/`.

See [EXAMPLE.md](EXAMPLE.md) for a detailed walkthrough.

---

## 🔄 The 4 Commands

| Command | What It Does | Output |
|---|---|---|
| `/pda-problem` | Generates and validates Problem Statement from research evidence | `docs/pda-problem.md` |
| `/pda-solution` | Generates and validates Solution Brief (business decisions only) | `docs/pda-solution-brief.md` |
| `/pda-context` | Generates Context Specification (technical decisions) from PS + SB | `docs/pda-context-spec.md` |
| `/pda-ai-build` | Builds code from all 3 docs: constitution → spec → plan → tasks → code → verify | `src/`, `.specify/`, `pda-verification/` |

All commands accept an optional path argument (e.g., `/pda-problem example/`) to use a subdirectory as the base.

---

## ❓ Something Went Wrong?

**Agent can't find my files**
Make sure your research is in `research/` (or `[path]/research/` if using a base path). The agents look for evidence files there.

**"Insufficient evidence" error**
The agent needs real evidence to work with. Claims without evidence are flagged as assumptions. Add more research or explicitly label assumptions in the output.

**Verification failed in /pda-ai-build**
This is working as intended. The agent stops when it finds a problem. Read the verification report in `pda-verification/` to understand what failed, fix the source document, and run again.

**Agent asks questions I don't know how to answer**
The agent asks when the Solution Brief is ambiguous about something it needs to decide. Go back to the SB, clarify the point, and re-run the context or build agent.

**I changed a document and now things don't match**
Always fix upstream. If you change the Problem Statement, re-run `/pda-solution`. If you change the Solution Brief, re-run `/pda-context`. Traceability flows in one direction.

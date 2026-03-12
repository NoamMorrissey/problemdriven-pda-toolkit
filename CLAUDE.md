# Problem-Driven AI (PDA) Toolkit — Project Instructions

## What This Project Is

This is the PDA Toolkit — an open-source framework that connects human problem-solving with AI-assisted code generation. PDA ensures that everything built traces back to a validated problem.

## Core Principle

The AI builds. Humans think. When the AI starts building, it should not need to make any important decision. Only execute.

## 4 Phases, 4 Agents, 4 Gates

| Phase | Agent | Input | Output | Gate |
|---|---|---|---|---|
| 1. Problem | `/pda-problem` | Research evidence | `docs/pda-problem.md` | Human approves PS |
| 2. Solution | `/pda-solution` | Approved PS | `docs/pda-solution-brief.md` | Human approves SB |
| 3. Context | `/pda-context` | Approved PS + SB | `docs/pda-context-spec.md` | Human approves Context Spec |
| 4. AI Build | `/pda-ai-build` | PS + SB + Context Spec | Working code in `src/` | Human approves build |

All agents accept an optional base path argument (e.g., `/pda-ai-build example/`). Default base directory is the project root.

## Key Files

- `docs/pda-problem.md` — Problem Statement (9 elements). Source of truth for the problem.
- `docs/pda-solution-brief.md` — Solution Brief (business decisions only). Source of truth for the solution.
- `docs/pda-context-spec.md` — Context Specification (technical decisions). Generated in Phase 3.
- `.claude/agents/pda-*.md` — The 4 PDA agents for Claude Code.
- `.github/prompts/pda-*.md` — The 4 PDA agents for GitHub Copilot.
- `.cursor/rules/pda-*.mdc` — The 4 PDA agents for Cursor.
- `templates/` — Empty templates for PS, SB, and Context Spec.

## Rules

1. **Never invent.** If information is insufficient, flag it. Do not fill gaps with assumptions.
2. **Traceability is mandatory.** Every artifact must trace to Solution Brief → Problem Statement → Evidence.
3. **Only humans modify PDA artifacts.** Agents generate drafts and verify, but humans approve.
4. **SB = business decisions. Context Spec = technical decisions.** Never mix them.
5. **Verify at every gate.** Each agent validates before asking for human approval.

## Evidence Weighting

When evidence conflicts, apply this hierarchy:
1. Behavioral > declared
2. First-hand > secondary
3. Quantitative with sample > individual qualitative
4. More recent > older
5. Real user validation > internal validation

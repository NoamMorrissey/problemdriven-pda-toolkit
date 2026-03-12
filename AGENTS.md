# Problem-Driven AI (PDA) Toolkit — Agent Instructions

This file provides context for AI coding agents (GitHub Copilot, Cursor, and others).

## Project Context

This project uses the Problem-Driven AI methodology. Four AI agents guide the user from research evidence to working code. Each agent has a specific job and a mandatory human approval gate. The AI does not make important decisions — it generates, validates, and presents artifacts for human review.

## The 4 Agents

| Agent | Purpose | Reads | Writes |
|---|---|---|---|
| `pda-problem` | Generate + validate Problem Statement from research evidence | `research/` | `docs/pda-problem.md` |
| `pda-solution` | Generate + validate Solution Brief (business decisions only) | `docs/pda-problem.md` | `docs/pda-solution-brief.md` |
| `pda-context` | Generate Context Specification (technical decisions) | `docs/pda-problem.md`, `docs/pda-solution-brief.md` | `docs/pda-context-spec.md` |
| `pda-ai-build` | Build code from all 3 docs via spec pipeline | All 3 docs | `.specify/`, `src/`, `pda-verification/` |

All agents accept an optional base path argument (e.g., `/pda-problem example/`). Default base directory is the project root.

## Agent Locations

- **Claude Code:** `.claude/agents/pda-*.md` (canonical source)
- **GitHub Copilot:** `.github/prompts/pda-*.md`
- **Cursor:** `.cursor/rules/pda-*.mdc`

## Key Files

- `docs/pda-problem.md` — Problem Statement. Source of truth for the problem.
- `docs/pda-solution-brief.md` — Solution Brief. Source of truth for business decisions.
- `docs/pda-context-spec.md` — Context Specification. Source of truth for technical decisions.
- `templates/` — Empty templates for PS, SB, and Context Spec.

## Rules

1. **Never invent.** Flag gaps instead of filling them with assumptions.
2. **Traceability is mandatory.** Every artifact traces to Solution Brief → Problem Statement → Evidence.
3. **Agents generate drafts and verify, but only humans approve.**
4. **SB = business decisions. Context Spec = technical decisions.** Never mix them.
5. **Verify before presenting.** Each agent validates its output before asking for human approval.

## Evidence Weighting

When evidence conflicts, apply this hierarchy:
1. Behavioral > declared
2. First-hand > secondary
3. Quantitative with sample > individual qualitative
4. More recent > older
5. Real user validation > internal validation

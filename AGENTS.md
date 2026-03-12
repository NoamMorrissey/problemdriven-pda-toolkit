# Problem-Driven AI (PDA) Toolkit — Agent Instructions

This file provides context for AI coding agents (GitHub Copilot, Cursor, and others).

## Project Context

This project uses the Problem-Driven AI methodology. Phases 1-3: Humans write documents, AI agents validate them. Phase 4: AI builds, humans supervise. Each agent has a specific job and a mandatory human approval gate.

## The 4 Agents

| Agent | Role | Reads | Writes |
|---|---|---|---|
| `pda-problem` | **Validates** human-written Problem Statement | `docs/pda-problem.md` + `research/` | Nothing (read-only) |
| `pda-solution` | **Validates** human-written Solution Brief | `docs/pda-solution-brief.md` + `docs/pda-problem.md` | Nothing (read-only) |
| `pda-context` | **Validates** human-written Context Specification | `docs/pda-context-spec.md` + PS + SB | Nothing (read-only) |
| `pda-ai-build` | **Generates** code from all 3 validated docs (only generator) | All 3 docs | `.specify/`, `src/`, `pda-verification/` |

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
3. **Agents validate (Phases 1-3), only `/pda-ai-build` generates. Humans always approve.**
4. **SB = business decisions. Context Spec = technical decisions.** Never mix them.
5. **Verify before presenting.** Each agent validates its output before asking for human approval.

## Evidence Weighting

When evidence conflicts, apply this hierarchy:
1. Behavioral > declared
2. First-hand > secondary
3. Quantitative with sample > individual qualitative
4. More recent > older
5. Real user validation > internal validation

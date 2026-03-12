# Problem-Driven AI (PDA) Toolkit — Agent Instructions

This file provides context for AI coding agents (GitHub Copilot, Cursor, and others).

## Project Context

This project uses Problem-Driven AI (PDA) methodology. PDA ensures that AI-built artifacts trace back to a validated problem through 4 phases, each with its own agent and human approval gate.

## 4 Agents

| Agent | Purpose | Reads | Writes |
|---|---|---|---|
| `pda-problem` | Generate + validate Problem Statement from research evidence | `research/` | `docs/pda-problem.md` |
| `pda-solution` | Generate + validate Solution Brief (business decisions only) | `docs/pda-problem.md` | `docs/pda-solution-brief.md` |
| `pda-context` | Generate Context Specification (technical decisions) | `docs/pda-problem.md`, `docs/pda-solution-brief.md` | `docs/pda-context-spec.md` |
| `pda-ai-build` | Build code from all 3 docs via Spec Kit pipeline | All 3 docs | `.specify/`, `src/` |

## Key Files

- `docs/pda-problem.md` — Problem Statement. Source of truth for the problem.
- `docs/pda-solution-brief.md` — Solution Brief. Source of truth for business decisions.
- `docs/pda-context-spec.md` — Context Specification. Source of truth for technical decisions.
- `templates/` — Empty templates for PS, SB, and Context Spec.

## Rules

1. Never invent information. Flag gaps instead of filling them with assumptions.
2. Every artifact must trace to Solution Brief → Problem Statement → Evidence.
3. Agents generate drafts and verify, but only humans approve.
4. SB contains business decisions only. Context Spec contains technical decisions only.
5. Each agent validates its output before asking for human approval.

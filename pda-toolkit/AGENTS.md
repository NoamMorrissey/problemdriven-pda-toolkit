# Problem-Driven AI × Spec Kit — Agent Instructions

This file provides context for AI coding agents (GitHub Copilot, Cursor, and others).

## Project Context

This project uses Problem-Driven AI (PDA) methodology with Spec Kit for spec-driven development. PDA ensures that AI-built artifacts trace back to a validated problem through two verification agents.

## Key Files

- `docs/pda-problem.md` — Problem Statement. Source of truth for the problem.
- `docs/pda-solution-brief.md` — Solution Brief. Source of truth for the solution.
- `.pda/agents/pda-problem-validator.md` — Verification rules and skills for problem traceability.
- `.pda/agents/pda-solution-brief.md` — Verification rules and skills for solution coverage.
- `.pda/scripts/adapter.md` — Translation guide from PDA artifacts to Spec Kit inputs.

## Rules

1. Never invent information. Flag gaps instead of filling them with assumptions.
2. Every spec element must trace to the Solution Brief, which traces to the Problem Statement.
3. Only humans modify the Problem Statement and Solution Brief.
4. The constitution.md is generated from the Solution Brief, not written from scratch.
5. Run PDA verification after every Spec Kit generation step.

## Workflow

Fill Problem Statement → validate → Fill Solution Brief → validate → adapt to Spec Kit → specify → verify → plan → verify → tasks → verify → implement → verify build.

# Problem-Driven AI — Toolkit V1

> **Think first. Build second. Let the AI execute what humans decided.**
>
> **Piensa primero. Construye después. Deja que la IA ejecute lo que los humanos decidieron.**

An open-source toolkit that implements the [Problem-Driven AI](https://problemdriven.ai) methodology. Four AI agents guide you from research evidence to working code, ensuring everything built traces back to a validated problem.

Un toolkit open-source que implementa la metodología [Problem-Driven AI](https://problemdriven.ai). Cuatro agentes IA te guían desde evidencia de investigación hasta código funcional, garantizando que todo lo construido tiene trazabilidad a un problema validado.

---

## What This Solves / Qué resuelve

**EN:** AI coding agents are powerful builders, but they need to know *what* to build and *why*. Problem-Driven AI fills that gap: it structures the human thinking that must happen before any code exists, then translates those decisions into context the AI can execute from — without inventing.

**ES:** Los agentes de código IA son constructores potentes, pero necesitan saber *qué* construir y *por qué*. Problem-Driven AI llena ese vacío: estructura el pensamiento humano que debe ocurrir antes de que exista cualquier código, y luego traduce esas decisiones en contexto que la IA puede ejecutar — sin inventar.

```
Phase 1:  Human defines the problem      → /pda-problem
Phase 2:  Human defines the solution      → /pda-solution
Phase 3:  Human defines the how           → /pda-context
Phase 4:  AI builds, verifies, delivers   → /pda-ai-build

Fase 1:   Humano define el problema       → /pda-problem
Fase 2:   Humano define la solución       → /pda-solution
Fase 3:   Humano define el cómo           → /pda-context
Fase 4:   IA construye, verifica, entrega → /pda-ai-build
```

---

## The Four Agents / Los cuatro agentes

| Agent | Phase | What it does / Qué hace |
|---|---|---|
| `pda-problem` | 1 | Reads research evidence, generates a Problem Statement with 9 elements, validates every claim against evidence, asks human to approve. / Lee evidencia de investigación, genera un Problem Statement con 9 elementos, valida cada afirmación contra evidencia, pide aprobación humana. |
| `pda-solution` | 2 | Reads the approved PS, generates a Solution Brief with business decisions only (no tech stack), validates traceability, asks human to approve. / Lee el PS aprobado, genera una Solution Brief solo con decisiones de negocio (sin stack técnico), valida trazabilidad, pide aprobación humana. |
| `pda-context` | 3 | Reads PS + SB, generates a Context Specification with all technical decisions (stack, architecture, data model, accessibility, error handling), asks human to approve. / Lee PS + SB, genera una Context Specification con todas las decisiones técnicas, pide aprobación humana. |
| `pda-ai-build` | 4 | Reads all three documents, generates spec → plan → tasks → code, verifies each step, stops if any check fails. / Lee los tres documentos, genera spec → plan → tasks → código, verifica cada paso, para si alguna verificación falla. |

---

## Why Two Documents Instead of One / Por qué dos documentos en vez de uno

The **Solution Brief** defines *what* to build and *why* — product decisions, business components, success criteria, constraints.

The **Context Specification** defines *how* to build it — stack, architecture, data model, interaction patterns, visual design, accessibility.

**En proyectos pequeños** puede parecer redundante: la misma persona piensa el qué y el cómo. Pero la separación tiene valor incluso ahí: obliga a tomar decisiones técnicas *después* de haber definido el producto, no al mismo tiempo.

**En proyectos grandes** los escribe gente distinta: producto define la SB, ingeniería define la Context Spec. La separación evita que decisiones técnicas contaminen el diseño de producto, y viceversa.

---

## The Five Actors / Los cinco actores

| Actor | Type / Tipo | Phases / Fases | Role / Rol |
|---|---|---|---|
| Product team | Person | 1, 2 | Operates `/pda-problem` and `/pda-solution`. Investigates, synthesizes, decides the what and why. / Opera `/pda-problem` y `/pda-solution`. Investiga, sintetiza, decide el qué y por qué. |
| Context Engineer | Person | 3, 4 | Operates `/pda-context` and supervises `/pda-ai-build`. Translates product decisions into technical specs, reviews built output. / Opera `/pda-context` y supervisa `/pda-ai-build`. Traduce decisiones de producto en specs técnicas, revisa el output construido. |
| `pda-problem` | AI Agent | 1 | Generates and validates the Problem Statement / Genera y valida el Problem Statement |
| `pda-solution` | AI Agent | 2 | Generates and validates the Solution Brief / Genera y valida la Solution Brief |
| `pda-context` | AI Agent | 3 | Generates the Context Specification / Genera la Context Specification |
| `pda-ai-build` | AI Agent | 4 | Builds and verifies code / Construye y verifica código |

---

## Quick Start

### Prerequisites / Prerrequisitos

- An AI coding agent / Un agente de código IA: [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [GitHub Copilot](https://github.com/features/copilot), [Cursor](https://cursor.sh)

### Setup

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project
```

### The Flow / El flujo

```
PHASE 1 — PROBLEM
  /pda-problem → generates + validates PS → human approves → Gate 1

PHASE 2 — SOLUTION
  /pda-solution → generates + validates SB (business only) → human approves → Gate 2

PHASE 3 — CONTEXT
  /pda-context → generates Context Spec (technical) → human approves → Gate 3

PHASE 4 — BUILD
  /pda-ai-build → constitution → spec → plan → tasks → code → verify → Gate 4
```

See `docs/QUICKSTART.md` for detailed step-by-step instructions.

**Agents** are available for Claude Code (`.claude/agents/`), GitHub Copilot (`.github/prompts/`), and Cursor (`.cursor/rules/`).

---

## File Structure / Estructura de archivos

```
your-project/
├── docs/
│   ├── pda-problem.md                  ← Problem Statement (9 elements)
│   ├── pda-solution-brief.md           ← Solution Brief (business decisions)
│   ├── pda-context-spec.md             ← Context Specification (technical decisions)
│   └── QUICKSTART.md                   ← Step-by-step guide (EN+ES)
│
├── templates/
│   ├── pda-problem.template.md         ← Empty PS template
│   ├── pda-solution-brief.template.md  ← Empty SB template
│   └── pda-context-spec.template.md    ← Empty Context Spec template
│
├── .claude/agents/                     ← Claude Code agents
│   ├── pda-problem.md
│   ├── pda-solution.md
│   ├── pda-context.md
│   └── pda-ai-build.md
│
├── .github/prompts/                    ← GitHub Copilot prompts
│   ├── pda-problem.md
│   ├── pda-solution.md
│   ├── pda-context.md
│   └── pda-ai-build.md
│
├── .cursor/rules/                      ← Cursor rules
│   ├── pda-problem.mdc
│   ├── pda-solution.mdc
│   ├── pda-context.mdc
│   └── pda-ai-build.mdc
│
├── .specify/                           ← Spec Kit artifacts (generated by /pda-ai-build)
│   ├── memory/constitution.md
│   └── specs/001-feature/
│
├── pda-verification/                   ← Verification reports (generated)
├── CLAUDE.md                           ← Claude Code instructions
├── AGENTS.md                           ← Copilot / generic agent instructions
└── README.md
```

---

## Gate Reviews

### Gate 1: Problem → Solution

- 9 PS elements present and complete / 9 elementos del PS presentes y completos
- Each element cites evidence / Cada elemento cita evidencia
- No unresolved contradictions / Sin contradicciones sin resolver
- Human approval / Aprobación humana

### Gate 2: Solution → Context

- Solution Brief complete (business decisions only) / Solution Brief completa (solo decisiones de negocio)
- Every component has `gap_ref` + `success_ref` to PS / Cada componente tiene trazabilidad al PS
- Translatability map: no insufficient dimensions / Mapa de traducibilidad: sin dimensiones insuficientes
- Human approval / Aprobación humana

### Gate 3: Context → Build

- Context Specification complete (all technical decisions) / Context Specification completa (todas las decisiones técnicas)
- Every technical decision justified against SB constraint or component / Cada decisión técnica justificada contra restricción o componente de la SB
- Human approval / Aprobación humana

### Gate 4: Build → Market

- All verification reports pass / Todos los informes de verificación pasan
- Output addresses the PS gap / El output aborda la brecha del PS
- Success criteria verifiable in output / Criterios de éxito verificables en el output
- Human approval / Aprobación humana

---

## Multi-Agent Support / Soporte multi-agente

| Agent | Location | Format |
|---|---|---|
| Claude Code | `.claude/agents/pda-*.md` | Agents with frontmatter |
| GitHub Copilot | `.github/prompts/pda-*.md` | Prompt files |
| Cursor | `.cursor/rules/pda-*.mdc` | Rule files with frontmatter |

All formats encode the same behavior. The Claude Code agents (`.claude/agents/`) are the canonical source.

---

## Included Example / Ejemplo incluido

The `example/` directory contains a fully worked project: **TeamTasks**, a shared task list for small teams. It includes research evidence, a completed Problem Statement, Solution Brief, and Context Specification. Use it to see the full PDA flow in action.

El directorio `example/` contiene un proyecto completamente trabajado: **TeamTasks**, una lista de tareas compartida para equipos pequeños. Incluye evidencia de investigación, Problem Statement, Solution Brief y Context Specification completados. Úsalo para ver el flujo completo de PDA en acción.

---

## Methodology / Metodología

Problem-Driven AI structures work in five phases where 90% of value is generated before the AI builds anything:

1. **Problem** — Investigate the real problem through evidence
2. **Solution** — Define the solution with team consensus
3. **Context** — Translate human decisions into AI-processable context
4. **AI Build** — AI builds; humans verify fidelity
5. **Market** — User behavior feeds the next iteration

Learn more at [problemdriven.ai](https://problemdriven.ai).

---

## Roadmap

| Version | Trigger | Added |
|---|---|---|
| **V1** (current) | — | 4 PDA agents (problem, solution, context, ai-build) |
| **V2** | Quality gaps in V1 | Context validation agent, formal Gate 3 checks |
| **V3** | Product in market | `pda-market-monitor`, Phase 5 artifacts |
| **V4** | Scale needs | Custom PDA generators |

---

## License

MIT

---

*The problem is sacred. The AI just changed what happens after you find it.*

*El problema es sagrado. La IA solo cambió lo que ocurre después de encontrarlo.*

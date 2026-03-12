# Problem-Driven AI × Spec Kit — Toolkit V1

> **Think first. Build second. Let the AI execute what humans decided.**
>
> **Piensa primero. Construye después. Deja que la IA ejecute lo que los humanos decidieron.**

An open-source toolkit that connects [Problem-Driven AI](https://problemdriven.ai) with [GitHub Spec Kit](https://github.com/github/spec-kit). Two AI verification agents ensure that everything the AI builds traces back to a real, validated problem.

Un toolkit open-source que conecta [Problem-Driven AI](https://problemdriven.ai) con [GitHub Spec Kit](https://github.com/github/spec-kit). Dos agentes de verificación IA garantizan que todo lo que la IA construye tiene trazabilidad a un problema real y validado.

---

## What This Solves / Qué resuelve

**EN:** Spec Kit turns specifications into code. But it starts *after* the thinking is done. It assumes you already know what to build and why. Problem-Driven AI fills that gap: it structures the human thinking that must happen *before* any specification exists. This toolkit connects both systems.

**ES:** Spec Kit convierte especificaciones en código. Pero empieza *después* de que el pensamiento esté hecho. Asume que ya sabes qué construir y por qué. Problem-Driven AI llena ese vacío: estructura el pensamiento humano que debe ocurrir *antes* de que exista cualquier especificación. Este toolkit conecta ambos sistemas.

```
Phases 1–2:  Human thinking, verified by PDA agents
Phase 3:     PDA adapter translates into Spec Kit inputs
Phase 4:     Spec Kit builds, PDA agents verify fidelity

Fases 1–2:   Pensamiento humano, verificado por agentes PDA
Fase 3:       El adaptador PDA traduce a inputs de Spec Kit
Fase 4:       Spec Kit construye, agentes PDA verifican fidelidad
```

---

## The Five Actors / Los cinco actores

| Actor | Type / Tipo | Phases / Fases | Role / Rol |
|---|---|---|---|
| Human (team) | Person | 1, 2 | Investigates, synthesizes, decides / Investiga, sintetiza, decide |
| `pda-problem-validator` | AI Agent | 1–4 | Verifies against evidence and Problem Statement / Verifica contra evidencia y Problem Statement |
| `pda-solution-brief` | AI Agent | 2–3 | Verifies coverage and translatability / Verifica cobertura y traducibilidad |
| Spec Kit | Toolkit | 3–4 | Generates technical artifacts / Genera artefactos técnicos |
| Human (Context Engineer) | Person | 3–4 | Operates adapter, reviews outputs / Opera el adaptador, revisa outputs |

---

## Quick Start

### Prerequisites / Prerrequisitos

- An AI coding agent / Un agente de código IA: [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [GitHub Copilot](https://github.com/features/copilot), [Cursor](https://cursor.sh), or any Spec Kit-compatible agent
- [Spec Kit CLI](https://github.com/github/spec-kit): `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git`

### Setup

```bash
git clone https://github.com/problemdriven/pda-toolkit.git my-project
cd my-project

# Initialize Spec Kit with your AI agent
specify init --here --ai claude      # Claude Code
specify init --here --ai copilot     # GitHub Copilot
specify init --here --ai cursor      # Cursor

# The repo includes a complete example project (SaaS onboarding).
# To start fresh with empty templates:
cp docs/templates/pda-problem.template.md docs/pda-problem.md
cp docs/templates/pda-solution-brief.template.md docs/pda-solution-brief.md
```

### The Flow / El flujo

```
PHASE 1 — PROBLEM
  Fill docs/pda-problem.md → /pda.validate-problem → Gate 1

PHASE 2 — SOLUTION
  Fill docs/pda-solution-brief.md → /pda.validate-solution → Gate 2

PHASE 3 — CONTEXT (PDA → Spec Kit adapter)
  /pda.adapt-constitution  →  .specify/memory/constitution.md
  /pda.adapt-specify       →  prepare inputs → /speckit.specify
  /pda.verify-specify      →  traceability check
  /speckit.plan            →  /pda.verify-plan
  /speckit.tasks           →  /pda.verify-tasks

PHASE 4 — BUILD
  /speckit.implement       →  /pda.verify-build
```

**Slash commands** work in Claude Code (`.claude/commands/`), GitHub Copilot (`.github/prompts/`), and Cursor (`.cursor/rules/`).

---

## File Structure / Estructura de archivos

```
your-project/
├── docs/
│   ├── pda-problem.md                  ← Problem Statement (example included)
│   ├── pda-solution-brief.md           ← Solution Brief (example included)
│   ├── templates/                      ← Empty templates to start fresh
│   │   ├── pda-problem.template.md
│   │   └── pda-solution-brief.template.md
│   ├── examples/                       ← Completed example (SaaS onboarding)
│   │   ├── pda-problem-example.md
│   │   └── pda-solution-brief-example.md
│   └── QUICKSTART.md                   ← Step-by-step guide (EN+ES)
│
├── .pda/
│   ├── agents/
│   │   ├── pda-problem-validator.md    ← 11 rules, 7 skills
│   │   └── pda-solution-brief.md       ← 8 rules, 3 skills
│   ├── scripts/
│   │   └── adapter.md                  ← PDA → Spec Kit translation guide
│   └── templates/
│       └── verify-report.template.md
│
├── .specify/                           ← Spec Kit directory
│   └── memory/
│       └── constitution.md             ← Generated by /pda.adapt-constitution
│
├── .claude/commands/                   ← Claude Code slash commands
├── .github/prompts/                    ← GitHub Copilot slash commands
├── .cursor/rules/                      ← Cursor rules
│
├── pda-verification/                   ← Verification reports (generated)
├── CLAUDE.md                           ← Claude Code instructions
├── AGENTS.md                           ← Copilot / generic agent instructions
└── README.md
```

---

## PDA Agents / Agentes PDA

### `pda-problem-validator`

**EN:** The Problem Statement guardian. It never generates insights — only verifies that what humans documented is evidence-based, complete, and consistent. 11 rules, 7 skills, operates across Phases 1–4.

**ES:** El guardián del Problem Statement. Nunca genera insights: solo verifica que lo que los humanos documentaron está basado en evidencia, es completo y consistente. 11 reglas, 7 skills, opera en Fases 1–4.

### `pda-solution-brief`

**EN:** The Solution Brief guardian. Ensures every component traces back to the problem and that the brief is precise enough for AI translation. 8 rules, 3 skills, operates in Phases 2–3.

**ES:** El guardián de la Solution Brief. Garantiza que cada componente tiene trazabilidad al problema y que el brief es lo suficientemente preciso para traducción IA. 8 reglas, 3 skills, opera en Fases 2–3.

---

## Gate Reviews

### Gate 1: Problem → Solution

- 9 PS elements present and complete / 9 elementos del PS presentes y completos
- Each element cites evidence / Cada elemento cita evidencia
- No unresolved contradictions / Sin contradicciones sin resolver
- Stakeholder approval / Aprobación de stakeholders

### Gate 2: Solution → Context

- Solution Brief complete (8 sections) / Solution Brief completa (8 secciones)
- Solution validated with users / Solución validada con usuarios
- Translatability map: no insufficient dimensions / Mapa de traducibilidad: sin dimensiones insuficientes
- Team consensus verified / Consenso del equipo verificado

### Gate 3: Context → Build

- All `verify-*.md` reports pass / Todos los informes `verify-*.md` pasan
- Human approval of spec, plan, and tasks / Aprobación humana de spec, plan y tasks

### Gate 4: Build → Market

- `verify-build.md` confirms fidelity to PS gap / confirma fidelidad a la brecha del PS
- Success criteria verifiable in output / Criterios de éxito verificables en el output

---

## Multi-Agent Support / Soporte multi-agente

| Agent | Commands location | Setup |
|---|---|---|
| Claude Code | `.claude/commands/pda.*.md` | `specify init --here --ai claude` |
| GitHub Copilot | `.github/prompts/pda-*.md` | `specify init --here --ai copilot` |
| Cursor | `.cursor/rules/pda-*.mdc` | `specify init --here --ai cursor` |

All agents use the same PDA agent definitions (`.pda/agents/`) and adapter (`.pda/scripts/adapter.md`). Only the command format differs.

---

## Included Example / Ejemplo incluido

The `docs/` directory ships with a fully worked example: a **SaaS onboarding optimization** project with completed Problem Statement and Solution Brief. Run `/pda.validate-problem` and `/pda.validate-solution` to see the agents in action.

El directorio `docs/` incluye un ejemplo completo: un proyecto de **optimización de onboarding SaaS** con Problem Statement y Solution Brief terminados. Ejecuta `/pda.validate-problem` y `/pda.validate-solution` para ver los agentes en acción.

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
| **V1** (current) | — | 2 PDA agents + Spec Kit adapter |
| **V2** | Quality gaps in V1 | `pda-context-validator`, formal Gate 3 |
| **V3** | Product in market | `pda-market-monitor`, Phase 5 artifacts |
| **V4** | Spec Kit doesn't scale | Custom PDA generators |

---

## License

MIT

---

*The problem is sacred. The AI just changed what happens after you find it.*

*El problema es sagrado. La IA solo cambió lo que ocurre después de encontrarlo.*

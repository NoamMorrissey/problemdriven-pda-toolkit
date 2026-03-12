# 📊 The Process

How Problem-Driven AI works, from research to working code.

---

## 🎯 The Core Idea

90% of the value in a software project is generated **before the AI writes a single line of code**.

The AI does not think. The AI executes. Humans think. Humans investigate, synthesize, and decide. The toolkit structures that human thinking into artifacts the AI can execute from — without inventing, without guessing, without making decisions it shouldn't make.

When the AI starts building, it should not need to make any important decision. Only execute.

---

## 📊 The 4 Phases

### Phase 1: Problem

**What happens:** You investigate the real problem through evidence — user interviews, surveys, analytics, competitor analysis. The AI agent reads this evidence, generates a Problem Statement with 9 elements, and validates every claim against the evidence.

**Who participates:** The product team provides the research. The AI agent structures and validates it.

**Output:** `docs/pda-problem.md` — the Problem Statement.

**Gate Review (Gate 1):**
- All 9 elements are present and complete
- Every element cites specific evidence
- No unresolved contradictions in the evidence
- Assumptions are explicitly labeled
- Human approves

---

### Phase 2: Solution

**What happens:** Based on the approved Problem Statement, you define what to build and why. The AI agent generates a Solution Brief with business decisions only — components, success criteria, constraints, actor map.

**Who participates:** The product team makes business decisions. The AI agent structures and validates traceability.

**Output:** `docs/pda-solution-brief.md` — the Solution Brief.

**Gate Review (Gate 2):**
- Every component traces to a gap and success criterion in the PS
- No technical decisions are included (no stack, no architecture)
- All dimensions in the translatability map are sufficient
- Human approves

---

### Phase 3: Context

**What happens:** The approved Problem Statement and Solution Brief are translated into technical decisions. The AI agent generates a Context Specification covering stack, architecture, data model, interaction patterns, visual design, accessibility, and error handling.

**Who participates:** The technical team (or Context Engineer) makes technical decisions. The AI agent structures and validates them against the SB.

**Output:** `docs/pda-context-spec.md` — the Context Specification.

**Gate Review (Gate 3):**
- Every technical decision is justified against a SB constraint or component
- No ambiguity was resolved by inventing — the agent asked the human
- Human approves

---

### Phase 4: Build

**What happens:** The AI reads all three documents and executes the full build pipeline: constitution → spec → plan → tasks → code → verification. Each step is verified before proceeding. If any check fails, the agent stops.

**Who participates:** The AI builds. The human reviews and approves.

**Output:** Working code in `src/`, spec artifacts in `.specify/`, verification reports in `pda-verification/`.

**Gate Review (Gate 4):**
- All verification reports pass
- The output addresses the gap defined in the PS
- Success criteria are verifiable in the output
- Human approves

---

## 🔑 Key Concept: Solution Brief vs Context Specification

The **Solution Brief** defines **what** to build and **why**. It contains product decisions: components, success criteria, constraints, actor map, priorities. It does not mention any technology.

The **Context Specification** defines **how** to build it. It contains technical decisions: stack, architecture, data model, interaction patterns, visual design, accessibility, error handling.

**In small projects** it can feel redundant — the same person writes both. But the separation forces you to make product decisions *before* technical decisions, not at the same time. This prevents technology choices from distorting what you're building.

**In large projects** different people write them. The product team writes the SB. The engineering team writes the Context Spec. The separation ensures product thinking and technical thinking don't contaminate each other.

---

## 🔗 Go Deeper

The full Problem-Driven AI methodology covers five phases (this toolkit implements the first four), ten principles, and detailed guidance on anti-patterns and edge cases.

- [problemdriven.ai/methodology](https://problemdriven.ai/methodology) — Full methodology reference
- [problemdriven.ai/methodology/phases](https://problemdriven.ai/methodology/phases) — The 5 phases in depth
- [problemdriven.ai/methodology/principles](https://problemdriven.ai/methodology/principles) — The 10 principles

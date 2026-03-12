# 🧭 Methodology

A summary of the Problem-Driven AI framework. For the full reference, visit [problemdriven.ai](https://problemdriven.ai).

---

## What Is Problem-Driven AI?

Problem-Driven AI is a methodology that structures the human thinking required before AI builds anything. It ensures that every line of AI-generated code traces back to a validated problem through a chain of human decisions. The AI does not think — it executes what humans decided.

---

## 🏗️ The 5 Phases

1. **Problem** — Investigate the real problem through evidence
2. **Solution** — Define what to build and why, with team consensus
3. **Context** — Translate human decisions into technical specifications
4. **AI Build** — AI builds and verifies; humans approve
5. **Market** — User behavior feeds the next iteration

This toolkit implements **phases 1 through 4**. Phase 5 (Market) involves real-world deployment and feedback loops that happen outside the toolkit.

Full reference: [problemdriven.ai/methodology/phases](https://problemdriven.ai/methodology/phases)

---

## 📐 The 10 Principles

1. The Problem Is Sacred
2. Evidence Over Opinion
3. Humans Think, AI Executes
4. Traceability Is Non-Negotiable
5. Separate What from How
6. Verify at Every Gate
7. Never Invent
8. Fix Upstream
9. Simplicity Over Completeness
10. The User Is the Final Judge

Full reference: [problemdriven.ai/methodology/principles](https://problemdriven.ai/methodology/principles)

---

## 🔧 This Toolkit Implements Phases 1–4

The PDA Toolkit is the practical implementation of the methodology. Each phase has a dedicated AI agent that generates, validates, and presents artifacts for human approval:

| Phase | Agent | Artifact |
|---|---|---|
| 1. Problem | `/pda-problem` | Problem Statement |
| 2. Solution | `/pda-solution` | Solution Brief |
| 3. Context | `/pda-context` | Context Specification |
| 4. AI Build | `/pda-ai-build` | Working code |

---

## 📚 Full Reference

- [problemdriven.ai](https://problemdriven.ai) — Home
- [Vision](https://problemdriven.ai/vision) — Why this methodology exists
- [Methodology](https://problemdriven.ai/methodology) — Phases, principles, and anti-patterns
- [Planning](https://problemdriven.ai/planning) — Strategic planning with PDA
- [Operational](https://problemdriven.ai/operational) — Day-to-day execution patterns
- [Resources](https://problemdriven.ai/resources) — Templates, examples, and tools

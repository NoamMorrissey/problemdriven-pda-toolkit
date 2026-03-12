# 🤖 How Agents Work

PDA agents are instructions that tell the AI how to generate and verify artifacts. Each agent has one specific job, a set of validation rules, and a mandatory human approval gate.

---

## The 4 Agents

### `/pda-problem` — Problem Statement Generator

**What it does:** Reads your research evidence (interviews, surveys, analytics, competitor analysis) and generates a Problem Statement with 9 elements: gap, who is affected, success criteria, root causes, current alternatives, constraints, cost of inaction, scope boundaries, and assumptions.

**What it validates:**
- Every element cites specific evidence with IDs
- No insights are invented — only evidence-supported claims
- Contradictions in evidence are flagged, not hidden
- Assumptions are explicitly labeled with risk and validation plan

**When it stops:** If it finds contradictions in the evidence that it cannot resolve, it flags them and asks you to decide.

---

### `/pda-solution` — Solution Brief Generator

**What it does:** Reads the approved Problem Statement and generates a Solution Brief with business decisions only: solution summary, components, success criteria, constraints, actor map, and priorities.

**What it validates:**
- Every component traces to a gap and success criterion in the PS
- Traceability is complete — no orphan components
- The translatability map has no insufficient dimensions

**What it rejects:** Technical decisions. If the agent detects stack choices, architecture patterns, or data model details, it flags them. Those belong in the Context Specification.

---

### `/pda-context` — Context Specification Generator

**What it does:** Reads the approved PS and SB, then generates a Context Specification covering: stack, architecture, data model, interaction patterns, visual design, accessibility, and error handling.

**What it validates:**
- Every technical decision is justified against a SB constraint or component
- The SB conflict resolution clause applies: if SB and Context Spec conflict, SB prevails

**When it asks you:** If the SB is ambiguous about something the Context Spec needs to decide, the agent asks instead of inventing. It will never fill gaps with assumptions.

---

### `/pda-ai-build` — Build Pipeline

**What it does:** Reads all three documents (PS, SB, Context Spec) and executes the full chain:

1. **Constitution** — Extracts rules and constraints from the Context Spec
2. **Spec** — Generates a detailed specification
3. **Plan** — Breaks the spec into an implementation plan
4. **Tasks** — Creates individual implementation tasks
5. **Build** — Writes the code
6. **Verify** — Checks fidelity against the Problem Statement

**When it stops:** If any verification step fails, the agent stops immediately and reports what went wrong. It does not continue building on a broken foundation.

---

## 🔒 Verification Rules

Each agent carries its own set of validation rules (labeled R1–R8, S1–S8, C1–C4, B1–B5). The common thread across all agents:

- **Never invent.** If information is missing, flag it. Don't fill gaps.
- **Traceability is mandatory.** Every claim traces back through the chain: Code → Spec → Context Spec → SB → PS → Evidence.
- **Verify before presenting.** Every agent runs its own validation before asking for your approval.

---

## 💡 Human Approval Is Always Required

No agent makes final decisions. Every agent generates a draft, validates it against its rules, and then presents it to you for review. You can:

- **Approve** — The agent writes the artifact and you move to the next phase
- **Request changes** — Tell the agent what to fix, it regenerates and presents again
- **Reject** — Go back to the source and rework the input

The agents work for you. You have the final say at every gate.

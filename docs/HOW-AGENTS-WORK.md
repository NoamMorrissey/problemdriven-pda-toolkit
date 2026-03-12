# How Agents Work

PDA has 4 agents. Three of them **validate** human-written documents. One of them **generates** code. Each agent has a specific job, a set of validation rules, and a mandatory human approval gate.

---

## The 4 Agents

### `/pda-problem` — Problem Statement Validator

**What it does:** Reads your Problem Statement (that you wrote in `docs/pda-problem.md`) and your research evidence, then validates the PS against the evidence. It checks that all 9 elements are present, every claim cites evidence, contradictions are flagged, and assumptions are labeled.

**What it validates:**
- Every element cites specific evidence with IDs
- No insights are invented — only evidence-supported claims
- Contradictions in evidence are flagged, not hidden
- Assumptions are explicitly labeled with risk and validation plan

**What it never does:** Generate, modify, or propose Problem Statement content. The human writes the PS. The agent only verifies.

---

### `/pda-solution` — Solution Brief Validator

**What it does:** Reads your Solution Brief (that you wrote in `docs/pda-solution-brief.md`) and the approved Problem Statement, then validates traceability and completeness.

**What it validates:**
- Every component traces to a gap and success criterion in the PS
- Traceability is complete — no orphan components
- The translatability map has no insufficient dimensions

**What it rejects:** Technical decisions. If the agent detects stack choices, architecture patterns, or data model details, it flags them. Those belong in the Context Specification.

**What it never does:** Generate, modify, or propose Solution Brief content. The human writes the SB. The agent only verifies.

---

### `/pda-context` — Context Specification Validator

**What it does:** Reads your Context Specification (that you wrote in `docs/pda-context-spec.md`) and both PS and SB, then validates technical coherence against the Solution Brief.

**What it validates:**
- Every technical decision is justified against a SB constraint or component
- No technical decision contradicts a SB constraint
- No gaps where the build agent would need to invent decisions

**What it flags:** Gaps where the SB is ambiguous for a technical decision — the agent never resolves these, it flags them for the human to decide.

**What it never does:** Generate, modify, or propose Context Specification content. The human writes the Context Spec. The agent only verifies.

---

### `/pda-ai-build` — Build Pipeline (the only generator)

**This is the only PDA agent that generates content.** The other three validate human-written documents.

**What it does:** Reads all three validated documents (PS, SB, Context Spec) and executes the full chain:

1. **Constitution** — Extracts rules and constraints from the Context Spec
2. **Spec** — Generates a detailed specification
3. **Plan** — Breaks the spec into an implementation plan
4. **Tasks** — Creates individual implementation tasks
5. **Build** — Writes the code
6. **Verify** — Checks fidelity against the Problem Statement

**When it stops:** If any verification step fails, the agent stops immediately and reports what went wrong. It does not continue building on a broken foundation.

---

## Verification Rules

Each agent carries its own set of validation rules (labeled R1–R7, S1–S4, C1–C3, B1–B5). The common thread across all agents:

- **Never invent.** If information is missing, flag it. Don't fill gaps.
- **Traceability is mandatory.** Every claim traces back through the chain: Code → Spec → Context Spec → SB → PS → Evidence.
- **Verify before presenting.** Every agent runs its own validation before reporting results.

---

## Human Approval Is Always Required

No agent makes final decisions. The three validation agents report PASS or FAIL — the human decides what to do with the result. The build agent presents its output — the human approves or rejects.

You can:

- **Fix and re-validate** — Fix the issues the agent found, run the agent again
- **Override** — If you disagree with a FAIL, you decide. The agents work for you.
- **Reject a build** — Go back to the source documents and rework them

The agents work for you. You have the final say at every gate.

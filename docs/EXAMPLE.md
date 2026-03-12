# 📖 Example Walkthrough: TeamTasks

A narrated guide through the included TeamTasks example. Follow along while looking at the files in `example/`.

---

## 📖 About This Example

**TeamTasks** is a local task board for small teams. HTML + CSS + JS vanilla, localStorage for persistence, zero dependencies. You open a single HTML file in a browser and it works.

The app itself is deliberately simple. That's the point. The value is not the app — it's the **process** of getting to it. Every line of code traces back through tasks → spec → Context Specification → Solution Brief → Problem Statement → evidence from real (fictional) people.

This walkthrough tells the story of how four PDA agents turned research evidence into working code, and what was verified at each gate.

---

## 🔍 Phase 1: Problem (What We Investigated)

### The Evidence

The `example/research/` folder contains fictional but realistic research:

- **3 user interviews** (`research/interviews/`)
  - **Maria** — team lead at a 6-person design agency. Tasks assigned in Slack DMs get buried. Two designers worked on the same icon set, wasting 8 hours.
  - **James** — freelance developer managing 2–3 subcontractors. Spends 20 minutes every morning sending WhatsApp messages asking for status updates. A missed dependency caused a client-facing deadline miss.
  - **Priya** — co-founder of a 4-person startup. Each team member knows only about 70% of what everyone else is working on. Her Google Sheet "Master Task List" had 8 blank statuses and 5 overdue tasks.

- **Survey data** (`research/analytics/usage-data-summary.md`)
  - N=127 respondents from small teams (2–8 people)
  - 53% lose or forget tasks at least once per week
  - 53% have tried and abandoned a dedicated task management tool
  - Top abandonment reason: "too complex for our team size" (58%)

- **Competitor analysis** (`research/benchmarks/competitor-analysis.md`)
  - 5 tools evaluated: Trello, Todoist, Asana, Linear, Google Sheets
  - None designed for teams of 2–8 with near-zero setup

- **Evidence index** (`research/evidence.jsonl`)
  - 12 pieces of evidence (E-001 through E-012), each with source, type, date, and confidence level

### The Resulting Problem Statement

The `/pda-problem` agent reads all this evidence and generates a Problem Statement with **9 elements**:

1. **Gap** — Tasks assigned through chat and verbal agreements have no persistent shared record. Each member knows ~70% of what the team is doing.
2. **Who Is Affected** — Team leads, individual contributors, and founders of small teams (2–8 people).
3. **Success Criteria** — 100% task visibility, under 15 seconds to create a task, under 10% weekly forgotten tasks, under 5 min daily coordination overhead, 80% still using after 2 weeks.
4. **Root Causes** — Ephemeral assignment channels, no single source of truth, no passive visibility mechanism, existing tools too complex.
5. **Current Alternatives** — Chat messages (64%), personal notes (52%), spreadsheets (34%), dedicated tools (28%), memory only (18%).
6. **Constraints** — Must work in a browser without installation. No backend. Free. Under 2 minutes onboarding.
7. **Cost of Inaction** — ~430 hours/year per team in coordination overhead. 16–64 hours/year wasted on duplicate work. Client relationship damage.
8. **Scope Boundaries** — Not a PM tool. No file sharing, chat, accounts, or mobile native app.
9. **Assumptions** — 4 assumptions listed with risk levels and validation plans.

Every element cites specific evidence IDs. The agent validates all citations before presenting.

**Output:** `example/docs/pda-problem.md`

### Gate 1: What Was Verified

- All 9 elements present and complete
- Every element cites evidence with correct IDs
- No contradictions found in the evidence base
- Assumptions explicitly labeled with risk and validation status
- Evidence weighting applied: behavioral observations (E-006, E-010) weighted above declared preferences

**Google Doc reference:** [Problem Statement](https://docs.google.com/document/d/1H1z7gSJiWOhQwOr7u6XmoFFtSbS_wZm8/edit)

---

## 💡 Phase 2: Solution (What the Team Decided)

### Product Decisions

The `/pda-solution` agent reads the approved Problem Statement and generates a Solution Brief with **business decisions only**:

- **What to build:** A shared task board where every task, its owner, deadline, and status are visible to all team members in one place.
- **Core components:**
  - Task creation (under 15 seconds, zero friction)
  - Shared board with real-time visibility of all tasks
  - Status management (column-based: To Do → Doing → Done)
  - Data persistence (survives page reload)
  - Export/import (backup and portability)

### What Was Deliberately Discarded

- Task hierarchies or subtasks
- Complex permissions or roles
- Integrations with other tools
- Real-time sync across devices
- User accounts or authentication
- Comments, attachments, or file sharing
- Timelines, Gantt charts, sprints, or epics

These decisions come directly from the evidence: the #1 reason teams abandon tools is complexity (E-008). Every feature adds friction.

### Important Note

This Solution Brief contains **no technical decisions**. No stack, no architecture, no data model. Those belong in the Context Specification (Phase 3). The SB defines **what** to build and **why**.

**Output:** `example/docs/pda-solution-brief.md`

### Gate 2: What Was Verified

- Every component traces to a gap (`gap_ref`) and success criterion (`success_ref`) in the PS
- No orphan components — everything connects to the validated problem
- No technical decisions present in the SB
- Translatability map has no insufficient dimensions

**Google Doc reference:** [Solution Brief](https://docs.google.com/document/d/1Y7aiZH-INSYB-vPSAF_KD3Cjq3mdUXCj/edit)

---

## ⚙️ Phase 3: Context (How the Technical Team Translated It)

### The Context Specification

The `/pda-context` agent reads the PS and SB, then generates a Context Specification with all technical decisions:

- **Stack:** Vanilla HTML + CSS + JavaScript. No frameworks, no build tools, no dependencies. Chosen for the example's simplicity constraint — a user opens one HTML file and it works.
- **Architecture:** 3 files (index.html, style.css, app.js). In-memory state synced to localStorage. Native browser dialogs for confirmation.
- **Data Model:** Tasks stored as JSON objects with id, title, description, assignee, dueDate, status, createdAt. Column states: todo, doing, done.
- **Interaction Decisions:** Drag-and-drop for status changes with click fallback for accessibility. Quick-add form at the top.
- **Visual Design:** CSS custom properties for theming. CSS Grid layout. 768px responsive breakpoint.
- **Accessibility:** WCAG AA compliance. ARIA roles on columns. Keyboard navigation. Focus management on dialogs.
- **Export/Import:** Blob + FileReader API. JSON format. Download as file, upload to restore.
- **Error Handling:** localStorage full graceful fallback. Input validation with inline messages. Empty state messaging.

**Output:** `example/docs/pda-context-spec.md`

**Google Doc reference:** [Context Specification](https://docs.google.com/document/d/1Z0Kvot2_LQTr4U02lZslJJHHnGQ0oyGQ/edit)

### What /pda-ai-build Generated

From the three approved documents (PS + SB + Context Spec), the `/pda-ai-build` agent generates a chain of spec artifacts before writing any code:

- **`example/.specify/memory/constitution.md`** — The rules and constraints extracted from the Context Spec. This is the AI's "operating contract" — it cannot deviate from these rules while building.

- **`example/.specify/specs/001-feature/spec.md`** — The detailed specification. Translates the PS + SB + Context Spec into executable requirements with acceptance criteria for each component.

- **`example/.specify/specs/001-feature/plan.md`** — The implementation plan. Describes the architecture, file structure, and the order of implementation phases.

- **`example/.specify/specs/001-feature/tasks.md`** — The concrete tasks. Each task has a description, acceptance criteria, and traceability to the spec. This is what the AI actually executes.

### PDA Verifications

Before building and after building, the agent runs verification reports:

- **`example/pda-verification/verify-spec.md`** — Checks that the spec covers all PS requirements and SB components. Catches scope creep (features not in the PS) and gaps (requirements not in the spec).

- **`example/pda-verification/verify-plan.md`** — Checks that the plan addresses all spec items. Catches orphan plan items and uncovered spec requirements.

- **`example/pda-verification/verify-tasks.md`** — Checks that every task traces to the plan and spec. Catches orphan tasks and uncovered plan items.

- **`example/pda-verification/verify-build.md`** — After the code is built, checks fidelity to the Problem Statement. Verifies that success criteria are addressable in the output.

Gate 3 passes when every technical decision is justified against the SB and no ambiguity was resolved by inventing.

---

## 🏗️ Phase 4: AI Build (What the AI Built)

### The Output

The AI generates 3 files in `example/src/`:

- **`index.html`** — The HTML structure: task board with three columns (To Do, Doing, Done), quick-add form, export/import controls.
- **`style.css`** — The styles: CSS Grid layout, custom properties, responsive breakpoint at 768px, accessible focus indicators.
- **`app.js`** — The logic: task CRUD, drag-and-drop with click fallback, localStorage persistence, JSON export/import, empty state handling.

### How to Test It

```bash
open example/src/index.html
```

Or just double-click the file. It opens in your browser. No server needed.

### What Was Verified

The `verify-build.md` report confirms:

- All 5 core components from the SB are implemented
- Success criteria from the PS are addressable in the output
- No features were added that aren't in the spec (no scope creep)
- The output addresses the gap defined in the Problem Statement

---

## 🎓 Lessons Learned

### Gaps Found During the Process

- **Evidence misattributions:** During PS validation, the agent found that two citations attributed data to E-009 that actually belonged to E-008. This was caught by the `/pda-problem` agent's evidence validation rules and corrected before Gate 1.
- **Data inconsistency:** The PS table said "47% abandon" but the evidence (E-008) says 53%. Caught and corrected.
- **Technical language in the SB:** Early drafts of the Solution Brief included references to "localStorage sync." This was flagged because the SB should contain no technical decisions.

### What a Real Team Would Do Differently

- **Real evidence, not fictional.** The research in this example is realistic but invented. In a real project, you'd talk to actual users, run real surveys, and analyze real usage data. The evidence would be messier but more valuable.
- **More iteration at Gate 1.** The Problem Statement is the foundation. Real teams typically go through 2–3 rounds of revision before the PS is solid enough for Gate 1.
- **Team discussions at Gate 2.** The Solution Brief reflects team consensus. In this example there's no team to discuss with. In reality, the SB is where product debates happen — and they should happen here, not during the build.
- **A real tech stack in Phase 3.** Vanilla HTML/CSS/JS was chosen for example simplicity. A real project would use whatever stack fits the team and the problem: React, Vue, Swift, Go, whatever the Context Specification decides.

For a deeper understanding of the process, see [PROCESS.md](PROCESS.md).

---

## 🔗 Reference Documents

| Document | Local File | Google Doc |
|---|---|---|
| Research evidence | `example/research/evidence.jsonl` | — |
| User interview 01 (Maria) | `example/research/interviews/user-interview-01.md` | — |
| User interview 02 (James) | `example/research/interviews/user-interview-02.md` | — |
| User interview 03 (Priya) | `example/research/interviews/user-interview-03.md` | — |
| Survey data | `example/research/analytics/usage-data-summary.md` | — |
| Competitor analysis | `example/research/benchmarks/competitor-analysis.md` | — |
| Problem Statement | `example/docs/pda-problem.md` | [Google Doc](https://docs.google.com/document/d/1H1z7gSJiWOhQwOr7u6XmoFFtSbS_wZm8/edit) |
| Solution Brief | `example/docs/pda-solution-brief.md` | [Google Doc](https://docs.google.com/document/d/1Y7aiZH-INSYB-vPSAF_KD3Cjq3mdUXCj/edit) |
| Context Specification | `example/docs/pda-context-spec.md` | [Google Doc](https://docs.google.com/document/d/1Z0Kvot2_LQTr4U02lZslJJHHnGQ0oyGQ/edit) |
| Constitution | `example/.specify/memory/constitution.md` | — |
| Spec | `example/.specify/specs/001-feature/spec.md` | — |
| Plan | `example/.specify/specs/001-feature/plan.md` | — |
| Tasks | `example/.specify/specs/001-feature/tasks.md` | — |
| Built app | `example/src/index.html` | — |

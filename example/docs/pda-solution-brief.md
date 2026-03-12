# Solution Brief — TeamTasks: Shared Task List for Small Teams

> **Formatted version for humans:** https://docs.google.com/document/d/1-Gxw2TIrU7FmiKM4jDJBAyRAeMU26jdu/edit

**Status:** APPROVED
**Version:** 2.0
**Last updated:** 2026-03-12
**Approved by:** Product Lead, Research Lead
**Problem Statement:** docs/pda-problem.md (v1.0)

---

## 1. Solution Summary

A browser-based shared task list where small teams (2-8 people) can create, assign, and track tasks with zero setup. No accounts, no installation, no configuration. Open the page, add a team member name, create a task, assign it. Everyone on the team sees the same list via shared browser access (same device or shared browser access).

**gap_ref:** PS element 1 (tasks assigned in ephemeral channels, 30% visibility gap)
**success_ref:** PS element 3 (100% task visibility, creation under 15 seconds, adoption >80% at 2 weeks)

---

## 2. Proposed Solution

A web application with three functional areas:

**Team setup (one-time):** A simple input where the user types team member names. No accounts, no emails, no passwords. Just names. These names become the assignee options for tasks.

**Task creation:** A minimal form with three fields: task title (text), assigned to (dropdown from team members), due date (date picker). One click to create. Task appears immediately in the shared list.

**Task list:** A filterable list showing all tasks with columns: title, assigned to, due date, status (to do / done). Clicking a task toggles it complete. Filter by team member to see "my tasks" or "Ana's tasks". Sort by due date. Overdue tasks highlighted.

**Data persistence:** Data persists across browser sessions. For team sharing in this example: team members access the same device or the app is deployed as a static page.

---

## 3. Key Decisions

| Decision | Options Considered | Chosen | Rationale |
|---|---|---|---|
| Accounts vs. no accounts | Email login, magic links, name-only | Name-only | E-009: 24% of survey respondents want no account requirement. Accounts are the #1 barrier to team-wide adoption in small teams. |
| Feature scope | Full PM (boards, timelines), task list + chat, task list only | Task list only | PS scope boundaries explicitly exclude PM features. E-009: "Simplicity / minimal features" is #1 requested attribute (56%). |
| Data sharing model | Real-time sync, shared URL, same device | Same device / static deploy | Simplest approach that demonstrates the concept. Real deployment would need a backend (documented in A-002). |

---

## 4. Solution Dimensions

### Business Components

| Component | Description | gap_ref | success_ref | Priority |
|---|---|---|---|---|
| Team member manager | Add/remove team member names. Simple text input + list. | PS-1 (no shared location for assignments) | Tool adoption (zero setup) | Must |
| Task creation form | 3-field form: title, assignee, due date. One-click create. | PS-1 (task creation takes 2-5 min) | Task creation speed (<15 sec) | Must |
| Task list view | Filterable, sortable list of all tasks with status toggle. | PS-1 (30% visibility gap) | Task visibility (100%) | Must |
| Filter by person | Click a team member name to see only their tasks. | PS-1 (no passive visibility) | Coordination overhead (<5 min/day) | Must |
| Overdue highlighting | Tasks past their due date shown in a distinct visual style. | PS-1 (tasks forgotten) | Forgotten tasks (<10% weekly) | Should |
| Data persistence | Read/write for all tasks and team members across sessions. | PS-6 (must work without backend) | Tool adoption (data survives refresh) | Must |

---

## 5. Assumptions and Risks

| ID | Assumption | Source | Risk | Constraint | Status |
|---|---|---|---|---|---|
| A-001 | A zero-setup shared list will achieve higher adoption than Trello/Asana in small teams | PS | High | Must measure 2-week retention against 53% abandonment baseline (E-008) | Unverified |
| A-002 | Browser-local persistence is sufficient for single-device usage in an example | PS | Low | Document limitation clearly; real deployment would need a backend | Active → constraint: README must state persistence limitation |
| A-003 | Teams will check the shared list without push notifications | PS | Medium | Must be fast enough to load that "checking" feels effortless | Active → constraint: page load under 1 second |
| A-004 | Three fields (title, person, date) are enough for a task | New | Low | If users need more fields, that's a V2 signal, not a V1 blocker | Active |

---

## 6. Success Criteria

### Global (from PS)

| PS Criterion | Metric | Target | Components |
|---|---|---|---|
| Task visibility | % active tasks visible to all | 100% | Task list view, Filter by person |
| Task creation speed | Time to create and assign | <15 seconds | Task creation form |
| Forgotten tasks | Frequency of weekly forgotten tasks | <10% report weekly | Task list view, Overdue highlighting |
| Coordination overhead | Daily time on status checking | <5 minutes | Task list view, Filter by person |
| Tool adoption | Consistent usage after 2 weeks | >80% still using | All components (simplicity is the driver) |

### Per Component

| Component | Criterion | Metric | Target |
|---|---|---|---|
| Team member manager | Setup speed | Time from opening app to first team member added | <30 seconds |
| Task creation form | Creation speed | Time from clicking "new" to task visible in list | <15 seconds |
| Task list view | Scan speed | Time to answer "what's on my plate today?" | <10 seconds |
| Filter by person | Filter speed | Time from wanting to see someone's tasks to seeing them | <3 seconds (one click) |
| Overdue highlighting | Noticeability | Can a user spot overdue tasks without reading dates? | Yes (visual differentiation) |
| Data persistence | Reliability | Data survives browser refresh and restart | 100% |

---

## 7. Constraints

### Business
- Free. No pricing model. This is an example project. (PS business constraint)
- Must be understandable by non-technical users. (E-004: creative, consulting, marketing users)

### Organizational
- Onboarding under 2 minutes. User should be creating tasks within 30 seconds of opening. (E-008: 27% abandoned tools due to long onboarding)

---

## 8. Translatability Map

| Dimension | Rating | Issues | Action |
|---|---|---|---|
| Business | Sufficient | All 6 components defined with clear gap_ref and success_ref | None |
| Constraints | Sufficient | All constraints sourced and justified | None |
| Success criteria | Sufficient | All metrics defined with current and target values | None |
| Technical | Deferred | Architecture, data, and stack decisions in Context Specification | See docs/pda-context-spec.md |

---

## Actor Map

| Actor | Problem | Solution | Authority |
|---|---|---|---|
| Team lead | Experiences directly (assigns tasks, loses track) | Creates tasks, checks team status | Approves |
| Team member | Affected (doesn't see what's assigned to them) | Views own tasks, marks complete | Uses |
| Client/stakeholder | Affected downstream (late deliverables) | Does not interact with tool | None |

---

## Decision Matrix

| Criterion | Weight | Single HTML app | React SPA | Notion template |
|---|---|---|---|---|
| Zero setup / dependencies | 35% | 10 | 4 | 7 |
| Simplicity of codebase | 25% | 10 | 5 | N/A |
| Demonstrates PDA flow | 20% | 9 | 9 | 3 |
| Real-world usability | 15% | 6 | 8 | 7 |
| Shareability | 5% | 8 | 6 | 9 |
| **Weighted Total** | | **9.15** | **5.85** | **5.60** |

---

## Feedback Log

| Date | Source | Feedback | Action | Status |
|---|---|---|---|---|
| 2026-02-22 | Internal review | "Should tasks have priority levels?" | Deferred to V2. Three fields is the minimum viable. | Resolved |
| 2026-02-24 | Internal review | "How do teams share if it's localStorage?" | Documented as known limitation. Real deployment needs backend. Example focuses on the flow, not production architecture. | Resolved |
| 2026-02-26 | Internal review | "Should there be a 'delete task' option?" | Added as implicit: completed tasks can be cleared. Core flow is create → assign → complete. | Resolved |

---

> **Note:** Technical decisions (stack, architecture, data model, interaction patterns, visual design, accessibility, and error handling) are defined in the **Context Specification** (`docs/pda-context-spec.md`), generated during Phase 3. This document focuses on product decisions and business traceability. If there is a conflict between this Solution Brief and the Context Specification, the Solution Brief prevails.

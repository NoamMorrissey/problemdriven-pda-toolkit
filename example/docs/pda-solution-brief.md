# Solution Brief — TeamTasks

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-02-16
**Problem Statement:** docs/pda-problem.md (v1.0)
**Gate 2:** PASS

---

## 1. Summary

TeamTasks is a shared task list for small teams of 2-8 people. It runs entirely in the browser with no server, no accounts, and no installation. A team lead opens the app, adds team member names, creates tasks, and assigns them. All team members sharing the same browser (or same device) see the same list. The goal is to replace task assignments scattered across chat messages and personal notes with a single, persistent, shared view of who is doing what.

---

## 2. Proposed Solution

A local browser-based application that provides:

- **A single shared task list** where all tasks are visible to anyone who opens the app on that browser. This directly addresses the 30% visibility gap [PS §1, E-002].
- **Instant task creation** with three fields: task name, assigned person, and due date. This matches the "under 30 seconds" requirement [PS §3.2, E-009].
- **Team member management** where the team lead adds names (plain text strings, not accounts). Members are labels for assignment, not users with logins [PS §6 C-1, E-009].
- **Task status tracking** through manual status changes (To Do, In Progress, Done) so any team member can see and update progress [PS §3.1].
- **Drag-and-drop reordering** for prioritization, so the team lead can arrange tasks by importance [PS §3.1].
- **Data export and import** so teams can back up their data or move it to another browser [PS §8 — no sync, but migration is possible].

---

## 3. Key Decisions

| Decision | Rationale |
|---|---|
| Local-only, no server | Zero setup requirement [PS §6 C-1]. No accounts, no login, no server means instant usability. Tradeoff: no cross-device sync. |
| Team members are name strings, not user accounts | 24% of respondents explicitly requested no login [E-009]. Real accounts would require authentication infrastructure, violating the zero-setup constraint. |
| Three-field task creation (name, person, date) | 56% requested simplicity, 38% requested fast creation [E-009]. Every additional field increases friction and risks the same adoption failure as existing tools [E-008]. |
| Manual status updates (no automation) | Keeps the tool predictable and simple. Automation would require defining workflows, which is what these teams explicitly rejected [E-008]. |
| No notifications | Assumption A-2 in the PS: teams will check the shared list proactively. Adding notifications would require accounts or contact information, violating C-1. |
| No integrations | PS §8 explicitly scopes out integrations. This keeps the tool independent and avoids the complexity that caused 44% of tool abandonments [E-008]. |

---

## 4. Business Components

### BC-1: Team Setup
Create and manage a list of team member names. These names are used as assignment labels throughout the app.
- **Gap ref:** PS §1 — tasks assigned to people not tracked in any shared system
- **Success ref:** PS §3.5 — zero adoption friction, no accounts needed

### BC-2: Task Creation
Create a task with a name, assigned team member, and optional due date. Task creation must feel faster than sending a chat message.
- **Gap ref:** PS §1 — no shared persistent location for task assignments
- **Success ref:** PS §3.2 — task creation under 30 seconds

### BC-3: Task Board
Display all tasks organized by status (To Do, In Progress, Done) in a single view. All team members see the same board.
- **Gap ref:** PS §1 — 30% visibility gap, fragmented task information
- **Success ref:** PS §3.1 — all team members see all tasks, owners, and status

### BC-4: Task Management
Update task status, edit task details, reassign tasks, reorder by priority, and delete tasks. All changes are reflected immediately.
- **Gap ref:** PS §4 RC-2 — no shared persistent registry
- **Success ref:** PS §3.4 — no manual polling needed, status visible at a glance

### BC-5: Overdue Visibility
Tasks past their due date are visually distinct without requiring the user to read or calculate dates. The overdue state is immediately apparent.
- **Gap ref:** PS §5 — Priya's spreadsheet had 5 overdue tasks still marked "In Progress" [E-010]
- **Success ref:** PS §3.1 — task status visible at a glance

### BC-6: Data Persistence
All data survives browser refreshes and tab closures. Data is stored locally in the browser.
- **Gap ref:** PS §4 RC-1 — tasks in chat are ephemeral
- **Success ref:** PS §3.3 — tasks persist until explicitly completed or removed

### BC-7: Data Export and Import
Export all data as a downloadable file. Import data from a previously exported file. This allows backup and migration between browsers.
- **Gap ref:** PS §4 RC-4 — abandoned tracking systems lose all historical data
- **Success ref:** PS §3.3 — tasks are not lost

### BC-8: Filter by Assignee
View tasks filtered by team member to quickly answer "what is [person] working on?" without scanning the entire board.
- **Gap ref:** PS §2 — coordinators need the full picture of who is doing what
- **Success ref:** PS §3.4 — reduced coordination overhead, no manual polling needed

---

## 5. Assumptions

| ID | Assumption | Impact if wrong |
|---|---|---|
| SA-1 | A single shared browser is sufficient — the team lead's device serves as the "team hub" | If team members need individual access from their own devices, a local-only app doesn't work. This is the most significant product risk. |
| SA-2 | Three task statuses (To Do, In Progress, Done) are sufficient for small team workflows | Some teams may need custom statuses (Blocked, Review, etc.), limiting adoption |
| SA-3 | Teams don't need subtasks or task dependencies | Teams managing projects with sequential steps may find the flat list insufficient |
| SA-4 | Export/import is an acceptable substitute for cross-device sync | If teams need real-time sync, this is not the right product |
| SA-5 | A team lead will take responsibility for initial setup (adding team members) | If no one takes the initiative, the tool won't get started |

---

## 6. Success Criteria

| ID | Criterion | Measurement | Source |
|---|---|---|---|
| SC-1 | All tasks visible to all team members in a single view | The task board shows every task regardless of who created it | PS §3.1 |
| SC-2 | Task creation takes under 30 seconds | Time from "I want to add a task" to "task appears on the board" | PS §3.2, E-009 |
| SC-3 | Tasks persist until explicitly completed or removed | Close browser, reopen — tasks are still there | PS §3.3 |
| SC-4 | No manual polling needed for status updates | Status is visible on the board, updated by whoever changes it | PS §3.4, E-005 |
| SC-5 | No accounts, no login, no installation required | Open the file in a browser and start using it | PS §3.5, E-009 |
| SC-6 | Overdue tasks are visually distinct | Past-due tasks have a visual indicator that doesn't require reading the date | PS §3.1, E-010 |
| SC-7 | Works on mobile browsers | Layout is usable on phone-sized screens | PS §6 C-4, E-009 |

---

## 7. Constraints

### Business Constraints

| ID | Constraint | Source |
|---|---|---|
| BC-C1 | No server, no backend, no network requests | PS §6 C-1 — zero setup, no accounts |
| BC-C2 | No user accounts, no authentication, no sessions | PS §6 C-1, E-009 — 24% requested no login |
| BC-C3 | No cost to the user | PS §6 C-3, E-008 — free tier limitations caused 31% of abandonments |
| BC-C4 | Must work on mobile web browsers without app installation | PS §6 C-4, E-009 |

### Organizational Constraints

| ID | Constraint | Source |
|---|---|---|
| OC-1 | No external dependencies or services | Eliminates maintenance, hosting costs, and service availability risks |
| OC-2 | Single-developer buildable | The entire app must be buildable by one AI agent in one session |

---

## 8. Translatability Map

This map connects Solution Brief components to the technical decisions that will need to be made in the Context Specification (Phase 3).

| SB Component | Technical Decision Needed (Phase 3) |
|---|---|
| BC-1: Team Setup | Data model for team members, storage format |
| BC-2: Task Creation | Form UI pattern, validation rules, ID generation |
| BC-3: Task Board | Layout architecture, rendering strategy, status columns |
| BC-4: Task Management | State mutation approach, drag-and-drop implementation |
| BC-5: Overdue Visibility | Date comparison logic, CSS visual treatment |
| BC-6: Data Persistence | Storage mechanism, serialization format, storage limits |
| BC-7: Data Export/Import | File format, download mechanism, import validation |
| BC-C1: No server | File-based architecture (static HTML/CSS/JS) |
| BC-C4: Mobile web | Responsive design approach, touch interactions |

---

## 9. Actor Map

| Actor | Role | Key Actions |
|---|---|---|
| Team Lead | Sets up the team, creates and assigns tasks, manages priorities | Add team members, create tasks, assign tasks, reorder tasks, update status |
| Team Member | Views tasks, updates their own task status | View task board, change task status, see deadlines |

**Note:** Both actors use the same interface. There are no permissions or role-based access — everyone can do everything. The "Team Lead" distinction is behavioral (who takes initiative to set up), not technical.

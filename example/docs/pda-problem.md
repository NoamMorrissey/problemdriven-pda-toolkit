# Problem Statement — Shared Task Visibility for Small Teams

> **Formatted version for humans:** https://docs.google.com/document/d/1Y8eqTz0Ra8-kzm4p6SPzerZGqr3XbUuu/edit

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-02-20
**Approved by:** Product Lead, Research Lead

---

## 1. Gap

Small teams (2-8 people) working on shared projects assign tasks through chat messages, verbal agreements, and personal notes. These assignments are not captured in a shared, persistent location visible to everyone. The result is that at any given moment, each team member knows only about 70% of what everyone else is working on. That 30% visibility gap causes forgotten tasks, duplicate work, and missed commitments.

The expected state is that every task, its owner, and its deadline are visible to the entire team in a single shared location that requires no effort to maintain.

**Evidence:**
- [E-001] User interview 01 (Maria), 1st-hand declared, 2026-02-10 → Tasks assigned in Slack DMs and group messages, no shared persistent record. Two designers worked on the same icon set because the assignment was made in separate conversations.
- [E-002] User interview 03 (Priya), 1st-hand declared, 2026-02-14 → "Each person only knows about 70% of what everyone else is working on. That 30% gap causes problems at least twice a week."
- [E-003] Survey data (N=127), 1st-hand quantitative, 2026-02-05 → 53% of respondents lose or forget tasks at least once per week. 38% experience duplicate work multiple times per month.

---

## 2. Who Is Affected

**Primary:** Team leads and members of small teams (2-8 people) who coordinate shared work without a dedicated project management tool. Typically in creative agencies, freelance collaborations, early-stage startups, and small consulting firms.

**Secondary:** Clients and stakeholders who experience the downstream effects: late deliverables, miscommunication about status, and quality issues from rushed catch-up work.

**Evidence:**
- [E-004] Survey demographics, 1st-hand quantitative, 2026-02-05 → Respondents: team leads (42%), individual contributors (34%), founders (24%). Industries: tech (31%), creative (22%), consulting (18%), marketing (14%).
- [E-005] User interview 02 (James), 1st-hand declared, 2026-02-12 → "The real cost is the awkward conversation with the client when I have to explain why the deliverable is late because of an internal coordination failure."

---

## 3. Success Criteria

| Criterion | Metric | Current Value | Target Value |
|---|---|---|---|
| Task visibility | % of active tasks visible to all team members | ~70% (self-reported, E-002) | 100% |
| Task creation speed | Time to create and assign a task | 2-5 minutes (message + context, E-006) | Under 15 seconds |
| Forgotten tasks | Frequency of forgotten/lost tasks per week | 53% report weekly (E-003) | Under 10% report weekly |
| Coordination overhead | Daily time spent manually checking task status | ~20 min median (E-007) | Under 5 minutes |
| Tool adoption | Consistent usage after 2 weeks | 47% abandon dedicated tools (E-008) | 80% still using after 2 weeks |

**Evidence:**
- [E-006] User interviews 01-03, 1st-hand behavioral, 2026-02 → Observed task assignment via Slack/WhatsApp takes 2-5 minutes including context-switching and searching for the right conversation.
- [E-007] Survey data, 1st-hand quantitative, 2026-02-05 → Median daily coordination time: ~20 minutes. 48% spend 20+ minutes per day.
- [E-008] Survey data, 1st-hand quantitative, 2026-02-05 → 53% of respondents have tried and abandoned a dedicated task management tool.

---

## 4. Root Causes

| Symptom | Root Cause | Evidence |
|---|---|---|
| Tasks are forgotten | Assignments happen inside ephemeral channels (chat, verbal) with no persistent shared record | [E-001] Maria: task buried under 200 messages. [E-002] Priya: decisions live in Slack, nobody logs them. |
| Duplicate work happens | No single source of truth for who is working on what. Each person has partial visibility. | [E-001] Maria: two designers on same icon set. [E-003] 38% report duplicate work monthly. |
| Status is unknown | The only way to know task status is to ask the person directly. No passive visibility mechanism. | [E-005] James: spends 20 min/day manually polling subcontractors via WhatsApp. |
| Tools are abandoned | Existing tools are designed for larger teams. Setup, learning curve, and maintenance overhead exceed perceived value for 2-8 person teams. | [E-008] 53% tried and abandoned. [E-009] Top reason: "too complex for our team size" (58%). |

---

## 5. Current Alternatives

Teams currently cope through a combination of methods, averaging 2.3 simultaneous tools per team:

- **Chat messages (64%):** Tasks assigned in Slack, Teams, or WhatsApp. Fast to create but ephemeral and unsearchable.
- **Personal notes (52%):** Phone notes, Notion, paper. Solves personal tracking but invisible to teammates.
- **Spreadsheets (34%):** Google Sheets with manual columns. Works initially but nobody maintains it after the first week.
- **Dedicated tools (28%):** Trello, Asana, Linear. Tried and abandoned by 53% of users who attempted them.
- **Memory (18%):** No system at all. Relies on recall and verbal check-ins.

None of these alternatives provide shared visibility with near-zero maintenance effort.

**Evidence:**
- [E-003] Survey data, 1st-hand quantitative, 2026-02-05 → Tool usage breakdown and multi-method average.
- [E-010] User interview 03 (Priya), 1st-hand behavioral, 2026-02-14 → Google Sheet "Master Task List" had 8 of 23 tasks with blank status, 5 with overdue dates still marked "In Progress."

---

## 6. Constraints

**Technical:**
- Must work in a browser without installation or downloads. Small teams will not install apps for task tracking. [E-009] Survey: "No account/login requirement" mentioned by 24%; "works without installation" scored high. [E-012] No existing competitor offers a zero-install, no-account solution for this segment.
- Must function without a backend or server. The example implementation should be cloneable and runnable by opening a single HTML file. [E-008] 53% abandoned tools partly due to setup complexity; zero-server removes that barrier entirely.

**Business:**
- Target users will not pay for a task tracking tool at this stage. The solution must be free. [E-009] Survey: "Free" mentioned by 21% as a requirement.
- The solution must work for teams where not everyone is technically skilled. [E-004] Industry spread includes creative, consulting, marketing — not just tech.

**Organizational:**
- Team members may resist adding another tool. Adoption must require less than 2 minutes of onboarding. [E-009] Survey: "Onboarding took too long" cited by 27% who abandoned tools.

**Evidence:**
- [E-009] Survey open-ended responses, 1st-hand qualitative, 2026-02-05 → Coded themes on what would make a tool useful.

---

## 7. Cost of Inaction

**Time cost:** At 20 minutes/day median coordination overhead across a 5-person team, that's approximately 8.3 hours/week spent on manual status checking instead of productive work. Over a year: ~430 hours per team.

**Quality cost:** Duplicate work occurs in 38% of teams multiple times per month. At an estimated 4-8 hours per incident (based on Maria's 8-hour duplicate icon set), this represents 16-64 hours of wasted work per team per year.

**Relationship cost:** Missed deadlines from coordination failures damage client relationships and team trust. James described this as the highest-impact consequence: client-facing failures from internal visibility gaps.

**Compounding cost:** As teams grow from 3 to 5 to 8, informal coordination degrades non-linearly. Survey data shows teams of 4-5 report the highest rate of weekly forgotten tasks (61%), suggesting a critical breakpoint where informal methods fail.

**Evidence:**
- [E-007] Survey: 20 min/day median coordination time.
- [E-003] Survey: 38% duplicate work, 53% weekly forgotten tasks.
- [E-001] Maria: 8 hours lost to duplicate icon set work.
- [E-005] James: client relationship damage from coordination failure.
- [E-011] Survey statistical analysis, 2026-02-05 → Teams of 4-5 report 61% weekly forgotten tasks, highest of any size bracket.

---

## 8. Scope Boundaries

**Out of scope:**
- Project management features (timelines, Gantt charts, sprints, epics). This is a task list, not a project management tool. [E-009] Survey: "Simplicity / minimal features" was the #1 requested attribute (56%). [E-012] Competitor analysis confirms existing PM tools are the reason for abandonment.
- File sharing or document management. Tasks are text entries with owners and dates. [E-008] Feature complexity is the #1 reason tools are abandoned by small teams (58% cite "too complex").
- Real-time collaboration or chat. The tool shows tasks, not conversations. [E-001, E-002, E-005] Communication channels already exist (Slack, WhatsApp, Teams); the gap is visibility, not communication.
- Backend infrastructure, user accounts, or authentication. The example implementation uses localStorage. [E-009] 24% of respondents explicitly want no account requirement.
- Mobile native app. Browser-based only. [E-009] Survey: 22% want mobile web, but 0% mentioned needing a native app.

---

## 9. Assumptions

| Assumption | Risk | Validation Plan | Status |
|---|---|---|---|
| A shared task list with zero setup will be adopted more consistently than tools like Trello/Asana | High | Compare 2-week retention against survey abandonment rates | Unverified |
| Teams of 2-8 are underserved by existing tools (not just under-adopting them) | Medium | Validate with competitor feature analysis | Confirmed (E-009, competitor analysis) |
| localStorage persistence is sufficient for an example implementation | Low | Test data persistence across browser sessions | Unverified |
| Team members will voluntarily check a shared list without notifications | Medium | Observe usage patterns in testing | Unverified |

---

## Evidence Index

| ID | Source | Type | Date | Confidence | Phase |
|---|---|---|---|---|---|
| E-001 | User interview 01 — Maria (research/interviews/user-interview-01.md) | 1st-hand declared + behavioral | 2026-02-10 | High | 1 |
| E-002 | User interview 03 — Priya (research/interviews/user-interview-03.md) | 1st-hand declared + behavioral | 2026-02-14 | High | 1 |
| E-003 | Survey data (research/analytics/usage-data-summary.md) | 1st-hand quantitative | 2026-02-05 | Medium | 1 |
| E-004 | Survey demographics (research/analytics/usage-data-summary.md) | 1st-hand quantitative | 2026-02-05 | Medium | 1 |
| E-005 | User interview 02 — James (research/interviews/user-interview-02.md) | 1st-hand declared | 2026-02-12 | High | 1 |
| E-006 | User interviews 01-03, behavioral observations | 1st-hand behavioral | 2026-02 | High | 1 |
| E-007 | Survey: coordination time (research/analytics/usage-data-summary.md) | 1st-hand quantitative | 2026-02-05 | Medium | 1 |
| E-008 | Survey: tool abandonment (research/analytics/usage-data-summary.md) | 1st-hand quantitative | 2026-02-05 | Medium | 1 |
| E-009 | Survey: open-ended responses (research/analytics/usage-data-summary.md) | 1st-hand qualitative | 2026-02-05 | Medium | 1 |
| E-010 | User interview 03 — Priya, behavioral (research/interviews/user-interview-03.md) | 1st-hand behavioral | 2026-02-14 | High | 1 |
| E-011 | Survey statistical analysis (research/analytics/usage-data-summary.md) | 1st-hand quantitative | 2026-02-05 | Medium | 1 |
| E-012 | Competitor analysis (research/benchmarks/competitor-analysis.md) | Secondary competitive | 2026-02-08 | Medium | 1 |

# Problem Statement — TeamTasks

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-02-15
**Gate 1:** PASS

---

## 1. Gap

Small teams of 2-8 people lack a shared, persistent location for task assignments. Tasks are assigned through communication channels (Slack, WhatsApp, email) where they are buried, forgotten, or duplicated. 53% of people in these teams lose or forget tasks at least once per week [E-003]. The information about who is doing what exists only in fragments — scattered across chat messages, personal notes, and abandoned spreadsheets — creating a persistent visibility gap where each team member knows only about 70% of what everyone else is working on [E-002].

---

## 2. Who Is Affected

**Primary:** Team leads and coordinators in teams of 2-8 people who are responsible for assigning and tracking work. They bear the highest coordination burden, spending a median of 20 minutes per day manually polling team members for status updates [E-005, E-007].

**Secondary:** Individual contributors and subcontractors on these teams, who receive assignments through ephemeral messages and have no shared view of team priorities or dependencies [E-001, E-005].

**Demographics:** Team leads (42%), individual contributors (34%), founders (24%). Industries: tech (31%), creative/design (22%), consulting (18%), marketing (14%). Team sizes: 2-3 (38%), 4-5 (35%), 6-8 (27%) [E-004].

---

## 3. Success Criteria

1. **Task visibility:** All team members can see all tasks, their owners, and their status in a single shared location, eliminating the 30% visibility gap [E-002].
2. **Task creation speed:** Adding a new task takes less than 30 seconds, matching or beating the speed of sending a chat message [E-006, E-009].
3. **Reduced task loss:** Tasks assigned through the tool are not lost or forgotten — they persist until explicitly completed or removed [E-003].
4. **Reduced coordination overhead:** The team lead no longer needs to manually poll each person for status updates [E-005, E-007].
5. **Zero adoption friction:** Team members can start using the tool with no training, no account creation, and no learning curve [E-008, E-009].

---

## 4. Root Causes

### RC-1: Task assignments happen in ephemeral communication channels
Tasks are assigned via Slack DMs, WhatsApp messages, and verbal agreements. These channels are designed for conversation, not persistence. Messages get buried under hundreds of subsequent messages within days [E-001, E-005, E-006].

### RC-2: No shared, persistent task registry exists
Personal tracking methods (phone notes, Notion pages, mental lists) are private by design. The person who assigns the task has a record; the person doing the work may not. This creates information asymmetry [E-001, E-005, E-010].

### RC-3: Existing tools are disproportionately complex for small teams
53% of respondents have tried and abandoned a dedicated task management tool. The primary reason (58%) is that the tool was too complex for their team size. These tools assume organizational maturity (sprints, boards, workflows) that teams of 2-8 people do not have [E-008, E-012].

### RC-4: Maintenance burden exceeds perceived value
DIY solutions (Google Sheets, Notion tables) require deliberate effort to maintain. When maintaining the tracking system feels harder than the informal coordination it replaces, the system is abandoned. Priya's Google Sheet had 8 tasks with blank status and 5 with overdue dates still marked "In Progress" [E-010, E-008].

---

## 5. Current Alternatives

| Alternative | How it works | Why it fails |
|---|---|---|
| Chat messages (Slack, WhatsApp) | Tasks assigned inline in conversations | Messages buried within hours. No persistence, no status tracking, no shared view [E-001, E-005, E-006] |
| Personal notes (phone, Notion) | Team lead tracks tasks privately | Creates information asymmetry. Team members can't see their own assignments [E-001, E-005] |
| Google Sheets / Notion DIY | Shared spreadsheet with columns for task, owner, status, date | Requires manual discipline. Abandoned within weeks when maintenance burden exceeds value [E-010, E-008] |
| Dedicated tools (Trello, Asana, Linear) | Full project management platforms | Too complex for teams of 2-8. 58% abandoned for being too complex for team size. 49% had inconsistent team adoption [E-008, E-012] |
| Todoist | Personal task management with team features | Designed for personal use. Team visibility is a paid afterthought [E-012] |
| Memory / verbal agreements | "I'll handle it" said in a meeting or call | No persistence, no accountability, no visibility. "That's not a commitment, that's a hope" [E-002, E-010] |

---

## 6. Constraints

### C-1: Zero setup requirement
Team members must be able to use the tool without creating accounts, downloading apps, or completing onboarding. 24% of respondents explicitly requested no account/login requirement [E-009]. 27% of tool abandoners cited onboarding length as a factor [E-008].

### C-2: Extreme simplicity
The tool must be simpler than the alternatives it replaces. If it takes more than 3 clicks to add a task, the target users will not adopt it [E-009, E-008]. 56% of respondents listed simplicity/minimal features as the most important quality [E-009].

### C-3: Free
The tool must be free for small teams. 31% of tool abandoners cited limited free tiers as a factor. 21% of respondents listed "free" as a key requirement [E-008, E-009].

### C-4: Works on mobile web
22% of respondents need mobile access without installing an app [E-009]. The tool must be responsive and functional on mobile browsers.

---

## 7. Cost of Inaction

**Quantitative:**
- 53% of small teams lose tasks weekly [E-003]. For a team of 4-5, this means at least one forgotten task per week.
- Median 20 minutes per day spent on manual coordination [E-007]. Over a 5-person team, this is ~8 hours per week of coordination overhead.
- 38% experience duplicate work multiple times per month [E-003]. Maria's team lost 8 hours to a single duplicate work incident [E-001].

**Qualitative:**
- Client-facing deadline misses due to internal coordination failures [E-005].
- Erosion of accountability: "There's no task — there's a message from Tuesday that said 'let's try to get this done by Friday'" [E-002].
- Teams that grow past 3 people hit a coordination ceiling that pushes them toward tools designed for 50-person companies, creating a lose-lose: either suffer the coordination pain or suffer the tool complexity [E-011, E-012].

---

## 8. Scope Boundaries

**In scope:**
- Shared task visibility for teams of 2-8 people
- Task creation, assignment, status tracking, and completion
- Simple team member management (names only — not user accounts)

**Out of scope:**
- Project management features (Gantt charts, sprints, workflows, dependencies)
- Integrations with other tools (Slack, email, calendar)
- Notifications or alerts
- Analytics or reporting
- User accounts, authentication, or access control
- Multi-team or organization-level features
- File attachments or rich media

---

## 9. Assumptions

| ID | Assumption | Risk if wrong |
|---|---|---|
| A-1 | Teams of 2-8 prefer a tool that does less but is instantly usable over a full-featured tool that requires setup | The tool may be too limited for teams that need more structure, limiting adoption to the smallest teams |
| A-2 | A shared task list without notifications is valuable enough — teams will check it proactively | Without notifications, the tool may be abandoned like the Google Sheets it replaces |
| A-3 | Team members are willing to use a browser-based tool (no native app needed) | Some teams may require native mobile apps for consistent adoption |
| A-4 | Text-only task descriptions are sufficient — no need for file attachments, subtasks, or rich formatting | Teams with complex task requirements may find the tool too limited |
| A-5 | The survey sample (self-selected from indie/freelancer communities) represents the broader small-team population | Results may skew toward tech-aware teams; traditional small businesses may have different needs [E-003 methodology note] |

---

## Evidence Index

| ID | Source | Type | Date | Confidence | Key Claims |
|---|---|---|---|---|---|
| E-001 | User interview 01 — Maria, team lead at 6-person design agency | 1st-hand declared + behavioral | 2026-02-10 | High | Tasks assigned in Slack DMs get buried. 8 hours wasted on duplicate icon work. Only 32% of trial signups create tasks in a shared location. |
| E-002 | User interview 03 — Priya, co-founder of 4-person startup | 1st-hand declared + behavioral | 2026-02-14 | High | 70% visibility, 30% gap. Duplicate work and missed commitments twice weekly. |
| E-003 | Online survey — small team task management (N=127) | 1st-hand quantitative | 2026-02-05 | Medium | 53% lose tasks weekly. 38% experience duplicate work monthly. Average 2.3 tracking methods. |
| E-004 | Online survey — demographics section (N=127) | 1st-hand quantitative | 2026-02-05 | Medium | Team leads 42%, ICs 34%, founders 24%. Tech 31%, creative 22%, consulting 18%. |
| E-005 | User interview 02 — James, freelance developer | 1st-hand declared + behavioral | 2026-02-12 | High | 20 min/day polling for updates. Missed dependency caused client deadline miss. |
| E-006 | Behavioral observations across interviews 01-03 | 1st-hand behavioral | 2026-02 | High | 90 seconds to find task in Slack. 2+ minutes in WhatsApp. 3 minutes to determine task completion status. |
| E-007 | Online survey — coordination time (N=127) | 1st-hand quantitative | 2026-02-05 | Medium | Median 20 min/day on coordination. 48% spend 20+ minutes. |
| E-008 | Online survey — tool abandonment (N=67) | 1st-hand quantitative | 2026-02-05 | Medium | 53% tried and abandoned tools. Too complex (58%), inconsistent adoption (49%), overhead (44%). |
| E-009 | Online survey — open-ended coded responses | 1st-hand qualitative | 2026-02-05 | Medium | Simplicity 56%, shared visibility 50%, fast creation 38%, no login 24%, mobile 22%, free 21%. |
| E-010 | User interview 03 — Priya, behavioral observation | 1st-hand behavioral | 2026-02-14 | High | Google Sheet with 23 rows: 8 blank status, 5 overdue. Last updated 3 weeks ago. |
| E-011 | Online survey — statistical analysis (N=127) | 1st-hand quantitative | 2026-02-05 | Medium | Teams of 4-5 have highest forgotten task rate (61%). 3+ methods correlates with higher task loss (r=0.42). |
| E-012 | Competitor analysis — 5 tools evaluated | Secondary competitive | 2026-02-08 | Medium | No tool designed for 2-8 person teams with shared visibility and near-zero setup. Market gap identified. |

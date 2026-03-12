# Context Specification — TeamTasks

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-03-12
**Solution Brief:** docs/pda-solution-brief.md (v2.0)
**Problem Statement:** docs/pda-problem.md (v1.0)

This document contains all technical decisions for the TeamTasks implementation. It is generated during Phase 3 (Context) from the Solution Brief and Problem Statement. Product decisions remain in the Solution Brief; this document translates them into buildable specifications.

---

## 1. Stack

| Layer | Choice | Justification |
|---|---|---|
| Markup | HTML5 | Universal browser support. No compilation needed. |
| Styling | Vanilla CSS | Zero-dependency constraint (SB §7). No framework, no preprocessor. Keeps codebase readable for non-technical inspection (E-004). |
| Logic | Vanilla JavaScript (ES6+) | Zero-dependency constraint. No build step, no bundler, no transpiler. Single file deliverable. |
| Persistence | localStorage | PS technical constraint: must work without backend. SB A-002: sufficient for single-device/single-browser example. |
| External dependencies | None | SB Decision Matrix: zero setup/dependencies weighted at 35%. Any dependency adds adoption friction that contradicts the core thesis (E-008: 53% abandoned tools due to complexity). |

---

## 2. Architecture

### File Structure

```
index.html      — Main application (HTML + CSS + JS embedded)
style.css       — Extracted styles (optional separation for readability)
app.js          — Extracted logic (optional separation for readability)
```

Three files maximum. The application must also work as a single `index.html` with everything embedded. File separation is for development readability, not a build requirement.

### State Management

- **In-memory state:** Two JavaScript arrays (`members`, `tasks`) serve as the source of truth during a session.
- **Persistence cycle:** Every mutation → update in-memory array → `save()` to localStorage → `render()` full UI.
- **Full re-render:** No virtual DOM, no diffing. Full re-render on every state change. Acceptable for data volumes of 2-8 person teams (<200 tasks).
- **No routing:** Single-page, single-view. No URL routing. No history API.
- **Dialogs:** Native `<dialog>` element for any modal interactions (edit task, confirmations). No custom modal library.

### Initialization

1. `DOMContentLoaded` fires.
2. `load()` reads localStorage, parses JSON, populates in-memory arrays. Handles missing/corrupt data gracefully (defaults to `[]`).
3. `render()` draws the full UI from in-memory state.

---

## 3. Data Model

### Team Member

```json
{
  "id": "string (generated, unique)",
  "name": "string (1-50 characters, trimmed, required)"
}
```

- **Storage key:** `teamtasks_members`
- **Storage format:** JSON array
- **Limits:** Maximum 20 members (sufficient for target team size 2-8, with margin)

### Task

```json
{
  "id": "string (generated, unique)",
  "title": "string (1-200 characters, trimmed, required)",
  "assignedTo": "string (must match an existing member name, required)",
  "dueDate": "string (ISO 8601 date: YYYY-MM-DD, required)",
  "status": "string (enum: 'todo' | 'done')",
  "createdAt": "string (ISO 8601 datetime)"
}
```

- **Storage key:** `teamtasks_tasks`
- **Storage format:** JSON array
- **Limits:** Maximum 500 tasks (localStorage ~5MB budget; each task ~200 bytes = ~100KB for 500 tasks, well within limits)

### ID Generation

`Date.now().toString(36) + Math.random().toString(36).substr(2)` — unique enough for single-browser, non-concurrent usage. No external library.

---

## 4. Interaction Decisions

### Task Status Toggle
- Click/tap on a task row toggles between `todo` and `done`.
- No intermediate states (no "in progress"). SB §3: task list only, not PM tool.

### Task Reordering (Drag-and-Drop)
- **Primary:** Native HTML Drag and Drop API (`draggable`, `dragstart`, `dragover`, `drop` events).
- **Fallback for mobile/touch:** Click-based "move up / move down" controls visible on touch devices. HTML DnD API has inconsistent mobile support.
- **Scope:** Reorder within the task list only. No cross-list dragging.

### Task Editing
- Click an edit affordance (icon or button) on a task to open a native `<dialog>` with pre-filled form fields.
- Same three fields as creation: title, assignee, due date.
- Save updates the in-memory array → `save()` → `render()`.

### Task Deletion
- Available via the edit dialog or a dedicated control.
- No confirmation dialog for deletion (lightweight tool, undo is not in scope for V1).

### Team Member Removal
- Removing a member does not delete their assigned tasks. Tasks remain with the original assignee name.
- The assignee dropdown no longer includes the removed name for new tasks.

---

## 5. Visual Design Decisions

### CSS Architecture
- **CSS Custom Properties (variables)** for all colors, spacing, and radii. Defined in `:root`. Enables easy theming and consistent values.
- **CSS Grid** for the main layout. Flexbox for inline elements (form rows, filter bar, member tags).
- **No CSS framework.** No utility classes. Semantic class names.

### Responsive Breakpoint
- **768px** single breakpoint. Above: multi-column or wider layout. Below: stacked single-column.
- Mobile-first approach: base styles are mobile, `@media (min-width: 768px)` adds desktop enhancements.

### Color by Column / Status
- **Default task:** Neutral background (white/light gray).
- **Overdue task (todo + past due date):** Red-tinted background + left border in red. Must be visible without reading the date (SB §6: overdue noticeability).
- **Done task:** Muted opacity + strikethrough title. Visually recedes.
- **Filter active state:** Primary color background on active filter button.

### Typography
- System font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.
- No web fonts. Zero network requests.

---

## 6. Accessibility

### Semantic HTML
- `<header>`, `<main>`, `<section>`, `<form>`, `<button>`, `<table>` or `<ul>` for task list.
- `<dialog>` for modals (native focus trapping).
- `<label>` elements associated with all form inputs via `for` attribute.

### ARIA
- `aria-label` on icon-only buttons (remove member, toggle task).
- `aria-live="polite"` on the task list container to announce changes to screen readers.
- `role="status"` on empty-state messages.

### Focus Management
- When a `<dialog>` opens, focus moves to the first input.
- When a `<dialog>` closes, focus returns to the trigger element.
- All interactive elements reachable via Tab key.

### Target Compliance
- **WCAG 2.1 AA** as the baseline. Specifically:
  - Color contrast ratio ≥ 4.5:1 for text, ≥ 3:1 for large text and UI components.
  - Touch targets ≥ 44×44px on mobile.
  - No information conveyed by color alone (overdue uses color + border).

---

## 7. Export / Import

### Export
- "Export" button generates a JSON file containing `{ members: [...], tasks: [...], exportedAt: "ISO datetime" }`.
- Uses `Blob` + `URL.createObjectURL` + programmatic `<a>` click for download. No server needed.
- Filename: `teamtasks-export-YYYY-MM-DD.json`.

### Import
- "Import" button opens a file picker (hidden `<input type="file" accept=".json">`).
- Uses `FileReader` to read the file contents.
- **Validation:** Checks that the file contains valid JSON with `members` (array) and `tasks` (array) keys. Each member must have `id` and `name`. Each task must have `id`, `title`, `assignedTo`, `dueDate`, `status`, `createdAt`.
- **On valid import:** Replaces current state entirely (members + tasks). Calls `save()` + `render()`.
- **On invalid import:** Shows an error message. Does not modify current state.

---

## 8. Error Handling

### localStorage Full
- Wrap `localStorage.setItem` in a try/catch.
- If `QuotaExceededError` is caught, show a visible warning: "Storage is full. Some changes may not be saved. Consider exporting your data and clearing old tasks."
- Do not crash. In-memory state remains valid for the current session.

### Input Validation
- **Member name:** Trim whitespace. Reject empty. Reject duplicates (case-insensitive). Max 50 characters.
- **Task title:** Trim whitespace. Reject empty. Max 200 characters.
- **Assignee:** Must match an existing member. If the select is empty (no members), disable the task form.
- **Due date:** Must be a valid date. No past-date restriction (users may log tasks after the fact).

### Empty States
- **No members:** Show message in team panel: "Add your first team member to get started."
- **No tasks:** Show message in task list: "No tasks yet. Create one above."
- **No tasks matching filter:** Show message: "No tasks for [name]."
- **Empty states are not errors.** They guide the user to the next action.

### Corrupt localStorage
- If `JSON.parse` fails on load, default to empty arrays `[]`. Do not show an error. The user starts fresh.

---

> **Conflict resolution:** If any decision in this Context Specification conflicts with the Solution Brief (`docs/pda-solution-brief.md`), the Solution Brief prevails. The Solution Brief captures human product decisions; this document translates them into technical specifications.

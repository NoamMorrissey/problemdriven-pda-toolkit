# Context Specification — TeamTasks

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-02-17
**Solution Brief:** docs/pda-solution-brief.md (v1.0)
**Problem Statement:** docs/pda-problem.md (v1.0)
**Gate 3:** PASS

---

## HARD CONSTRAINTS

**These constraints are absolute and non-negotiable. Every technical decision in this document operates within them. If any requirement from the Solution Brief seems to need infrastructure beyond these constraints, the requirement is descoped — the constraints are not relaxed.**

- **Three files only:** `index.html`, `style.css`, `app.js`. Nothing else.
- **Storage:** localStorage ONLY. No server, no database, no API, no network requests.
- **Dependencies:** ZERO. No npm, no CDN, no frameworks, no libraries. Vanilla HTML, CSS, and JavaScript only.
- **No accounts, no login, no authentication, no sessions.**
- **No sync between browsers or devices.**

---

## 1. Stack

| Layer | Choice | Justification |
|---|---|---|
| Markup | HTML5 (single file: `index.html`) | SB §7 BC-C1: no server. A static HTML file can be opened directly in a browser with zero setup [PS §6 C-1]. |
| Styling | CSS3 (single file: `style.css`) | SB §7 OC-1: no external dependencies. Custom properties for theming, no preprocessor needed. |
| Logic | Vanilla JavaScript ES6+ (single file: `app.js`) | SB §7 BC-C1: no server, no build step. Modern browsers support ES6+ natively. No framework means zero learning curve for maintenance. |
| Persistence | `localStorage` | SB §7 BC-C1: no server. localStorage persists across browser sessions without any backend. Limit: ~5MB, more than sufficient for task data. |
| ID generation | `crypto.randomUUID()` | Native browser API. No library needed. Supported in all modern browsers. |

**Rejected alternatives:**

| Layer | Rejected | Why |
|---|---|---|
| Logic | React, Vue, Svelte | SB §7 OC-1: no external dependencies. Frameworks require build tools, npm, and CDN loads — all violate the zero-dependency hard constraint. |
| Logic | TypeScript | Requires a build step (tsc). Violates the three-files-only constraint. |
| Persistence | IndexedDB | Overly complex for flat task data. localStorage's key-value API is sufficient for the data volumes involved (<1000 tasks). |
| Persistence | SQLite (WASM) | External dependency. Violates zero-dependency constraint. |
| Persistence | Server-side database | SB §7 BC-C1: no server. |
| Styling | Tailwind, Bootstrap | External dependencies. Violates zero-dependency constraint. |

---

## 2. Architecture

### File Structure

```
index.html    ← Markup + structure. Inline <link> to style.css and <script> to app.js.
style.css     ← All styles. CSS custom properties for design tokens.
app.js        ← All logic. State management, DOM manipulation, localStorage, event handlers.
```

No other files. No folders. No assets. No build artifacts.

### State Management

- **In-memory state:** A single JavaScript object (`appState`) holds the current state: team members array, tasks array, and UI state (current filter, modal state).
- **Persistence cycle:** On every mutation (add, edit, delete, reorder), the full state is serialized to `localStorage` as a JSON string under a single key (`teamtasks-data`).
- **Load cycle:** On page load, read from `localStorage`, parse JSON, populate `appState`. If no data exists, initialize with empty arrays.
- **No partial updates:** The entire state is written and read as a single unit. This is simpler than managing individual keys and the data volume (<100KB for 500 tasks) makes it performant.

### Rendering

- **Full re-render on mutation:** When state changes, re-render the affected section of the DOM. Use `innerHTML` for list rendering and direct DOM manipulation for single-element updates.
- **No virtual DOM:** Not needed. The maximum expected data volume (~200 tasks) produces a DOM size that browsers handle without performance issues with direct manipulation.
- **Template approach:** JavaScript template literals for generating HTML strings. No external templating engine.

### Navigation

- **No routing.** The application is a single view. There are no pages, no URL changes, no browser history manipulation.
- **Modal dialogs** for task creation/editing overlay the main view using the native `<dialog>` element.

---

## 3. Data Model

### Team Member

```json
{
  "id": "string (UUID, required)",
  "name": "string (required, 1-50 characters, trimmed)"
}
```

- **Storage:** Part of the main `teamtasks-data` localStorage key.
- **Limits:** Maximum 20 team members (SB targets teams of 2-8; 20 provides generous headroom without UI clutter).

### Task

```json
{
  "id": "string (UUID, required)",
  "title": "string (required, 1-200 characters, trimmed)",
  "assigneeId": "string (UUID, required — references a Team Member)",
  "dueDate": "string (ISO 8601 date, YYYY-MM-DD, optional — null if not set)",
  "status": "string (enum: 'todo' | 'in-progress' | 'done', required, default: 'todo')",
  "createdAt": "string (ISO 8601 datetime, required)",
  "position": "number (integer, required — used for drag-and-drop ordering within status column)"
}
```

- **Storage:** Part of the main `teamtasks-data` localStorage key.
- **Limits:** Maximum 500 tasks. Beyond this, the UI becomes unwieldy and localStorage approaches its limit. Display a warning at 450 tasks.

### Full Storage Schema

```json
{
  "version": 1,
  "members": [{ "id": "...", "name": "..." }],
  "tasks": [{ "id": "...", "title": "...", "assigneeId": "...", "dueDate": "...", "status": "...", "createdAt": "...", "position": 0 }]
}
```

- **Storage key:** `teamtasks-data`
- **Storage format:** JSON string via `JSON.stringify()` / `JSON.parse()`
- **Version field:** Enables future schema migrations without breaking existing data.

### ID Generation

Use `crypto.randomUUID()`. This is a native browser API that generates RFC 4122 v4 UUIDs. No library required. Supported in all modern browsers (Chrome 92+, Firefox 95+, Safari 15.4+).

---

## 4. Interaction Decisions

### Drag-and-Drop Task Reordering

- **Primary approach:** Native HTML Drag and Drop API (`draggable`, `dragstart`, `dragover`, `drop` events). Tasks can be reordered within a status column and moved between status columns by dragging.
- **Mobile fallback:** On touch devices, drag-and-drop is unreliable. Provide click-based controls: a "Move to" dropdown or status buttons on each task card to change status. Reordering on mobile uses up/down arrow buttons.
- **Scope:** Drag-and-drop applies only to task cards. Team member list is not reorderable.

### Task Creation / Editing

- **Pattern:** Native `<dialog>` element for the creation/edit form. Opens as a modal overlay.
- **Fields:** Task title (text input, required), Assignee (select dropdown populated from team members, required), Due date (date input, optional).
- **Submit:** Single "Save" button. On success, dialog closes and task board re-renders.
- **Edit:** Same dialog, pre-populated with existing values. Triggered by clicking an edit button on the task card.

### Task Deletion

- **Pattern:** Confirm before deleting. Use native `confirm()` dialog.
- **Scope:** Individual task deletion only. No bulk delete.

### Team Member Management

- **Add:** Text input with "Add" button. Name is trimmed and validated (1-50 characters, no duplicates).
- **Remove:** Only allowed if the member has no assigned tasks. If they have tasks, show a message explaining why removal is blocked.
- **Edit:** Click to edit name inline.

### Filtering

- **By assignee:** Dropdown filter to show tasks for a specific team member or all members.
- **By status:** The board is already organized by status columns, providing visual filtering by default.

---

## 5. Visual Design Decisions

### CSS Architecture

- **Methodology:** CSS custom properties (variables) for all design tokens (colors, spacing, typography, shadows). No BEM, no utility classes — simple, scoped selectors.
- **Token categories:**
  - `--color-*` for all colors (background, text, borders, status indicators)
  - `--spacing-*` for margin/padding scale (4px base unit: 4, 8, 12, 16, 24, 32, 48)
  - `--radius-*` for border-radius values
  - `--shadow-*` for box shadows
  - `--font-*` for font families and sizes

### Responsive Strategy

- **Approach:** Mobile-first. Base styles target phone screens (320px+).
- **Breakpoints:**
  - `640px` — Tablet: task columns display side by side (2 columns)
  - `1024px` — Desktop: all three status columns visible simultaneously
- **Mobile layout:** Status columns stack vertically. Each column is collapsible with a tap to expand/collapse.

### Visual States

| State | Visual Treatment |
|---|---|
| Default task | White card with light border, assignee name, due date |
| Overdue task | Red left border (4px), due date text in red, overdue badge. Visually distinct without reading the date [SB §SC-6]. |
| Done task | Reduced opacity (0.7), strikethrough title, muted colors |
| Dragging task | Elevated shadow, slight rotation (2deg), reduced opacity on original position |
| Empty column | Light gray background with prompt text ("No tasks yet — drag one here or create a new task") |
| Empty board (no tasks at all) | Centered illustration placeholder with "Create your first task" call to action |

### Typography

- **Font stack:** System fonts only. `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`.
- **Rationale:** Zero external dependencies (no Google Fonts CDN). System fonts load instantly and match the OS aesthetic.
- **Scale:** 14px base, 16px for task titles, 20px for column headers, 24px for app title.

---

## 6. Accessibility

### Semantic HTML

- `<main>` for the task board area
- `<header>` for the app title and team management
- `<section>` for each status column, with `<h2>` headings ("To Do", "In Progress", "Done")
- `<article>` for each task card
- `<dialog>` for modal forms (task creation/editing)
- `<button>` for all clickable actions (never `<div onclick>`)
- `<form>` for task creation/editing with proper `<label>` elements

### ARIA

- `aria-live="polite"` on the task board container to announce changes (task added, moved, deleted)
- `aria-label` on icon-only buttons (delete, edit, drag handle)
- `role="status"` on task count displays
- `aria-describedby` linking task cards to their due date status (overdue warning)

### Focus Management

- When a dialog opens, focus moves to the first form field
- When a dialog closes, focus returns to the element that triggered it
- After task deletion, focus moves to the next task card (or the column heading if the last task was deleted)
- Tab order follows visual layout: header → team members → task board (left to right, top to bottom)

### Target Compliance

- **WCAG 2.1 AA**
- Color contrast ratio: minimum 4.5:1 for normal text, 3:1 for large text
- Touch targets: minimum 44x44px
- Overdue state must be distinguishable without color alone (uses border + badge + text, not just red color)
- All functionality available via keyboard

---

## 7. Error Handling

### Storage Errors

- **Trigger:** localStorage is full, disabled, or in private browsing mode
- **Behavior:** Catch the error on write. Display a persistent banner at the top: "Unable to save. Your browser storage may be full or disabled. Changes will be lost when you close this tab."
- **No silent failure:** If data cannot be saved, the user must know immediately.

### Validation Errors

- **Task title empty:** Prevent form submission. Show inline error "Task title is required" below the input field.
- **No assignee selected:** Prevent form submission. Show inline error "Please select a team member."
- **Team member name empty or duplicate:** Prevent add. Show inline error below the input.
- **Team member name too long (>50 chars):** Truncate input with maxlength attribute.
- **Task title too long (>200 chars):** Truncate input with maxlength attribute.

### Empty States

| Context | Display |
|---|---|
| No team members yet | "Add your team members to get started" with the add-member input prominently displayed |
| No tasks yet (but members exist) | "Create your first task" with a visible create-task button |
| No tasks in a specific column | "No [status] tasks" in light gray text |
| Filter shows no results | "No tasks for [member name]" with a "Show all" link |

### Data Corruption / Invalid State

- **On load:** Wrap `JSON.parse()` in try/catch. If parsing fails, show: "Your saved data appears to be corrupted. You can start fresh or try importing a backup."
- **Offer two options:** "Start Fresh" (clear localStorage) or "Export Raw Data" (download the raw string for manual recovery).
- **Schema validation:** On load, verify that the data object has the expected shape (version, members array, tasks array). If fields are missing, attempt to repair with defaults rather than discarding everything.

---

## 8. Data Export and Import

### Export

- **Format:** JSON file matching the storage schema.
- **Filename:** `teamtasks-backup-YYYY-MM-DD.json`
- **Mechanism:** Create a Blob, generate an object URL, trigger download via a temporary `<a>` element with `download` attribute.
- **Location:** Export button in the app header or settings area.

### Import

- **Mechanism:** File input (`<input type="file" accept=".json">`).
- **Validation:** Parse the file, verify it matches the expected schema (version, members, tasks). If invalid, show an error and do not import.
- **Behavior:** Import replaces all current data (after confirmation: "This will replace all current data. Continue?").
- **No merge:** Import is a full replacement, not a merge. This keeps the logic simple and predictable.

---

## 9. What Is NOT Decided Here

This Context Specification covers **technical implementation decisions only**. The following remain in the Solution Brief and are not duplicated here:

- Product scope and feature boundaries
- Business components and their traceability to the Problem Statement
- Success criteria and metrics
- Business and organizational constraints
- Actor map and user roles
- Assumptions and risks

> **Conflict resolution:** If any decision in this Context Specification conflicts with the Solution Brief, the Solution Brief prevails on product decisions. However, the hard constraints at the top of this document are non-negotiable on technical decisions. If a product decision from the SB requires infrastructure that violates the hard constraints (e.g., cross-device sync would require a server), the product decision is descoped — the technical constraints are not relaxed. When in doubt, ask the human.

> **Final authority:** If any requirement from the Solution Brief seems to need infrastructure beyond these constraints, the requirement is descoped — the constraints are not relaxed.

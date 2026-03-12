# Context Specification — [Project Name]

**Status:** DRAFT
**Version:** 0.1
**Last updated:** [YYYY-MM-DD]
**Solution Brief:** docs/pda-solution-brief.md (v[X.X])
**Problem Statement:** docs/pda-problem.md (v[X.X])

## Prerequisites

- [ ] Problem Statement approved (Gate 1 PASS)
- [ ] Solution Brief approved (Gate 2 PASS)

This document is generated during **Phase 3 (Context)**. It translates product decisions from the Solution Brief into technical specifications that an AI agent can build from without inventing. Do not write this document until both gates have passed.

---

## 1. Stack

[What technology stack will be used and why. List every layer (markup, styling, logic, persistence, external services) with the specific choice and its justification traced to Solution Brief constraints or Problem Statement evidence. Include what was explicitly rejected and why — this prevents the AI from revisiting decided questions.]

| Layer | Choice | Justification |
|---|---|---|
| [Layer name] | [Technology] | [Why this choice, referencing SB constraint or PS evidence] |

**Rejected alternatives:**

| Layer | Rejected | Why |
|---|---|---|
| [Layer name] | [Technology] | [Why rejected, referencing SB constraint or PS evidence] |

---

## 2. Architecture

[How the application is structured: file organization, state management approach, rendering strategy, and navigation model. Every decision here must be buildable without ambiguity — if the AI needs to choose between two approaches, this section hasn't done its job.]

### File Structure

```
[List every file or directory the AI will create. Be explicit — "the AI will figure out the structure" is not acceptable here.]
```

### State Management

[How data flows through the application: where state lives in memory, how mutations happen, how the UI stays in sync. Include the persistence cycle if applicable.]

### Rendering

[How the UI updates: framework reactivity, manual re-render, server-side, etc. Include the rationale for the approach given the expected data volumes.]

### Navigation

[Routing model: single-page, multi-page, no routing. If single-page, how views change. If no routing, say so explicitly.]

---

## 3. Data Model

[Complete schema for every data object the application manages. Include field names, types, constraints, and storage details. The AI should be able to write the data layer directly from this section without guessing any field names or types.]

### [Entity Name]

```json
{
  "field": "type (constraints, required/optional)"
}
```

- **Storage key/table:** [Where this entity is persisted]
- **Storage format:** [Serialization format]
- **Limits:** [Maximum records, size constraints, and rationale]

### ID Generation

[How unique IDs are created. Specify the algorithm or library.]

---

## 4. Interaction Decisions

[Key UI interaction patterns that the AI must implement in a specific way. Focus on decisions where multiple valid approaches exist and the team has chosen one. Without this section, the AI will pick its own interaction patterns.]

### [Interaction Pattern Name]

- **Primary approach:** [The chosen implementation]
- **Fallback:** [Alternative for contexts where primary doesn't work, e.g., mobile/touch]
- **Scope:** [Boundaries of this interaction]

---

## 5. Visual Design Decisions

[The visual system the AI must follow. Not a full design spec — just the architectural decisions that affect how CSS is written and organized.]

### CSS Architecture

[Methodology: custom properties, BEM, utility classes, CSS modules, etc. How colors, spacing, and typography are systematized.]

### Responsive Strategy

[Breakpoints, approach (mobile-first vs desktop-first), and what changes at each breakpoint.]

### Visual States

[How different data states appear: default, active, error, disabled, empty. Especially important for states where visual differentiation is a success criterion (e.g., overdue items must be visible without reading text).]

### Typography

[Font stack, loading strategy (system fonts vs web fonts), and rationale.]

---

## 6. Accessibility

[Technical accessibility requirements. These are implementation constraints, not aspirational goals — the AI must build to these specifications.]

### Semantic HTML

[Which HTML elements are required for which UI components. Be specific: "use `<dialog>` for modals" not "use semantic HTML."]

### ARIA

[Required ARIA attributes and where they apply. Include `aria-live` regions, `aria-label` for icon-only controls, and role attributes.]

### Focus Management

[How focus moves: dialog open/close, after destructive actions, keyboard navigation order.]

### Target Compliance

[WCAG level (e.g., 2.1 AA). Specific requirements: contrast ratios, touch target sizes, color-independence.]

---

## 7. Error Handling

[How the application handles errors and edge cases. The AI must implement these patterns, not invent its own.]

### [Error Category]

- **Trigger:** [What causes this error]
- **Behavior:** [What the application does]
- **User communication:** [What the user sees]

### Empty States

[How the application handles zero-data scenarios for each view. Empty states are not errors — they are guidance toward the next user action.]

### Data Corruption / Invalid State

[What happens when persisted data is corrupt or doesn't match the expected schema.]

---

## 8. What Is NOT Decided Here

This Context Specification covers **technical implementation decisions only**. The following remain in the Solution Brief and are not duplicated here:

- Product scope and feature boundaries
- Business components and their traceability to the Problem Statement
- Success criteria and metrics
- Business and organizational constraints
- Actor map and user roles
- Assumptions and risks

> **Conflict resolution:** If any decision in this Context Specification conflicts with the Solution Brief (`docs/pda-solution-brief.md`), the Solution Brief prevails. The Solution Brief captures human product decisions; this document translates them into technical specifications.

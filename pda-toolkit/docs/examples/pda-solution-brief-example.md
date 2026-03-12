# Solution Brief — SaaS Onboarding Optimization

> **This is an example.** It shows a completed Solution Brief ready for Gate 2.
> To start your own project, replace this file with a copy of `docs/templates/pda-solution-brief.template.md`.
>
> **Esto es un ejemplo.** Muestra una Solution Brief completada y lista para Gate 2.
> Para empezar tu propio proyecto, reemplaza este archivo con una copia de `docs/templates/pda-solution-brief.template.md`.

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-03-05
**Approved by:** VP Product, Head of CS, CTO
**Problem Statement:** docs/pda-problem.md (v1.0)

---

## 1. Solution Summary

An interactive onboarding wizard that guides new trial users from signup to their first productive moment (project created + teammate invited + task completed) through a step-by-step experience with pre-built templates. Reduces median time-to-first-project from 22 minutes to under 8 minutes.

**gap_ref:** PS element 1 (68% of trial users never create a first project)
**success_ref:** PS element 3 (activation rate 32% → 55%, time to first project 22 → 8 min)

---

## 2. Proposed Solution

A 4-step interactive wizard embedded in the main application on first login:

1. **Welcome + goal selection:** User selects primary use case (software dev, marketing, operations, other). Personalizes template in step 2.
2. **Template project creation:** Pre-populated project with sample tasks and structure. Project creation goes from 7 fields to 2 (name + template).
3. **Team invitation:** Inline teammate invitation. Preview of collaboration with sample project.
4. **First task completion:** Prompt to complete/modify a sample task, demonstrating core interaction.

Post-completion: populated project dashboard with contextual tips overlay (dismissible).

---

## 3. Key Decisions

| Decision | Options Considered | Chosen | Rationale |
|---|---|---|---|
| Wizard vs. checklist | Interactive wizard, progressive checklist, video walkthrough | Interactive wizard | Session recordings show users need hand-holding. Wizard ensures linear completion. |
| Template vs. blank | Pre-built templates, blank with hints, AI-generated | Pre-built templates | Lowest technical risk. Validates core hypothesis before AI investment. |
| V1 scope | Full redesign, wizard only, wizard + email drip | Wizard only | 1 engineer + 1 designer constraint. Wizard covers critical path. |

---

## 4. Solution Dimensions

### Business

| Component | Description | gap_ref | success_ref | Priority |
|---|---|---|---|---|
| Wizard engine | Step navigation, progress tracking, state persistence | PS-1 (empty dashboard) | Activation rate, time to first project | Must |
| Template system | 4 pre-built project templates (one per use case) | PS-1 (7-field creation) | Time to first project | Must |
| Team invitation flow | Inline email invitation in wizard step 3 | PS-1 (buried invitation) | Team invitation rate | Must |
| Contextual tips | Post-wizard overlay for key features | PS-1 (don't know where to start) | Activation rate | Should |
| Analytics tracking | Events for each wizard step + completion + drop-off | PS-3 (measuring success) | All criteria | Must |

### Architecture

- **Frontend:** React components within existing app. Wizard as modal overlay.
- **Backend:** Node.js API for template CRUD and wizard state persistence.
- **Database:** Existing PostgreSQL. New tables: `onboarding_templates`, `onboarding_progress`. No core model changes.
- **Infrastructure:** Same Vercel deployment. No new services.
- **Security:** Existing auth. No new permissions.

### Data

- **Templates:** JSON structures in database. Seed data by product team.
- **Wizard state:** Persisted per user for resume capability.
- **Analytics:** Existing Mixpanel. New event taxonomy for onboarding funnel.

### Model

Not applicable for V1. AI-generated projects deferred to V2.

---

## 5. Assumptions and Risks

| ID | Assumption | Source | Risk | Constraint | Status |
|---|---|---|---|---|---|
| A-001 | Wizard completers convert higher | PS | High | Must measure cohorts | Unverified |
| A-002 | Guided experience beats docs | PS | Medium | Must beat 32% activation | Unverified |
| A-003 | 4 templates cover majority use cases | New | Medium | Include "Other"; track distribution | Active |
| A-004 | Users willing to complete 4 steps | PS | Medium | Each step <2 min. Allow skip on 3-4. | Active |

---

## 6. Success Criteria

### Global (from PS)

| PS Criterion | Metric | Target | Components |
|---|---|---|---|
| Activation rate | % trial users creating project in 7 days | 55% | Wizard engine, Template system |
| Time to first project | Minutes signup → project | 8 min median | Wizard engine, Template system |
| Team invitation rate | % activated users inviting 1+ | 40% | Team invitation flow |
| Trial-to-paid | % converting in 30 days | 7% | All (indirect) |

### Per Component

| Component | Criterion | Metric | Target |
|---|---|---|---|
| Wizard engine | Completion rate | % start → finish all steps | 65% |
| Wizard engine | Drop-off per step | % dropping at each step | <15%/step |
| Template system | Selection rate | % choosing template vs. skip | 80% |
| Team invitation | Invitations sent | Avg per user completing step 3 | 1.5 |
| Analytics | Event capture | % interactions tracked | 99% |

---

## 7. Constraints

### Technical
- Integrate with existing React frontend (PS)
- No core data model changes (PS)
- Wizard state persists across sessions (from A-004)

### Business
- 1 engineer + 1 designer (PS)
- Ship within current quarter (PS)
- Templates by product team, not generated (decision)

### Regulatory
- GDPR. Existing consent covers analytics (PS)

---

## 8. Translatability Map

| Dimension | Rating | Issues | Action |
|---|---|---|---|
| Business | Sufficient | Components defined with priorities | None |
| Architecture | Sufficient | Stack and integration points clear | None |
| Data | Sufficient | Template format, storage, analytics defined | None |
| Model | N/A | No AI/ML in V1 | None |
| Constraints | Sufficient | All sourced and justified | None |
| Success criteria | Sufficient | All metrics with current + target values | None |

---

## Actor Map

| Actor | Problem | Solution | Authority |
|---|---|---|---|
| Trial user (PM/lead) | Experiences directly | Primary wizard user | None |
| Teammate | Affected (never invited) | Invitation recipient | None |
| Product team | Observes (analytics) | Creates templates, owns design | Approves |
| CS team | Affected (manual calls) | Reduced load | Informs |
| Sales team | Affected (low-quality leads) | Better qualified leads | Informs |

---

## Decision Matrix

| Criterion | Weight | Wizard | Checklist | Video |
|---|---|---|---|---|
| Guides linear completion | 30% | 9 | 5 | 3 |
| Development effort | 25% | 6 | 8 | 9 |
| Measurability | 20% | 9 | 7 | 4 |
| Personalization | 15% | 8 | 6 | 3 |
| Mobile adaptability | 10% | 7 | 8 | 5 |
| **Weighted Total** | | **7.75** | **6.55** | **4.55** |

---

## Feedback Log

| Date | Source | Feedback | Action | Status |
|---|---|---|---|---|
| 2026-02-20 | User testing (N=5) | Template names confusing | Renamed to use-case language | Resolved |
| 2026-02-22 | CTO | What if they want to skip? | Added "Skip for now" + track skip rate | Resolved |
| 2026-02-25 | CS Lead | See wizard completion in CRM? | Added event to Mixpanel → HubSpot sync | Resolved |

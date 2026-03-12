# Problem Statement — SaaS Onboarding Optimization

> **This is an example.** It shows a completed Problem Statement ready for Gate 1.
> To start your own project, replace this file with a copy of `docs/templates/pda-problem.template.md`.
>
> **Esto es un ejemplo.** Muestra un Problem Statement completado y listo para Gate 1.
> Para empezar tu propio proyecto, reemplaza este archivo con una copia de `docs/templates/pda-problem.template.md`.

**Status:** APPROVED
**Version:** 1.0
**Last updated:** 2026-03-01
**Approved by:** VP Product, Head of CS, CTO

---

## 1. Gap

New users of a B2B SaaS platform (project management tool) sign up but fail to reach their first productive moment. 68% of trial users never create their first project. The expected behavior is that users create a project, invite at least one teammate, and complete a task within their first session.

**Evidence:**
- [E-001] Product analytics, 1st-hand quantitative, 2026-02 → Only 32% of trial signups create a first project within 7 days.
- [E-002] Session recordings (N=45), 1st-hand behavioral, 2026-01 → Users spend avg 4.2 minutes on empty dashboard before abandoning.

---

## 2. Who Is Affected

**Primary:** Trial users at B2B companies (10-50 employees) who signed up through self-serve. Typically project managers or team leads evaluating the tool.

**Secondary:** Sales team (receives low-quality leads from users who never experienced the product). Customer Success team (spends 40% of time on manual onboarding calls).

**Evidence:**
- [E-003] CRM data, 1st-hand quantitative, 2026-02 → 1,200 trial signups/month, 85% self-serve.
- [E-004] CS team survey (N=8), 1st-hand declared, 2026-01 → 6/8 reps spend majority of time on users who "don't know where to start."

---

## 3. Success Criteria

| Criterion | Metric | Current | Target |
|---|---|---|---|
| Activation rate | % trial users creating first project in 7 days | 32% | 55% |
| Time to first project | Minutes from signup to first project creation | 22 min (median) | 8 min (median) |
| Team invitation rate | % activated users inviting 1+ teammate | 18% | 40% |
| Trial-to-paid conversion | % trials converting within 30 days | 4.1% | 7% |

**Evidence:**
- [E-001] Product analytics → current activation rate
- [E-005] ProductLed Benchmarks 2025, secondary analytical → industry median activation for PM tools is 48%

---

## 4. Root Causes

| Symptom | Root Cause | Evidence |
|---|---|---|
| Users stare at empty dashboard | No guided first experience; dashboard assumes existing data | [E-002] |
| Users don't create projects | Project creation requires 7 fields; users don't know what to fill | [E-006] Usability tests (N=12) |
| Users don't invite teammates | Invitation flow buried in settings; no prompt during onboarding | [E-007] Heatmap analysis |
| Low trial-to-paid conversion | Users never reach "aha moment" | [E-008] Cohort analysis |

---

## 5. Current Alternatives

Users rely on a generic welcome email (12% open rate) and an optional "book a demo" CTA. Some find the documentation (avg 6 page views in first session). CS team conducts manual calls for enterprise leads but this doesn't scale to self-serve.

**Evidence:**
- [E-009] Email analytics, 1st-hand quantitative, 2026-02 → 12% open rate
- [E-004] CS survey → manual calls cover ~15% of trial signups

---

## 6. Constraints

**Technical:** Platform is React + Node.js. Must integrate with existing frontend. Cannot modify core data model.

**Business:** Budget: 1 product engineer + 1 designer. Must ship within current quarter.

**Regulatory:** GDPR compliance required. Existing consent mechanism covers analytics.

---

## 7. Cost of Inaction

At current 4.1% conversion with 1,200 trials/month and $200 ARPU: monthly revenue from trials = $9,840. At target 7%: $16,800. Annual gap: ~$83,520.

CS team capacity at 95%. Without improving self-serve onboarding, scaling acquisition requires proportional CS hiring.

**Evidence:**
- [E-010] Finance report, 2026-Q1 → revenue and conversion figures
- [E-011] CS capacity planning, 2026-01 → 95% utilization

---

## 8. Scope Boundaries

**Out of scope:**
- Redesigning core product (projects, tasks, collaboration)
- Changing pricing or packaging
- Enterprise onboarding (handled by CS)
- Mobile onboarding (web only for V1)
- Existing user onboarding (new trial signups only)

---

## 9. Assumptions

| Assumption | Risk | Validation Plan | Status |
|---|---|---|---|
| Users who create a project in session 1 convert significantly more | High | Cohort analysis | Confirmed (E-008) |
| Guided experience more effective than documentation | Medium | A/B test | Unverified |
| Users willing to complete 3-5 step wizard | Medium | Prototype test (N=10) | Unverified |
| Template-based creation reduces friction vs. blank | Low | Usability test | Unverified |

---

## Evidence Index

| ID | Source | Type | Date | Confidence | Phase |
|---|---|---|---|---|---|
| E-001 | Product analytics (Mixpanel) | 1st-hand quantitative | 2026-02 | High | 1 |
| E-002 | Session recordings (Hotjar, N=45) | 1st-hand behavioral | 2026-01 | High | 1 |
| E-003 | CRM data (HubSpot) | 1st-hand quantitative | 2026-02 | High | 1 |
| E-004 | CS team survey (N=8) | 1st-hand declared | 2026-01 | Medium | 1 |
| E-005 | ProductLed Benchmarks 2025 | Secondary analytical | 2025-09 | Medium | 1 |
| E-006 | Usability tests (N=12) | 1st-hand behavioral | 2026-01 | High | 1 |
| E-007 | Heatmap analysis (Hotjar) | 1st-hand behavioral | 2026-02 | High | 1 |
| E-008 | Cohort analysis (internal) | 1st-hand quantitative | 2026-02 | High | 1 |
| E-009 | Email analytics (Resend) | 1st-hand quantitative | 2026-02 | High | 1 |
| E-010 | Finance Q1 report | 1st-hand quantitative | 2026-Q1 | High | 1 |
| E-011 | CS capacity planning | 1st-hand quantitative | 2026-01 | High | 1 |

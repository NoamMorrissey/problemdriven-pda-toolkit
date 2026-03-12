# PDA Toolkit V1 — First Run Test Script
# Script de prueba para la primera ejecución end-to-end

> Run this in Claude Code after setting up the repo.
> Ejecuta esto en Claude Code después de configurar el repo.
>
> For each step: run the command, review the output, and note the result below.
> Para cada paso: ejecuta el comando, revisa el output y anota el resultado abajo.

---

## Setup

```bash
# 1. Clone and enter the repo
git clone [YOUR_REPO_URL] pda-test
cd pda-test

# 2. Initialize Spec Kit for Claude Code
specify init --here --ai claude

# 3. Verify slash commands loaded
# In Claude Code, type /pda. and check that all 8 commands appear:
# /pda.validate-problem
# /pda.validate-solution
# /pda.adapt-constitution
# /pda.adapt-specify
# /pda.verify-specify
# /pda.verify-plan
# /pda.verify-tasks
# /pda.verify-build
```

**Result / Resultado:** [ ] Commands loaded / Comandos cargados
**Issues:** ___

---

## Phase 1: Validate Problem Statement

```
/pda.validate-problem
```

**Expected / Esperado:**
- Report generated at `pda-verification/verify-problem.md`
- All 9 elements: PASS (the example is complete)
- Evidence quality: all pieces have full metadata
- No contradictions
- Gate 1 verdict: READY

**Result / Resultado:** [ ] READY / [ ] NOT READY
**Issues:** ___
**Report matches expected?** ___

---

## Phase 2: Validate Solution Brief

```
/pda.validate-solution
```

**Expected / Esperado:**
- Report generated at `pda-verification/verify-solution.md`
- All components have gap_ref + success_ref: PASS
- No orphan components
- All PS criteria covered by components
- Translatability: all Sufficient or N/A
- Gate 2 verdict: READY

**Result / Resultado:** [ ] READY / [ ] NOT READY
**Issues:** ___
**Report matches expected?** ___

---

## Phase 3a: Generate Constitution

```
/pda.adapt-constitution
```

**Expected / Esperado:**
- File generated at `.specify/memory/constitution.md`
- Contains: constraints from SB section 7, architecture from SB section 4, success criteria from SB section 6
- PDA traceability block at the end
- Human review requested before proceeding

**Result / Resultado:** [ ] Generated / [ ] Failed
**Constitution content makes sense?** ___
**Issues:** ___

---

## Phase 3b: Prepare Specification Inputs

```
/pda.adapt-specify
```

**Expected / Esperado:**
- A structured prompt is presented (NOT executed)
- Prompt includes: gap context, success criteria, solution description, components, actor map, translatability warnings
- Human is asked to review before running /speckit.specify

**Result / Resultado:** [ ] Prompt generated / [ ] Failed
**Prompt quality (1-5):** ___
**Missing information:** ___
**Issues:** ___

---

## Phase 3c: Run Spec Kit Specify

Take the prompt from the previous step and run:

```
/speckit.specify [paste or reference the prepared prompt]
```

**Expected / Esperado:**
- Spec Kit generates `spec.md` in `.specify/specs/001-*/`
- Contains user stories, acceptance criteria, structure

**Result / Resultado:** [ ] Generated / [ ] Failed
**Issues:** ___

---

## Phase 3d: Verify Specification

```
/pda.verify-specify
```

**Expected / Esperado:**
- Report at `pda-verification/verify-specify.md`
- Most spec elements trace to SB components
- No major scope violations
- Possible: minor coverage gaps or additions by Spec Kit

**Result / Resultado:** [ ] PASS / [ ] FAIL
**Traceability accuracy:** ___
**Scope creep detected:** ___
**Issues:** ___

---

## Phase 3e: Run Spec Kit Plan

```
/speckit.plan [reference SB architecture: React frontend, Node.js backend, PostgreSQL, Vercel]
```

**Result / Resultado:** [ ] Generated / [ ] Failed
**Issues:** ___

---

## Phase 3f: Verify Plan

```
/pda.verify-plan
```

**Expected / Esperado:**
- Report at `pda-verification/verify-plan.md`
- Plan elements trace to spec requirements
- SB components have coverage in plan
- Architecture decisions respected

**Result / Resultado:** [ ] PASS / [ ] FAIL
**Issues:** ___

---

## Phase 3g: Run Spec Kit Tasks

```
/speckit.tasks
```

**Result / Resultado:** [ ] Generated / [ ] Failed
**Issues:** ___

---

## Phase 3h: Verify Tasks

```
/pda.verify-tasks
```

**Expected / Esperado:**
- Report at `pda-verification/verify-tasks.md`
- Tasks trace to user stories
- No orphan tasks
- No uncovered requirements

**Result / Resultado:** [ ] PASS / [ ] FAIL
**Issues:** ___

---

## Phase 4: Build (optional for first test)

```
/speckit.implement
```

Then:

```
/pda.verify-build
```

**Note:** This step is optional for the first test. The critical validation is Phases 1-3. If Phase 3 works cleanly, Phase 4 is Spec Kit's core competency.

---

## Summary / Resumen

| Step | Status | Issues |
|---|---|---|
| Setup + commands loaded | | |
| validate-problem | | |
| validate-solution | | |
| adapt-constitution | | |
| adapt-specify | | |
| speckit.specify | | |
| verify-specify | | |
| speckit.plan | | |
| verify-plan | | |
| speckit.tasks | | |
| verify-tasks | | |
| speckit.implement | | |
| verify-build | | |

## Gaps Detected / Gaps detectados

*Document gaps here. These are the triggers for V2.*

1. ___
2. ___
3. ___

## Decisions for V2 / Decisiones para V2

*Based on gaps, what should change?*

1. ___
2. ___

---
name: verify-spec
description: Use to check alignment between spec.md, plan.md, tasks.md when needed, and the current codebase. Reports drift — spec behavior not in code, code behavior not in spec, or plan/done criteria not satisfied — and updates last-verified only on a clean pass.
---

# Verify Spec

Check spec-to-code and plan-to-project alignment, report drift, and update last-verified only when clean.

## Steps

1. Read `AGENTS.md`, `spec/spec.md`, and `spec/plan.md`.
2. For every behavior rule, validation rule, error condition, and runtime constraint in spec.md, verify the code implements it:
   - Trace from the rule to the implementation (function, module, test)
   - Note any rule with no corresponding code
3. For every build/process constraint and done criterion in plan.md, verify the project satisfies it:
   - Read `spec/tasks.md` if task completion state is part of a done criterion.
   - Trace test, dependency, build, sequencing, or completion requirements to evidence in the repo.
   - Note any plan requirement with no corresponding evidence.
4. For every externally observable behavior in the codebase, check whether it is described in spec.md:
   - Note any behavior in code that has no spec rule (undocumented behavior = drift)
5. Check that all error exit codes and messages match spec.md exactly.
6. Check that configuration options in spec.md match what the code accepts.
7. Produce a drift report:
   - **Spec → Code gap**: rules in spec with no implementation
   - **Code → Spec gap**: implemented behavior not in spec
   - **Plan → Project gap**: build constraints or done criteria not satisfied
   - **Mismatch**: implemented differently from spec
8. If the drift report is clean (no gaps, no mismatches):
   - Update `last-verified` in spec.md: `last-verified: YYYY-MM-DD @ <current commit sha>`
   - Report: "Spec verified. No drift found. last-verified updated."
9. If drift is found:
   - Do not update `last-verified`
   - Report each drift item with suggested resolution (`$change-scope`, `$add-feature`, or `$start-task`)

## Rules

- Do not fix drift during this skill — report only
- Do not modify spec.md except to update `last-verified` on a clean pass
- A passing test suite does not guarantee no drift — tests may be incomplete

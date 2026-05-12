---
name: bootstrap
description: Use when starting a brand-new project whose spec.md, plan.md, and tasks.md are empty or still contain the untouched template placeholders. Fills all three files by interviewing the user about the system. Do not use if project-specific spec content already exists — use $change-scope or $add-feature instead.
---

# Bootstrap

Fill spec.md, plan.md, and tasks.md from scratch for a new project.

## Steps

1. Read `AGENTS.md` and `spec/README.md` to understand the system conventions.
2. Ask the user the following questions (one at a time, wait for each answer):
   - What does this system do? (one sentence)
   - Who uses it and how? (user, API caller, another system?)
   - What does it take as input?
   - What does it produce as output?
   - Are there any hard runtime/product constraints? (performance, environment, data limits)
   - Are there any hard build/process constraints? (dependencies, test requirements, deployment environment)
   - What test coverage or verification is required before work is considered done?
   - What is explicitly out of scope?
3. Write `spec/spec.md`:
   - Fill Purpose, Input, Output, Behavior Rules, Validation Rules, Error Handling, Configuration, Constraints
   - Include only runtime/product constraints
   - Set `last-verified: not yet verified`
   - State all behavior rules in declarative, testable form
4. Write `spec/plan.md`:
   - Fill Goal (one sentence), Core Slice (smallest working version), Constraints, Execution Order
   - Include only build/process constraints
   - Break work into phases with T-N task IDs
   - Fill Out Of Scope and Done Criteria
   - Include the user's testing and verification expectations in Done Criteria
5. Write `spec/tasks.md`:
   - Create task rows for every T-N in plan.md; set all states to Todo
   - Leave the Decisions table empty with a placeholder row
6. Confirm with the user: "Spec system initialized. Run `$start-task` to begin implementation."

## Rules

- Do not invent behavior rules — only write what the user confirms
- Runtime/product constraints belong only in spec.md; build/process constraints belong only in plan.md
- Every task must have a unique T-N ID
- Keep task descriptions short enough to complete in one agent session

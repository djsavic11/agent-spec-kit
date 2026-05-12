---
name: change-scope
description: Use when existing system behavior needs to change — modifying a behavior rule, validation rule, error condition, configuration option, or runtime constraint. For adding new capabilities without touching existing behavior, use $add-feature instead. Always goes through the spec before touching code.
---

# Change Scope

Modify existing system behavior safely through the spec system.

## Steps

1. Read `AGENTS.md`, `spec/spec.md`, `spec/plan.md`, and `spec/tasks.md`.
2. Ask the user to describe the behavior change precisely:
   - What currently happens?
   - What should happen instead?
   - Why is this change needed?
3. Identify which section of spec.md the change affects (Behavior Rules, Validation Rules, Error Handling, Configuration, or runtime Constraints).
4. If the change requires a new build/process constraint, update plan.md too after confirming with the user.
5. Show the user the proposed spec change before writing it. Wait for confirmation.
6. Update spec.md (and plan.md if build/process constraints changed).
7. Add a task to tasks.md for the implementation work:
   - Assign the next T-N ID
   - State: Todo
   - Note in the task description: "implements spec change from <date>"
8. Reset `last-verified` in spec.md to `not yet verified`.
9. Report: what changed in spec, task ID created, files modified.

## Rules

- Never change code before updating the spec — spec is always updated first
- Do not add new sections or capabilities — use `$add-feature` for that
- Do not remove a behavior rule without explicit user confirmation
- One scope change per invocation — if the user describes multiple changes, handle them sequentially

---
name: start-task
description: Use when ready to implement one task. Continues the current Doing task if present; otherwise picks the top Todo task from tasks.md, reads the spec, implements it, marks it Done, records decisions, and commits the result. Do not use if no tasks are Todo or Doing — use $add-feature or $bootstrap instead.
---

# Start Task

Continue the current Doing task, or pick, implement, finish, and commit the next Todo task from tasks.md.

## Steps

1. Read `AGENTS.md`, `spec/spec.md`, `spec/plan.md`, and `spec/tasks.md`.
2. Check task state:
   - If exactly one task is **Doing**, continue that task.
   - If more than one task is **Doing**, stop and ask the user which task state to repair.
   - If no task is **Doing**, find the first task in **Todo** state, earliest in phase order.
   - If no task is **Todo** or **Doing**, stop and suggest `$add-feature`, `$change-scope`, or `$verify-spec` as appropriate.
3. If a **Todo** task was selected, move it to **Doing** state in tasks.md.
4. Implement the task:
   - Follow the behavior rules in spec.md exactly
   - Follow constraints in plan.md
   - Do not change behavior rules or add features — if something seems missing, stop and ask
5. When implementation is complete, run existing tests. Fix failures before proceeding.
6. Move the task to **Done** state in tasks.md.
7. If a non-obvious trade-off was made during implementation, add a Decision entry:
   - Format: `D-N (T-N): chose X over Y because Z`
   - Assign the next available D-N ID
   - Add it to the Decisions table in tasks.md
8. Stage all changes with `git add`.
9. Commit the staged changes with message `feat(T-N): <short description>` (include `D-N` in the body if a decision was recorded).
10. Report: task ID, Done state, tests run, decision recorded (if any), commit created, commit message used.

## Rules

- Work on exactly one task at a time
- Continue an existing Doing task before starting any Todo task
- If the task is blocked by a missing dependency, set state to Blocked and note the blocker in the Notes column
- Do not mark the task Done or commit if tests are failing
- Do not modify spec.md or plan.md during implementation — raise changes through `$change-scope` or `$add-feature`
- Commit messages must reference the task ID: `feat(T-N): <description>`

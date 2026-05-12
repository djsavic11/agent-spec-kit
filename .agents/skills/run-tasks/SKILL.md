---
name: run-tasks
description: "Use when the user wants Codex to run the spec task queue continuously: pick the next Todo task, implement it, test it, mark it Done, commit it, verify the checkpoint, then continue with the next Todo task until all tasks are Done or a blocker/failure requires human input."
---

# Run Tasks

Run the task queue end-to-end while preserving the same safeguards as `$start-task`: one active task at a time, spec first, tests before Done, decisions recorded, and commits per task.

## Workflow

1. Read `AGENTS.md`, `spec/spec.md`, `spec/plan.md`, and `spec/tasks.md`.
2. Check the queue state before starting:
   - If any task is **Doing**, continue only that task first.
   - If no task is **Doing**, pick the first **Todo** task in phase order.
   - If there are no **Todo** or **Doing** tasks, run the final verification step.
3. For the active task, follow the `$start-task` workflow:
   - Move a picked **Todo** task to **Doing**.
   - Implement only that task.
   - Run relevant tests and fix failures.
   - Move the task to **Done** only after tests pass.
   - Record a Decision entry for any non-obvious trade-off.
   - Stage changes and commit with `feat(T-N): <description>`.
4. After each task commit, perform a checkpoint:
   - Confirm the task row is **Done**.
   - Confirm no task remains **Doing**.
   - Confirm the worktree has no unintended unstaged or untracked task changes.
   - Summarize the task ID, tests run, commit created, and any decision recorded.
5. Repeat from step 2 until no **Todo** tasks remain.
6. Run `$verify-spec` once at the end:
   - If clean, update `last-verified` according to `$verify-spec`.
   - If drift remains, report it and suggest the appropriate next skill.

## Stop Conditions

- Stop immediately if tests fail and cannot be fixed in the current task.
- Stop if the active task is ambiguous or would require changing `spec/spec.md` or `spec/plan.md`; recommend `$change-scope` or `$add-feature`.
- Stop if a dependency, missing credential, unavailable service, or approval requirement blocks progress; mark the task **Blocked** with a short note.
- Stop if the user interrupts, redirects, or asks to review before continuing.

## Rules

- Do not work on more than one task at the same time.
- Do not skip task order unless the user explicitly asks.
- Do not mark a task Done without passing tests.
- Do not batch multiple task implementations into one commit; create one commit per task.
- Do not run full `$verify-spec` after every task if later Todo tasks intentionally remain; reserve full verification for the end of the queue.

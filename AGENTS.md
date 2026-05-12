# AGENTS.md

Read this file before doing anything else in this repository.

## Project Context

<!-- Fill in: what this system does, who uses it, what problem it solves. -->

---

## File Roles

| File             | Role                                                             | Who updates it |
| ---------------- | ---------------------------------------------------------------- | -------------- |
| `AGENTS.md`      | Your entry point. Read this first, always.                       | Human + agent  |
| `spec/spec.md`   | What the system does. Behavior, rules, runtime constraints.      | Human          |
| `spec/plan.md`   | How and when we build it. Phases, sequencing, build constraints. | Human          |
| `spec/tasks.md`  | What to work on. Task queue (T-N) and decisions log (D-N).       | Agent          |
| `README.md`      | Onboarding for humans. Not read by agents.                       | Human          |

---

## Reading Policy

When starting any session:

1. Always read `AGENTS.md` first.
2. Read spec files on demand:
   - Read `spec/spec.md` when behavior, validation, errors, configuration, or runtime constraints matter.
   - Read `spec/plan.md` when phases, sequencing, build constraints, or done criteria matter.
   - Read `spec/tasks.md` when selecting, updating, or auditing task state.
3. Follow the selected skill's `SKILL.md` if it defines a stricter read set.

---

## Working Rules

- **Spec first** — never change code to alter behavior without updating `spec/spec.md` first
- **One task at a time** — pick the top Todo task; do not start a second task while one is Doing, even when using `$run-tasks`
- **One home per fact** — behavior rules and runtime constraints live only in `spec/spec.md`; build constraints and sequencing live only in `spec/plan.md`; do not duplicate
- **Finish every task** — `$start-task` must run tests, mark the task Done, record any non-obvious decision, stage changes, and create the commit
- **Ask, don't assume** — if a behavior rule is ambiguous or a task is unclear, ask before implementing

---

## Skills

Repo-local skills live in `.agents/skills/`.

Use a skill when the user names it explicitly (`$start-task`) or when the request clearly matches its description. Read the selected skill's `SKILL.md` before acting.

Common workflow:

- `$bootstrap` initializes an untouched template project.
- `$start-task` implements one queued task and commits it.
- `$run-tasks` keeps running queued tasks until done or blocked.
- `$change-scope` changes existing behavior through the spec.
- `$add-feature` adds new behavior through the spec.
- `$verify-spec` checks code/spec drift.

---

## Decision Escalation

Stop and ask the human when:

- A task would require modifying a behavior rule in `spec/spec.md`
- A task would require adding a new capability not in `spec/plan.md`
- Two behavior rules conflict with each other
- A runtime constraint in `spec/spec.md` or build constraint in `spec/plan.md` makes a task impossible as written
- A decision would be non-obvious to a future agent reading the code

Record non-obvious decisions in the Decisions table of `spec/tasks.md` using D-N IDs.

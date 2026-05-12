# Spec System — Onboarding

This document is for **humans only**. Agents read `AGENTS.md` instead.

---

## What's in this folder

| File        | What it is          | What belongs here                                                |
| ----------- | ------------------- | ---------------------------------------------------------------- |
| `spec.md`   | Behavior spec       | What the system does: inputs, outputs, rules, validation, errors, runtime constraints |
| `plan.md`   | Implementation plan | How we build it: phases, sequencing, build constraints, done criteria |
| `tasks.md`  | Task queue          | T-N tasks by phase; D-N decisions for non-obvious trade-offs     |
| `README.md` | This file           | Onboarding only                                                  |

---

## How to read the spec

Start with `spec.md` to understand what the system does. Then read `plan.md` to understand the build approach. Check `tasks.md` to see what's active.

**Scope rules** — each file has a scope rule at the top. If you're unsure where a fact belongs, the scope rule tells you:

- Behavior and runtime/product constraints belong in `spec.md`
- Build/process constraints and sequencing belong in `plan.md`
- Work items belong in `tasks.md`

Never duplicate facts across files. One home per fact.

---

## How to run skills

Skills are reusable workflows invoked directly in Codex. Type `$` to see available skills, or invoke explicitly:

| Skill           | When to use                                                      |
| --------------- | ---------------------------------------------------------------- |
| `$bootstrap`    | Starting a brand-new project — replaces untouched templates with project-specific spec, plan, and tasks |
| `$start-task`   | Pick up the next Todo task, implement it, mark it Done, and commit |
| `$run-tasks`    | Keep running Todo tasks one by one until the queue is done or blocked |
| `$change-scope` | Change existing system behavior through the spec                 |
| `$add-feature`  | Add a new capability (additive only, no behavior changes)        |
| `$verify-spec`  | Check spec-to-code alignment, find drift, update last-verified   |

Skills read `AGENTS.md` and the relevant spec files before acting. You don't need to paste context in.

---

## Task and Decision IDs

- **T-N** — task IDs (T-1, T-2, ...). Used in commits: `feat(T-3): add rate limiting`
- **D-N** — decision IDs (D-1, D-2, ...). Used in the Decisions section of `tasks.md` for non-obvious trade-offs git messages don't capture.

---

## What agents don't do without being asked

- Agents won't change `spec.md` behavior rules without `$change-scope`
- Agents won't add features without `$add-feature`
- Agents won't mark tasks Done or commit them unless `$start-task` or `$run-tasks` completes the task successfully

If an agent is uncertain about scope, it asks rather than assumes.

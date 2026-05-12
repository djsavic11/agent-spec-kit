# Agent Spec Kit - spec system

Agent Spec Kit is my simplified, minimal take on spec-driven development, built for working with the Codex agent.
It keeps project intent, implementation planning, task state, and verification in a small set of files the agent can reliably follow.

---

## What's in this repository

| File        | What it is          | What belongs here                                                |
| ----------- | ------------------- | ---------------------------------------------------------------- |
| `AGENTS.md` | Agent entry point   | Working rules, reading policy, decision escalation               |
| `spec.md`   | Behavior spec       | What the system does: inputs, outputs, rules, validation, errors, runtime constraints |
| `plan.md`   | Implementation plan | How we build it: phases, sequencing, build constraints, done criteria |
| `tasks.md`  | Work tracker        | The ordered work queue, current task state, and important implementation decisions |

---

## How to read the spec

Start with `spec/spec.md` to understand what the system does. Then read `spec/plan.md` to understand the build approach. Check `spec/tasks.md` to see what's active.

**Scope rules** — each file has a scope rule at the top. If you're unsure where a fact belongs, the scope rule tells you:

- Behavior and runtime/product constraints belong in `spec/spec.md`
- Build/process constraints and sequencing belong in `spec/plan.md`
- Work items belong in `spec/tasks.md`

Never duplicate facts across files. One home per fact.

---

## How to run skills

Skills are reusable workflows invoked directly in Codex. Type `$` to see available skills, or invoke explicitly:

| Skill           | When to use                                                      |
| --------------- | ---------------------------------------------------------------- |
| `$bootstrap`    | Starting a brand-new project — replaces untouched templates with project-specific spec, plan, and tasks |
| `$start-task`   | Pick up the next task, implement it, mark it Done, and commit    |
| `$run-tasks`    | Keep running Todo tasks one by one until the queue is done or blocked |
| `$change-scope` | Change existing system behavior through the spec                 |
| `$add-feature`  | Add a new capability without changing existing behavior          |
| `$verify-spec`  | Check spec-to-code alignment, find drift, update last-verified   |

Skills read `AGENTS.md` and the relevant spec files before acting. You don't need to paste context in.

---

## Task and Decision IDs

- **T-N** — task IDs (T-1, T-2, ...). Used in commits: `feat(T-3): add rate limiting`
- **D-N** — decision IDs (D-1, D-2, ...). Used in `spec/tasks.md` for non-obvious trade-offs git messages don't capture.

---

## What agents don't do without being asked

- Agents won't change `spec/spec.md` behavior rules without `$change-scope`
- Agents won't add features without `$add-feature`
- Agents won't mark tasks Done or commit them unless `$start-task` or `$run-tasks` completes the task successfully

If an agent is uncertain about scope, it asks rather than assumes.

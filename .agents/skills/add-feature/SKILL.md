---
name: add-feature
description: Use when adding a new capability that does not modify existing behavior. Adds new spec content, allows additive edits to existing spec sections, adds tasks, and leaves existing behavior unchanged. For changes to existing behavior, use $change-scope instead.
---

# Add Feature

Add a new capability end-to-end through spec → plan → task → code.

## Steps

1. Read `AGENTS.md`, `spec/spec.md`, `spec/plan.md`, and `spec/tasks.md`.
2. Ask the user to describe the new capability:
   - What does it do?
   - What input does it take (if any new input)?
   - What output does it produce?
   - Are there any new runtime constraints, build constraints, or validation rules?
3. Confirm the feature is **additive only** — it does not change any existing behavior rule. If it does, stop and use `$change-scope` instead.
4. Show the user the proposed spec additions before writing. Wait for confirmation.
5. Update spec.md with additive content only:
   - Add new rules, input/output fields, configuration options, validation rules, error conditions, or runtime constraints as needed.
   - Add to existing sections when that is the natural home for the new fact.
   - Do not change or remove existing behavior.
6. Update plan.md if new phases or out-of-scope boundaries change.
7. Add tasks to tasks.md:
   - Assign sequential T-N IDs following the last existing task
   - Set state to Todo
   - Group under a new phase if appropriate
8. Reset `last-verified` in spec.md to `not yet verified`.
9. Report: what was added to spec, task IDs created, files modified.

## Rules

- Do not change or remove any existing behavior rule, validation rule, or error condition
- Additive edits to existing sections are allowed when they describe only the new capability
- Do not touch existing task rows — only add new ones
- If the feature conflicts with an existing Out Of Scope item in plan.md, stop and ask the user to resolve it first
- Spec additions must be written before any implementation starts

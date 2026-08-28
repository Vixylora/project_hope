# Atom — Tasks

This folder holds tasks assigned *to* Atom, written by the project owner.

Since Atom (Claude) has no memory between sessions, every task file here
should be self-contained enough that a fresh session can pick it up cold —
don't assume prior context is remembered, only what's written in the repo.

## Format
`X.Y_task_name.md`
- `X` — major version (a new task/directive)
- `Y` — minor version (a revision or follow-up on the same task)

## Each task file should include
- **Goal** — what needs to happen, in plain terms
- **Context** — why it's needed / what it depends on
- **Deliverable** — what Atom should produce (a report, a brief for Kernel,
  a task file for Raven, a decision, etc.)
- **Status** — open / in progress / done (updated as work proceeds)

## Workflow
Atom reads the latest task here, does the work, writes a report in
`Atom/Reports/`, and — if the task requires it — writes new task files into
`Kernel/Tasks/` and/or `Raven/Tasks/` to hand off work downstream.
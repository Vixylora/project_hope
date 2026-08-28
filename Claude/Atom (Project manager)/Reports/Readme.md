# Atom — Reports

This folder holds Atom's own output: project state summaries, decisions
made, and the briefs/directives issued to Kernel and Raven. This is also
the primary way Atom "remembers" across sessions — a new session should be
able to read the latest report here and be fully caught up.

## Format
`X.Y_report_name.md`
- `X` — major version: a significant update (new decision, new phase,
  resolved conflict, major scope change)
- `Y` — minor version: a small addition or clarification within the same
  major version (resets to `.0` on the next major bump)

Example: `1.0_roles_and_stack.md` → `1.1_roles_and_stack.md` →
`2.0_hosting_decision.md`

## Each report should include
1. **What was done** — decisions made, briefs written, conflicts resolved
2. **Detailed explanation** — the actual reasoning, not just the outcome —
   enough that someone reading cold understands *why*, not just *what*
3. **What's next** — Atom's read on what needs deciding or doing next,
   clearly marked as a recommendation, not a directive already acted on

## Reading order
Always read the **highest major version** first for current state; older
majors are history, not current truth. Minor versions under the same major
are incremental context on top of it.
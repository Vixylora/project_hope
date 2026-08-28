# Kernel — Tasks

Tasks assigned to Kernel by Atom. Kernel reads the latest task, does the
architectural/technical work, writes a report in `Kernel/Reports/`, and
creates downstream task files for Prism, Nexus, and Sentry in their own
`Grok/<name>/Tasks/` folders.

## Format
`X.Y_task_name.md`
- `X` — major version: a new directive or significant scope change
- `Y` — minor version: a revision/follow-up within the same directive

## Each task file includes
- **Goal** — what Kernel needs to produce or decide
- **Context** — relevant background (linking to Atom's reports where
  useful, rather than repeating everything)
- **Constraints** — anything non-negotiable (stack already chosen,
  security requirements, legal constraints)
- **Deliverable** — architecture doc, task breakdown for the Groks, a
  specific technical decision, etc.
- **Open questions** — anything Atom needs Kernel's technical judgment on
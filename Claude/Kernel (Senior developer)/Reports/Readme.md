# Kernel — Reports

Kernel's reports are how Atom (and, transitively, the project owner)
stays current on the technical state of the project without reading
every Grok report individually.

## Format
`X.Y_report_name.md` — `X` major (architecture decisions, milestones,
scope changes), `Y` minor (small updates within that milestone).

## Each report includes
1. **What was decided/built** — architecture choices, schema changes,
   what got shipped
2. **Detailed explanation** — enough technical detail that Atom (and a
   cold-start future session) understands *why*, not just *what*:
   what the code/config actually does, what changed and why
3. **Grok task status** — a short summary of what's been assigned to
   Prism/Nexus/Sentry and where each stands (their own reports have the
   full detail; this is the roll-up)
4. **What's next** — Kernel's recommendation, clearly marked as a
   recommendation, not something already decided unilaterally
5. **Blockers/risks** — anything that needs Atom's or the project owner's
   input to resolve
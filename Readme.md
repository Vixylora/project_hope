# Project Amal

## What this is
Project Amal digitizes a paper form currently used by a pediatric
oncology unit, under the "Rihlat
al-Amal" (Road of Hope) program. Volunteers/interns and psychologists
currently fill out and physically archive a tracking card for each child
in the program, covering their educational, psychological, and health
follow-up across sessions. The goal is to move filling, storing, and
retrieving this data into a secure digital system — nothing more,
nothing less. This is not a general hospital EHR system.

## Data model
- **One patient → many sessions.** Each session record covers four areas
  taken directly from the paper form:
  - Educational (understanding level, participation, focus, language/
    motor/social skills)
  - Psychological/emotional (mood, peer interaction, need for extra
    support)
  - Health (general state during the session, relevant medical notes)
  - Volunteer/intern notes (session reflections, recommendations)

## Users & roles
| Role | Who | Access |
|---|---|---|
| Intern | Intern/trainee psychologists (what the paper form calls "volunteer") | Limited — likely their own patients/entries only |
| Psychologist | Full psychologists | Broader patient access, full session detail |
| Coordinator | Oversees and coordinates the program (senior/professor role) | Broad read access across patients and staff |
| Admin | System/account management | **Still being decided:** clinical admin (coordinator doubling up) vs. technical admin (IT-only, minimal clinical data exposure) — see latest Atom report for current status |

Role-based access is enforced at the **database level** (Postgres Row-Level
Security), not just hidden in the UI — so a frontend bug or bypass can't
expose data a role shouldn't see.

## Screens
- **Login**
- **Home/Dashboard** — overview stats, patients needing attention, personal
  task list
- **Logs** — live feed of all additions/edits/deletions across the system,
  filterable, role-scoped
- **Patients list** — grouped/searchable list of all patients
- **Patient profile** — near-fullscreen (desktop) / fullscreen (mobile)
  view with tabs matching the four form sections, latest data + history,
  role-gated change log, "new session" entry point
- **Psychologists/Interns list** — staff directory (role-gated)
- **Personal info** — own profile + personal stats
- **Settings** — app config, user management (role-gated)

Design direction: Notion/Linear-style — clean, low-visual-noise, muted
neutral palette, content-first.

## Language
The app is **multilingual** — the source form is in Arabic, so Arabic
(RTL) support is a core requirement, not an afterthought. Exact language
set (Arabic + French, + English, etc.) and default language are still to
be finalized, but the frontend architecture must support RTL layout and
language switching from the start, not be retrofitted later.

## Tech stack
**Status: not fully finalized — two proposals exist and need reconciling
(see Atom's latest report for the current decision).**

- **Option A (local-first):** Next.js + TypeScript, Tailwind, shadcn/ui
  (Radix primitives), TanStack Table/Query, cmdk, React Hook Form + Zod,
  Framer Motion — backed by self-hosted Supabase (Postgres + GoTrue Auth +
  Realtime + Storage + PostgREST) via Docker Compose, on a server hosted
  physically inside the hospital. Staff access it over the hospital's
  internal network; a WireGuard VPN allows authorized remote access
  (e.g., for the coordinator) without exposing the server to the public
  internet.
- **Option B (MVP-first):** Vite + React + Tailwind, hosted Supabase
  (cloud), deployed on Vercel — faster to ship as a solo one-month MVP,
  but data leaves the hospital's physical control and likely leaves
  Algeria depending on Supabase's region, which is in tension with the
  legal considerations below.

The core trade-off: Option A better fits Algeria's data-protection
requirements for this kind of data but needs more infrastructure work and
ongoing maintenance (backups, patching, an IT presence) than a solo
one-month build realistically allows. Option B ships faster but should be
treated as a pilot/prototype, not yet cleared for real patient data, until
migrated to a compliant hosting setup.

## Legal context (Algeria)
This system handles children's health and psychological data — Algeria's
Law 18-07 (amended by Law 25-11, 2025) classifies health data as
sensitive personal data, with related requirements around lawful
processing, security measures, and (per current draft understanding)
possible declaration to the ANPDP. This is **not settled by AI judgment**
— the hospital should confirm exact obligations with local legal counsel
before handling real patient data. Known requirements already factored
into the design:
- Parental consent step (can be a physical, paper-based step referencing
  the digital system)
- A defined data retention policy (how long a child's record is kept
  after leaving the program)
- Data minimization — only what the paper form actually asks for

## Team structure
- **Claude/Atom** — project manager. Maintains the full project picture,
  issues briefs to Kernel and tasks to Raven, resolves cross-cutting
  conflicts (like the stack decision above).
- **Claude/Kernel** — senior developer. Translates Atom's direction into
  technical architecture, assigns implementation tasks to the Grok
  developers.
- **Claude/Raven** — researcher/reporter. Handles deep research, tracks
  and reports on project progress.
- **Grok/Prism** — frontend developer
- **Grok/Nexus** — backend developer
- **Grok/Sentry** — security engineer, vulnerability checks

Each AI has a `Tasks/` folder (what's assigned to them) and a `Reports/`
folder (what they produced) under their name. Reports use `X.Y_name.md`
versioning — `X` for major changes, `Y` for minor ones — so state can
always be reconstructed by a fresh session reading the latest major
version. The project owner is the only line of communication between all
AI participants; no AI here interacts with another directly.
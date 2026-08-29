# Project Hope

This README is the **universal source of truth** for this project. Any
AI session — Claude, Grok, or otherwise — or any human, should be able to
read this file alone and fully understand what this project is, why it's
built the way it is, and how work happens on it. If you're an AI reading
this as part of a task, treat this as complete background, not a summary
of something you're expected to already know from elsewhere.

---

## What this is
Project Hope digitizes a paper tracking form currently used at a
pediatric oncology follow-up program at a public hospital in Algeria.
Volunteers/interns and psychologists currently fill out and physically
archive a tracking card for each child in the program, covering
educational, psychological, and health follow-up across sessions. The
goal is to move filling, storing, and retrieving this data into a
secure digital system — nothing more. This is **not** a general hospital
EHR system, and it is not trying to become one.

**No real institution name, real patient name, or other identifying
detail should ever appear anywhere in this repository** — not in code,
comments, seed/test data, commit messages, task files, or reports. This
repository is public.

## Data model
One patient → many sessions. Each session has four sections, taken
directly from the source paper form:
- **Educational** — understanding level, participation, focus,
  language/motor/social skills
- **Psychological/Emotional** — mood, peer interaction, need for extra
  psychological support
- **Health** — general state during the session, relevant medical notes
- **Volunteer/Intern notes** — session reflections, recommendations

Exact field-by-field structure (labels, option sets) should be requested
from Atom if not already available — never guessed or invented.

## Roles
- **Intern** — intern/trainee psychologists. (The source paper form
  calls this role "volunteer" — same people, corrected naming.) Limited
  access, likely restricted to their own patients/entries.
- **Psychologist** — full clinical access.
- **Coordinator** — oversees and coordinates the program (a senior
  clinical role); broad read access across patients and staff.
- **Admin** — system/account management. Scope still open: possibly a
  clinical admin (coordinator doubling up) vs. a technical admin
  (IT-only, minimal clinical data exposure). Build as a role distinct
  from `coordinator` regardless of how that's ultimately resolved.

All role-based access must be enforced at the **database level**
(Postgres Row-Level Security) — never through frontend hiding alone.
This matters: a frontend bug or bypass must never expose data a role
shouldn't see.

## hosting & tech stack (local first)
- **Frontend:** Next.js (App Router) + TypeScript, Tailwind CSS,
  shadcn/ui (built on Radix UI primitives), TanStack Table + TanStack
  Query, cmdk (command palette / search), React Hook Form + Zod, Framer
  Motion, Lucide icons.
- **Backend/DB:** Self-hosted Supabase — PostgreSQL + GoTrue (auth) +
  Realtime + Storage + PostgREST (auto-generated API) — run together via
  Docker Compose.
- **Hosting:** A single on-premise server, on the institution's internal
  network only — no public internet exposure. Authorized remote access
  (e.g. for the coordinator) goes through a WireGuard VPN, never a public
  endpoint.
- **Why local, not cloud:** this system handles children's health and
  psychological data. Algerian law (Law 18-07, amended by Law 25-11 in
  2025) classifies health data as sensitive personal data. Local,
  on-premise hosting is the safer default for data control and
  residency, even though it demands more infrastructure work than a
  cloud-hosted MVP. **This decision is final** unless Atom explicitly
  reopens it — don't re-litigate cloud vs. local as part of unrelated
  tasks.

## Requirement: multilingual, Arabic RTL included (confirmed)
The source form is entirely in Arabic. The app must support multiple
languages — Arabic with full right-to-left layout included — from the
start. This is not something to retrofit later:
- Architect for RTL from day one: Tailwind's RTL utilities, logical CSS
  properties instead of directional ones, RTL-aware behavior across
  Radix, TanStack, and cmdk.
- Use a real i18n solution from the start (e.g. `next-intl`), never
  hardcoded UI strings.
- The exact language set and default language are still to be confirmed
  — architecture should not block on that answer, but should be ready
  for it.

## UI specification
Visual direction throughout: **Notion/Linear-style** — clean, low visual
noise, muted neutral palette, generous spacing, content-first. Every
screen below must work correctly mirrored for RTL — not as a bolted-on
separate mode.

**Global shell** — sidebar (collapsible on tablet, becomes a
hamburger/bottom nav on phone): Home, Logs, Patients, Psychologists/
Interns (role-gated), Personal Info, Settings. Top bar: search trigger
(opens the cmdk command palette), current user's avatar/name, language
switcher.

1. **Login** — centered card, logo, email + password fields, single
   primary button, language switcher visible. No sidebar — this screen's
   only job is getting people in fast, including non-technical staff.
2. **Home / Dashboard** — stat cards (active patients, sessions logged
   this week, patients flagged as needing support) pulled from a
   Postgres view, small charts where a bare number isn't enough.
   "Patients needing attention" list (avatar, name, one-line reason) →
   opens the patient profile. Role-relevant "Your tasks" list where
   applicable.
3. **Logs** — chronological activity feed: actor, action verb
   (added/edited/deleted), target, timestamp, expandable diff for edits.
   Filterable by user/action/date. Streamed live via Supabase Realtime.
   Role-scoped — interns likely see only logs touching patients they can
   access, not the full feed.
4. **Patients list** — grouped, Discord-forum style (by status, e.g.
   Active / Needs Support / Completed, or by ward/room), collapsible
   sections, each row = avatar, name, age, status badge, last session
   date. cmdk-powered live search across name/room/status. Click a row →
   opens the patient profile.
5. **Patient profile** — near-fullscreen `Dialog` on desktop (rounded
   corners, backdrop blur, Framer Motion slide/scale-in); fullscreen
   `Sheet` on mobile, same content. Header: avatar, name, age, room,
   status badges. Tabs matching the four form sections (Educational /
   Psychological / Health / Volunteer notes) — latest entry shown
   prominently, small expandable history beneath. Role-gated per-patient
   change log. Prominent "+ New Session" button opens the session form
   (React Hook Form + Zod), matching the paper form's fields, pre-filled
   with patient identity.
6. **Psychologists/Interns list** (role-gated: coordinator/admin) — same
   list pattern as Patients: avatar, name, role badge, assigned patient
   count, last active. Click → their profile, assigned patients, their
   own activity log.
7. **Personal Info** — own avatar/name/contact details, editable.
   Personal stats: sessions logged, patients followed, activity over
   time.
8. **Settings** (role-gated, likely admin) — user management
   (invite/remove/change roles), retention-policy settings, language/
   notification preferences.

## Legal context (Algeria)
This system handles children's health and psychological data. Algeria's
Law 18-07 (amended by Law 25-11, 2025) treats health data as sensitive
personal data, with requirements around lawful processing, security
measures, and — likely, still being researched — declaration to the
ANPDP (National Authority for Personal Data Protection). **This is not
settled by AI judgment** — the institution should confirm exact
obligations with local legal counsel before handling real patient data.
Already factored into the design regardless:
- A parental consent step (can be paper-based, referencing the digital
  system)
- A defined data retention policy (how long a child's record is kept
  after leaving the program)
- Data minimization — the system should only collect what the paper form
  already asks for, nothing extra "just in case"

## Team structure
This project is built by a small team of AI agents, each a **separate,
independent session** with no shared memory between them and no direct
communication with each other. The project owner is the only line of
communication — every prompt, task, and report passes through them.

- **Atom** (Claude) — project manager and prompt/context engineer. Holds
  the full product picture, resolves cross-cutting decisions, writes
  complete prompts for Kernel and Raven. See `Claude/Atom/Readme.md`.
- **Kernel** (Claude) — senior developer. Turns Atom's direction into
  technical architecture, writes complete prompts for the Grok
  developers. See `Claude/Kernel/Readme.md`.
- **Raven** (Claude) — researcher. Investigates legal, technical, and
  best-practice questions and reports sourced findings. See
  `Claude/Raven/Readme.md`.
- **Nexus** (Grok) — backend developer.
- **Prism** (Grok) — frontend developer.
- **Sentry** (Grok) — security engineer, vulnerability review.

Because no agent retains memory across sessions, **this README plus each
agent's own role README are the entire shared context of the project**.
Any current task/prompt should point back here rather than repeat this
content — if something important isn't written down in this repo, it
effectively doesn't exist for the next session.

## Repo structure
```
Project-Hope
├─ Claude
│  ├─ Atom     (project manager — Readme.md explains role in detail)
│  ├─ Kernel   (senior developer)
│  └─ Raven    (researcher)
├─ Grok
│  ├─ Nexus    (backend)
│  ├─ Prism    (frontend)
│  └─ Sentry   (security)
├─ Project     (shared/versioned context artifacts)
└─ Readme.md   (this file)
```

## Changelog
- **v1.0** — initial consolidated context: roles finalized, Option A
  (local-first) locked in, multilingual/RTL confirmed, UI spec
  finalized.
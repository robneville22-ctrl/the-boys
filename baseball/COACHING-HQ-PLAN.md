# Coaching HQ — Architecture Plan for Yeager Baseball Portal

> Technical plan for adding coaching tools to the Yeager Baseball Portal. Designed for Rob's 9U team initially, but built so any Yeager coach can use it.
>
> **Portal:** LIVE at https://yeager-baseball.vercel.app
> **Database:** PostgreSQL on shared Supabase (18 `yb_` tables + 9 enums)
> **Auth:** Magic link only (password + OAuth removed)
>
> Last updated: 2026-03-24

---

## Phase 0 — SQLite → PostgreSQL Migration ✅ COMPLETE

Completed 2026-03-23. The portal is now running PostgreSQL on the shared Supabase instance.

### What was done
- Rewrote all 18 tables from `sqliteTable` → `pgTable` in `drizzle/schema.ts`
- All tables prefixed with `yb_` (shares Supabase with ATS Pick'Em + Rob's OS)
- Converted: booleans (integer → real boolean), timestamps (integer → timestamp), enums (text → pgEnum)
- Swapped `better-sqlite3` → `postgres` (postgres.js driver)
- Schema pushed to live Supabase via MCP (6 migrations, all 18 tables confirmed)
- Deployed to Vercel with Build Output API v3 (esbuild-bundled serverless function)
- Magic link auth consolidated (password auth + OAuth removed by Codex C5/C6)
- Admin routes hardened with `adminProcedure` (Codex C1)
- 12 tests passing, 1 skipped (DB-backed tests hit live Supabase)

### Current infrastructure
- **Hosting:** Vercel (auto-deploys from `main` branch)
- **Database:** Supabase PostgreSQL (pooler URL, same instance as other projects)
- **Build:** `scripts/build-vercel.mjs` — Vite frontend + esbuild API bundle → Build Output API v3
- **API:** Single serverless function wrapping Express (tRPC + 3 custom routes)
- **Auth:** Admin cookie auth + parent magic link today; moving to unified magic-link accounts/roles per `Yeager Baseball/REDESIGN.md`
- **Email:** Gmail SMTP via nodemailer (auth verified, end-to-end delivery not yet confirmed)

---

## Overview

Add a `/coaching/*` section to the Yeager Baseball Portal with a dedicated dashboard and tools inside the unified role-based portal. Coaches become another role in the shared auth system rather than a separate auth silo.

---

## Phase A — Foundation ✅ SUPERSEDED BY UNIFIED PORTAL REDESIGN

> **UPDATE (3/23):** Phase A's separate coach auth system has been replaced by a unified portal redesign. See `Yeager Baseball/REDESIGN.md` for the full plan.
>
> Instead of 3 separate auth systems (admin, parent, coach), the portal will use **one `yb_accounts` table** with a `roles` column. Coach auth is just another role — no separate tables needed.
>
> The separate `yb_coachAccounts`, `yb_coachSessions`, `yb_coachLoginTokens` tables below are **no longer needed**.

### What Changed
- Single `/login` page for everyone (not `/coaching/login`)
- Single `yeager_session` cookie (not `yeager_coach_session`)
- `yb_accounts.roles` = `"coach"` or `"admin,coach"` (not separate tables)
- `coachProcedure` middleware reads `coachId` from the unified account
- Coach features live at `/coaching/*` within the shared `PortalLayout` sidebar

### Original Plan (kept for reference)

The original plan called for separate coach auth tables mirroring the parent system. This was reasonable when the portal had separate login flows, but the unified redesign makes it unnecessary.

**Deliverable (unchanged):** Coach can log in and see their coaching dashboard.

---

## Phase B — Player Profiles + Game Notes (Highest Value) — PARTIALLY COMPLETE

> **Status (3/24):** Player roster page and seed script DONE. 12 players imported from `roster.md` with full stat lines, attention levels, strengths, weaknesses, coaching notes. Route live at `/coaching/players`. Game notes UI still TODO.

### Player Development Profiles
The coach's working view of their roster. Separate from the `yb_registrations` table (different purpose — registration is legal/admin data, this is the coach's working view).

```
yb_coachingPlayers
├── id (PK, serial)
├── coachId → yb_coaches.id
├── name
├── jerseyNumber
├── position (primary)
├── strengths (text)
├── weaknesses (text)
├── currentFocus (what to work on NOW)
├── notes (general)
├── attentionLevel ("low" / "medium" / "high")
├── createdAt
└── updatedAt
```

### Game Notes
One record per game, with per-player breakdowns.

```
yb_gameNotes
├── id (PK, serial)
├── coachId → yb_coaches.id
├── gameDate
├── opponent
├── result ("win" / "loss" / "tie")
├── ourScore
├── theirScore
├── summary (text)
├── keyObservations (JSON array stored as text)
├── areasToImprove (JSON array stored as text)
├── audioTranscriptUrl (S3 link to Plaud transcript)
├── createdAt
└── updatedAt

yb_gamePlayerNotes
├── id (PK, serial)
├── gameNoteId → yb_gameNotes.id
├── playerId → yb_coachingPlayers.id
├── observations (text)
├── areasToImprove (text)
└── createdAt
```

**New routes:**
- `/coaching/players` — Card grid of roster
- `/coaching/players/:id` — Full player profile + game-by-game timeline
- `/coaching/games` — Game notes list
- `/coaching/games/new` — Create game notes (from Plaud transcript or manual)
- `/coaching/games/:id` — Game note detail view

**Deliverable:** Coach can manage player profiles, record game notes, and see per-player timelines.

---

## Phase C — Drill Library + Practice Plans — ✅ COMPLETE

### Drill Library
Reusable drill definitions. Some are global (seeded), some are coach-created.

```
yb_drills
├── id (PK, serial)
├── name
├── description (how to run it)
├── category ("hitting" / "fielding" / "baserunning" / "pitching" / "catching" / "warmup")
├── durationMinutes
├── equipment (comma-separated)
├── minAge / maxAge
├── coachId (null = global, otherwise coach-specific)
├── createdAt
└── updatedAt
```

### Practice Plans
Structured plans with time-allocated stations.

```
yb_practicePlans
├── id (PK, serial)
├── coachId → yb_coaches.id
├── practiceDate
├── title
├── durationMinutes
├── notes
├── createdAt
└── updatedAt

yb_practicePlanStations
├── id (PK, serial)
├── practicePlanId → yb_practicePlans.id
├── drillId → yb_drills.id (nullable for ad-hoc)
├── stationName
├── durationMinutes
├── sortOrder
├── focusPlayerIds (JSON array)
├── equipment
└── notes
```

**New routes:**
- `/coaching/drills` — Filterable drill library (category tabs)
- `/coaching/practice` — Practice plans list
- `/coaching/practice/new` — Practice plan builder (drag drills, set times, tag players)
- `/coaching/practice/:id` — Practice plan detail

**Key feature:** `duplicate` mutation — copy an existing practice plan to a new date and tweak it. Coaches reuse structures week to week.

**Seed data:** All 24 drills seeded into `yb_drills` via `scripts/seed-drills.ts`. ✅

> **Status (3/24):** All Phase C UI pages and seed scripts DONE.
> - `/coaching/drills` — Drill library with category filters + search (DrillLibrary.tsx)
> - `/coaching/practice` — Practice plans list with duplicate/delete (PracticePlans.tsx)
> - `/coaching/practice/:id` and `/coaching/practice/new` — Plan builder with station management (PracticePlanDetail.tsx)
> - `scripts/seed-drills.ts` — 24 drills seeded from drill-library.md

---

## Phase D — Stats Import + Dashboard Polish

### Stats Import
Upload GameChanger CSV exports, parse server-side, store as JSON blob.

```
yb_statImports
├── id (PK, serial)
├── coachId → yb_coaches.id
├── filename
├── s3Key
├── importType ("batting" / "pitching")
├── seasonYear
├── parsedData (JSON blob)
└── importedAt
```

**Why JSON blob instead of normalized tables?** GameChanger CSV formats vary. Parsing into JSON that the frontend renders as a table is fastest to ship. Normalize later if we need cross-game analytics.

**New routes:**
- `/coaching/stats` — Upload CSV + view past imports as rendered tables

### Season Dashboard
The `/coaching` home page aggregates everything:
- Win/loss record
- Last 5 game results
- Players flagged as "high attention"
- Next practice plan
- Quick links: add game notes, create practice plan, upload stats

---

## tRPC Router Structure

New file: `server/coaching-router.ts`

```
coaching.auth
├── requestMagicLink (public)
├── verifyMagicLink (public)
├── me (public, returns coach or null)
└── logout

coaching.players (coachProcedure)
├── list
├── getById
├── create
├── update
└── delete

coaching.gameNotes (coachProcedure)
├── list
├── getById (includes gamePlayerNotes)
├── create (with player notes array)
├── update
└── delete

coaching.drills (coachProcedure)
├── list (global + own, filterable by category)
├── getById
├── create
├── update (own only)
└── delete (own only)

coaching.practicePlans (coachProcedure)
├── list
├── getById (includes stations with drill details)
├── create (with stations array)
├── update
├── duplicate (copy to new date)
└── delete

coaching.stats (coachProcedure)
├── upload (parse CSV server-side)
├── list
├── getById
└── delete

coaching.dashboard (coachProcedure)
└── overview (aggregated data)
```

---

## Page Components

All in `client/src/pages/coaching/`:

| Component | Route | Purpose |
|-----------|-------|---------|
| CoachLogin | /coaching/login | Magic link email form |
| CoachVerify | /coaching/verify | Token validation redirect |
| CoachDashboard | /coaching | Season overview cards |
| PlayerList | /coaching/players | Roster card grid |
| PlayerProfile | /coaching/players/:id | Full profile + game timeline |
| GameNotesList | /coaching/games | Game notes table |
| GameNoteForm | /coaching/games/new | Create/edit game notes |
| GameNoteDetail | /coaching/games/:id | Read view with player notes |
| DrillLibrary | /coaching/drills | Filterable drill cards |
| PracticePlansList | /coaching/practice | Plans list with duplicate action |
| PracticePlanBuilder | /coaching/practice/new | Build plan with drill stations |
| PracticePlanDetail | /coaching/practice/:id | View plan detail |
| StatsImport | /coaching/stats | CSV upload + rendered tables |

Shared: `CoachingLayout.tsx` (sidebar nav) + `CoachAuthGuard.tsx` (session check)

---

## Prerequisites
1. ✅ **Database on PostgreSQL** — Done. 18 `yb_` tables live on shared Supabase.
2. ✅ **Deployed to Vercel** — Done. Auto-deploys from `main`.
3. ✅ **Magic link auth pattern proven** — Parent magic link works in prod. Coach auth will clone this pattern.
4. ⚠️ **Email end-to-end delivery** — SMTP auth verified but nobody has confirmed a real email arrives in an inbox yet. Must verify before coach magic links will work.
5. **Rob's coach email must be set** in the `yb_coaches` table
6. **S3 access** — Already configured (used for birth certificates)

## Design Decisions
- **Separate coach auth from admin auth** — Different roles, different permissions. A coach can't accidentally access admin functions.
- **`yb_coachingPlayers` is separate from `yb_registrations`** — Registration is legal/admin data. Coaching players is the coach's working roster view.
- **Magic link over password** — Only ~13 coaches. Simpler, more secure, matches parent pattern (password auth was already removed from the portal in C5/C6).
- **JSON blobs for flexible data** — Stats, observations, and improvement areas stored as JSON text. Avoids premature schema complexity. PostgreSQL's native JSON support makes this cleaner than the old SQLite text approach.
- **Practice plan duplication** — Coaches reuse plans weekly. One-click copy to new date.
- **`yb_` table prefix** — All Yeager Baseball tables use this prefix to coexist with Rob's OS and ATS Pick'Em tables in the shared Supabase instance.

## Relationship to Coaching HQ (this repo)

The markdown-based Coaching HQ in `the-boys/baseball/` and the Yeager Baseball Portal serve **different purposes**:

| | Coaching HQ (this repo) | Yeager Portal |
|---|---|---|
| **Audience** | Rob only | All coaches, parents, admins |
| **Format** | Markdown files + Claude Code | Web app (React + tRPC) |
| **Data** | Plaud transcripts, CSVs, notes | Database (PostgreSQL) |
| **Best for** | Quick capture, AI processing | Shared access, structured data |

**Keep them separate for now.** The markdown system is faster for Rob's personal workflow. When the portal's coaching features are built (Phases A-D above), the portal becomes the shared version that any Yeager coach can use — and the markdown system stays as Rob's personal notebook / AI processing pipeline.

**Migration path:** When Phase B is built, Rob can optionally import his existing player profiles and game notes from the markdown files into the portal's database. The markdown files remain the source of truth until then.

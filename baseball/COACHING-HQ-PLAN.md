# Coaching HQ — Architecture Plan for Yeager Baseball Portal

> Technical plan for adding coaching tools to the Yeager Baseball Portal. Designed for Rob's 9U team initially, but built so any Yeager coach can use it.
>
> **Important:** The Yeager Baseball Portal uses **SQLite** (via Drizzle ORM's `sqliteTable`), not PostgreSQL. All table definitions below should use `sqliteTable`, `integer`, and `text` imports from `drizzle-orm/sqlite-core`. The existing schema pattern uses integer timestamps with `{ mode: "timestamp" }`.

---

## Overview

Add a `/coaching/*` section to the Yeager Baseball Portal with its own auth, dashboard, and tools. Coaches log in via magic link (like parents already do), and get a dedicated workspace for managing their team.

---

## Phase A — Foundation (Build First)

### Coach Authentication
Mirrors the parent auth pattern (magic link → session cookie). Coaches already exist in the `coaches` table with email addresses.

**New tables:**

```
coachAccounts
├── id (PK)
├── coachId → coaches.id
├── email (unique)
├── createdAt
└── lastLoginAt

coachSessions
├── id (PK)
├── coachAccountId → coachAccounts.id
├── sessionToken (unique)
├── expiresAt (30 days)
└── createdAt

coachLoginTokens
├── id (PK)
├── email
├── token (unique, one-time-use)
├── coachId
├── expiresAt (15 min)
├── usedAt
└── createdAt
```

**Auth flow:**
1. Coach visits `/coaching/login`, enters email
2. Server checks `coaches` table — if found and active, sends magic link
3. Coach clicks link → session created → `yeager_coach_session` cookie set
4. All coaching routes protected by `coachProcedure` middleware

**New routes:**
- `/coaching/login` — Email input
- `/coaching/verify?token=xxx` — Magic link landing
- `/coaching` — Dashboard (after login)

**Deliverable:** Coach can log in and see an empty dashboard.

---

## Phase B — Player Profiles + Game Notes (Highest Value)

### Player Development Profiles
The coach's working view of their roster. Separate from the registration table (different purpose).

```
coachingPlayers
├── id (PK)
├── coachId → coaches.id
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
gameNotes
├── id (PK)
├── coachId → coaches.id
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

gamePlayerNotes
├── id (PK)
├── gameNoteId → gameNotes.id
├── playerId → coachingPlayers.id
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

## Phase C — Drill Library + Practice Plans

### Drill Library
Reusable drill definitions. Some are global (seeded), some are coach-created.

```
drills
├── id (PK)
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
practicePlans
├── id (PK)
├── coachId → coaches.id
├── practiceDate
├── title
├── durationMinutes
├── notes
├── createdAt
└── updatedAt

practicePlanStations
├── id (PK)
├── practicePlanId → practicePlans.id
├── drillId → drills.id (nullable for ad-hoc)
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

**Seed data:** ~24 drills from the drill-library.md already written.

---

## Phase D — Stats Import + Dashboard Polish

### Stats Import
Upload GameChanger CSV exports, parse server-side, store as JSON blob.

```
statImports
├── id (PK)
├── coachId → coaches.id
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
1. **Email must work** — Magic link auth requires SMTP. This is already top priority in TASKS.md.
2. **Rob's coach email must be set** in the `coaches` table
3. **S3 access** — Already configured (used for birth certificates)

## Design Decisions
- **Separate coach auth from admin auth** — Different roles, different permissions. A coach can't accidentally access admin functions.
- **`coachingPlayers` is separate from `registrations`** — Registration is legal/admin data. Coaching players is the coach's working roster view.
- **Magic link over password** — Only ~13 coaches. Simpler, more secure, matches parent pattern.
- **JSON blobs for flexible data** — Stats, observations, and improvement areas stored as JSON text. Avoids premature schema complexity.
- **Practice plan duplication** — Coaches reuse plans weekly. One-click copy to new date.

# The Brothers Arcade + Coaching HQ

## What This Is
Two things in one repo:
1. **The Brothers Arcade** — 10-game HTML5 sports arcade (`index.html`). Built for Rob's boys. All games in a single HTML file with vanilla JS, no dependencies.
2. **Coaching HQ** — Rob's command center for coaching his son Grayson's 9U travel baseball team (Jaegers, Yeager Baseball org, Cincinnati OH).

## Project Structure
```
the-boys/
├── index.html          ← The Brothers Arcade (all 10 games, ~3800 lines)
├── SKILL.md            ← Design taste enforcement (from robs-os)
├── CLAUDE.md           ← You are here
├── .gitignore
└── baseball/           ← Coaching HQ (see baseball/COACHING-HQ.md for full details)
    ├── COACHING-HQ.md          ← Master command center, start here
    ├── COACHING-HQ-PLAN.md     ← Yeager Baseball Portal integration plan
    ├── drill-library.md        ← 24 drills with web references
    ├── season-analytics.md     ← Power rankings, tiers, splits
    ├── pitch-count-tracker.md  ← Arm health tracking
    ├── game-notes/             ← One file per game (from Plaud transcripts)
    ├── game-prep/              ← Pre-game scouting & lineup plans
    ├── player-profiles/        ← roster.md — living doc, updated after each game
    ├── practice-plans/         ← Structured practice plans
    ├── stats/                  ← GameChanger CSV exports
    ├── lineups/                ← Game day lineup spreadsheets
    └── templates/              ← Reusable templates for game notes, practice, prep
```

## The Brothers Arcade
- Single `index.html` file, no build tools, no dependencies
- 11 games: Baseball, Football (Pass/Run/Defense/Coverage), Basketball, Soccer, Math Challenge, Running, Dodgeball, Volleyball
- High score dashboard with localStorage persistence
- Responsive canvas-based games with HUD overlay
- Font: Outfit (Google Fonts)
- Color scheme: Dark (#0f1117 bg), red accent (#e53935)

## Coaching HQ
Full documentation in `baseball/COACHING-HQ.md`. Key workflow:
1. Record games with Plaud Note Pin S
2. Export Plaud transcript + GameChanger CSVs
3. Paste into Claude Code → auto-generates game notes, player updates, practice plans, game prep

### Key Context
- **Team:** Jaegers 9U, Yeager Baseball (Cincinnati, OH)
- **Rob's son:** Grayson Neville (#1, 2B/C)
- **Best player:** Zach Martini (#21) — .667 AVG, 1.917 OPS
- **12 players total**, all tracked in `player-profiles/roster.md`
- **Season:** Spring 2026, 3 games played through 3/22
- **Tools:** Plaud Note Pin S (game recordings), GameChanger (live stats), Claude Code (processing)

### Processing Game Notes
When Rob says "process game notes" with a Plaud transcript:
1. Create game notes file from `templates/post-game-template.md`
2. Update `player-profiles/roster.md` with per-player observations
3. Update `season-analytics.md` with new metrics
4. Update `pitch-count-tracker.md` with pitch counts
5. Create next practice plan from `templates/practice-plan-template.md`
6. Create next game prep from `templates/game-prep-template.md`
7. Update `COACHING-HQ.md` season record and team stats

## Yeager Baseball Portal (Separate Repo)
The Yeager Baseball Portal is a separate web app at `/Users/Rob/Projects/Yeager Baseball/`, LIVE at https://yeager-baseball.vercel.app. It handles registration, parent portal, admin dashboard, and schedule for the whole Yeager org.

The coaching HQ markdown system in `baseball/` stays **separate** from the portal — different audiences, different UX. See `baseball/COACHING-HQ-PLAN.md` for the phased integration plan (Phase 0 done, Phases A-D planned but not started).

## Conventions
- Keep arcade games in the single index.html (no splitting)
- Baseball files use markdown — designed for Claude Code processing, not a web UI
- Player jersey numbers are consistent across all files
- Stats come from GameChanger CSVs — always use those as source of truth
- Drill references use the numbered system from `drill-library.md` (e.g., #14 = Primary Lead & Steal Break)
- Coaching tone: positive, fun-first. Read Rob's coaching philosophy in COACHING-HQ.md.

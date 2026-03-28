# Jaegers 9U — Coaching HQ

> Rob's command center for the 2026 spring season. Combines Plaud game recordings, GameChanger stats, and coaching observations into one system.

## How This Works

### After Every Game (Repeatable Process)
1. **Record with Plaud Note Pin S** — wear it during the game, capture everything
2. **Capture photos/videos** — team photo, big plays, dugout energy → drop into `media/photos/` and `media/videos/`
3. **Export Plaud summary** — text export, drop into `game-notes/` folder (or paste transcript into Claude Code)
4. **Export GameChanger stats** — download updated batting/pitching CSVs into `stats/`
5. **Run through Claude Code** — paste transcript + say "process game notes" → auto-generates:
   - Game summary in `game-notes/YYYY-MM-DD-event.md` (from `templates/post-game-template.md`)
   - Updated player profiles in `player-profiles/roster.md`
   - Updated `season-analytics.md` with new power rankings and metrics
   - Updated `pitch-count-tracker.md` with game pitch counts
   - Next practice plan in `practice-plans/YYYY-MM-DD-day.md` (from `templates/practice-plan-template.md`)
   - Game prep for next opponent in `game-prep/YYYY-MM-DD-opponent.md` (from `templates/game-prep-template.md`)
   - Updated season record and team stats in this file

### Folder Structure
```
baseball/
├── COACHING-HQ.md              ← You are here
├── COACHING-HQ-PLAN.md         ← Technical plan for Yeager Baseball Portal integration
├── drill-library.md            ← 24 named drills with references + practice templates
├── season-analytics.md         ← Power rankings, tiers, splits, key metrics
├── pitch-count-tracker.md      ← Arm health tracking + availability
├── game-notes/                 ← One file per game
│   └── 2026-03-22-bracket-play.md
├── game-prep/                  ← Pre-game scouting & lineup planning
│   └── 2026-03-25-raiders.md
├── player-profiles/
│   └── roster.md               ← Living doc, updated after each game
├── practice-plans/
│   └── 2026-03-24-tuesday.md
├── stats/                      ← GameChanger CSV exports (current season only)
│   ├── batting-2026-spring.csv
│   └── pitching-2026-spring.csv
├── lineups/                    ← Game day lineup spreadsheets
│   └── 2026-03-22-bracket-play.xlsx
├── media/                      ← Photos + videos for season collage
│   ├── photos/                 ← Game day photos, team pics
│   └── videos/                 ← Highlight clips, game footage
└── templates/                  ← Reusable templates (copy for each new game)
    ├── post-game-template.md
    ├── practice-plan-template.md
    ├── game-prep-template.md
    └── parent-update-template.md
```

## Season Record
| Game | Date | Opponent | Result | Score | Notes |
|------|------|----------|--------|-------|-------|
| 1 | 3/21 | TBD | — | — | First games of the season (bracket play day 1) |
| 2 | 3/21 | TBD | — | — | Bracket play day 1 game 2 |
| 3 | 3/22 | TBD | Tie | — | Ran out of time (1.5 hr limit). Were about to win. |

## Team Stats (Through 3 Games)
| Stat | Value | Note |
|------|-------|------|
| Team AVG | .308 | Solid for 9U |
| Team OBP | .514 | Elite — getting on base over half the time |
| Team OPS | .975 | Near 1.000 — very strong |
| Total Runs | 26 | Scoring well |
| Stolen Bases | 33 (97% rate) | Speed is a weapon |
| Team K Rate | 40.4% (21 K in 52 AB) | Too high — need more contact |
| BA/RISP | .217 | Improved from .067 — still work to do |
| Team ERA | 16.91 | Giving up too many runs — walks are the problem |
| Team WHIP | 3.455 | 18 BB in 11 IP — walks killing us |
| Fielding % | 1.000 | Perfect on recorded chances (0 errors) |

## Roster Quick Reference (Updated 3/22)

| # | Player | AVG | OBP | OPS | Key Stat | Status |
|---|--------|-----|-----|-----|----------|--------|
| 1 | Grayson Neville | .200 | .500 | 1.300 | 1 HR, 3 RBI | Hot — hit a bomb |
| 2 | Crew Powers | .600 | .667 | 1.467 | 0 K, 3 RBI | On fire |
| 3 | Lukas Adams | .600 | .667 | 1.267 | 5 SB, 2 HHB | Locked in |
| 6 | Porter Mills | .000 | .571 | .571 | 4 BB, 0 H | Walks machine, hitless |
| 9 | Alex Todd | .000 | .500 | .500 | 4 SB, 3 K | Patient but can't connect |
| 10 | Blake Lasita | .200 | .500 | .700 | 5 SB, 1st hit | First hit! Speed. |
| 11 | Mason Floyd | .000 | .200 | .200 | 3 K (2 looking) | Biggest concern |
| 15 | Charlie Ruther | .250 | .500 | .750 | .500 BA/RISP | Clutch, primary C |
| 17 | Owen Niemer | .000 | .200 | .200 | 4 K pitching | Can't hit, can pitch |
| 19 | Blake Fristoe | .500 | .500 | 1.250 | 1 2B, power | ON VACATION this week |
| 21 | Zach Martini | .667 | .750 | 1.917 | 1 3B, 0 K | Best player. THE guy. |
| 56 | Kayson Sander | .250 | .400 | .650 | 0 K, 1st hit | First hit! Improving. |

### Players Needing Most Attention
1. **Mason Floyd** — 0-for-4, 3 K (2 looking). Frozen at the plate. Needs confidence + timing work.
2. **Owen Niemer** — 0-for-4, 3 K. Can't hit at all. But has pitching upside (4 K in 1.1 IP).
3. **Alex Todd** — 0-for-3, 3 K. Patient (.500 OBP via walks) but 0% contact rate on swings.
4. **Porter Mills** — 0-for-3 hitting but .571 OBP. The walks are valuable but he needs to eventually hit.

### Players on Hot Streaks
1. **Zach Martini** — .667 AVG, 1.917 OPS, 0 strikeouts. Absurd.
2. **Crew Powers** — .600 AVG, 100% contact rate. Never strikes out.
3. **Lukas Adams** — .600 AVG, 5 SB. Scoring machine.
4. **Grayson Neville** — Hit a HOME RUN. .500 OBP. Trending up big time.

## Season Themes (Updated 3/22)

### Team Strengths
- Plate discipline — team .514 OBP is elite for 9U
- Speed — 97% stolen base rate (33 of 34)
- Contact from top of lineup — Zach, Crew, Lukas all .600+
- Pitching has strikeout potential — 14 K in 11 IP
- Perfect fielding percentage on recorded chances

### Team Weaknesses
- Base running IQ — getting caught in no man's land, not aggressive enough with secondaries
- Walks allowed — 18 BB in 11 IP. Pitchers giving away too many free bases.
- Bottom of lineup hitting — Mason, Owen, Alex all hitless. 9 combined Ks.
- Hitting with RISP — .217 BA/RISP (improved from .067 but still cold)
- Pace of play — not getting enough innings in time limit games

### Coaching Philosophy (Rob's Notes to Self)
- "You don't go to a symphony to hear the last note." — Enjoy the process.
- Keep it positive. No negativity. Your anxiety rubs off on the boys.
- Say as little as possible during the game. Let them communicate. Let them play.
- If parents have issues with the ump, they come to YOU. No chirping.
- Don't pull a kid for two bad pitches. This isn't the WBC. It's 9-year-old baseball.
- Every at-bat should be fun. Every defensive play should be fun. That's the whole point.
- Zach and Porter are the emotional leaders. Keep them up and the team follows.

## Rules Reminder (This League)
- No drop third strike
- Stealing is allowed (including home)
- Pitch count limit: ~55 pitches (can finish the batter if close)
- Watch for fatigue around 30 pitches
- Time limit: 1.5 hours per game (NEED to play faster to get more innings)

## Upcoming Schedule
- **Tue 3/24** — Practice (focus: base running, fielding, wiffle ball hitting)
- **Wed 3/25** — Game vs Cincinnati Raiders (Tim Teppy's team)
- **Weekend** — Likely tournament play (may see Raiders again)

## Shopping List
- [ ] Wiffle balls — variety pack (big + small)
- [ ] Two colors of small wiffle balls (white + yellow) for swing/don't swing drill
- [ ] Extra batting donut
- [ ] Strike zone target for pitching accuracy drill
- [ ] Tape roll for front foot direction drill

## Yeager Baseball Portal Integration

The portal is **LIVE** at https://yeager-baseball.vercel.app (deployed 3/23, PostgreSQL on Supabase, magic link auth). Full technical plan in `COACHING-HQ-PLAN.md`.

**What's done:**
- ✅ Phase 0: SQLite → PostgreSQL migration (18 `yb_` tables + 9 enums on shared Supabase)
- ✅ Vercel deployment with serverless API
- ✅ Parent magic link auth + coach login working (Rob logged in 3/25)
- ✅ Admin authorization hardened
- ✅ SKILL.md design system enforced (Outfit font, Phosphor icons, tinted shadows, 20+ files updated)
- ✅ Drill Library — 24 drills seeded from `drill-library.md` into portal DB, searchable UI at `/coaching/drills`
- ✅ Practice Plans — create/edit with station builder at `/coaching/practice`

**What's next:**
- **Player Roster page** — Data exists in `roster.md` (12 players), schema exists (`yb_coaching_players`), needs seed script + UI page at `/coaching/players`
- **Game Notes page** — Sidebar link exists but no UI yet
- **Stats import** — GameChanger CSVs ready, `yb_stat_imports` table exists
- **Deploy to production** — Coaching pages + design changes need to be pushed to Vercel

**This markdown system stays as Rob's personal coaching notebook.** The portal becomes the shared version for all Yeager coaches. No rush to merge — the markdown workflow is faster for Rob's AI-powered game processing.

## Open Brain Integration

Rob's "second brain" MCP server at `/Users/Rob/Projects/open-brain/`. Codex built a Plaud transcript import pipeline (3/24) that extracts structured notes from recordings and stores them with embeddings for semantic search.

**Status:** Code complete, NOT yet runnable — needs `.env` file with API keys.
**Next step:** Create `.env` → test with `--dry-run` on a Plaud transcript → `--commit` to start building the brain.
**How it connects:** Plaud game recordings can be imported into Open Brain for unstructured semantic search, while the structured game processing still flows through this Coaching HQ markdown system.

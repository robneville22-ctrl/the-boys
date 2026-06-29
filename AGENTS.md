# The Brothers Arcade + Coaching HQ — Agent Context

> Canonical context file (read by Claude Code, Codex, etc.). `CLAUDE.md` imports this.
> Two things in one repo: (1) **The Brothers Arcade** — a single-file HTML5 sports arcade Rob built with his sons; (2) **Coaching HQ** — Rob's command center for coaching his son's 9U travel baseball team (Yeager 9U, Cincinnati OH).

## Project structure
```
the-boys/
├── index.html          # The Brothers Arcade (all games, ~3800 lines)
├── SKILL.md            # Design-taste enforcement (from robs-os)
├── AGENTS.md           # this file (CLAUDE.md imports it)
└── baseball/           # Coaching HQ — see baseball/COACHING-HQ.md (start there)
    ├── COACHING-HQ.md / COACHING-HQ-PLAN.md   # command center + portal-integration plan
    ├── drill-library.md (24 drills) · season-analytics.md · pitch-count-tracker.md
    ├── game-notes/ · game-prep/ · player-profiles/ (roster.md) · practice-plans/
    ├── stats/ (GameChanger CSVs) · lineups/ · templates/
```

## The Brothers Arcade
- Single `index.html` — HTML/CSS/JS, **zero dependencies, no build step**. Hosted on GitHub Pages (push and play).
- ~11 games on an 800×500 HTML5 Canvas (2D `ctx`): Baseball, Football (Pass/Run/Defense/Coverage), Basketball, Soccer, Math, Running, Dodgeball, Volleyball. High-score dashboard via localStorage.
- **Per-game pattern:** `init[Game]()` sets up/resets state; `update[Game]()` runs each frame (draw, move, collisions); `click[Game](x,y)` handles input. State in a global object per game (`bb`, `fb`, `fr`, `fd`, `cv`, `bk`, `sc`, `mt`, `rn`, `db`, `vb`).
- **Routing in three places:** `startGame(game)` → right `init`; `update()` → right `update`; `handleClick()` → right `click`.
- **Add a game:** pick a 2-letter state var → write `initXx/updateXx/clickXx` → add routing in those three functions → add a `.game-buttons` menu button → add a setup overlay + picker if it needs one (like Math/Running).
- **Design:** dark (`#0f1117`), red accent (`#e53935`), Outfit font; HUD bar (score+timer) top, scoreboard panel right, game-over overlay with restart/menu.

## Coaching HQ
Full docs in `baseball/COACHING-HQ.md`. Team: **Yeager 9U** (Cincinnati). Rob's son Grayson (#1, 2B/C). 12 players tracked in `baseball/player-profiles/roster.md` (source of truth for names/numbers — don't duplicate the list elsewhere). Season: Spring 2026. Tools: Plaud Note Pin S (recordings), GameChanger (live stats), Claude Code (processing).

**When Rob says "process game notes" (with a Plaud transcript):**
1. Create a game-notes file from `templates/post-game-template.md`.
2. Update `player-profiles/roster.md` with per-player observations.
3. Update `season-analytics.md` (metrics) and `pitch-count-tracker.md` (pitch counts).
4. Create the next practice plan (`templates/practice-plan-template.md`) and game prep (`templates/game-prep-template.md`).
5. Update `COACHING-HQ.md` season record + team stats.

## Relationship to the Yeager Baseball Portal
The portal is a **separate** web app at `/Users/Rob/Projects/Yeager Baseball/` (LIVE: https://yeager-baseball.vercel.app) for registration/parent portal/admin/schedule across the whole org. The `baseball/` markdown coaching system stays separate (different audience/UX). Phased integration in `baseball/COACHING-HQ-PLAN.md` (Phase 0 done; A–D planned, not started).

## Conventions
- Keep arcade games in the single `index.html` (no splitting).
- Baseball files are markdown — designed for Claude Code processing, not a web UI.
- Jersey numbers consistent across all files. Stats come from GameChanger CSVs (source of truth).
- Drill references use the numbered system in `drill-library.md` (e.g., #14 = Primary Lead & Steal Break).
- Coaching tone: positive, fun-first (see philosophy in `COACHING-HQ.md`).

## Future ideas
**Arcade:** homework mode (paste math/spelling), per-game difficulty, same-keyboard multiplayer, more sports (hockey/tennis/golf), sound effects.
**Coaching:** Yeager Portal integration; Open Brain MCP semantic search over coaching observations; automated lineup generator (availability + stats); tournament bracket predictor.

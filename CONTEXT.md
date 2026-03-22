# The Boys

Everything for Rob's sons — games, baseball stats, lineups, and whatever else comes up.

## What's In Here

### 1. The Brothers Arcade (`index.html`)
A single-file HTML5 Canvas sports arcade game built by Rob with his sons. Designed to be fun, expandable, and educational. Hosted on GitHub Pages.

## Tech

- **Single file**: `index.html` — everything lives here (HTML, CSS, JS)
- **No dependencies**: Zero npm, no build step, no frameworks
- **HTML5 Canvas**: All games render on an 800x500 canvas with 2D context (`ctx`)
- **Hosting**: GitHub Pages (static file, just push and play)

## How It Works

Each game follows the same pattern:
- `init[Game]()` — sets up state object and resets everything
- `update[Game]()` — runs every frame (draws background, moves things, checks collisions)
- `click[Game](x, y)` — handles mouse/tap input
- State lives in a global object (`bb`, `fb`, `fr`, `fd`, `bk`, `sc`, `mt`, `rn`, `db`, `vb`)

Routing happens in three places:
- `startGame(game)` — calls the right `init` function
- `update()` — calls the right `update` function each frame
- `handleClick()` — routes clicks to the right `click` function

## Current Games

1. **Baseball** (`bb`) — batting game with pitcher and infielders
2. **Football Pass** (`fb`) — QB with receivers, OL blocking, defenders
3. **Football Run** (`fr`) — running back dodges defenders to end zone
4. **Football Defense** (`fd`) — play as defender, tackle the runner
5. **Football Coverage** (`cv`) — play CB, cover WR routes, break up passes
6. **Basketball** (`bk`) — move + shoot with shot meter, teammates + defenders
7. **Soccer** (`sc`) — dribble + shoot with power meter, goalie + defenders
8. **Math** (`mt`) — pick operation + time limit, vertical problem display, 4 choices
9. **Running** (`rn`) — hold-to-run sprint races, pick 50m/100m/150m
10. **Dodgeball** (`db`) — two teams, throw + dodge
11. **Volleyball** (`vb`) — beach volleyball, bump/set/spike

## Adding a New Game

1. Pick a 2-letter state variable (e.g., `let xx = {};`)
2. Write `initXx()`, `updateXx()`, `clickXx()` functions
3. Add routing in `startGame()`, `update()`, and `handleClick()`
4. Add a menu button in the HTML `.game-buttons` div
5. If it needs a setup screen (like math or running), add an overlay div + picker function

## Design

- Dark theme (#0f1117 background)
- Red accent (#e53935)
- Outfit font (Google Fonts)
- Consistent HUD bar (score + timer) at top
- Scoreboard panel on the right
- Game-over overlay with restart/menu buttons

## Future Ideas (Arcade)

- Homework mode: paste in math problems or spelling words
- Custom difficulty settings per game
- Multiplayer (two players on same keyboard)
- More sports: hockey, tennis, golf
- Sound effects

### 2. Coaching HQ (`baseball/`)

Full coaching command center for Jaegers 9U (Yeager Baseball, Cincinnati OH) — Spring 2026 season. See `baseball/COACHING-HQ.md` for the complete system and `CLAUDE.md` for processing instructions.

**Roster (12 players):** Grayson Neville (#1), Crew Powers (#2), Lukas Adams (#3), Porter Mills (#6), Alex Todd (#9), Blake Lasita (#10), Mason Floyd (#11), Charlie Ruther (#15), Owen Niemer (#17), Blake Fristoe (#19), Zachary Martini (#21), Kayson Sander (#56)

**What's in here:**
- Game notes (from Plaud Note Pin S recordings)
- Player development profiles (updated after each game)
- Practice plans (with drill references)
- Game prep / scouting reports
- Season analytics (power rankings, tiers, splits)
- Pitch count tracker (arm health)
- Drill library (24 drills with web references)
- GameChanger CSV stat exports
- Lineup spreadsheets
- Reusable templates for all document types
- Architecture plan for Yeager Baseball Portal integration

**Repeatable workflow:**
1. Record game with Plaud Note Pin S
2. Export Plaud transcript + GameChanger CSVs
3. Paste into Claude Code → auto-generates all coaching docs

## Future Ideas

### Arcade
- Homework mode: paste in math problems or spelling words
- Custom difficulty settings per game
- Multiplayer (two players on same keyboard)
- More sports: hockey, tennis, golf
- Sound effects

### Baseball / Coaching
- Integration with Yeager Baseball Portal (see `baseball/COACHING-HQ-PLAN.md`)
- Open Brain MCP integration for semantic search across coaching observations
- Automated lineup generator based on availability + stats
- Tournament bracket predictor

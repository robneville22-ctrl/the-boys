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
5. **Basketball** (`bk`) — move + shoot with shot meter, teammates + defenders
6. **Soccer** (`sc`) — dribble + shoot with power meter, goalie + defenders
7. **Math** (`mt`) — pick operation + time limit, vertical problem display, 4 choices
8. **Running** (`rn`) — hold-to-run sprint races, pick 50m/100m/150m
9. **Dodgeball** (`db`) — two teams, throw + dodge
10. **Volleyball** (`vb`) — beach volleyball, bump/set/spike

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

### 2. Yeager Baseball (`baseball/`)

Stats, lineups, and game planning for Yeager 9U (Spring 2026) and historical data from 8U (Spring 2025). Same 12 players both seasons.

**Roster:** Grayson Neville, Crew Powers, Lukas Adams, Porter Mills, Alex Todd, Blake Lasita, Mason Floyd, Charlie Ruther, Owen Niemer, Blake Fristoe, Zachary Martini, Kayson Sander

**Folder structure:**
```
baseball/
  stats/
    batting-2025-spring.csv    # Full season 8U stats (27 games)
    pitching-2025-spring.csv   # Full season 8U pitching
    batting-2026-spring.csv    # Current season 9U (running)
    pitching-2026-spring.csv   # Current season 9U pitching
  lineups/
    2026-03-22-bracket-play.xlsx   # Bracket play lineups (B1 + B3)
```

**How lineup files work:**
- Each Excel file has one sheet per game
- Each sheet has: batting order, pitching plan, field positions by inning, bench rotation
- Bench rules: max 2 sits per player per game, never back-to-back
- Download fresh stats CSVs from GameChanger (Export button on team stats page)

**How to build a new lineup:**
1. Export latest stats from GameChanger
2. Drop CSVs into `baseball/stats/`
3. Ask Claude to analyze pitching tiers + batting order + bench rotation
4. Save the `.xlsx` to `baseball/lineups/YYYY-MM-DD-event-name.xlsx`

## Future Ideas (Baseball)

- Season-long pitch count tracker
- Player development trends (compare 2025 vs 2026 stats)
- Automated lineup generator based on who's available
- Tournament bracket predictor

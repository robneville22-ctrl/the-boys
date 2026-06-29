# TourneyMachine: Platform Critique & Cincinnati-Area 9U Tournaments (May–June 2026)

*Researched April 9, 2026 — Live team count data pulled directly from TourneyMachine by clicking through every tournament page*

---

## Part 1: TourneyMachine — What It Is and Why It's Frustrating

TourneyMachine (now rebranded as **SportsEngine Tourney** after being acquired) is the dominant tournament management platform for youth baseball. Organizers use it to publish tournaments, collect registrations, set schedules, and post results. For coaches and parents, it's supposed to be a discovery tool — but that's where it falls apart.

### What the search actually does

The homepage has a single text box: *"Search by Tournament/League Name, Sport, City, State, Month."* This sounds like it has filters baked in. It does not. There are no actual filter controls. It's one box, and the results come from a text match against tournament names and locations in their database. Here's the proof:

- Typing `baseball Cincinnati` → Shows a dropdown of Cincinnati-area tournaments. ✅ Works.
- Typing `baseball Cincinnati May` → **"NO MATCHING TOURNAMENTS FOUND. Please expand your search criteria."** ❌ Broken.

The month parameter in the placeholder is essentially lying. You can't actually filter by month alongside a city. The search is purely a name/location autocomplete, not a true filtered search.

### The five things you cannot do on TourneyMachine

1. **Filter by age group.** There is no 9U filter. None. If you want 9U tournaments, you open every single tournament and check whether it includes that division. The division data is in the system — it's just never surfaced in search.

2. **Filter by radius.** You can search by city or state, but there's no "within X miles" filter. Searching Ohio gives you Tallmadge, Findlay, Columbus, and Cincinnati all mixed together with no distance info. You have to eyeball it.

3. **See team counts in search results.** The single most important piece of information for deciding whether a tournament is worth entering — how many teams are registered — is buried inside each tournament page, and even then it's not prominently displayed. You have to click in, find the right division tab, and count.

4. **Filter by price.** If your budget is under $500, there's no way to filter to that. Free-entry tournaments and $800 tournaments appear side by side with no distinction in search results.

5. **Search month + location together.** As proven above. They list "Month" as a searchable field but it only works as a standalone term, not combined.

### The UX problems beyond search

- Search results appear in a **floating dropdown** that disappears the moment you scroll the page. There is no dedicated search results page.
- Tournament cards show **name, date, location** — no age groups, no team count, no entry fee, no registration status (open/closed/full).
- The mobile app is better for following specific tournaments you're already registered for, but still useless for discovery.
- They have a **legacy mobile API endpoint** (`/public/mobile/TournamentList.aspx?sport=Baseball&state=OH&start=...&end=...`) that actually works well and gives a proper paginated list by state + date range. This endpoint is hidden — it's not linked anywhere on the new site. I used it to pull all the tournament data below.
- **No map view.** There is literally no way to see on a map where tournaments are located relative to you.

### What it does well (to be fair)

Once you're inside a tournament you've found, TourneyMachine is solid. Bracket display, live score updates, schedule by field, and the mobile app notifications are genuinely good. The problem is entirely on the discovery/search side. It was built by organizers, for organizers, and the parent/coach experience was an afterthought.

---

## Part 2: Cincinnati-Area 9U Team Counts — Every Tournament, Clicked Through

*All tournaments within approximately 30–40 minutes of Cincinnati, OH/KY. Data pulled live from TourneyMachine April 9, 2026 by navigating to every individual tournament page. These are live registration counts — numbers will rise as tournaments approach.*

---

### 🏆 The Best Bets (5+ 9U Teams Already Committed)

| Tournament | Dates | Location | 9U Teams | Notes |
|---|---|---|---|---|
| **8U,9U,13U & 14U SWOL Tournaments** | Jun 12–14 | Cincinnati / Lebanon / Mason | **Bronze: 7, Silver: 9, Gold: 6 → 22 total** | Three separate 9U brackets by skill level. Massive local tournament. |
| **CWBC Midseason Classic 2026** | Apr 30–May 3 | Cincinnati / Harrison / Miamitown | **8** | Already large in late April. CWBC is one of the biggest local orgs. |
| **Mother's Day Maddness** | May 9–10 | Cincinnati / Lebanon | **7** | Tournaments for a Cause series. Strong field. |
| **All American Classic — Memorial Day (TFC)** | May 23–24 | Cincinnati / Harrison / Miamitown | **7** | Same organizer as SWOL. Big multi-field setup. Includes multiple age groups. |
| **2026 Hits for Heroes** | May 29–31 | Cincinnati / Lebanon / Mason | **6** | Memorial Day weekend. Multi-location. Very well attended across all age groups. |

---

### ✅ Decent Options (3–4 Teams Committed)

| Tournament | Dates | Location | 9U Teams | Notes |
|---|---|---|---|---|
| MAY SLUGFEST (Free Entry) | May 2–3 | OH | **3** | Free entry. Location TBD. |
| Bombs for Moms 2026 | May 9 | Miamitown, OH | **3** | 1-day format. |
| SUMMER SIZZLER (Free Entry) | May 16–17 | Cincinnati / Fairfield / Amelia | **3** | Free entry, multi-location. |
| ALL AMERICAN CLASSIC (Free Entry) | May 22–24 | Fairfield / Cincinnati / Amelia | **3** | Free entry version (different from the TFC one above). |
| BATTLE FOR THE RINGS | May 29–31 | Miamisburg / Springboro | **9U D2: 3** | ~40 min away (Dayton-area). Two skill divisions, D2 has 3. Experienced organizer. |
| CARDINAL CLASSIC (Free Entry) | May 29–31 | OH (MVP Tournaments) | **9U Bronze: 3** | Location listed as "OH" — contact mvptournaments@gmail.com to confirm. |
| OHIO STATE CHAMPIONSHIPS (Free Entry) | Jun 12–14 | OH (MVP Tournaments) | **9U Bronze: 3** | Same note — confirm location. |
| FATHERS DAY CLASSIC (Free Entry) | Jun 19–21 | OH (MVP Tournaments) | **9U Bronze: 2, 9U open: 1** | Three 9U brackets but low committed so far. |

---

### ⚠️ Low Team Count (1–2 Teams, Risky)

| Tournament | Dates | Location | 9U Teams | Notes |
|---|---|---|---|---|
| "BOWNET" Ohio Valley Championships | May 2–3 | Hamilton, OH | **2** | Hamilton is ~30 min N. Only 2 teams — risky. |
| ONE Collision Classic | May 15–17 | Miamitown, OH | **2** | Yeager is already one of the 2. |
| "BOWNET" Rocks Mid-America (All Turf) | May 16–17 | Mid-America Ballyard | **2** | Turf but only 2 teams in 9U. |
| QUEEN CITY CUP (All Turf) | Jun 13–14 | Mid-America Ballyard | **2** | All turf, but slim field. |
| "BOWNET" Amateur Baseball Championships (8U–12U) | May 30–31 | Mid-America Ballyard | **1** | Turf. Only 1 team committed so far — still early. |
| "BOWNET" Super Select (All Turf) | May 9–10 | Mid-America Ballyard | **1** | Only 1. |
| BOMBS 4 MOMS (Free Entry) | May 9–10 | Fairfield / Amelia | **1** | Only 1. |
| OHIO "BATTLE 4 THE BELT" (Free Entry) | Jun 5–7 | OH (MVP Tournaments) | **Bronze: 1, open: 1** | Low so far. |
| TFC Summer Extravaganza | Jun 20–21 | Cincinnati, OH | **1** | Only 1 team in 9U. |
| "DRIP KINGS" CLASSIC (All Turf) | Jun 27–28 | Mid-America Ballyard | **1** | Late June, only 1. |

---

### ❌ No 9U Division (Or Zero Teams Committed)

| Tournament | Dates | Location | 9U Status |
|---|---|---|---|
| Queen City Sports May Mayhem A/AA | May 2–3 | Cincinnati | A/AA only — no 9U |
| TFC Silver/D2/AA Championships | May 2–3 | Covington, KY | No 9U div |
| Triple Play Into May | May 2–3 | Morningview, KY | No 9U div |
| CAN O' CORN CLASSIC (Free) | May 2–3 | Amelia, OH | 0 committed |
| Mother's Day Mayhem TURF (1-day) | May 9 | Mid-America Ballyard | No 9U div |
| EAST SIDE COLLIDE (Free) | May 16–17 | Amelia, OH | 0 committed |
| Queen City May Days Classic A/AA | May 16–17 | Cincinnati | A/AA only |
| TFC Bronze/D3/A Championships | May 16–17 | Covington, KY | No 9U div |
| Diamond Elite Memorial Weekend | May 22–24 | Liberty Twp, OH | No 9U div |
| Queen City Memorial Weekend Slugfest A/AA | May 22–24 | Fairfield, OH | A/AA only |
| Triple Play Memorial Day Madness | May 22–25 | Taylor Mill, KY | 0 committed |
| 2026 Mid-Season Swing Fest | May 30–31 | Morningview, KY | No 9U (10U–13U only) |
| DEFEND YOUR HOUSE (Free) | Jun 6–7 | Amelia, OH | 0 committed |
| Queen City Sports Battle of the Bases A/AA | Jun 6–7 | Cincinnati / Fairfield | A/AA only |
| Summer Jam | Jun 13–14 | Milford, OH | 0 committed (early) |
| 2026 King of Spring | Jun 13–14 | Morningview, KY | No 9U (10U–13U only) |
| Show Me the Money | Jun 20–21 | Covington, KY | No 9U div |
| 2026 PYO Mid-Summer Classic (9U weekend) | Jun 18–21 | West Chester, OH | 0 committed |
| MID-SUMMER SLUGFEST (Free) | Jun 26–28 | OH (MVP) | 0 committed |
| BASEBALL CITY CLASSIC (Free) | Jun 27–28 | Dayton, OH | 0 committed + too far |

---

### 📍 Outside 30-Min Range (For Reference)

| Tournament | Dates | Location | 9U Teams | Distance |
|---|---|---|---|---|
| BATTLE FOR THE RINGS | May 29–31 | Miamisburg / Springboro | **9U D2: 3** | ~40 min (Dayton area) |
| SWING FOR THE RINGS | Jun 26–28 | Miamisburg / Springboro | **9U D1: 2, D2: 4** | ~40 min (Dayton area) |

---

## Part 3: The Decision Grid — Which Ones to Target

Here's how to think about the list above given that you're a 9U Yeager team looking for good competition without wasting a weekend on a 2-team bracket.

**Must-seriously-consider:**
- **SWOL Tournaments (Jun 12–14)** — 22 teams across 3 skill brackets means you'll actually have fair matchups. Pick your bracket level (Bronze/Silver/Gold) correctly and you'll get 3+ competitive games. This is the best June option in the area by far.
- **Hits for Heroes (May 29–31)** — 6 teams in 9U, Cincinnati-area fields, Memorial Day stretch. Solid.
- **Mother's Day Maddness (May 9–10)** — 7 teams, Tournaments for a Cause, well-run series.
- **All American Classic Memorial Day TFC (May 23–24)** — 7 teams, same organizer, same quality.
- **CWBC Midseason Classic (Apr 30–May 3)** — 8 teams but starts in April. If the schedule works, this is the biggest early-season field you'll find.

**Register and monitor:**
- CARDINAL CLASSIC, OHIO STATE CHAMPIONSHIPS, FATHERS DAY CLASSIC (all MVP Tournaments / Free Entry) — 3 9U teams committed but location listed as "OH." Contact mvptournaments@gmail.com to confirm these are in the Cincinnati area before committing.
- BATTLE FOR THE RINGS (May 29–31, Miamisburg) — 3 teams in D2, but Dayton area. Worth it if you don't mind the drive and want competition that weekend.

**Avoid for now:**
- Anything with 0–1 teams committed and no history you know of
- All Queen City Sports A/AA Belt Championship events — these are competitive-level restricted and designed for AA-classified teams
- All Triple Play KY events — none have 9U divisions or teams registered

---

## Part 4: How to Build Something Better

This is genuinely a product gap worth thinking about — especially since you already have a portal infrastructure in Yeager Baseball. Here's what a better version of TourneyMachine's discovery experience would look like.

### The Core Problem to Solve

A coach with a 9U team near Cincinnati opens TourneyMachine and sees 200+ Ohio baseball tournaments in May/June. Zero of those are labeled by age group in the list view. Zero show team count. Zero show distance. He has to open each one and look. This takes an hour and he still doesn't have a clean comparison.

I just did that work for the entire Cincinnati area for May–June 2026. It took clicking through 46 individual tournament pages across two browser tabs.

### What "Better" Looks Like

**Discovery filters that actually work:**
- Age Group (9U, 10U, 11U, etc.) — searchable on the list page, not buried inside each tournament
- Distance radius (10mi / 25mi / 50mi) from a zip code — not just state
- Date range (weekend picker, not month text)
- Entry fee range
- Registration status (Open / Closing Soon / Full)
- Organization/sanction type (USSSA, Bownet, Independent, etc.)
- Field type (turf / grass / mixed)

**Tournament card redesign** — Every card in the list should show:
- Tournament name + dates
- Location + distance from the user's home location
- Age groups available (badges: 8U 9U 10U 11U 12U)
- Team count per division (e.g., "9U: 6 teams registered / 16 max")
- Entry fee
- Registration status
- Organizer name + contact

**"Is this worth my weekend?" view:** For each tournament, a single summary panel showing: field quality, game guarantee, nearby hotels, past years' participation, and which local teams you'd likely see there (based on registration data).

**A map view:** Drop all results on a map. Let coaches see what's happening in their region at a glance. Filter by clicking on a region.

**Saved searches + alerts:** "Notify me when a new 9U tournament opens within 30 miles of Cincinnati in May or June."

**Team count transparency:** This is the single highest-value add. If you're a 9U team and a tournament only has 2 other 9U teams registered, that's a bad tournament. Surfacing this — or letting coaches filter out tournaments with fewer than 4 teams in their division — would save everyone enormous time.

### Is This Buildable for Yeager?

A lightweight version of this could be added to the Yeager portal **specifically for the Cincinnati travel baseball market** as a coach tool. The data is publicly available from TourneyMachine's mobile API (the legacy endpoint I used above). A simple scraper could pull OH/KY/IN tournaments on a nightly basis, parse them, and present them with a proper filtering UI.

That said, team count data requires either scraping each tournament's registration page (fragile) or partnerships with organizers. The more realistic near-term version is:
1. Pull the raw tournament list from TourneyMachine's hidden API
2. Allow coaches to add known age groups manually (crowdsourced)
3. Show a filtered, sortable table with distance from Cincinnati built in

This would already be 10x better than what TourneyMachine's public-facing site offers today.

---

## Quick Reference: Organizers to Watch in Cincinnati Area

| Organizer | Website / Contact | Known For |
|---|---|---|
| Tournaments for a Cause | tournamentsforacause.com | SWOL, CWBC, Mother's Day Maddness, Hits for Heroes, All American Classic — most active local multi-age organizer |
| MVP Tournaments | mvptournaments.org / playmvptournaments@gmail.com | Bownet series, Mid-America Ballyard turf events, Cardinal/Ohio State/Fathers Day/Drip Kings Classics |
| Queen City Sports | (via TourneyMachine listings) | Belt Championship series (A/AA focused), every other weekend |
| CWBC (Cincinnati West Baseball Club) | (via TourneyMachine) | Large local org, Harrison/Miamitown fields, Midseason Classic |
| Triple Play Tournaments | (via TourneyMachine) | Northern KY (Morningview/Taylor Mill) — no 9U divisions currently |
| TFC (Tournaments for Champions) | tournamentsforacause.com | Covington KY and Cincinnati multi-age — Silver/D2 and Bronze/D3 focus |
| Dan's Tournament Series | 937-620-2513 | Battle for the Rings / Swing for the Rings — Miamisburg/Springboro (~40min), well-reviewed |

---

*Data sourced by navigating to 46 individual TourneyMachine tournament pages — tourneymachine.com — April 9, 2026*

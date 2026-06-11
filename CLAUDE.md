# Football Night — Project Context

## What this is
A collection of single-file TV-optimized multiplayer football party games:
- **Home page** (`app/index.html`) — game selector linking to the games below (plain HTML/CSS/JS, no React)
- **The Scout** (`app/scout.html`) — managers "invest" in real footballers blindly across 9 seasons, seeing only stats and market values — never names. At the final reveal, identities unmask and net profit decides the winner. Inspired by: F3/eToro YouTube video "We BLINDLY Invested in Footballers Using Only Their Stats."
- **World Cup Trivia** (`app/trivia.html`) — pass-and-play quiz with 51 inlined World Cup history questions (1930–2022). 25-second clock with speed bonus, difficulty ramps per round (easy → medium → hard, same difficulty for every player in a round), staggered answer reveal (lock in → suspense beat → verdict slam → fun fact), leaderboard finish. 1–6 players, 3/5/7 questions each.

## Output format
**Single HTML file per page** — no build step, opens by double-click. React 18 + Babel via CDN, all data inlined. Pages link to each other with plain relative `href`s.

## Target screen
**TV / 16:9 landscape** — not a phone. Design for ~1920×1080 or 1280×720. Text readable from 3 metres.

## The Scout — game rules (authoritative)

### Core loop (9 seasons, 2016/17–2024/25)
Each draft season: 5 anonymous player cards shown. Stats + market value only — no names, no photos. Each manager picks 1 card. Two left on the shelf (available as transfer window replacements for that position).

### Season order
| Season | Event | Position | Stats shown |
|--------|-------|----------|-------------|
| 2016/17 | Draft | CB | Age · Yellow cards · Goals · League clean sheets |
| 2017/18 | Draft | WF | Age · League G/As · League · UCL G/As |
| 2018/19 | Draft | DM | Yellow cards · Assists · League · League G/As |
| 2019/20 | Transfer Window 1 | — | Hold or sell each player |
| 2020/21 | Draft | GK | Saves/game · League clean sheets · Pens saved · League |
| 2021/22 | Draft | ST | League goals · National caps · League · Height |
| 2022/23 | Draft | AM | League assists · UCL assists · Total goals · National caps |
| 2023/24 | Transfer Window 2 | — | Hold or sell each player |
| 2024/25 | Draft | CB #2 | Same 4 stats as CB round |
| 2025/26 | FINAL REVEAL | — | All identities + values unmasked |

### Transfer window flow
For each manager's player (one at a time):
1. Position + buy price shown (identity hidden)
2. Manager says HOLD or SELL
3. SELL → sell price revealed → identity revealed → replacement shelf shown → manager picks replacement
4. Banked profit = sell price − buy price (added to final score)

### Staggered reveal — THE core UX mechanic
**Everything reveals in deliberate stages to build tension.** This is the single most important design principle. Never show name/photo until after the financial moment has landed.

The user explicitly explained: "note how i sent some images in parts to show how they stagger parts intentionally — e.g. 5th set first they show origin value then mid year value then sell value then the player — it's not all at once."

**Transfer window reveal sequence (per sold player, one click per stage):**
1. Position badge + "Player X" label + buy season + buy price — identity still hidden
2. "OUT →" arrow / sell price appears (suspense beat)
3. Player photo + name unmasked
4. If replacing: anonymous replacement silhouette shown first
5. Replacement's current value revealed
6. Replacement's identity revealed
7. **PROFIT / MADE: €XM** displayed big

**Final reveal sequence (one click per player):**
- Formation pitch shown with all 7 positions as circles, values hidden
- Players revealed back-to-front (GK first, strikers last)
- Running TOTAL ticks up/down with each reveal (can go negative then positive)
- Individual player name appears as each slot is clicked
- Final TOTAL = current squad value − total amount spent = net gain/loss

### Scoring
`Final score = current squad value (all 7 players) − total amount spent + banked transfer profits`

The "total" shown on the final pitch screen IS this net. Individual players can show negative contributions (e.g. a declined CB showing −€16M).

### Host device model
One person (the host) runs the app on a TV-connected device. Other managers give picks verbally. Host enters decisions for everyone. No networking required. (Same model applies to World Cup Trivia.)

## Stats system
**Real football stats only** — NOT FIFA game attributes (not PAC/SHO/PAS/DRI/DEF/PHY).
Position-specific 4-stat rows:
- **CB**: Age · Yellow cards · Goals · League clean sheets
- **WF**: Age · League G+A · League · UCL G+A
- **DM**: Yellow cards · Assists · League · League G+A
- **GK**: Avg saves/game · League clean sheets · Penalties saved · League
- **ST**: League goals · National caps · League · Height
- **AM**: League assists · UCL assists · Total goals · National caps

## Real players (F3 video reference)
These are the players used in the source video. Use these as the canonical draft pools:
- **CB 2016/17**: John Stones (~€50M buy → €35M sell), Antonio Rüdiger (~€9M buy), William Saliba (~€15M → €90M)
- **WF 2017/18**: Mohamed Salah (~€43M → €150M 43 G/A), Luis Díaz (~€1.5M → €75M)
- **DM 2018/19**: Sandro Tonali (~€80M)
- **GK 2020/21**: Emiliano Martínez
- **ST 2021/22**: (from video stats)
- **AM 2022/23**: Arda Güler (~€90M)
- **CB #2 2024/25**: Alessandro Bastoni (~€75K → €75M)

Each draft pool has 5 cards: managers collectively pick 3, 2 remain on the shelf for window replacements.

## Data
- `data/pl-2025-26.tsv` — 551 real Premier League players, FBref 2025/26 stats
  - Columns: Rk, Player, Nation, Pos, Squad, Age, Born, MP, Starts, Min, 90s, Gls, Ast, G+A, G-PK, PK, PKatt, CrdY, CrdR, Gls90, Ast90, G+A90, G-PK90, G+A-PK90, Matches
- Real player data for draft pools is hardcoded/inlined in the HTML — not fetched at runtime

## Tech stack
- React 18 via CDN (esm.sh or unpkg) + Babel Standalone
- Vanilla JS state machine
- All CSS inlined in the HTML
- **No build step, no npm, no server** — network is locked down, all data must be bundled
- Do not fetch live data at runtime

## Design tokens
- Background: `#0d1117` (deep navy, TV-safe, low eye strain for long sessions)
- Accent / position badges: `#c8ff00` (lime-yellow, punchy at TV viewing distance)
- Stat label color: `#00d4b4` (teal)
- Card / surface highlight: `#1a2340`
- Font: **Barlow Condensed** (numbers/headings — readable across a room) + **Inter** (body text)
- Load fonts from Google Fonts CDN
- Text must be readable from 3 metres — minimum 18px body, headings 32px+

## Proposed screen flow (TV 16:9)
1. **Setup** — game title + manager name entry (up to 4), Start button
2. **Season Announcement** — full-screen interstitial: big year, position badge, brief description
3. **The Draft Board** — 5 anonymous player columns, stat rows, current manager highlighted, pick by number key 1–5
4. **Pick Recap** — what each manager drafted this round (still anonymous: position + value only)
5. **Transfer Window (Hold/Sell)** — one player per manager per screen, identity hidden, HOLD/SELL buttons
6. **Transfer Window Reveal** — staggered per sold player (buy price → sell price → identity → replacement → profit)
7. **Squad Overview** — pitch formation showing all positions + current values, running total
8. **Final Reveal** — pitch with hidden values, one click per reveal, running total ticks, names appear
9. **Final Standings** — leaderboard ranked by total score, winner highlighted

## Prototype (Football scout.zip) — reference notes
The zip contains a Claude-generated design prototype. It is **visual reference only**:
- Uses wrong stats (FIFA attributes: PAC/SHO/PAS/DRI/DEF/PHY) — discard
- Built for portrait phone layout (402×874px iOS frame) — discard
- Has useful animation patterns worth reusing:
  - `useCountUp` hook (proto-screens-2.jsx) — animates number counts
  - `useTween` hook (proto-screens-reveal.jsx) — smooth running total
  - `Snake` draft order indicator (proto-card.jsx)
  - `Rail` season progress bar (proto-card.jsx)
  - Card tier system: gold (≥€12M), silver (≥€5M), bronze (<€5M)
  - Dossier slide-up overlay pattern (proto-screens-1.jsx)

## Branch
Development happens on the session's designated `claude/*` branch (see session instructions).

## What NOT to do
- Don't use the prototype for rules or stats — it has many errors
- Don't fetch live data at runtime (network is locked down in the remote execution environment)
- Don't build for portrait/phone layout
- Don't show player names or photos before the reveal moment
- Don't add FIFA-style attributes (PAC, SHO, PAS, DRI, DEF, PHY) — use real football stats only

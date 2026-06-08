# The Scout

A TV-optimized multiplayer football scouting game where managers blindly invest in real footballers across 9 seasons using only stats and market values — no names, no photos.

## How to play

Open `app/index.html` in a browser connected to a TV. One person hosts, everyone else gives picks verbally.

### The loop
- Each season, 5 anonymous player cards appear on screen
- Stats + market value only — identity completely hidden
- Each manager picks one card (host taps their choice)
- Two transfer windows let you sell for profit and replace from the leftover shelf
- Final reveal unmasks every player and calculates who invested best

### Scoring
`Final score = current squad value − total spend + banked transfer profits`

## Season timeline

| Season | Event | Position |
|--------|-------|----------|
| 2016/17 | Draft | CB |
| 2017/18 | Draft | WF |
| 2018/19 | Draft | DM |
| 2019/20 | Transfer Window | — |
| 2020/21 | Draft | GK |
| 2021/22 | Draft | ST |
| 2022/23 | Draft | AM |
| 2023/24 | Transfer Window | — |
| 2024/25 | Draft | CB #2 |
| 2025/26 | Final Reveal | — |

## Files

```
app/index.html    — the game (single file, no install needed)
data/             — raw FBref player data used to build draft pools
CLAUDE.md         — full project context for AI sessions
```

## Design
Deep navy background, lime-yellow accents, Barlow Condensed for numbers — built for readability at TV viewing distance.

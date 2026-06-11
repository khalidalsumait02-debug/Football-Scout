# Football Night

A collection of TV-optimized multiplayer football party games. Open `app/index.html` in a browser connected to a TV and pick a game — one person hosts, everyone else plays along verbally.

## The games

### The Scout (`app/scout.html`)
Managers blindly invest in real footballers across 9 seasons using only stats and market values — no names, no photos.

### World Cup Trivia (`app/trivia.html`)
A pass-and-play quiz on World Cup history — 51 questions from 1930 to 2022 across winners, records, legends, moments, hosts and awards. Each player answers on a 25-second clock; faster correct answers earn a speed bonus, difficulty ramps up round by round, and the leaderboard decides the champion.

## The Scout — how to play

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
app/index.html    — home page: pick a game (single file, no install needed)
app/scout.html    — The Scout
app/trivia.html   — World Cup Trivia
data/             — raw FBref player data used to build draft pools
CLAUDE.md         — full project context for AI sessions
```

## Design
Deep navy background, lime-yellow accents, Barlow Condensed for numbers — built for readability at TV viewing distance.

# 🥒 PICKLE JAM '95

A 90s-flavored pickleball game. **One button per player.** Two players, one keyboard.

Everything lives in a single `index.html` — no build step, no dependencies, no asset
files. The music and sound effects are synthesized live in the browser with Web Audio.

## Play

Open `index.html`. That's it. It also runs fine from a double-click on the desktop.

## Controls

| | Player 1 | Player 2 |
|---|---|---|
| Key | `A` (also `Q`, `Z`, `Shift`, `Space`) | `L` (also `P`, `/`, `Right Shift`) |
| Touch | left half of the screen | right half of the screen |
| Gamepad | pad 1, any button | pad 2, any button |

Menus are one-switch navigable: **tap** your button to move down, **hold** it to
select. Arrow keys, `Enter` and the mouse work too.

`M` tunes the radio · `N` mutes · `Esc` pauses

## How one button plays pickleball

Your player runs to the ball on their own. The only thing you do is swing, and *when*
you swing is the entire game.

- **Tap** — drive the ball deep
- **Hold** — lob it over their head
- **Tap a low ball at the kitchen line** — dink it short
- **Press when the shrinking ring meets the white circle** — perfect contact, a ZINGER
- **Press early** and the ball goes one way, **late** and it goes the other — that's your aim

## The rules are the real ones

- Side-out scoring: only the serving side can score. Lose the rally on your serve and
  it's a **side out** — the serve goes over, no point.
- Serve underhand, diagonally, past the kitchen. Deeper is better, but overcook it and
  it sails long.
- **Pro rules** (on by default): the serve and the return must both bounce before
  anyone gets to smack it.
- No volleying with your feet in the kitchen (the non-volley zone).
- First to 11, win by 2. Also available at 7 and 15.

## Radio stations

| Dial | Station | Format |
|---|---|---|
| 104.5 | KRUD | Grunge / alt — detuned power chords and a sludgy backbeat |
| 92.3 | JAMZ | Hip-hop / R&B — boom-bap kit, fat sub bass, vinyl crackle |
| 99.7 | PULSE | Eurodance — four-on-the-floor, offbeat bass, hoover leads |
| 88.1 | WAVE | New jack swing — swung kit, electric piano, sax line |
| --.- | STATIC | Radio off |

Every station is generated from scratch at runtime — chord progressions, drum
patterns and all. Nothing is streamed or downloaded.

## Accessibility

- **One button per player** — playable with a single switch, and the menus are too.
- **Timing assist** (on by default) adds the timing ring, the ball's landing marker
  and a wider sweet spot.
- **Screen FX: REDUCED** turns off the scanlines, screen shake, flashes and the
  drifting VHS tracking bar.
- Nothing relies on color alone; players are distinguished by position and shape.
- Gamepad buttons map to the same single input, so adaptive controllers work.

## Publishing to GitHub Pages

Push `index.html` to a repo, then in **Settings → Pages** pick the branch and the
root folder. The game is one static file, so it will just work.

## Tinkering

The whole game is in `index.html` under one IIFE. Useful entry points:

- `COURT` constants and `proj()` — the pseudo-3D court projection (all in feet)
- `hit()` — shot selection, power, aim from timing error
- `SWING_IDEAL` / `swingTol()` — the timing window; widen these to make it easier
- `updateAI()` — CPU reaction error per difficulty
- `Audio90.STATIONS` — add your own station with a 16-step `play(step, time, bar)`

`window.PJ` exposes the live game state in the console (`PJ.S`, `PJ.ball`, `PJ.pl`,
`PJ.opt`) if you want to poke at it while it runs.

---

© 1995 NO COAST GAMES — all rights reserved, dude.

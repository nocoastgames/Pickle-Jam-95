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

Press `M` to tune. Every preset has **two** sources: a live station, and a
built-in synth "tape" that stands in when the stream can't be reached.

| Dial | Station | Live source (SomaFM) | Backup tape |
|---|---|---|---|
| 104.5 | KRUD | Indie Pop Rocks! | Grunge — detuned power chords, sludgy backbeat |
| 92.3 | JAMZ | Fluid | Boom-bap kit, fat sub bass, vinyl crackle |
| 99.7 | PULSE | The Trip | Eurodance — four-on-the-floor, hoover leads |
| 88.1 | WAVE | Underground 80s | New jack swing — swung kit, Rhodes, sax line |
| 101.3 | VHS | Vaporwaves | Slowed major-9 chords drowned in delay |
| --.- | STATIC | — | Radio off |

**How the failover works.** The tape starts immediately and keeps playing while
the stream connects, so the game is never silent. If the stream connects, it
takes over and the panel shows a red `● LIVE` dot plus the current track. If it
fails — no internet, a blocked network, a dead node — the panel shows `TAPE` and
the synth just keeps going. It tries three stream hosts before giving up, which
takes about twenty seconds worst case, all of it covered by the tape.

Turn **LIVE RADIO: OFF** in the options to skip streaming entirely and always use
the built-in tapes. Worth doing on a metered or filtered network, or offline —
each live station pulls a continuous 128 kbps. Muting with `N` also drops the
stream rather than just silencing it, so a muted game uses no bandwidth.

Live streams come from [SomaFM](https://somafm.com), a listener-supported
independent radio station. They're free to listen to and cost SomaFM real money
to run — if your class ends up using them, [consider donating](https://somafm.com/support/).

## Accessibility

- **One button per player** — playable with a single switch, and the menus are too.
- **Timing assist** (on by default) adds the timing ring, the ball's landing marker
  and a wider sweet spot.
- **Screen FX: REDUCED** turns off the scanlines, screen shake, flashes and the
  drifting VHS tracking bar.
- Nothing relies on color alone; players are distinguished by position and shape.
- Gamepad buttons map to the same single input, so adaptive controllers work.
- **LIVE RADIO: OFF** removes all network use, for filtered school networks or
  offline play. The game is fully playable with no internet connection.

## Publishing to GitHub Pages

Push `index.html` to a repo, then in **Settings → Pages** pick the branch and the
root folder. The game is one static file, so it will just work.

## Tinkering

The whole game is in `index.html` under one IIFE. Useful entry points:

- `COURT` constants and `proj()` — the pseudo-3D court projection (all in feet)
- `hit()` — shot selection, power, aim from timing error
- `SWING_IDEAL` / `swingTol()` — the timing window; widen these to make it easier
- `updateAI()` — CPU reaction error per difficulty
- `STATIONS` in `Audio90` — each entry is `{dial, name, genre, soma, play}`. Add a
  station by giving it a SomaFM channel id and a 16-step `play(step, time, bar)`
  tape; `https://somafm.com/channels.json` lists every available channel id.

`window.PJ` exposes the live game state in the console (`PJ.S`, `PJ.ball`, `PJ.pl`,
`PJ.opt`) if you want to poke at it while it runs.

---

© 1995 NO COAST GAMES — all rights reserved, dude.

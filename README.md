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

**Menus are teacher-only by default.** Arrow keys, `Enter`, and the mouse operate
them; player buttons are ignored, so a student resting on their switch can't walk
through the options and undo your setup. Change that with **MENU CONTROL** under
SETUP & ACCESS if you want one-switch menus (tap = move down, hold = select).

`M` tunes the radio · `N` mutes · `Esc` pauses

## Access levels

**Set this first.** One setting moves everything that governs difficulty, so you
don't have to tune eight things per student.

| Level | Swing | Speed | Auto-play | Repeat filter |
|---|---|---|---|---|
| **EASIEST** | waits for the ball | 28% | on | 0.9s |
| **EASY** | waits for the ball | 45% | on | 0.6s |
| **STANDARD** | waits for the ball | 70% | off | 0.25s |
| **CLASSIC** | must be timed | 100% | off | 0.11s |

The important one is **SWING: WAITS FOR BALL**. Normally a swing lasts a fraction
of a second and you have to land it as the ball arrives. An armed swing holds the
paddle out until the ball gets there — so a student can press *whenever*, seconds
early or seconds late, and still connect. Reaction time stops being the thing the
game measures. Pressing at the right moment still earns a ZINGER, so timing is a
bonus rather than a requirement.

It's a player accommodation only: the CPU still has to time its own swing, or
neither side could ever miss and no point would ever be scored.

## Game modes

- **CO-OP RALLY** — no opponent and no score. Two players (or one player and the
  CPU) keep the ball alive and count hits in a row, with a running team best.
  Dropping it costs nothing: "GOOD TRY!", then straight into the next rally.
- **NO-FAIL MATCH** — points are scored, but the student cannot fault. Their shots
  always clear the net and land in, and the ball is aimed where the other player
  can actually reach it. Simple rally scoring, no side-outs to explain.
- **CLASSIC RULES** — the real game, unchanged: side-out scoring, the kitchen,
  the double-bounce rule, serves that can sail long.

In the two accessible modes the serve is not a second timing puzzle either — the
meter is replaced by **PRESS YOUR BUTTON TO SERVE**, and any press serves well.

## The rules are the real ones (in CLASSIC)

- Side-out scoring: only the serving side can score. Lose the rally on your serve and
  it's a **side out** — the serve goes over, no point.
- Serve underhand, diagonally, past the kitchen. Deeper is better, but overcook it and
  it sails long.
- **Pro rules**: the serve and the return must both bounce before anyone gets to
  smack it.
- No volleying with your feet in the kitchen (the non-volley zone).
- First to 11, win by 2. Also available at 5, 7 and 15.

In CO-OP and NO-FAIL, tap/hold shot selection is dropped and the game picks a good
shot for you, because a student who holds their switch down would otherwise lob
every single ball.

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

Built for students with significant physical and cognitive disabilities and slow
reaction times. Everything below is in **SETUP & ACCESS**.

- **One button per player**, and no reaction-time demand at all on the lower access
  levels — see [Access levels](#access-levels).
- **IGNORE FAST REPEATS** (0.6s by default) swallows switch chatter. A second press
  arriving too soon after the first is treated as the same press, so tremor,
  spasticity or a bounced switch never costs a rally.
- **Holding the switch down is safe.** A press registers on the way down, so a
  student who presses and keeps holding gets exactly one clean swing, not a
  stuck lob or a stream of swings.
- **AUTO-PLAY HELP** swings for them at the last moment if no press comes, so a
  student who cannot press — or simply doesn't this time — still sees a rally
  continue rather than a loss. Their own press always takes priority. If nobody
  serves, the game serves itself after twelve seconds.
- **MENU CONTROL: TEACHER ONLY** keeps player buttons out of the options screen.
- **Timing ring** (on by default) shows the ball's landing spot and when to press.
- **Pressing early is never punished.** With an armed swing, a student can press
  before the opponent has even hit the ball and it still counts.
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

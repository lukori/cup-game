# אין "לזרוק" — cup game

Speculative phone game about single-use cups: catch coffee drops in the air by moving the phone, drink, throw the cup away. The thrown cup stays, tied to the next one, and every new cup hangs lower and follows the hand more slowly. On the 7th cup it collapses, the years run on (+30 per cup), cups rain from the sky. No winning.

Live: https://lukori.github.io/cup-game/  — one file, `index.html` (cup textures are embedded).

Built first in a Claude.ai chat, reviewed and published from Claude Code on 2026-11-26.

## Tuning from the address

Every number in `TUNE` (top of the script) can be set in the URL, e.g. `?heavy=1.3&slow=1.2`.
Add `&debug` for a panel with live numbers, − / + buttons (they update the address, so the tuned link can be copied) and **Copy log** (a sample every 0.25 s).

| knob | default | meaning |
|---|---|---|
| `back` | 0.6 | how far behind your cup the hanging bunch floats |
| `under` | 3 | how strongly each old cup drifts back to its place under yours |
| `grav` | 1.4 | how hard old cups sink |
| `drag` | 1.6 | how thick the air is around them (higher = calmer, floatier) |
| `rope` | 1 | size of the hanging bunch / rope length |
| `tug` | 0.25 | how much the bunch pulls on your cup when you move |
| `heavy` | 1 | multiplies how far each cup hangs below your aim (sag) |
| `slow` | 1 | multiplies how slowly each cup follows the hand |
| `catchAngle` | 8.5 | degrees: how close the cup must get to a drop |
| `tiltToDrink` | 28 | degrees of sideways tilt that starts drinking |
| `yearsPerCup` | 30 | years counted per cup |
| `cupGrams` | 12 | weight of one paper cup in the readout |
| `cupMl` | 240 | coffee in a full cup, ml (= grams) |

Per-cup arrays (`stiffness`, `damping`, `sag`, `dropPitch`, `dropsPerCup`) are edited in the file.

## Changes from the chat version

- Drinking: tilt threshold 38° → 28°, and once you start pouring it keeps pouring until the cup is empty. Reason: at ~40°+ the iPhone may rotate the page to landscape mid-drink.
- Years count from the current year instead of a fixed 2026.
- Screen-awake lock is requested again when you come back to the page.
- Facilitator long-press (2.5 s on the end title clears cups from earlier games) no longer fires if the finger slides off.
- Added URL tuning and the `?debug` panel.

## v2 (2026-11-26): old cups hang under yours, every cup is solid

- A thrown cup flies out, then its rope reels it back (~2 s) into a bunch that hangs lower than your cup, a little behind it, left and right. It floats (thick air, slow bob, slow tumble) but sinks, and it tugs on your cup when you move.
- Hard rule: an old cup can never rise above the bottom of your cup. Measured on a scripted game: 0% of the time above (before the rule it was 24-37% when turning fast).
- Every cup (yours, the hanging ones, the falling rain at the end, cups from earlier games) is a solid capsule; they push each other and can't enter one another. Worst overlap measured: about 1-3 cm on a 80 cm cup, for a fraction of a frame.
- Cups from earlier games now stand farther out (6.5+) so they don't block the bunch.
- Trade-off: because your cup sags lower every round, the bunch is visible on a portrait phone about half the time at cups 2-3 and mostly below the screen by cups 5-6 (you see the ropes pulling down). `back` didn't change that (tested 0.6 / 1.6 / 2.6).

## v4 (2026-11-26): opening screen

No title, text or button: a single cup floats, sways and turns slowly on brown, with a very soft light breathing around it (5 s cycle, `#halo` / `@keyframes breathe` in the CSS). A tap anywhere starts (iOS needs a tap to ask for motion and camera). If motion is refused, dragging the screen still works, silently.

## v5 (2026-11-26): weight readout instead of the text

The sentence box in the middle is gone. In its place: a big white number in grams / ml that rolls to its value and never quite settles, with a small red needle on its right pointing at the middle of the number, trembling more when you move (like a dial in a car). Weight = `cupGrams` x (your cup + every cup tied to you) + the coffee now in your cup. At the collapse it runs up fast. Only the action hints stay, small, under the dots (first catch, drink, throw).

## Not verified

Real phone (iOS Safari motion permission, camera, auto-rotate while tilting). Tested only by a scripted full playthrough in a desktop browser.

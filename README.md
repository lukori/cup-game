# אין "לזרוק" — cup game

Speculative phone game about single-use cups: catch coffee drops in the air by moving the phone, drink, throw the cup away. The thrown cup stays, tied to the next one, and every new cup hangs lower and follows the hand more slowly. On the 7th cup it collapses, the years run on (+30 per cup), cups rain from the sky. No winning.

Live: https://lukori.github.io/cup-game/  — one file, `index.html` (cup textures are embedded).

Built first in a Claude.ai chat, reviewed and published from Claude Code on 2026-11-26.

## Tuning from the address

Every number in `TUNE` (top of the script) can be set in the URL, e.g. `?heavy=1.3&slow=1.2`.
Add `&debug` for a panel with live numbers, − / + buttons (they update the address, so the tuned link can be copied) and **Copy log** (a sample every 0.25 s).

| knob | default | meaning |
|---|---|---|
| `heavy` | 1 | multiplies how far each cup hangs below your aim (sag) |
| `slow` | 1 | multiplies how slowly each cup follows the hand |
| `catchAngle` | 8.5 | degrees: how close the cup must get to a drop |
| `tiltToDrink` | 28 | degrees of sideways tilt that starts drinking |
| `yearsPerCup` | 30 | years counted per cup |

Per-cup arrays (`stiffness`, `damping`, `sag`, `dropPitch`, `dropsPerCup`) are edited in the file.

## Changes from the chat version

- Drinking: tilt threshold 38° → 28°, and once you start pouring it keeps pouring until the cup is empty. Reason: at ~40°+ the iPhone may rotate the page to landscape mid-drink.
- Years count from the current year instead of a fixed 2026.
- Screen-awake lock is requested again when you come back to the page.
- Facilitator long-press (2.5 s on the end title clears cups from earlier games) no longer fires if the finger slides off.
- Added URL tuning and the `?debug` panel.

## Not verified

Real phone (iOS Safari motion permission, camera, auto-rotate while tilting). Tested only by a scripted full playthrough in a desktop browser.

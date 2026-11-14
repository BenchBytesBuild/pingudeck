# Wiring

| Folder | What | Tool (free) |
| --- | --- | --- |
| `src/kicad/` | The real schematic | [KiCad 9](https://www.kicad.org) |
| `src/drawio/` | Simple pin maps and block diagrams for on-screen GFX, in brand colors | [draw.io](https://www.drawio.com) (desktop or VS Code extension) |
| `exports/` | PDF / SVG / PNG, one per revision, never overwritten | |
| `pinout.md` | Which pin goes where, current revision | |

Optional: test ESP32 circuits in [Wokwi](https://wokwi.com) before soldering; save the
project link in `pinout.md`.

**Naming:** `pingudeck_wiring_rev-A.pdf`, `pingudeck_wiring_rev-B.pdf`, …
Sub-circuits and diagrams: `pingudeck_keyboard-matrix_rev-A.svg`.

**When the circuit changes:**
1. Edit the source, bump the rev in the schematic title block.
2. Export a new file to `exports/` (keep the old ones).
3. Update `pinout.md`.
4. Commit in this repo, and add a `[wiring]` line to the project `CHANGELOG.md` saying what changed and why.

A rev-A vs rev-B side-by-side is a ready-made GFX shot.

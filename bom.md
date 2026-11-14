# Parts list (BOM): PinguDeck

Status: `have` · `need` · `ordered` · `arrived` · `installed` · `dead` · `spare`

Parts for the first build are chosen; the rest are still drafts from the storyboard.
`ordered` = bought, not yet arrived. Set the date and cost when they arrive.

| Part | Qty | Purpose | Source / link | Cost | Status | Ordered | Arrived | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Sanyo Pingu Computer IT-5 | 1 | Donor: shell, keyboard, mouse pad | | | have | | | Condition untested; original board gets framed |
| WT32-SC01 Plus (ESP32-S3 dev board, 3.5" 320×480 capacitive multi-touch LCD) | 1 | Main brain and the new screen | | ¥5,360 | have | | | I2C bus on GPIO5/6 is shared with the touch controller. Free GPIO count ❓ (see `wiring/pinout.md`) |
| TCA8418 keypad scanner (I2C, fixed address 0x34) | 2 | #1: Pingu keyboard matrix, up to 8 rows × 10 columns (Ep 4, Ep 5). #2: Plan B only, reads the six TTP223 outputs | | ¥3,020 (¥1,510 × 2) | ordered | | | Replaces the MCP23017 in the draft. Needs 3.3 V |
| MPR121 capacitive touch breakout (I2C, 0x5A) | 1 | Plan A: the touch pads, through the plastic (Ep 6) | | ¥328 | ordered | | | Try first. Electrodes need copper tape wired to its pins |
| PCA9548A I2C multiplexer | 5 | Plan B: puts the two TCA8418s on separate channels (same address) | | ¥671 (total for 5) | ordered | | | A variant (address 0x70–0x77). Four spare |
| TTP223 touch sensor module | 20 | Plan B: six touch buttons (Ep 6) | | ¥372 (total for 20) | ordered | | | 14 spare. Power from 3.3 V |
| Color display | — | New screen in original bezel (Ep 8) | | | have | | | Covered by the WT32-SC01 Plus screen (320×480). Measure the bezel window against the board first |
| Copper tape (single-sided, conductive adhesive) | 1 roll | Touch electrodes stuck to the inside of the plastic (Ep 6) | | | ordered | | | Check it is real copper and solderable. Pads about 10–15 mm |
| Battery + charger board | 1 | Portable power | | | need | | | |
| Jumper wires / breadboard | — | Prototyping | | | need | | | |
| ROM reader (optional) | 1 | Back up original programs (Ep 3) | | | need | | | |
| Shadow-box frame | 1 | Frame the original board (Ep 3) | | | need | | | Props |
| IT-SC1 expansion cartridge (optional) | 0–1 | Study the cartridge interface; maybe a bonus short | auction listings (S2–S5) | | need | | | Not mentioned on the box; only if Q16 finds a slot on the unit |
| Penguin figurine (original) | 1 | The Mascot | | | need | | | Props, not Pingu |
| Small box labeled "Heritage" | 1 | Holds the saved chip (Ep 3 → 9) | | | need | | | Props |

## Touch plan

| Plan | Parts | When |
| --- | --- | --- |
| **A (first)** | ESP32 → I2C → TCA8418 #1 (keyboard) + MPR121 (touch). No multiplexer | Try first |
| **B (fallback)** | ESP32 → I2C → PCA9548 → channel 0: TCA8418 #1 (keyboard), channel 1: TCA8418 #2 (six TTP223 outputs) | If the MPR121 through the plastic isn't reliable |

Spares: 1 TCA8418 is unused in Plan A; the PCA9548As and TTP223s are unused in Plan A.

**Total so far:** ¥9,751 (WT32-SC01 Plus ¥5,360 + TCA8418 ¥3,020 + PCA9548A ¥671 + TTP223 ¥372 + MPR121 ¥328; copper tape cost not entered yet) · **Parts ordered twice:** 0

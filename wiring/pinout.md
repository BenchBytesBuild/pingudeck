# Pinout: rev-A

| MCU pin | Connected to | Direction | Notes |
| --- | --- | --- | --- |
| | | | |

**Board:** WT32-SC01 Plus (ESP32-S3, 3.5" 320×480 capacitive touch LCD). Pin facts below come from
the RIOT OS board docs and the vendor datasheet; confirm against the schematic before wiring.

## Pins already used by the board

| Use | Pins | Notes |
| --- | --- | --- |
| I2C bus (touch controller FT6336U) | SCL GPIO5, SDA GPIO6 | **Shared bus: our TCA8418, MPR121, PCA9548A go on the same two wires** |
| Touch interrupt / reset | INT GPIO7, RST GPIO4 | Not free. GPIO4 is also the LCD reset |
| LCD 8-bit parallel data | GPIO 9, 46, 3, 8, 18, 17, 16, 15 | Not I2C or SPI, so no bus conflict |
| LCD control | WR 47, RS 0, TE 48, backlight 45 | GPIO0 is also BOOT |
| microSD (SPI) | GPIO 39, 38, 40, 41 | Per one source |
| RS485 | GPIO 1 (RX), 2 (RTS), 42 (TX) | Per one source; unconfirmed on this board |

**Free pins:** ❓ not confirmed. By elimination GPIO10–14 and 19–25 look unused, but that is my
inference, not a sourced fact. GPIO26–32 normally serve the flash/PSRAM and GPIO43–44 are
UART0, so avoid those. One source says the board exposes 8 GPIO on its extension connector;
check which connector yours has and which pins reach it.

The TCA8418 and MPR121 interrupt lines are optional (polling over I2C works), so free GPIO
count doesn't block either plan.

## I2C map

| Device | Address | Plan | Notes |
| --- | --- | --- | --- |
| TCA8418 #1 (keyboard) | 0x34 | A, B | INT to its own ESP32 pin (optional; polling works) |
| MPR121 (touch) | 0x5A | A | INT optional; ADDR to GND |
| PCA9548 (mux) | 0x70 | B | Channel 0: TCA8418 #1, channel 1: TCA8418 #2 |
| TCA8418 #2 (TTP223 inputs) | 0x34 (behind mux) | B | Same address as #1, separate channel |
| Touch controller FT6336U (on the board) | ❓ (typically 0x38, verify) | A, B | Already on this bus. Should not clash with 0x34, 0x5A, 0x70 |
| LCD | n/a | A, B | 8-bit parallel, not on I2C |

All devices on 3.3 V. Keep the touch wires short and away from the display cable.

## Keyboard matrix (needs measuring, Q10)

Rows ❓ · columns ❓ (must be ≤ 8 rows and ≤ 10 columns for one TCA8418)

## Revision history
- rev-A (2026-11-12): initial.

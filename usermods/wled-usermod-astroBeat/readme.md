# astroBeat

Control panel for the hulaweenAstronaut LED costume, running on a LilyGO T-ETH-Lite S3 (ESP32-S3-WROOM-1 N16R8).

## Wiring

| Function | GPIO |
|---|---|
| Buttons 1–4 (to GND) | 2, 3, 4, 5 |
| Toggles T1–T4 (to GND) | 6, 7, 8, 21 |
| Button lights 1–4 | 38, 39, 40, 41 |
| 10K pot wiper (ends to 3V3 / GND) | 1 |
| MAX7219 DIN / CLK / CS | 47 / 48 / 45 |
| W5500 RST (held low, chip unused) | 14 |

Pins can be overridden with `-D ASTRO_BTN_PINS=...`, `ASTRO_TOGGLE_PINS`, `ASTRO_LIGHT_PINS`, `ASTRO_POT_PIN`, `ASTRO_MAX7219_PINS` and `W5500_RST_PIN`.

## Controls

- **Buttons 1–3** start Fire, Ripple Rainbow, or Noise Pal. Pressing the running pattern's button again blacks out the strips. The running pattern's light toggles every second.
- **Button 4**
  - A short press turns audio reactivity on or off. Light 4 is solid while it's on.
  - Hold it and turn the pot to set the reaction depth (0–255).
  - With audio reactivity on, sound raises the effect intensity: Fire sparks, Ripple waves, Noise scale. In the Fire MDMA and FREAK OUT modes, the colour also follows pitch.
- **Toggles:** with exactly one engaged, the pot adjusts its value. Otherwise the value field shows `----`.

| Toggle | Pot adjusts |
|---|---|
| T1 | brightness |
| T2 | speed (Fire: cooling) |
| T3 | intensity (Fire: spark rate) |
| T4 | Fire colour mode: 1 Fire, 2 MDMA, 3 FREAK OUT |

- **Display:**
  - Digits 7–4 show `P  n` for the running program, or `----` when stopped.
  - Digits 3–0 show the selected value.

## One-time WLED setup

- **LED Preferences:** enable "Make a segment for each output" so each strip gets its own segment. The usermod applies the same settings to every segment, so the strips mirror each other.
- **Usermods → AudioReactive:** enable it. The mic is an INMP441 on generic I2S, with L/R tied to GND.

## Dependencies

- [wayoda/LedControl](https://github.com/wayoda/LedControl) (bit-banged MAX7219 driver)
- the `audioreactive` usermod, for audio reactivity

# CM300DU-24NFH IGBT Gate Driver / Protection Shield

KiCad files for a small daughter-board that mounts directly over a Mitsubishi
**CM300DU-24NFH** dual IGBT module to provide gate drive coupling and
collector–emitter transient protection. Designed for use in my first
[DRSSTC](https://en.wikipedia.org/wiki/Tesla_coil#Solid-state_Tesla_coil)
build.

## What the board does

The shield carries four electrically isolated circuits on a single PCB:

- **Two gate-drive networks** — one per IGBT in the module. Each takes the
  output of a gate-drive transformer and feeds the gate through an
  anti-parallel resistor / Schottky diode pair. The asymmetric turn-on vs.
  turn-off impedance adds a small amount of switching hysteresis, which
  prevents both IGBTs in a half-bridge from being briefly in conduction at the
  same time and shorting the DC bus.
- **Two collector–emitter clamp networks** — one per IGBT. Each is a string of
  series TVS diodes across the C–E terminals to catch fast switching
  transients that the main bus snubber may not absorb quickly enough,
  protecting the IGBT from voltage spikes during turn-off.

Mounting the protection on its own PCB directly above the module keeps the
loop area between the clamps and the IGBT terminals as small as possible,
which is what makes the clamps actually effective at high di/dt.

## Key components

| Function | Part |
| --- | --- |
| IGBT module (footprint) | Mitsubishi CM300DU-24NFH |
| Primary TVS (C–E clamp string) | Vishay 1.5KE220CA (×8) |
| Secondary TVS | P6KE30CA (×2) |
| Gate-drive Schottky | 1N5819 (×2) |
| Gate trim pot | Bourns 3362X-1-100LF (×2) |
| Gate-drive headers | Molex 22-01-2021 (×2) |
| Output headers | Molex 171857-0002 (×2) |

See [`bom.csv`](bom.csv) for the full bill of materials.

## Repository contents

- `Gate_Driver.kicad_*` — KiCad 7+ project (schematic, PCB, design rules)
- `PowerIGBTs.kicad_sym` — symbol library for the IGBT module
- `Library.pretty/` — footprint library
- `CM300DU-24NFH Outline*.dxf` — mechanical outline of the IGBT module
- `Gate_Driver*.step` — 3D models of various board revisions
- `Custom-Connector.stp` — 3D model of the gate-drive connector
- `BoardTop.png`, `Logo.png` — render and silkscreen artwork
- `bom.csv` — bill of materials

## License

Released under the MIT License — see [`LICENSE`](LICENSE).

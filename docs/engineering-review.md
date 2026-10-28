# Engineering Review

Reviewed 2026-10-28 against the supplied design and KiCad 10.0.5 checks. This is an unbuilt design study, with two functional issues requiring correction before it is presented as fabrication-ready.

## PCB manufacturing dimensions

The board uses two copper layers, nominal 1.6 mm FR-4 thickness and 35 um copper per side. Its nominal outline is 66.04 x 33.02 mm.

| Feature | Design evidence | Comparison for JLCPCB two-layer, 1 oz FR-4 |
| --- | --- | --- |
| Routed track width | 353 segments: 265 at 0.20 mm, 88 at 0.30 mm | Above the 0.10 mm minimum. |
| Different-net clearance | Closest measured track/via gap about 0.150 mm; separate DRC passes with an explicit 0.15 mm global minimum | Meets 0.10 mm track spacing and 0.15 mm SMD pad spacing criteria. |
| Through vias | 80 vias, each 0.60 mm diameter / 0.30 mm drill | Within the published via sizing capability. |
| Via annular ring | 0.15 mm nominal | Within the published via sizing capability; component plated-hole requirements differ. |
| Copper-to-board-edge rule | 0.50 mm; closest measured copper is about 0.501 mm from the outline | Above the 0.20 mm routed-edge criterion. |

These checked dimensions look compatible with ordinary fabrication. Comparison source: [JLCPCB manufacturing capabilities](https://jlcpcb.com/capabilities/pcb-capabilities/), accessed 2026-10-28. This is not a full DFM approval; final drill/slot, mask, finish, assembly, and Gerber review remain necessary. Do not assume the same clearance is acceptable with thicker copper.

The supplied global minimum clearance and track-width constraints are both zero. The Default net-class clearance still applies, but its preferred track width is not a global minimum-width check. See [KiCad 10 design-rule documentation](https://docs.kicad.org/10.0/en/pcbnew/pcbnew.html#configuring-design-rules). The additional dimensional probe is described in the [verification notes](checks/README.md); no source rules were weakened or changed during packaging.

## Circuit issues to resolve

### Q1 and Q2: MOSFET selection / power switching

Both are specified as **DMG3414U**, an N-channel device ([Diodes Incorporated](https://www.diodes.com/part/view/DMG3414U)). Their saved connections are:

| Device | Gate | Source | Drain |
| --- | --- | --- | --- |
| Q1 | VBUS | +BATT | VHI, the regulator input rail |
| Q2 | NEOPIX_EN | +3.3V | NEOPIX_PWR |

Q2's gate is driven between ground and 3.3 V while its source is at 3.3 V, so it cannot obtain positive gate-to-source drive for normal N-channel turn-on; its body diode can still feed the load. Q1's USB-controlled battery power path likewise needs a topology review: USB can bias the device on between the system and battery rails, while battery-only operation relies on the body diode with the channel off. That can defeat the intended isolation and charging behavior.

Resolve the intended power-path and load-switch behavior, select suitable devices, and verify source/drain orientation and reverse-current behavior. A part-name substitution alone is not a sufficient correction. No substitutions or rerouting were made during packaging.

### D4: LED symbol and footprint pin mapping

The generic WS2812B symbol uses pins 1=VDD, 2=DOUT, 3=GND, 4=DIN, but the selected **WS2812B-2020** footprint references a device with pins 1=DO, 2=GND, 3=DI, 4=VDD. See the [Worldsemi datasheet, pages 2-3](https://cdn-shop.adafruit.com/product-files/4684/4684_WS2812B-2020_V1.3_EN.pdf).

Consequently, the present mapping does not wire that physical LED correctly. That datasheet also lists a 3.7-5.3 V supply range, while this circuit derives the LED rail from 3.3 V. Choose the exact LED variant and a matching symbol/footprint, verify its operating voltage, then update the PCB connections. This needs a circuit/part-selection decision, so it was left unchanged.

## Scope and dependencies

The ESP32 module footprint contains a copper/track/via keepout on both copper layers, and the saved copper fills respect it. PCB material remains below the antenna; RF performance and enclosure effects require validation. USB impedance and compliance, power/thermal behavior, and charging behavior have not been validated.

All assigned symbol and footprint identifiers resolve in the standard KiCad 10 libraries; no custom symbol or footprint libraries are required.

The ESP32-S3-MINI-1 symbol uses the standard ESP32-S2-MINI-1 footprint assignment also found in KiCad 10's stock symbol. Its name alone does not establish a mismatch. Missing 3D bodies are documented in the [visual guide](visuals.md); they do not remove the footprints.

The exported component list includes generic selections and is not a procurement-ready BOM. Hardware remains unbuilt and untested. The clean ERC/DRC reports establish consistency under the documented rules; the findings above come from circuit and datasheet review, which those automated checks do not replace.

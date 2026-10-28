# Engineering Review

[Project overview](../README.md) · [Design gallery](README.md) · [Verification](checks/README.md)

**Review date:** 2026-10-28 · **Stage:** CAD design, unbuilt

## Review summary

The inspected PCB dimensions are compatible with the fabrication capabilities compared below. The recorded ERC and DRC checks pass. Circuit review identified three open items: Q1 battery power switching, Q2 LED power switching, and D4 LED selection and pin mapping.

## Manufacturing dimensions

**Stackup:** two copper layers, 35 µm copper per side, nominal 1.6 mm FR-4. **Outline:** 66.04 × 33.02 mm.

| Feature | Design evidence | JLCPCB two-layer, 1 oz comparison |
| --- | --- | --- |
| Track width | 265 segments at 0.20 mm; 88 at 0.30 mm | Above the 0.10 mm minimum. |
| Copper clearance | Closest measured track/via gap ≈0.150 mm; explicit 0.15 mm minimum passes DRC | Compatible with the 0.10 mm track-spacing and 0.15 mm SMD-pad-spacing criteria. |
| Through vias | 80 vias, each 0.60 mm diameter / 0.30 mm drill | Within the published via-sizing capability. |
| Via annular ring | 0.15 mm nominal | Within the published via-sizing capability. |
| Copper to board edge | Closest measured gap ≈0.501 mm; saved minimum 0.50 mm | Above the 0.20 mm routed-edge criterion. |

Comparison: [JLCPCB manufacturing capabilities](https://jlcpcb.com/capabilities/pcb-capabilities/), accessed 2026-10-28. This assessment covers the listed dimensions for the stated process. Final fabrication release includes Gerber, drill/slot, solder-mask, finish, and assembly review.

The supplied global minimum clearance and track-width settings are zero. The Default net-class clearance remains active; its preferred track width is a routing setting. A separate copy passed the explicit minimum constraints documented in [verification](checks/README.md). See [KiCad 10 design-rule documentation](https://docs.kicad.org/10.0/en/pcbnew/pcbnew.html#configuring-design-rules).

## Open design items

### Q1 — USB/battery power path

Q1 is a DMG3414U N-channel MOSFET with gate at VBUS, source at +BATT, and drain at VHI, the regulator input rail. With USB present, positive gate-to-source voltage can connect the system rail to the battery outside the charger-controlled path. Battery-only operation can instead rely on the body diode while the channel is off.

**Next action:** establish the intended power-path behavior, select the device, and verify source/drain orientation and reverse-current isolation.

### Q2 — LED power switch

Q2 is also a DMG3414U. Its source is fixed at 3.3 V and its gate receives a 0–3.3 V GPIO signal, so the channel cannot obtain positive gate-to-source drive. The body diode can still feed the LED rail.

**Next action:** select a suitable high-side switch and confirm its enable polarity and pin connections.

Device reference for Q1/Q2: [Diodes Incorporated DMG3414U](https://www.diodes.com/part/view/DMG3414U).

### D4 — LED selection and pin mapping

The generic WS2812B symbol and selected WS2812B-2020 footprint reference different pin assignments:

| Pin | Schematic symbol | WS2812B-2020 device |
| --- | --- | --- |
| 1 | VDD | Data out |
| 2 | Data out | GND |
| 3 | GND | Data in |
| 4 | Data in | VDD |

The referenced device also lists a 3.7–5.3 V supply range; the design derives its LED rail from 3.3 V.

**Next action:** choose the exact LED variant, align its symbol and footprint pin mapping, confirm the supply requirement, and update the PCB connections. Reference: [Worldsemi WS2812B-2020 datasheet, pages 2–3](https://cdn-shop.adafruit.com/product-files/4684/4684_WS2812B-2020_V1.3_EN.pdf).

## Layout and library notes

- The module's antenna keepout is present on both copper layers and respected by the saved fills. PCB material remains beneath the antenna.
- All symbol and footprint identifiers resolve in the standard KiCad 10 libraries. No custom symbol or footprint libraries are required.
- The ESP32-S3-MINI-1 symbol uses the ESP32-S2-MINI-1 footprint assignment also supplied by KiCad 10's stock library.
- Missing U2/D4 component bodies are identified in the [3D CAD view](README.md#3d-cad-view).
- The component list contains generic selections; exact purchasing part numbers remain part of assembly preparation.

## Validation scope

Evidence comprises CAD geometry, saved automated checks, and targeted circuit/datasheet review. Hardware, RF/enclosure performance, USB compliance, and power/thermal behavior remain to be validated on a built board. The open circuit items above were preserved for correction in the design source.

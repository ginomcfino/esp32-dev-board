# ESP32-S3 Development Board

A two-layer development board built around the ESP32-S3-MINI-1, integrating native USB-C connectivity, battery charging, fuel monitoring, and accessible GPIO.

**Design stage:** CAD, unbuilt · **Design tool:** KiCad 10

![Front PCB layout: copper, silkscreen, and board outline](docs/images/pcb-front.svg)

## Design overview

| Subsystem | Implementation |
| --- | --- |
| Processing and radio | ESP32-S3-MINI-1 module |
| USB | USB-C connector with native ESP32-S3 USB data interface |
| Power | AP2112K 3.3 V regulator and USB/battery power circuitry |
| Battery management | MCP73831 single-cell charger and LC709203F fuel gauge |
| Expansion and controls | GPIO headers, I2C connector, reset/boot buttons, and indicator LEDs |
| PCB | 66.04 × 33.02 mm; two copper layers; 1.6 mm FR-4 |

## Project files

| Resource | Contents |
| --- | --- |
| [KiCad project](hardware/esp32-s3-development-board.kicad_pro) | Editable schematic, layout, and project settings; open with KiCad 10 and its standard libraries. |
| [Schematic](exports/schematic.pdf) | Complete single-sheet circuit diagram. |
| [Component list](exports/bom.csv) | References, values, footprints, and quantities. |
| [Design gallery](docs/README.md) | Labeled PCB views, schematic preview, and 3D CAD render. |
| [Verification](docs/checks/README.md) | ERC, DRC, connectivity, and schematic/PCB consistency reports. |
| [Engineering review](docs/engineering-review.md) | Manufacturing dimensions and open design items. |

## Verification status

Recorded KiCad 10.0.5 checks report **0 errors, 0 warnings, 0 unconnected items, and 0 schematic/PCB mismatches** under the saved project rules.

Open design items cover Q1/Q2 power switching and D4 LED pin mapping and supply selection. Details and next actions are consolidated in the [engineering review](docs/engineering-review.md).

## Authorship

Circuit and PCB design developed manually by me. Component libraries, manufacturer models, and other third-party assets retain their original attribution.

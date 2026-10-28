# ESP32-S3 USB-C and Battery Development Board

A manually designed, two-layer development board built around the ESP32-S3-MINI-1 module. It combines native USB, 3.3 V regulation, single-cell battery charging and fuel-gauge circuitry, GPIO headers, an I2C connector, and reset/boot controls.

![Front copper and silkscreen layout](docs/images/pcb-front.svg)

**Status:** unbuilt CAD design study. KiCad 10.0.5 reports zero ERC/DRC errors or warnings under the saved rules. The [engineering review](docs/engineering-review.md) records circuit issues that need resolution before fabrication; passing automated checks does not verify circuit operation.

This is my manually developed circuit and PCB design. The ESP32 module, standard component libraries, and manufacturer models retain their original attribution.

- [Hardware source](hardware/): open `esp32-s3-development-board.kicad_pro` in KiCad 10 with its standard libraries.
- [Schematic PDF](exports/schematic.pdf) and [component list](exports/bom.csv).
- [Visual guide](docs/visuals.md): labeled schematic, front/back layout, and 3D views.
- [Verification](docs/checks/README.md) and [manufacturing / circuit review](docs/engineering-review.md).

The component list is a design BOM; generic component values still require exact purchasing part numbers before assembly.

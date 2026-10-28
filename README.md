# ESP32-S3 Development Board

An ESP32-S3 development board design combining USB-C connectivity, 3.3 V regulation, battery charging and fuel monitoring, GPIO headers, and an I2C interface.

![PCB front copper and silkscreen layout](docs/images/pcb-front.svg)

**Status:** CAD design study; not yet fabricated or bench-tested. ERC, DRC, and schematic-to-board checks report zero findings in KiCad 10.0.5 under the saved project rules. Open circuit items are recorded in the check notes.

This is my manually developed circuit and PCB design. Component libraries, manufacturer models, and other supplied assets retain their original attribution.

- [Hardware source](hardware/): schematic, PCB, and project settings.
- [Schematic PDF](exports/schematic.pdf) and [component list](exports/bom.csv).
- [Visual guide](docs/README.md): labeled board and schematic views.
- [Check notes](docs/checks/README.md): automated-check results and circuit review findings.

Open `hardware/esp32-s3-development-board.kicad_pro` with KiCad 10 and its standard symbol, footprint, and 3D model libraries.

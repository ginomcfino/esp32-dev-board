# Visual Guide

Generated from the packaged hardware files using KiCad 10.0.5. These are CAD exports of an unbuilt board.

| Visual | What it shows |
| --- | --- |
| [Front PCB layout](images/pcb-front.svg) | Front copper, front silkscreen, and board outline, viewed from above. |
| [Back PCB layout](images/pcb-back.svg) | Back copper, back silkscreen, and board outline, mirrored to show the underside. |
| [Schematic overview](images/schematic-overview.png) | Single-sheet preview; use the vector PDF for readable detail. |
| [Schematic PDF](../exports/schematic.pdf) | Complete electrical schematic. |
| [3D CAD render](images/pcb-3d-render.png) | Angled top view, with incomplete component-body coverage. |

![Angled CAD render; U2 and D4 component bodies are unavailable](images/pcb-3d-render.png)

The installed standard library does not contain the assigned 3D models for **U2 (ESP32 module)** or **D4 (WS2812B-2020 LED)**. Those footprints remain present in the design and component list. The render therefore does not represent a fully populated assembly. Mounting holes and the test point do not have component-body models.

![Front copper and silkscreen, top view](images/pcb-front.svg)

![Back copper and silkscreen, underside view](images/pcb-back.svg)

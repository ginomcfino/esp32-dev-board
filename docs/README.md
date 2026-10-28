# Design Gallery

[Project overview](../README.md) · [Schematic PDF](../exports/schematic.pdf) · [Verification](checks/README.md)

Native exports from the packaged KiCad 10.0.5 design. Layout SVGs and the schematic PDF provide scalable detail.

## Front PCB layout

Top view showing front copper, front silkscreen, and the board outline.

![Front PCB layout, viewed from above](images/pcb-front.svg)

## Back PCB layout

Underside view showing back copper, back silkscreen, and the board outline. The export is mirrored for this viewing direction.

![Back PCB layout, viewed from underneath](images/pcb-back.svg)

## Schematic

Single-sheet overview. Open the [schematic PDF](../exports/schematic.pdf) for readable circuit detail.

![Complete schematic overview](images/schematic-overview.png)

## 3D CAD view

Angled top view of the board and available component models.

![Angled top CAD view; U2 and D4 component bodies are absent](images/pcb-3d-render.png)

**Model coverage:** the installed library lacks the assigned U2 ESP32 module and D4 LED bodies. Their footprints are present in the PCB. Mounting holes and the test point have no assigned component-body models.

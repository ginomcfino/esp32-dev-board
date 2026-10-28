# Design Verification

[Project overview](../../README.md) · [Design gallery](../README.md) · [Engineering review](../engineering-review.md)

**Recorded check date:** 2026-10-28 · **Tool:** KiCad 10.0.5

## Results

Checks used the saved project rules and included error, warning, and exclusion severities.

| Check | Errors | Warnings | Excluded findings | Report |
| --- | ---: | ---: | ---: | --- |
| Schematic ERC | 0 | 0 | 0 | [ERC](erc.json) |
| PCB DRC | 0 | 0 | 0 | [DRC](drc.json) |
| Unconnected PCB items | 0 | 0 | 0 | [Connectivity](drc.json) |
| Schematic/PCB consistency | 0 | 0 | 0 | [Parity](drc.json) |

## Dimensional check

A separate copy also passed with these explicit global constraints; the packaged project retains its supplied settings.

| Constraint | Minimum |
| --- | ---: |
| Copper clearance | 0.15 mm |
| Track width | 0.20 mm |
| Connection width | 0.10 mm |

[Dimensional-check report](drc-dimension-probe.json). All other settings were retained. Manufacturing comparisons and circuit findings are recorded in the [engineering review](../engineering-review.md).

## Rule configuration

There are no finding-specific ERC or DRC exclusions. The saved configuration ignores the following categories:

| Check | Ignored categories |
| --- | --- |
| ERC | `single_global_label`, `four_way_junction`, `simulation_model_issue`, `footprint_filter` |
| DRC | `missing_courtyard`, `track_not_centered_on_via`, `tuning_profile_track_geometries`, `footprint_filters_mismatch`, `pth_inside_courtyard`, `npth_inside_courtyard`, `footprint_type_mismatch` |

## Reproduce the checks

Run from the package root with KiCad 10's `kicad-cli` on your PATH:

```sh
kicad-cli sch erc --format json --severity-all --exit-code-violations --output erc-local.json hardware/esp32-s3-development-board.kicad_sch
kicad-cli pcb drc --format json --schematic-parity --severity-all --exit-code-violations --output drc-local.json hardware/esp32-s3-development-board.kicad_pcb
```

For the dimensional check, duplicate the hardware directory, set the three global constraints above in Board Setup, and run DRC on that copy.

## File provenance

Packaging standardized the native filenames and matching project/sheet references, and updated the standard 3D-model variable from KiCad 9 to KiCad 10. Circuit connectivity, routing, rule severities, and exclusions were retained. Exports were generated from the packaged design.

[SHA-256 manifest](files-sha256.json) records package contents, excluding the manifest itself. These saved verification reports are unchanged by the documentation cleanup.

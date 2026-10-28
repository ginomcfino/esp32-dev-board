# Verification Notes

Checked on 2026-10-28 with **KiCad 10.0.5**. Reports include error, warning, and exclusion severities. No circuit, routing, rule severity, or exclusion changes were made during packaging.

| Check | Errors | Warnings | Excluded findings |
| --- | ---: | ---: | ---: |
| Schematic ERC | 0 | 0 | 0 |
| PCB DRC | 0 | 0 | 0 |
| Unconnected PCB items | 0 | 0 | 0 |
| Schematic / PCB consistency | 0 | 0 | 0 |

Native reports: [ERC](erc.json), [DRC and schematic parity](drc.json).

## Additional dimensional check

A separate scratch copy passed the same checks after setting global minimum copper clearance to **0.15 mm**, minimum track width to **0.20 mm**, and minimum connection width to **0.10 mm**. All other settings were retained. The packaged project keeps the supplied settings unchanged. The [scratch-copy report](drc-dimension-probe.json) is a limited dimensional check, not a complete fabricator-specific DFM approval.

The supplied project has no finding-specific ERC or DRC exclusions. These categories are already ignored by its saved configuration:

- ERC: `single_global_label`, `four_way_junction`, `simulation_model_issue`, `footprint_filter`.
- DRC: `missing_courtyard`, `track_not_centered_on_via`, `tuning_profile_track_geometries`, `footprint_filters_mismatch`, `pth_inside_courtyard`, `npth_inside_courtyard`, `footprint_type_mismatch`.

## Reproduce

Run from the package root with KiCad 10's `kicad-cli` on your PATH:

```sh
kicad-cli sch erc --format json --severity-all --exit-code-violations --output erc-local.json hardware/esp32-s3-development-board.kicad_sch
kicad-cli pcb drc --format json --schematic-parity --severity-all --exit-code-violations --output drc-local.json hardware/esp32-s3-development-board.kicad_pcb
```

To repeat the dimensional probe, copy the hardware directory elsewhere and set the three minimum constraints above in Board Setup before running DRC.

## Packaging changes

Native filenames and matching internal project/sheet references were standardized to `esp32-s3-development-board`. Standard 3D model paths were updated from the KiCad 9 variable to the KiCad 10 variable. All other native design content is unchanged. PDFs, the component list, and images were regenerated from these files. Editor state, backups, and caches were omitted.

The [engineering review](../engineering-review.md) distinguishes the clean automated reports from unresolved functional concerns. No fabrication, bench measurements, RF validation, or USB compliance testing has been performed.

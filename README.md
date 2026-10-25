# MSPM0 Microcontroller PCB

A custom two-layer microcontroller board built in KiCad 9 around the Texas Instruments MSPM0G3507. This project explores embedded hardware design from schematic capture and component selection through PCB layout review and fabrication and assembly file preparation.

![MSPM0 PCB layout](docs/Reviewed-board-front.svg)

## Hardware

- TI MSPM0G3507 microcontroller with an external 8 MHz crystal
- USB-C power input with USB data-line ESD protection
- SPX3819 3.3 V regulator
- CH340E USB-to-UART bridge
- LIS2DH three-axis accelerometer connected over I²C
- Tag-Connect SWD programming and debug access
- Two-layer PCB with ground pours; 32 fitted components

## Engineering work

Developed the schematic and component integration, then refined the board through datasheet review and assisted layout revisions. Review addressed the USB power path, open-drain UART pull-up, reset network, local decoupling, voltage-reference capacitance, regulator bypass and USB input capacitance. Prepared Gerber and drill exports, an assembly BOM, and component placement files with sourcing and orientation notes.

The project was a hands-on introduction to KiCad and electrical design fundamentals. AI tools assisted with design review, routing revisions, and manufacturing documentation.

## Current status

**Design and manufacturing files prepared; physical bring-up and firmware validation pending.**

- Saved-design checks reported zero PCB DRC errors, zero unconnected items, zero schematic parity differences, and zero schematic ERC errors under the configured rules.
- Nine library-footprint warnings and two library-symbol warnings remain documented in the [design review](docs/Final-review.md).
- The exact crystal still requires sourcing; sensor/USB land patterns and assembly-model rotations require manufacturer review before ordering.

Next steps are current-limited power-up, rail measurements, SWD connection, UART testing and I²C accelerometer communication. This is a USB bench prototype; hardware operation and flight suitability have not been demonstrated.

## Repository guide

| Files | Purpose |
| --- | --- |
| `TI MSPM0.kicad_pro`, `.kicad_sch`, `.kicad_pcb` | Editable KiCad project, schematic and board |
| `*.kicad_sym`, `sym-lib-table` | Project-local symbol libraries |
| [Schematic PDF](docs/Reviewed-schematic.pdf) | View the circuit without installing KiCad |
| [Board layout](docs/Reviewed-board.svg) | PCB layout overview |
| [Design review](docs/Final-review.md) | Circuit corrections, checks and remaining issues |
| [Manufacturing files](manufacturing/) | Gerbers, drills and export archives |
| [Assembly notes](manufacturing/assembly/README.md) | BOM, placement files, sourcing and assembly requirements |

Open `TI MSPM0.kicad_pro` in KiCad 9. Project-local symbol libraries resolve through `${KIPRJMOD}`. Preserve the reviewed board footprints when opening the project; some intentionally differ from library copies. External 3D models are not bundled.

**Author:** Isaac Nuriddin · Electrical Engineering, Embry-Riddle Aeronautical University

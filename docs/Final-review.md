# USB bench prototype — final review, 24 October 2026

The edited schematic and live PCB are saved. Gerber/drill exports are in ../manufacturing/gerbers, with a ZIP for bare-board fabrication review. This is a reviewed prototype, not hardware-qualified or factory-approved. Design review and routing revisions were assisted by AI tools.

## Checks on the final saved design

- PCB DRC: zero errors, zero unconnected items, zero schematic parity differences; nine library-footprint warnings.
- Schematic ERC: zero errors; two library-symbol warnings (USB and Tag-Connect).
- Zones refilled before saving and exporting. Schematic PDF and PCB plots generated for inspection.
- Checks use the project's configured rules; ignored categories are recorded in the JSON reports. No claim of exhaustive electrical, signal-integrity, thermal or manufacturing simulation.

## Changes and reasons

| Change | Why |
|---|---|
| R4 100 kΩ to 0 Ω, as authorized | The original value in series with USB power would prevent normal operation. A zero-ohm link is not a fuse. |
| R9 2.2 kΩ from UART TX to 3.3 V | MCU PA0 is open drain and needs a pull-up. Start UART testing at a modest baud rate. |
| C15 100 nF at MCU supply | Adds local high-frequency decoupling alongside existing bulk capacitance. |
| C16 10 µF by accelerometer | Adds local bulk capacitance alongside existing C14. |
| C3 470 nF to 1 µF | Brings external reference decoupling toward TI's recommendation. Select a capacitor with suitable effective capacitance under DC bias. |
| R2 5.1 kΩ to 47 kΩ; C4 470 nF to 10 nF | Uses the recommended reset network. |
| C11 470 nF to 10 nF | Uses SPX3819 recommended bypass capacitance, avoiding the excessive startup delay of the larger value. |
| C9 10 µF to 4.7 µF | Reduces nominal direct USB input capacitance from 10.94 to 5.64 µF. Actual inrush still needs measurement. |
| Shortened UART TX using a brief back-layer crossing | Replaces a long perimeter detour while preserving connectivity. |
| Earlier removal of tiny collinear routing segments | Reduced 539 track segments to 349 before the new functional additions. Segment count is not the same as circuit complexity. |
| J1 four ground lands changed from 0.60 × 1.15 mm to 0.60 × 1.10 mm, with more rounded corners | Clears the existing 0.254 mm copper-to-hole rule without moving holes. This is a custom footprint change, not a manufacturer-approved replacement land pattern. |
| Corrected stale part metadata and synchronized PCB fields | Prevents old resistor/capacitor purchasing values from silently overriding reviewed values. U1 spelling corrected to MSPM0G3507SPTR. |
| Added project-local CH340E and LIS2DH symbol variants | Models V3 as an input in external 3.3 V mode and SA0 as an input in I²C mode. These correct ERC pin semantics without changing the associated wiring. |

Earlier placement changes moved U2 from (55.9,81.9) to (55.9,88.25) mm and U4 from (61,89) to (61.4,89) mm. Board outline, mounting-hole positions and external connector positions were retained.

There is **no new 3.3 V plane**. Both copper zones are GND. The 3.3 V vias connect routed supply tracks between layers. Vias are normal on a two-layer board; using one where it avoids a long detour can improve layout.

## Remaining issues and disposition

1. **Fine-pitch accelerometer assembly:** the original LIS2DH footprint has 0.20 × 0.325 mm lands. JLC's generic capability page lists a 0.25 × 0.25 mm minimum SMD pad, so obtain their DFM acceptance for this footprint. JLC lists the exact LIS2DHTR as C155670 for Standard PCBA with X-ray inspection. That listing is evidence of assembly support, not approval of this particular artwork. Do not substitute LIS2DH12 without redesigning its different pinout.
2. **Library differences:** nine footprint warnings cover J1, J2, U4, U5, R9, C16 and three fiducials. They are library-copy differences, not reported clearance violations. Preserve the reviewed board copies; blindly refreshing library footprints can undo custom geometry. The two symbol warnings likewise remain disclosed.
3. **Procurement:** changed/new passives require actual manufacturer part selection. Removed stale purchasing fields are intentional. This package is bare-board fabrication data, not a verified turnkey assembly BOM/CPL. Choose suitable voltage ratings, dielectric, tolerance and effective capacitance; R3's 100 kΩ oscillator resistor must meet TI's 0.1% / 25 ppm requirement.
4. **Crystal:** C5/C6 remain 15 pF for the existing 8 MHz crystal. Load matching depends on stray capacitance. Check startup and frequency on a prototype; avoid loading the oscillator with an ordinary probe unnecessarily.
5. **USB and power:** short USB layer transitions remain. No controlled-impedance or eye-diagram qualification was performed. Check enumeration, repeated plug/unplug, both connector orientations, supply droop/inrush and regulator temperature under actual load.
6. **Reliability scope:** USB bench operation only. No flight, vibration, temperature-range or EMC qualification. Passing DRC/ERC cannot prove correct firmware, assembly quality or physical operation.

## Manufacturing settings and first power-up

Use two layers, 1.6 mm board thickness and 1 oz copper. Standard vias are at least 0.30 mm drill; the smallest signal tracks are around 0.152 mm. Inspect JLC's Gerber preview, outline, plated slots and separate plated/non-plated drills. Request factory review of the sensor lands and modified USB ground lands. If using JLC assembly, select Standard PCBA with the required sensor X-ray inspection. No order or upload was placed.

First inspect soldering and check power-to-ground resistance. Power through a current-limited USB source, verify 3.3 V and the MCU core rail, and check heating before attempting firmware. Verify SWD identification, reset, UART transmit/receive and I²C sensor communication. Then test repeated power cycles and USB reconnection. Configure MCU pin mux and external oscillator correctly in firmware. Use the debug connector's 3.3 V pin as target-voltage reference unless intentionally designing a separate power arrangement.

## What to learn from this layout

Place each IC's decoupling at its power pins before routing signals. Place power entry, protection and regulator as a compact group, and put communicating parts near one another. Route critical short connections first, keep ground return paths continuous, then use the other layer for crossings. A few deliberate vias usually beat a long perimeter detour. The significant problems here included circuit details—open-drain pull-up, reset and supply capacitors—not merely unattractive traces. A clean appearance and a successful DRC are useful checks, but neither replaces datasheet review and bench testing.

## References

- TI MSPM0G3507 datasheet: https://www.ti.com/lit/ds/symlink/mspm0g3507.pdf
- MaxLinear SPX3819 datasheet: https://www.maxlinear.com/document?id=22106
- WCH CH340E manufacturer datasheet mirror: https://cdn.sparkfun.com/assets/e/3/c/3/1/DS-16278-CH340E.pdf
- ST LIS2DH manufacturer datasheet mirror: https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/166/LIS2DH.pdf
- GCT USB4105 drawing: https://gct.co/files/drawings/usb4105.pdf
- JLC capabilities: https://jlcpcb.com/capabilities/Capabilities
- JLC original sensor listing: https://jlcpcb.com/partdetail/STMicroelectronics-LIS2DHTR/C155670

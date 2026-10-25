# Placement verification guide

Top view. Coordinates below use KiCad native placement coordinates in mm: X right, Y up (negative Y on this board). All 32 fitted parts are on Top. Compare actual pad numbers in JLC's placement preview, since a supplier model can use a different zero-degree orientation from KiCad. Native rotations in the CPL are not claimed to be JLC-model-verified.

| Reference | Pad | X (mm) | Y (mm) | Net |
|---|---|---:|---:|---|
| J1 | A1 | 49.930000 | -85.050000 | GND |
| J1 | A5 | 49.930000 | -87.000000 | /USBCC1 |
| J1 | A6 | 49.930000 | -88.000000 | /USBCD+ |
| J1 | A7 | 49.930000 | -88.500000 | /USBCD- |
| J1 | B5 | 49.930000 | -90.000000 | /USBCC2 |
| U1 | 1 | 71.637500 | -86.550000 | /UART0TX |
| U2 | 1 | 54.762500 | -87.300000 | /USBCD- |
| U3 | 1 | 64.562500 | -77.450000 | +VBUSF |
| U4 | 1 | 59.287500 | -88.000000 | /USBD+ |
| U5 | 1 | 82.825000 | -96.762500 | Net-(U1-PB2) |
| X1 | 1 | 67.900000 | -98.350000 | /HXFIN |
| X1 | 2 | 70.100000 | -98.350000 | GND |
| X1 | 3 | 70.100000 | -96.650000 | /HXFOUT |
| X1 | 4 | 67.900000 | -96.650000 | GND |

U1 must be the 48-pin LQFP PT package, not a QFN or 64-pin package. U5 must be the 14-pin LIS2DH, not the 12-pin LIS2DH12. U3 must be MaxLinear's original part, not a similarly named clone. X1 is a passive crystal: pins 1 and 3 are oscillator connections; pins 2 and 4 are grounded case pads. J1 opens toward the left board edge. Capacitors and resistors selected here are nonpolar.

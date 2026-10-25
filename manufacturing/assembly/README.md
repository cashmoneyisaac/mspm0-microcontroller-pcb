# JLCPCB assembly files

Upload **TI-MSPM0-BOM.csv** as BOM and **TI-MSPM0-CPL.csv** as CPL. Upload the refreshed TI-MSPM0-JLC-bare-board.zip as Gerbers; it now also includes solder-paste layers.

32 fitted components per board, 19 BOM groups, all Top. Quantities in the BOM are per board; choose the board quantity separately on JLC. The files have matching unique reference sets and no missing placement rows. Mounting holes H1–H4, FID1–FID3 and the J2 Tag-Connect contact pattern require no installed component and are excluded from both upload files. The reference holes/fiducials remain in the Gerbers.

## One sourcing action remains

**X1 retains the exact ECS-80-12-33-JGN-TR3 crystal.** Its MPN and specifications are filled in, but the LCSC code is intentionally empty because no exact JLC catalogue listing was verified. Use JLC Standard PCBA's sourcing process for that exact MPN. Do not accept an automatic crystal substitution without checking frequency, load capacitance, ESR, drive limit, package and pinout. A matching frequency and package alone is insufficient. The BOM is complete as an engineering parts list; it is not yet a fully stock-matched JLC order.

The remaining 18 groups have verified catalogue codes. Stock and customer-account availability must be checked during matching; public catalogue presence is not a stock reservation. Never skip U1 or U5 because they are unavailable. Do not replace the 14-pin LIS2DH with LIS2DH12.

## Placement confirmation before payment

Set Standard PCBA, Top only, and Confirm Parts Placement = Yes. The sensor listing requires X-ray inspection. Keep the separate stencil purchase off when JLC performs assembly.

The CPL uses native KiCad placement X/Y in millimetres and counterclockwise angles normalized to 0–360 degrees. Negative Y coordinates are intentional; they follow the native export and preserve the Gerber coordinate basis. Do not independently make them positive. All coordinate and rotation values were compared with KiCad's native export.

JLC's selected component models may have different zero-angle conventions. **Their placement preview has not yet been inspected**, so rotations are not certified against those models. Use Placement-guide.md and Assembly-top.svg to verify U1–U5 pin 1, crystal active/case pins, and J1's opening direction. Correct any model-dependent offsets in the JLC placement step before approval. Select confirmation so the factory supplies placement for approval.

Request factory acceptance of the original 0.20 × 0.325 mm sensor lands and modified USB ground lands, as described in the full PCB review. This task selected parts and generated assembly files; it did not change tracks, part positions, or circuit values.

## Part selection details

Passive manufacturers may differ from incomplete original purchasing fields, while electrical values and board packages are preserved. C3 is Samsung CL10B105KA8NNNC, 1 µF 25 V X7R; its typical DC-bias curve was inspected for the 3.3 V reference application. This does not certify worst-case capacitance over all temperatures and aging. C5/C6 are C0G 5% parts. R3 specifically retains 0.1% / 25 ppm performance. C9 is a 4.7 µF 25 V X7R part. J1 uses the footprint-family-compatible 0.60 mm shell-stake option USB4105-GF-A-060. U3 uses original MaxLinear SPX3819M5-L-3-3/TR. See Part-selections.md for catalogue links.

The source hashes and validation results are in validation.json. If board placement changes, regenerate the CPL and Gerbers together.

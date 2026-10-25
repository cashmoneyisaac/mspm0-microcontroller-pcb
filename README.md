# mspm0 microcontroller pcb

my first custom microcontroller board, built around the ti mspm0g3507 in kicad 9. i made this project to learn pcb design, component selection, and how to take a schematic through layout and manufacturing preparation.

![mspm0 pcb layout](docs/Reviewed-board-front.svg)

## hardware

- ti mspm0g3507 microcontroller with an external 8 mhz crystal
- usb-c power input with usb data-line esd protection
- spx3819 3.3 v regulator
- ch340e usb-to-uart bridge
- lis2dh three-axis accelerometer connected over i²c
- tag-connect swd programming and debug access
- two-layer pcb with ground pours and 32 fitted components

## files

- editable kicad project, schematic, board, and symbol libraries in the root folder
- [schematic pdf](docs/Reviewed-schematic.pdf)
- [board layout](docs/Reviewed-board.svg)
- [design review](docs/Final-review.md)
- [gerbers and drill files](manufacturing/gerbers/)
- [bom, placement files, and assembly notes](manufacturing/assembly/README.md)

isaac nuriddin · electrical engineering · embry-riddle aeronautical university

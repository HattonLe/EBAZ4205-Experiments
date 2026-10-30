# EBAZ4205-Experiments
Experiments and hacks using EBAZ4205 and an Adapter board.


Extra 2 FPGA signals mod
=========================
This modification provides a valuable extra two FPGA signals for user applications, e.g. as an I2c bus, or for a UART etc.

Examining an EBAZ4205 schematic diagram, two 'unused' FPGA signals are present, L14 and N16.

Both connect to resistors that are not fitted and they both sit next to unpopulated IC X3.
U31-L14 --> R2609, and U31-N16 --> R2608.
Adjacent is X3 which has pins 5 and 6 spare (due to not fitted R120, R122, R2438, R2439). This is an ideal
location to place a new board connector.

Fit a 1.25mm SMD JST MX male socket to X3, and using some 0.3mm copper wire connect up the following
	Righthand end of R2609 to X3 pin 5,
	Righthand end of R2608 to X3 pin 6.
	Connect X3 pin 4 across to X3 pin 7.
	Connect a SMD 0402 low ((or zero) ohm resistor to R1279 (one the rear side of the board).

I used a dab of Epoxy adhesive to secure the bottom of the JST connector to the PCB to help support it when
unplugging a cable from it.

<img width="3334" height="2879" alt="20261030_153558" src="https://github.com/user-attachments/assets/596aedf3-14e2-4bf2-b5e5-0e07653e9e59" />

This gets us the following pinout on the JST connector

3v3 X3 pin 8 --> JST pin 1 --> 3v3
GND X3 pin 7 --> JST pin 2 --> 0v
N\C X3 pin 6 --> JST pin 3 --> U31-N16
N\C X3 pin 5 --> JST pin 4 --> U31-L14

I used a readymade cable from AliExpress to plug into the new X3 JST socket, and and in a XDC file, added
in the following lines to define the new signals available at the X3 JST 1.25 Connector

set_property PACKAGE_PIN N16 [get_ports X3_YELLOW]
set_property PACKAGE_PIN L14 [get_ports X3_GREEN]
set_property IOSTANDARD LVCMOS33 [get_ports X3_YELLOW]
set_property IOSTANDARD LVCMOS33 [get_ports X3_GREEN]
<img width="3328" height="2721" alt="20261030_153545" src="https://github.com/user-attachments/assets/f5257b28-e31c-422e-a1e9-2193c7f82f0e" />



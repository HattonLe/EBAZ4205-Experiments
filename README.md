# EBAZ4205-Experiments
Experiments and hacks using EBAZ4205 and an Adapter board.


Extra 2 FPGA signals mod
=========================
Examining the schematic diagram, two 'unused' FPGA signals are present, 
U31-L14 --> R2609, and U31-N16 --> R2608.
Both connect to resistors that are not fitted and they both sit next to unpopulated IC X3.
X3 has pins 5 and 6 spare (due to not fitted R120, R122, R2438, R2439).

Fit a 1.25mm SMD JST MX male socket to X3, and using some 0.3mm copper wire connect up the following
	Righthand end of R2609 to X3 pin 5,
	Righthand end of R2608 to X3 pin 6.
	Connect X3 pin 4 across to X3 pin 7.
	Connect a SMD 0402 low ((or zero) ohm resistor to R1279 (one the rear side of the board).
	
This gets us the following pinout on the JST connector
3v3 X3 pin 8 --> JST pin 1 --> 3v3
GND X3 pin 7 --> JST pin 2 --> 0v
N\C X3 pin 6 --> JST pin 3 --> U31-N16
N\C X3 pin 5 --> JST pin 4 --> U31-L14

and in a XDC file, add in the following lines to define the new signals available at the X3 JST 1.25 Connector
set_property PACKAGE_PIN N16 [get_ports X3_YELLOW]
set_property PACKAGE_PIN L14 [get_ports X3_GREEN]
set_property IOSTANDARD LVCMOS33 [get_ports X3_YELLOW]
set_property IOSTANDARD LVCMOS33 [get_ports X3_GREEN]

# EBAZ4205-Experiments
Experiments and hacks using EBAZ4205 and an Adapter board.


FPGA Reset button mod (replaces the U30 ACGI voltage monitor, if fitted)
========================================================================
This modification provides a reset button signal input to the FPGA for user applications.

If U30 is populated (on the rear of the PCB), its output needs to be disconnected from the FPGA, and instead wired
to the reset button which will be situated on the front side of the PCB between U23 pin 1 and pins 2\4.

This can be done by removing R1481, and using some 0.3mm insulated wire, connect the now free upper pad
(that goes to FPGA U31.W20) to the left hand side of R2468.

<img width="1289" height="833" alt="Wire" src="https://github.com/user-attachments/assets/aac16332-650d-4aba-b7ae-d0e691298311" />

At U23, pins 2 and 4 are tied to GND via R2471. We can use this large pad to connect one side of a N/O pushbutton.
The other side of the button is soldered to U23 pin 1, the latter is routed to the rear of the PCB to R2468.

<img width="1245" height="1330" alt="Button" src="https://github.com/user-attachments/assets/d5bd5438-7d19-485c-bd3a-1f0d516404ba" />

In a XDC file, add in the following lines to define the new reset button signal

```
# FPGA Reset signal Button
set_property PACKAGE_PIN W20 [get_ports Reset]
set_property PULLUP TRUE [get_ports Reset]
set_property IOSTANDARD LVCMOS33 [get_ports Reset]
```

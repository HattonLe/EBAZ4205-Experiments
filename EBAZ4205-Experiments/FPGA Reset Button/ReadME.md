# EBAZ4205-Experiments
Experiments and hacks using EBAZ4205 and an Adapter board.


FPGA Reset button mod (replaces the U30 ACGI voltage monitor, if fitted)
========================================================================
This modification provides a reset signal input to the FPGA for user applications.

If U30 is populated (on the rear of the PCB), its output needs to be disconnected from the FPGA, and instead wired
to the reset supervisor output. This can be done by removing R1481, and using some 0.3mm insulated wire, connect the
now free upper pad (that goes to FPGA U31.W20) to the junction of R1950, R1401, R2392.

The U65 reset supervisor (U65) just requires a N\O pushbutton to be connected between GND and U65 MR (pin 1).


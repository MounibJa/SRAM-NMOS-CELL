![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg)

#  SRAM Documentation

- [Read the documentation for project](docs/info.md)

# **Description**:
This project's goal is to design an SRAM bit cell using the back-to-back inverter design utilizing NMOS inverters rather than traditional CMOS, to observe any potential advantages and drawbacks compared to CMOS.

The traditional design for a standard 6-transistor (6T) SRAM bit cell stores a single bit of data using two cross-coupled CMOS inverters that form a bistable latch. These inverters are connected in a feedback loop, with each inverter’s output driving the other’s input. This configuration produces two stable states representing a logical ‘1’ and a logical ‘0’.

To write/read from the inverters, access transistors are connected to their respective outputs. These access transistors are controlled through their gates, and their drains are connected to the bitlines, called BL and BL_N.
To write a 1, you raise BL high and BL_N low and turn WL high; to write a 0, you reverse the bitline values while keeping WL high.

For reading, you precharge the bitlines to around VDD/2 and then turn on WL. This causes a small voltage difference to appear on the bitlines, which a sense amplifier can detect and amplify to determine the stored value.
# **Designs**
We are experimenting with two designs: one using an NMOS inverter relying on a resistor acting as a pull-up. This is due to its simple nature and it being easier to control the resistor values for our needed use case, though it will likely end up requiring lots of space, limiting how many can fit on a singular tile.

The second design will rely on the NMOS inverter utilizing a PMOS acting partly in the triode region to produce a resistor that will act similar to our first design but will consume much less space. The drawback here is how testing and comparing the values will be harder at the start to validate our cells in LTspice.

# **Plan**
First, we are going to test and see if the design itself works. We will start with the NMOS resistor design, seeing how straightforward it is to decide on our resistor's value. Then we will follow that up with testing SNM for hold, writing, and reading. After that, we will replace our resistor with a PMOS and modify the width and length to adjust its values to match the first design's resistors in terms of resistance.

Following that, we will begin designing the layout in Magic utilizing Sky130nm, before extracting it for parasitics and testing it using ngspice to validate whether our values still match those of the designs in LTspice.


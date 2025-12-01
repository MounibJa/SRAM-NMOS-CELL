![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg)

#  SRAM Documentation

- [Read the documentation for project](docs/info.md)

# **Description**:
This project's goal is to desin an SRAM BitCell using the back to back inverter design utulizing NMOS inverters rather than traditional CMOS to see any potential advantages and drawbacks compared to CMOS.

The traditional design for a standard 6-transistor (6T) SRAM bit cell stores a single bit of data using two cross-coupled CMOS inverters that form a bistable latch. These inverters are connected in a feedback loop, resulting in one's output driving the other's input. This ends up producing two states representing a logical '1' and logic '0'.

To write/read to the inverters you end up having an access transistor connected to their respective outputs. These access transistors are controlled connected to their gates and their drain is connected to the bitlines called BL and BL_N.
To write a 1 you'd raise BL high, and BL_N low and turn the WL high and vice versa to write a 1 while maintaining WL to be high.
For reading you precharge the lines to around VDD/2 and then turn on the WL, this should apply a voltage change onto the lines allowing a sense amp to amplify and read the change in the lines to determine what is stored.
# **Designs**
We are experimenting with two designs one using an NMOS inverter relying on a resistor acting as a pull up. This is due to its simple nature and it being easier to control the resistor values for our needed use case. Though will likely end up requiring lots of space limiting how many can fit on a singular tile.
The second design will rely on the NMOS inverter utilziing a pmos acting in triode region to produce a resistor that will act similiar to our first design but consuming much less space. Though the drawback here is just how testing and comparing the values will be harder at the start to valdiate our cells in LTspice will be.

# **Plan**
First we are going to test and see if the design itself works. We will first go with the NMOS resistor design seeing how straight forward that is to decde on our resistor's value. Then follow that up with testing SNM for hold, writing, and reading. Then we will replace our resistor ith a pmos and modify the Width and Length to adjust its values to match the first design's resistors in terms of resistance.

Following up we will begin designing the layout in Magic utilizing Sky130nm, before then extracting it for parasitics and testing it out utilizing ngspice validating to see if our values still match that of designs in LTspice.


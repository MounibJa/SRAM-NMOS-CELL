<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

The traditional SRAM bit-cell is implemented using back-to-back inverters constructed from NMOS and PMOS transistors, forming a bistable latch. The two inverters are cross-coupled so that the output of each drives the input of the other, enabling the cell to hold a logic ‘0’ or ‘1’.

Access to the storage nodes is provided by two NMOS transistors controlled by the word line (WL). These access transistors connect to the internal outputs of the inverters to their corresponding bit-lines (BL and BLB).

Write operation: By driving BL and BLB with complementary values and asserting WL, the access transistors force the internal node voltages, overwriting the latch and storing a new bit.

Read operation: Before reading, the bit-lines are precharged to around VDD/2. When WL is turned on, the latch experiences a disturbance on the bit-lines depending on the stored value. A sense amplifier detects and amplifies this small voltage difference to determine whether the cell contains a logic ‘0’ or ‘1’.

## Parameters and Goals

|VDD| 1.8 V |

## Design and Testing
We are going with two designs. One utilizing a resistor nmos inverter, the other shall be using a PMOS modelling itself as a resistor by modifying its Width and Length values and maintaing it in the triode region.
1. Resistor Design
<img width="507" height="325" alt="image" src="https://github.com/user-attachments/assets/34532381-83a7-4635-9c89-fab942c0c8d6" />

2. PMOS design
<img width="496" height="325" alt="image" src="https://github.com/user-attachments/assets/33d87ba1-d22f-4b5b-b87a-aa27b877e583" />




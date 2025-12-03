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

## Parameters

| Parameter | Value |
|-----------|-------|
| VDD | 1.8 V |
| W/L pulldown transistor | 2 |
| W/L access transistor | 3 |
| Resistor resistance | 50 kΩ |
| PMOS width | 0.42 μm |
| PMOS length | 1.2 μm |

## Goals

| Goal | Value |
|------|-------|
| Speed | 20 ns |
| SNM (hold) | 150 mV |
| SNM (write) | 200 mV |

## Design and Testing
We are going with two designs. One utilizing a resistor nmos inverter, the other shall be using a PMOS modelling itself as a resistor by modifying its Width and Length values and maintaing it in the triode region when needed to model a 50K ohm resistor.
1. Resistor Design
<img width="507" height="325" alt="image" src="https://github.com/user-attachments/assets/34532381-83a7-4635-9c89-fab942c0c8d6" />

2. PMOS design
<img width="496" height="325" alt="image" src="https://github.com/user-attachments/assets/33d87ba1-d22f-4b5b-b87a-aa27b877e583" />

## Simulation Testing
Tests completed on the Sram Cells:
1. Speed
The speed test is preform by first setting our WL, BL, BL_N low and then settling in on a stored value through setting up Initial conditions (IC) to make the cell store either a 1 or 0. THen we raise the BL and BL_N high and low depending on what we want the store value to change to. Then start measuring the time it took for inverter output values to stabilize and taking whichever took longer to stabilize as the the speed of our Cell.

2. SNM (hold)
The SNM hold test is to see how resisitive our cell is to noise. This is done by keep WL, BL, BL_N low and sweeping a voltage between the input node of one inverter and the output node of the other. Then plotting out the values alongside the inverse of the function, producing for us a butterfly curve where we then utilize matlab to measure the largest area possible within the bounds of the butterfly curve.
3. SNM (write)
The SNM write test is similiar to the hold test instead to turn BL or BL_N high and the other line low while having WL also high. 
# Resistor Pull up Values
1. Speed:
<img width="325" height="505" alt="SRAM_RES_Speed" src="https://github.com/user-attachments/assets/bc9934ba-f4d8-4646-ac74-12fce292e222" />

2. SNM (HOLD)
<img width="325" height="505" alt="MATLAB_RESIS_HOLD" src="https://github.com/user-attachments/assets/03422a4e-8d90-4d03-bbcb-e2fb54875d87" />



# PMOS Pull up Values
1. Speed:
<img width="325" height="505" alt="SRAM_PMOS_Speed" src="https://github.com/user-attachments/assets/7f6b8f60-99ca-48e3-9353-800dc2086c04" />

2. SNM (HOLD)

<img width="325" height="505" alt="MATLAB_PMOS_HOLD" src="https://github.com/user-attachments/assets/52917cb6-532e-47b2-88e3-559d95cd3e4d" />

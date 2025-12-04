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

## PMOS Configuration
We needed to find a way to make the pmos transistor a pseudo-resistor that works similarly to the 50K resistor in that the pull-up is balanced for stability whilst still being able to write. 

Initally the way we set this up was by connecting the gate of the pmos to its drain. This is a diode connected pmos, however it was not a good choice for modelling a resistor. For starters, the output of the charging node gets capped at VDD-Vth, because Vgs must be > than Vth, but Vgs = Vds, So when Vds < Vth, the pmos closes. 

Instead, we opted to connect the gate to drain, and pick a W/L ratio that best models our resistor in the Vd range that we expect to see (0-VDD). This works quite well as can be seen below. 


## Simulation Testing
Tests completed on the Sram Cells:
1. Speed
The speed test is preformed by first setting our WL, BL, BL_N low, and then settling in on a stored value through setting up Initial conditions (IC) to make the cell store either a 1 or 0. Then we raise the BL and BL_N high and low depending on what we want the store value to change to. Then start measuring the time it took for inverter output values to stabilize and taking whichever took longer to stabilize as the the speed of our cell. Note that the side that takes longer is the one going from 0 to 1 as the pull-up element isn't as strong as the pull-down element. 

2. SNM (hold)
The SNM hold test is to see how resisitive our cell is to noise. This is done by keep WL, BL, BL_N low and sweeping a voltage between the input node of one inverter and the output node of the other. Then plotting out the values alongside the inverse of the function, producing for us a butterfly curve where we then utilize matlab to measure the largest area possible within the bounds of the butterfly curve.
3. SNM (write)
The SNM write test is similiar to the hold test instead to turn BL or BL_N high and the other line low while having WL also high. Though as will be discussed later this test was unable to be preformed due to software limitations and time.



# Resistor Pull up Values
1. Speed:
<img width="325" height="505" alt="SRAM_RES_Speed" src="https://github.com/user-attachments/assets/bc9934ba-f4d8-4646-ac74-12fce292e222" />

2. SNM (HOLD)
<img width="325" height="505" alt="MATLAB_RESIS_HOLD" src="https://github.com/user-attachments/assets/03422a4e-8d90-4d03-bbcb-e2fb54875d87" />

Resis

| Parameter | Value |
|------|-------|
| Speed | 0.4 ns |
| SNM (hold) | 218.6 mV |

PMOS

| Parameter | Value |
|------|-------|
| Speed | 1.3 ns |
| SNM (hold) | 265 mV |


# PMOS Pull up Values
1. Speed:
<img width="325" height="505" alt="SRAM_PMOS_Speed" src="https://github.com/user-attachments/assets/7f6b8f60-99ca-48e3-9353-800dc2086c04" />

2. SNM (HOLD)

<img width="325" height="505" alt="MATLAB_PMOS_HOLD" src="https://github.com/user-attachments/assets/52917cb6-532e-47b2-88e3-559d95cd3e4d" />


# Design problems

The first problem that occurred during this process was simulation. When simulation began we did not have proper access to the pdk instead relying on 180nm technology rather than the sky130nm technology we were going to begin testing on. So this led to us using Ltspice but as we would realize LTspice was not as flexible/capable of being controlled as easily as was NGspice and xschem that we would gain access to later.
Which would then result in us having our SNM test for writing to fail as it was not able to properly simulate it like it did for hold, we had compared our setup to a colleague who had the time to use xschem and NGspice to test his circuit and despite our setups being the same LTspice would not provide the results that we had expected even after testing it with a 6T circuit for comparison.

The second problem that is the reason we had two designs was our original layout being the one that relied on a resistor was too big. The size of the resistor took up the majority of the space and if we were going to fill a whole tile with only our cells we would likely not fit more than potentially 10. Which led to us redesigning once again.

The third problem testing for reading, if we were going to test reading properly we would need a precharger circuit and due to the fact we were working on Ltspice and our colleague on xschem it was harder to coordinate and setup our circuits to test them with each other. The reason we would need his precharger circuit is because if we would to just place 0.9V source on the access transistors, the bitlines we would be able to recieve a ripple in the voltage that they should have if it was being read by a sense amp. Instead, the BL were forced to remain at 0.9V while the internal nodes themselves would be the one to change. We decided to use this as more an opportunity to see if something like this did happen would our stored values changed which in both cases they did not.

# Test plan for Post Fabrication

If frabricated alone the testing procedure would be aimed towards reading and writing.

1. Reading
We would connect our cell to VDD and GND for their respective ports providing 1.8V to VDD. Then our Bitlines would be connected to a precharger or a tool that can act similarily to one being providing 0.9V but can experience and applied voltage forcing it to change. After a second or so has passed we would turn on the precharger/source online and measure the bitlines using an oscilloscope in order to measure the voltage drops on the line. Through that we can then determine what values our cell defaulted with allowing us to then move onto writing
2. Writing
For writing we would enable the WL and raise BL and BL_n high depending on what we wanted to overwrite if we are storing a 1 we would raise BL_N to high and BL to low and vice versa if we were storing a 0. Once we have waited we would repeat the test but for reading to check to see if the stored value had changed.
3. Speed
Speed can only be measured if we can access our inverter outputs, if we can we can committ the write test once again but instead use an oscilloscope using the trigger settingto measure the time it takes for the lines to change after WL is turned on.

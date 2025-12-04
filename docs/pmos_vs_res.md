## Key Differences Between PMOS and Resistor Design

1. Basic Characteristics
- While the idea of the PMOS is to replace the 50K resistor, there are key differences that explain the tradeoffs of each design. The PMOS operates in both saturation and triode regions. The triode region models the resistor almost 1:1, however the saturation part is where it tapers away from it. This is actually a positive difference in many ways, though there are drawbacks to consider as well (later deemed unimportant). Look below for the current vs node voltage characteristics of the pmos vs the resistor.
<img width="500" height="1168" alt="RES_vs_PMOS_characteristics" src="https://github.com/user-attachments/assets/9eaaf97c-dca9-44ce-a2ac-ae3642f9b027" />


2. Passive power
- This is the one of the biggest wins for the PMOS design, aside from the obvious size during the layout process. The PMOS cell uses significantly less power, which can be seen by analyzing the current leaking through over all possible node voltages. Comparing this to the resistor, the advantage is obvious. Look to the plot below for a clear view of this. The image is the steady state current leakage on the low node.
<img width="500" height="1164" alt="SRAM_passivePowerComp_lowNode" src="https://github.com/user-attachments/assets/a6343e08-f0f8-4b17-aa62-490eece909c7" />
- This can be explained by simply analyzing the characteristic graph once again. As the transistor enters saturation and the current tapers off for lower node voltages, where the resistor remains linear. 

3. Write speed
- Here is where the PMOS faces a drawback. Of course, since the PMOS pull-up strength weakens relative to the resistor for lower node voltages (this is what saves power), it won't be as quick to flip. This results in a slower write speed compared to the resistor cell. Look to the image below for the theoretical difference.
<img width="500" height="1166" alt="SRAM_PMOS_vs_RES_Speed" src="https://github.com/user-attachments/assets/ae1fdb82-355b-4018-9496-f5c99e5bc884" />
- Though this appears very significant, it turns out that 

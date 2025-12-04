## LTspice Files 
This file contains brief explanations for the LTSpice files in this folder. 

1. 4T+2T vs 4T2R SRAM Butterfly Curve: This file is the Static Noise Margin (SNM) test for the bit cell while holding data. It contains both circuit varaints. Plotting values of V(Q) gives the Butterfly Curve used to determine the static noise margin. This is done by taking V(Q) plotted against its inverse, and looking for the side length of the largest square that fits inside the smaller loop of the plot.

2. 4T+2T vs 4T2R SRAM Circuit Passive Power: This file is to look at the passive power consumption of the resistor circuit vs the pmos circuit. This is done by looking at the current through the pull-up device for different node voltages. Obviously higher overall current results in more passive power draw. 

3. 4T+2T vs 4T2R SRAM Write Speed: This of course analyses write speed. It has both circuit variants so that they may be plotted against one another. It simply looks at the time it takes for the cell to stabalize when forcing a write. One bit takes longer to stabalize than the other, and so this is the bit used to assess write time.

4. Sky130 PMOS Resistance Test: This file is purely meant to analyze the behaviour of the PMOS compared to the 50K resistor. By sweeping the node voltage and plotting current through each device, you can see that for lower node voltages, the PMOS current tapers off resulting in a weaker pull-up at this point. This is why it uses less passive power, and also one of the reasons it's slightly slower in theory to flip. As node voltage increases, the PMOS begins to enter triode region with a curve very similar to that of the 50k resistor, with them both eventually reaching 0 current as the node voltage reaches VDD.

5. 4T+2T vs 4T2R SRAM Write Margin Test: Simply tests the write margin of the bit cell. When one side fights the other, at what point is the write successful. Done by plotting voltage of the node against the swept bitline trying to flip it. 

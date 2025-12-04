## LTspice Files 
This file contains brief explanations for the LTSpice files in this folder. 

1. 4T+2T vs 4T2R SRAM Butterfly Curve: This file is the Static Noise Margin (SNM) test for the bit cell while holding data. It contains both circuit varaints. Plotting values of V(Q) gives the Butterfly Curve used to determine the static noise margin. This is done by taking V(Q) plotted against its inverse, and looking for the side length of the largest square that fits inside the smaller loop of the plot.

2. 4T+2T vs 4T2R SRAM Circuit Passive Power: This file is to look at the passive power consumption of the resistor circuit vs the pmos circuit. This is done by looking at the current through the pull-up device for different node voltages. Obviously higher overall current results in more passive power draw. 

3. 4T+2T vs 4T2R SRAM Write Speed: This of course analyses write speed. It has both circuit variants so that they may be plotted against one another. It simply looks at the time it takes for the cell to stabalize when forcing a write. One bit takes longer to stabalize than the other, and so this is the bit used to assess write time. 

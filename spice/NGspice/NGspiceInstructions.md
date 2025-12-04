# Structure

In this directory you will find two other directories, one leading you to testbenches designed for a cell having a resistor in its design another utilizing a PMOS for its design.
Inside both are files follow the structure 'BitCell{Resis/NoResis}.spice' and another following the same scheme but with the added term LVS (Layout vs Schematic).
The LVS spice is to be utilized more as an instruction guide as to what each port in your layout is connected to without. While the non LVS ersion is the one you shall be testing your layout with.

# TestBenches

Then there are testbench spice files we currently have a Read test and  Write/Speed test. The Read test does not properly work unless you replace the bitline connections to the access transistors with a precharger circuit.
While for the write/speed test, it will first allow the cell to settle and store a value before then writing to the cell, we can then check if writing functionality works and how much time it takes for the cells to flip the bit it has stored.

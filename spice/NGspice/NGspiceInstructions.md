# Structure

In this directory you will find two other directories: one leading to testbenches designed for a cell having a resistor in its design, and another utilizing a PMOS for its design.
Inside both are files following the structure BitCell{Resis/NoResis}.spice, and another following the same scheme but with the added term LVS (Layout vs. Schematic).
The LVS SPICE file is to be used more as an instruction guide for what each port in your layout is connected to. The non-LVS version is the one you should be testing your layout with.

# TestBenches

Then there are the testbench SPICE files. We currently have a read test and a write/speed test. The read test does not properly work unless you replace the bitline connections to the access transistors with a precharger circuit. As for the write/speed test, it will first allow the cell to settle and store a value before writing to the cell. We can then check if the writing functionality works and how much time it takes for the cells to flip the bit they have stored.

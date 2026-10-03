# Combinational Circuits — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Sum and carry swapped | Half-adder carry written as XOR | Sum is XOR, carry is AND |
| Full-adder carry is XOR | Three-input XOR used for \(C_{out}\) | Carry is majority |
| Select count | 8-to-1 mux given 8 selects | \(n\) selects for \(2^n\) inputs |
| Mux tree | 8-to-1 built from 4 or 8 of the 2-to-1 | The tree uses \(2^n-1\) |
| Decoder index | \(ABC=101\) called \(Y_6\) or \(Y_3\) | The integer value, with the stated MSB |
| Active-low OR | Active-low minterm pins OR-ed to make a SOP | NAND those pins |
| Priority | Lowest 1, or the OR of the indexes | Highest asserted index |
| Gray | Binary value incremented | XOR adjacent bits; MSB copied |
| Lookahead | \(C_2 = G_1 + P_1 C_0\) | Keep \(P_1 G_0\) |
| Ripple delay | Sum XOR of every bit added into the carry path | Follow the carry pins |
| Carry-out as overflow | \(C_{out}=1\) reported as signed overflow | Overflow compares carry into and out of the sign |

### PYQ-shaped traps

- Cascaded 2-to-1 muxes: write the select equation before picking an SOP option. A minimal SOP of that equation is a second step, not a different function.
- Half adder inside a full adder: the OR that merges the two half-adder carries is on the carry path. Its delay counts.
- Decoder-based RAM questions in this mapping are memory geometry plus a decoder. The decoder count is the combinational part; the word width is not a logic minimization.
- A truth table with \(V=0\) and index bits printed as x means the index is unspecified, not that those bits are the don’t-cares of a K-map for a different function.

### Calculation slips

- Cofactor order reversed, so \(C\) and \(C'\) are swapped on the data pins.
- Enable decoder forgotten, so a 6-to-64 design is counted as 8 instead of 9.
- Gray bit \(G_i\) XOR-ed with \(B_{i-1}\) instead of \(B_{i+1}\).

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |

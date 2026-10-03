# Fixed Point — Mistakes

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Endpoint \(-127\) on 8 bits | Ones’-complement extreme used for two’s complement | 8-bit two’s complement goes down to \(-128\) |
| Two zeros in two’s complement | \(111\ldots 1\) called a second zero | That pattern is \(-1\). Two zeros belong to ones’ complement and sign-magnitude |
| Carry-out as signed overflow | Every \(C_{out}=1\) rejected | Signed overflow is carry-into-sign \(\neq\) carry-out-of-sign |
| Negation of \(100\ldots 0\) | Reported as \(+2^{n-1}\) | Inside \(n\) bits the pattern returns to itself and stays \(-2^{n-1}\) |
| Sign extension | Zeros inserted on the left | Copy the sign bit |
| Logical versus arithmetic shift | Right shift of a negative value filled with 0 | Arithmetic shift fills with the sign |
| Booth scan | 1-bits of the multiplicand counted | Scan multiplier transitions, with \(Q_{-1}=0\) |
| End-around on two’s complement | Carry out added back into the LSB | End-around is ones’ complement |
| Same bits, silent code | A pattern converted without naming the code | Sign-magnitude, ones’, and two’s complement disagree |
| Fixed point versus float | An exponent invented for a printed binary point | Divide the integer reading by \(2^f\) |

### PYQ-shaped traps

- “Which of the following are correct representations of \(-6\)?” mixes widths and codes. A 4-bit pattern and an 8-bit pattern of the same value differ by sign extension, not by a new code.
- Overflow questions offer both the carry-out and the sign test. They are different predicates and can disagree on the same addition.
- \(8P\) from a hex two’s-complement word is a 3-place arithmetic left shift. Convert only after the shift if the decimal value is what is asked.
- The distinct-value comparison of 16-bit two’s complement and 16-bit sign-magnitude is \(2^{16} - (2^{16}-1) = 1\).
- Booth’s operation count ignores runs of identical bits. A block of 1s contributes one add and one subtract, not one operation per bit.

### Calculation slips

- Forgetting to add 1 after the flip, which yields the ones’ complement instead.
- Using weight \(+2^{n-1}\) on the MSB of a negative two’s-complement pattern.
- Dropping the carry into the sign when judging overflow from the bits alone.

### My Mistakes

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |

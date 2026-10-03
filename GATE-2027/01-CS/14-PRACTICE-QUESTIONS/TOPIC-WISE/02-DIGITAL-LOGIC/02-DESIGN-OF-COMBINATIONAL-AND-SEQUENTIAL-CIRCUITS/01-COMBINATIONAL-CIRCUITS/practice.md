# Combinational Circuits — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A half adder has inputs \(A\) and \(B\). Its sum and carry outputs are

A. \(\text{Sum} = A \oplus B\), \(\text{Carry} = AB\)

B. \(\text{Sum} = AB\), \(\text{Carry} = A \oplus B\)

C. \(\text{Sum} = A + B\), \(\text{Carry} = AB\)

D. \(\text{Sum} = A \odot B\), \(\text{Carry} = A + B\)

---

## Q2 — MSQ

Select all that apply. A full adder has inputs \(A\), \(B\) and \(C_{in}\), sum \(S\) and carry \(C_{out}\).

A. \(S = A \oplus B \oplus C_{in}\)

B. \(C_{out} = AB + BC_{in} + AC_{in}\)

C. \(S = 1\) for exactly 4 of the 8 input combinations

D. \(C_{out} = A \oplus B \oplus C_{in}\)

---

## Q3 — NAT

The number of select lines on a 16-to-1 multiplexer is ______.

---

## Q4 — MCQ

An enabled active-high 3-to-8 decoder has inputs \(ABC = 101\), with \(A\) the most significant bit. Which output is 1?

A. \(Y_0\)

B. \(Y_3\)

C. \(Y_5\)

D. \(Y_6\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The minimum number of 2-to-1 multiplexers needed to build an 8-to-1 multiplexer is

A. 4

B. 6

C. 7

D. 8

---

## Q6 — NAT

A 4-bit adder is built with a half adder in the least significant position and full adders above it. The incoming carry into the half adder is fixed at 0. The number of full adders used is ______.

---

## Q7 — MSQ

Select all that apply. A 4-bit binary-to-Gray converter uses \(G_3 = B_3\), \(G_2 = B_3 \oplus B_2\), \(G_1 = B_2 \oplus B_1\) and \(G_0 = B_1 \oplus B_0\).

A. The Gray code of binary \(1101\) is \(1011\).

B. Encodings of successive integers in this Gray code differ in exactly one bit.

C. The converter uses three 2-input XOR gates.

D. The Gray code of binary \(1101\) is \(1111\).

---

## Q8 — MCQ

A 4-to-1 multiplexer has select inputs \(S_1 S_0\) and data inputs \(I_0 = 0\), \(I_1 = 1\), \(I_2 = 1\), \(I_3 = 0\). As a function of \(S_1\) and \(S_0\), the output is

A. \(S_1 \oplus S_0\)

B. \(S_1 \odot S_0\)

C. \(S_1 S_0\)

D. \(S_1 + S_0\)

---

## Q9 — NAT

\(A\) and \(B\) are 2-bit unsigned integers. Over all 16 pairs \((A, B)\), the number of pairs with \(A > B\) is ______.

---

## Q10 — MCQ

In a ripple-carry adder, each full adder produces its carry output with a delay of 2 gate delays after its inputs are stable. The delay from the least significant carry-in to the most significant carry-out of a 4-bit ripple-carry adder is

A. 2 gate delays

B. 4 gate delays

C. 6 gate delays

D. 8 gate delays

---

## Level 3 — Multi-Step

## Q11 — MCQ

A 4-to-1 multiplexer realizes \(F(A, B, C) = \sum m(0, 2, 3, 5, 7)\). The select inputs are \(A\) and \(B\), with \(A\) more significant. The data input selected by \(AB = 10\) must be tied to

A. \(0\)

B. \(1\)

C. \(C\)

D. \(C'\)

---

## Q12 — NAT

Using only 2-input NAND gates, and with no complemented inputs supplied, the minimum number of gates in an XOR network for \(A \oplus B\) is ______.

---

## Q13 — MSQ

Select all that apply. A 3-to-8 decoder has active-low data outputs and is enabled. The pin for minterm \(m_i\) therefore carries \(m_i'\). The target is \(F = \sum m(1, 2, 4, 7)\).

A. \(F\) is the NAND of the four pins for \(m_1, m_2, m_4, m_7\).

B. \(F\) is the OR of those four active-low pins.

C. \(F = 1\) for exactly four input combinations.

D. \(F\) is the AND of those four active-low pins.

---

## Q14 — MCQ

In a carry-lookahead adder, \(G_i = A_i B_i\) and \(P_i = A_i \oplus B_i\). The carry into bit 2 is

A. \(C_2 = G_1 + P_1 G_0 + P_1 P_0 C_0\)

B. \(C_2 = G_1 + P_1 C_0\)

C. \(C_2 = G_0 + P_0 G_1\)

D. \(C_2 = P_1 + G_1 C_0\)

---

## Level 4 — Tricky / Trap-Based

## Q15 — MSQ

Select all that apply. A 2-to-1 multiplexer is defined by \(Y = S' I_0 + S I_1\).

A. If \(I_0 = 1\) and \(I_1 = 0\), then \(Y = S'\).

B. If those same data values are exchanged and \(S\) is left unchanged, the output becomes \(S\).

C. When \(S = 1\), the output depends on \(I_0\).

D. If \(I_0 = I_1 = 1\), then \(Y = 1\) for both values of \(S\).

---

## Q16 — NAT

\(F(A, B, C) = \sum m(1, 5) + d(3, 7)\) may use its don't cares. In a two-level sum-of-products implementation, the minimum number of AND and OR gates required is ______. Inverters are not counted. A lone literal needs no AND or OR gate.

---

## Q17 — MCQ

A 4-to-2 priority encoder treats \(I_3\) as the highest priority and \(I_0\) as the lowest. For the input vector \(I_3 I_2 I_1 I_0 = 0110\), the binary output \(Y_1 Y_0\) is

A. \(01\)

B. \(10\)

C. \(11\)

D. \(00\)

---

## Level 5 — Challenge

## Q18 — NAT

A 5-to-32 decoder is built from 3-to-8 decoders with enable, plus one 2-to-4 decoder whose outputs drive those enables. The number of 3-to-8 decoders required is ______.

---

## Q19 — NAT

A one-bit ALU has data inputs \(A, B\) and select inputs \(S_1 S_0\). The output \(Y\) is \(AB\) when \(S_1 S_0 = 00\), \(A + B\) when \(S_1 S_0 = 01\), \(A \oplus B\) when \(S_1 S_0 = 10\), and the sum bit of \(A + B\) with carry-in 0 when \(S_1 S_0 = 11\). Over all 16 combinations of \((A, B, S_1, S_0)\), the number of combinations with \(Y = 1\) is ______.

---

## Q20 — MSQ

Select all that apply. A 4-bit ripple-carry adder computes \(1011 + 0111\).

A. The four sum bits are \(0010\).

B. The carry out of the most significant bit is 1.

C. As unsigned integers the inputs are 11 and 7, and the five-bit result is 18.

D. Because the carry out is 1, the same addition overflows when the inputs are read as 4-bit two's-complement numbers.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 4 |
| 4 | MCQ | C |
| 5 | MCQ | C |
| 6 | NAT | 3 |
| 7 | MSQ | A, B, C |
| 8 | MCQ | A |
| 9 | NAT | 6 |
| 10 | MCQ | D |
| 11 | MCQ | C |
| 12 | NAT | 4 |
| 13 | MSQ | A, C |
| 14 | MCQ | A |
| 15 | MSQ | A, B, D |
| 16 | NAT | 0 |
| 17 | MCQ | B |
| 18 | NAT | 4 |
| 19 | NAT | 8 |
| 20 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: **A**

The sum bit is 1 when the inputs differ, so it is XOR. The carry is 1 only when both inputs are 1, so it is AND. Option (B) exchanges those two functions. Option (C) makes the sum an OR, which is also 1 when both inputs are 1, but the sum bit of \(1 + 1\) is 0. Option (D) is XNOR, the opposite of the sum.

### Q2

Answer: **A, B, C**

The sum is the parity of the three inputs, which is the three-input XOR. That parity is 1 for the three weights of one 1 and for the single weight of three 1s, so on exactly 4 rows. The carry is the majority function, which factors as \(AB + BC_{in} + AC_{in}\). Option (D) copies the sum equation onto the carry. The carry is 1 on a different set of four rows: the rows with at least two 1s, not the odd-parity rows.

### Q3

Answer: **4**

A \(2^k\)-to-1 multiplexer has \(k\) select lines. Here \(2^k = 16\), so \(k = 4\). Answering 16 counts data inputs rather than select inputs.

### Q4

Answer: **C**

The input word \(ABC = 101_2\) is the integer 5, so the active-high decoder asserts \(Y_5\) and holds the other outputs at 0. \(Y_6\) would be input \(110\). \(Y_3\) would be \(011\). The trap is to read the bits from the wrong end and select \(Y_5\)'s reversal.

### Q5

Answer: **C**

The first rank uses four 2-to-1 multiplexers to reduce eight data inputs to four signals. The second rank uses two multiplexers to reduce those four signals to two. One final multiplexer produces the output. The total is \(4 + 2 + 1 = 7\). Option (A) stops after the first rank. Option (D) counts one multiplexer per data input and forgets that the tree shares them.

### Q6

Answer: **3**

With the system carry-in fixed at 0, the least significant bit does not need a full adder: a half adder adds the two least significant data bits. Each of the other three bit positions must accept a carry from below, so each is a full adder. Answering 4 places a full adder in every position, which is a correct but larger implementation, not the one described.

### Q7

Answer: **A, B, C**

For \(B_3 B_2 B_1 B_0 = 1101\),

\[
G_3 = 1,\quad G_2 = 1 \oplus 1 = 0,\quad G_1 = 1 \oplus 0 = 1,\quad G_0 = 0 \oplus 1 = 1.
\]

The Gray word is \(1011\), not \(1111\). Only \(G_2, G_1, G_0\) need an XOR, so three gates are enough. Reflected binary Gray code changes exactly one bit between successive integers; that is the reason the XOR-of-neighbours formula is used. Option (D) is the binary word with the least significant 0 filled in, not the Gray image.

### Q8

Answer: **A**

The truth table on the select inputs is \(00 \to 0\), \(01 \to 1\), \(10 \to 1\), \(11 \to 0\). That is XOR. XNOR is the opposite table, \(1, 0, 0, 1\). AND is 1 only at \(11\), and OR is 0 only at \(00\).

### Q9

Answer: **6**

For \(A = 0, 1, 2, 3\) the number of strictly smaller 2-bit values of \(B\) is \(0, 1, 2, 3\). The sum is 6. There are also 6 pairs with \(A < B\) and 4 pairs with \(A = B\), and \(6 + 6 + 4 = 16\). Answering 8 uses half of 16 and forgets the four ties. Answering 12 counts \(A \ge B\).

### Q10

Answer: **D**

The carry ripples through all four stages. Each stage adds 2 gate delays, so the path from \(C_{in}\) of bit 0 to \(C_{out}\) of bit 3 takes \(4 \times 2 = 8\) gate delays. Option (A) is one stage. Option (B) counts stages but not the two delays inside each stage. A carry-lookahead adder is what would avoid this linear chain; this adder is ripple-carry.

### Q11

Answer: **C**

With select \(AB\), each data input is the function of \(C\) on that pair of minterms.

| \(AB\) | \(C = 0\) | \(C = 1\) | Data |
|---|---|---|---|
| 00 | \(m_0 = 1\) | \(m_1 = 0\) | \(C'\) |
| 01 | \(m_2 = 1\) | \(m_3 = 1\) | \(1\) |
| 10 | \(m_4 = 0\) | \(m_5 = 1\) | \(C\) |
| 11 | \(m_6 = 0\) | \(m_7 = 1\) | \(C\) |

The input selected by \(AB = 10\) is \(I_2 = C\). Tying it to 0 drops \(m_5\). Tying it to 1 adds the specified 0 at \(m_4\). Tying it to \(C'\) swaps those two rows.

### Q12

Answer: **4**

One standard NAND-only XOR is

\[
A \oplus B = \big(A \cdot (A \cdot B)'\big)' \;\mathrm{NAND}\; \big(B \cdot (A \cdot B)'\big)',
\]

which uses four 2-input NAND gates: one to form \((AB)'\), two to NAND that result with \(A\) and with \(B\), and one to NAND those two outputs. Fewer than four 2-input NANDs cannot produce both the positive and the mixed terms when complements are not already available. Counting an inverter as an extra fifth gate double-counts, because a NAND with tied inputs already supplies the inversion inside this network, and this particular network does not need a separate inverter.

### Q13

Answer: **A, C**

The four minterms are four distinct rows, so \(F = 1\) on exactly those four combinations. Each active-low pin is \(m_i'\). The NAND of the four pins is

\[
(m_1' \cdot m_2' \cdot m_4' \cdot m_7')' = m_1 + m_2 + m_4 + m_7 = F.
\]

The OR of the active-low pins is \(m_1' + m_2' + m_4' + m_7'\), which is 0 only when all four minterms are 1 simultaneously. That never happens, so the OR output is stuck at 1. The AND of the pins is \(F'\). The polarity trap is to attach an OR gate to active-low decoder outputs and expect a sum of minterms. With active-low outputs, the matching summing gate is NAND.

### Q14

Answer: **A**

The recurrence is \(C_{i+1} = G_i + P_i C_i\). So \(C_1 = G_0 + P_0 C_0\) and

\[
C_2 = G_1 + P_1 C_1 = G_1 + P_1(G_0 + P_0 C_0) = G_1 + P_1 G_0 + P_1 P_0 C_0.
\]

Option (B) replaces \(C_1\) by \(C_0\) and drops the generate from bit 0. Option (C) swaps the bit indices, so a generate at bit 1 would have to travel backward. Option (D) ORs a propagate with a generate, which is not the carry equation; \(P_1 = 1\) and \(G_1 = C_0 = 0\) would incorrectly force a carry.

### Q15

Answer: **A, B, D**

Substitute \(I_0 = 1\) and \(I_1 = 0\): \(Y = S' \cdot 1 + S \cdot 0 = S'\). After the data inputs are exchanged, the new \(I_0\) is 0 and the new \(I_1\) is 1, so \(Y = S\). If both data inputs are 1, then \(Y = S' + S = 1\).

When \(S = 1\), the formula retains \(I_1\) and kills \(I_0\). Option (C) has the select polarity backward. The output follows \(I_0\) only while \(S = 0\).

### Q16

Answer: **0**

The four cells with \(C = 1\) are \(m_1, m_3, m_5, m_7\). The first and the third are required 1s; the second and the fourth are don't cares. None is a specified 0. The specification therefore allows \(F = C\). A wire from input \(C\) to the output uses no AND gate and no OR gate.

Forcing the don't cares to 0 produces \(B'C\), which needs an inverter and a 2-input AND. That circuit is legal, because don't cares may be 0, but it is not gate-minimum once the don't cares may be 1. The don't-care misuse is paying for \(B'\) after the map has already offered a single literal.

### Q17

Answer: **B**

\(I_2\) and \(I_1\) are both asserted. Priority selects the highest index, which is 2. The encoding of 2 is \(Y_1 Y_0 = 10\). Option (A) is the lower asserted input. Option (C) is what a non-priority encoder may emit as the OR of the two asserted one-hot lines, and it is not a valid priority result. Option (D) would mean that no input is asserted.

### Q18

Answer: **4**

A 5-bit input splits into a 2-bit high part and a 3-bit low part. The 2-to-4 decoder decodes the high part and enables exactly one of four 3-to-8 decoders. The enabled decoder decodes the low part into 8 of the 32 outputs. The other three 3-to-8 decoders stay disabled. Thus four 3-to-8 decoders cover \(4 \times 8 = 32\) outputs. Answering 32 builds the function with no decoder sharing. Answering 2 undercounts the high-part cases \(00, 01, 10, 11\).

### Q19

Answer: **8**

There are four select combinations and, for each, four assignments of \((A, B)\).

- AND is 1 only at \(AB = 11\): 1 combination.
- OR is 1 at \(01, 10, 11\): 3 combinations.
- XOR is 1 at \(01, 10\): 2 combinations.
- The sum with carry-in 0 is \(A \oplus B\), also 1 at \(01, 10\): 2 combinations.

The total is \(1 + 3 + 2 + 2 = 8\). The last operation is not the carry. If the ALU had emitted \(AB\) again for select \(11\), the count would be \(1 + 3 + 2 + 1 = 7\). The sum bit with carry-in 0 really is XOR, so select \(10\) and select \(11\) contribute the same two rows.

### Q20

Answer: **A, B, C**

\(1011_2 + 0111_2 = 10010_2\). The lower four bits are \(0010\) and the carry out is the leading 1. As unsigned values, \(11 + 7 = 18\), and \(10010_2 = 18\).

As 4-bit two's-complement values the same bits are \(-5\) and \(+7\). Their sum is \(+2\), which is exactly the sum nibble \(0010\). The signs differ, so signed overflow is impossible. The carry out is 1 because the unsigned interpretation exceeded 15; that flag is not the signed-overflow flag. Signed overflow would be diagnosed from the carry into the sign bit differing from the carry out of the sign bit. Here those two carries are equal, and the true sum fits in four bits.

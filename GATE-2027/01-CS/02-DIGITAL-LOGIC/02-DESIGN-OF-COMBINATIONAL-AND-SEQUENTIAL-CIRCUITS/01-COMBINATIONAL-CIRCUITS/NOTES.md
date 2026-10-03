# Combinational Circuits

A combinational circuit’s outputs depend only on the inputs present now. There is no clock and no stored bit. The Boolean algebra and the K-map produce the equations; this topic is how those equations are packaged as adders, multiplexers, decoders, and encoders, and how small blocks are wired into larger ones.

The mapped stems that are actually this topic (see `PYQ.md`) are mux trees, decoder trees, a half-adder delay chain, a 4-to-1 mux’s SOP, and a 4-input encoder truth table. Several rows in the same file are cache or database questions. Chip-select and “how many decoders build this RAM” use the decoder count, but the surrounding arithmetic is memory organisation.

---

## 1. Adders

### Half adder

Inputs \(A, B\). No carry in.

| \(A\) | \(B\) | Sum | Carry |
|------:|------:|----:|------:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

\[
S = A \oplus B, \qquad C = AB
\]

**Why.** Sum is 1 when the bits differ. Carry is 1 only when both are 1. That is ordinary addition of two bits: \(0+0=0\), \(1+0=1\), \(1+1=0\) write 0 and carry 1.

### Full adder

Inputs \(A, B, C_{in}\).

\[
S = A \oplus B \oplus C_{in}
\]

\[
C_{out} = AB + BC_{in} + AC_{in}
\]

**Why the sum is three-way XOR.** Adding three bits gives a binary total 0, 1, 2, or 3. The units bit of that total is 1 precisely on an odd number of 1s, which is XOR. The carry bit is 1 when the total is 2 or 3, which is “at least two inputs are 1,” the majority function. Expanding majority gives the three products.

**Equivalent carry.** \(C_{out} = AB + C_{in}(A \oplus B)\). If \(A=B=1\), the carry is already 1. If \(A\) and \(B\) differ, the incoming carry is passed through. If \(A=B=0\), the carry is 0. Same function, and it is how two half adders plus an OR make a full adder:

- First half adder: \(A \oplus B\) and \(AB\).
- Second half adder: that sum XOR \(C_{in}\), and a second carry \((A \oplus B)C_{in}\).
- OR the two carries.

Exactly four of the eight input rows have \(S=1\) (the odd rows), and four have \(C_{out}=1\) (the rows with at least two 1s). Those counts are not equal to each other on every individual row: row 111 has both outputs 1.

### Ripple-carry adder

An \(n\)-bit adder is \(n\) full adders. The carry out of bit \(i\) is the carry in of bit \(i+1\). Bit 0 may be a half adder when \(C_0\) is tied to 0; then an \(n\)-bit adder uses \(n-1\) full adders and one half adder.

**Delay.** If each full adder’s carry is ready \(d\) gate delays after its inputs, the last carry waits \(n d\) after \(C_0\) and the operand bits. The carries form a chain. For \(d = 2\) and \(n = 4\), the delay from the first carry-in to the last carry-out is 8 gate delays.

The 2015 stem is this chain with given XOR and AND delays, a half adder at the bottom, and a full adder built from two half adders and an OR. Add the delays along the carry path only. The sum output of a later bit is not ready until its own carry arrives, then its local XOR finishes.

### Carry-lookahead

Define, at bit \(i\),

\[
G_i = A_i B_i, \qquad P_i = A_i \oplus B_i.
\]

\(G_i\) generates a carry by itself. \(P_i\) propagates an incoming carry. Then

\[
\begin{align*}
C_1 &= G_0 + P_0 C_0, \\
C_2 &= G_1 + P_1 G_0 + P_1 P_0 C_0, \\
C_3 &= G_2 + P_2 G_1 + P_2 P_1 G_0 + P_2 P_1 P_0 C_0.
\end{align*}
\]

**Why.** \(C_{i+1} = G_i + P_i C_i\). Unrolling the recurrence removes the long ripple from the logic depth. Each \(C_i\) is a two-level function of the \(G\)s, \(P\)s, and \(C_0\), once \(G\) and \(P\) themselves are ready. The pattern is: a carry is generated at some bit and then propagated through every bit above it.

**Trap.** \(C_2 = G_1 + P_1 C_1\), but if the option expands \(C_1\), the expansion is \(G_1 + P_1 G_0 + P_1 P_0 C_0\). An option that stops at \(G_1 + P_1 C_0\) has dropped \(G_0\).

Signed overflow is not “\(C_{out} = 1\).” That distinction is in the fixed-point notes. The adder here only produces the sum bits and the carry.

---

## 2. Multiplexer

A \(2^n\)-to-1 multiplexer has \(2^n\) data inputs, \(n\) select lines, and one output. The select number chooses which data input is copied.

\[
Y = \sum_{i=0}^{2^n - 1} m_i(S) \, I_i
\]

For a 2-to-1 mux, \(Y = S' I_0 + S I_1\).

**Why this is Shannon expansion.** Any function of the select bits plus extra variables can be written \(F = S' F(0) + S F(1)\). Tie \(I_0\) to the cofactor \(F(0)\) and \(I_1\) to \(F(1)\). Those cofactors are \(0\), \(1\), a leftover variable, or its complement.

**Worked tie.** \(F(A,B,C) = \sum m(1,2,4,7)\), selects \(A,B\) with \(A\) more significant.

| \(AB\) | Rows | Required \(F\) | Data input |
|--------|------|----------------|------------|
| 00 | \(m_0=0\), \(m_1=1\) | \(0\) when \(C=0\), \(1\) when \(C=1\) | \(C\) |
| 01 | \(m_2=1\), \(m_3=0\) | \(1\) when \(C=0\), \(0\) when \(C=1\) | \(C'\) |
| 10 | \(m_4=1\), \(m_5=0\) | same pattern | \(C'\) |
| 11 | \(m_6=0\), \(m_7=1\) | \(1\) when \(C=1\) | \(C\) |

**Constants on the data pins.** If \(I_0=0\), \(I_1=1\), \(I_2=1\), \(I_3=0\) on selects \(S_1 S_0\), then \(Y = S_1' S_0 + S_1 S_0' = S_1 \oplus S_0\).

**Building a wider mux from 2-to-1 muxes.** A \(2^n\)-to-1 mux needs \(2^n - 1\) copies of a 2-to-1 mux: \(2^{n-1}\) at the first rank, \(2^{n-2}\) at the next, down to 1. So an 8-to-1 uses \(4+2+1 = 7\), and a 16-to-1 uses 15. The sum of a geometric series \(1+2+\cdots+2^{n-1} = 2^n - 1\).

**Enable.** An active-low enable AND-combined as \(E'\) in front of \(Y\) forces the output to 0 when the mux is disabled, if the output is active-high. Read the stem’s polarity before using that.

**Trap.** When \(S=1\), \(Y\) does not depend on \(I_0\). Swapping \(I_0\) and \(I_1\) replaces \(Y\) by the function of \(S'\). If \(I_0 = I_1\), the select does not matter.

One mux plus inverters can implement any function of \(n\) variables if the mux is large enough to take \(n-1\) variables as selects and the remaining variable, its complement, 0, and 1 are available as data. The minimum size in that classic question is a \(2^{n-1}\)-to-1 mux. The mapped 2007 stem is filed under sequential circuits; the object is a multiplexer.

---

## 3. Decoder

An \(n\)-to-\(2^n\) decoder has \(n\) inputs and \(2^n\) outputs. Exactly one output is active when the decoder is enabled. Output \(Y_i\) is minterm \(m_i\) for an active-high decoder.

**Example.** A 3-to-8 decoder, \(ABC = 101\) with \(A\) the MSB, asserts \(Y_5\). The index is the integer value of the input.

**Active-low outputs.** The pin for minterm \(m_i\) carries \(m_i'\). To OR several minterms, NAND those pins:

\[
(m_a' \cdot m_b' \cdot m_c')' = m_a + m_b + m_c.
\]

ANDing the same pins produces \(m_a' m_b' m_c'\), which is not the sum. ORing them produces a product of complements, also not the sum.

**Building a wider decoder.** To make an \(n\)-to-\(2^n\) decoder from \(k\)-to-\(2^k\) decoders with enable:

- Use one decoder on the high \(n-k\) bits if \(n-k \le k\), or a tree of them.
- Its outputs drive the enables of \(2^{n-k}\) copies of the \(k\)-to-\(2^k\) decoder.
- Those copies all receive the low \(k\) bits.

**Example.** A 6-to-64 decoder from 3-to-8 decoders with enable, and no other gates. The high 3 bits need a 3-to-8 decoder. Its 8 outputs enable 8 further 3-to-8 decoders on the low 3 bits. Total \(1+8 = 9\). The mapped 2007 question is this count.

A 5-to-32 decoder from 3-to-8 decoders plus one 2-to-4 decoder: the 2-to-4 takes two bits and enables four 3-to-8 decoders. Four of the 3-to-8 blocks.

**AND-gate view.** Each active-high minterm output is an \(n\)-input AND of the appropriate literals, plus the enable. Disabling forces every output inactive.

---

## 4. Encoder and priority encoder

A \(2^n\)-to-\(n\) encoder is the reverse numbering: one asserted input line produces the binary index of that line. It assumes at most one input is 1. Two inputs asserted together is not a code word.

A **priority encoder** resolves that. The highest-index asserted input wins, and the others are ignored. A valid bit is 0 when every input is 0.

**Example.** Inputs \(I_3 I_2 I_1 I_0 = 0110\), \(I_3\) highest priority. \(I_2\) and \(I_1\) are both 1, so \(I_2\) wins. Index 2 is \(Y_1 Y_0 = 10\).

The 2013 stem is a four-input truth table with \(V = 1\) only on a legal input. Read \(V\) before reading \(X_0, X_1\): when \(V=0\) the index bits are don’t-cares in the table (printed as x), not a third code.

---

## 5. Code converters worth knowing

**Binary to Gray**, bit \(n-1\) is the MSB:

\[
G_{n-1} = B_{n-1}, \qquad G_i = B_{i+1} \oplus B_i \quad (i < n-1).
\]

**Why one bit changes between successive integers.** Consecutive integers differ by a block of trailing 1s turning into 0s and a 0 turning into 1. The XOR of adjacent bits cancels that block and leaves a single Gray-bit change. The mapped practice pattern, and the usual exam check, is to compute one example and to remember that successive integers differ in exactly one Gray bit.

**Example.** Binary \(1011\). \(G_3 = 1\), \(G_2 = 1 \oplus 0 = 1\), \(G_1 = 0 \oplus 1 = 1\), \(G_0 = 1 \oplus 1 = 0\). Gray \(1110\).

**Gray to binary.** \(B_{n-1} = G_{n-1}\), and \(B_i = B_{i+1} \oplus G_i\). The prefix XOR is the inverse because \(B_{i+1} \oplus G_i = B_{i+1} \oplus (B_{i+1} \oplus B_i) = B_i\).

---

## 6. A one-bit ALU slice

Select lines choose among functions you already have:

| Selects | Typical operation | Equation |
|---------|-------------------|----------|
| 00 | AND | \(AB\) |
| 01 | OR | \(A+B\) |
| 10 | XOR | \(A \oplus B\) |
| 11 | sum bit, \(C_{in}=0\) | \(A \oplus B\) |

XOR and the carry-free sum bit are the same function. A question that counts input combinations where the output is 1 must not double-count those two select codes as different functions, but it must still count both select codes: each pair \((A,B)\) is a different input row for each select value.

**Comparator.** \(A>B\), \(A=B\), \(A<B\) for one bit:

\[
A>B = AB', \quad A=B = A \odot B, \quad A<B = A'B.
\]

For \(n\) bits, compare from the MSB: the first bit that differs decides. A two-bit unsigned count of pairs with \(A>B\) is a truth table of 16 rows, not a formula to memorise. Count them.

---

## 7. Delay, levels, and active levels

- A two-level SOP is one AND rank and one OR rank, after literals exist. Inverters are extra if complements are not supplied.
- NAND-NAND implements SOP. NOR-NOR implements POS. That is De Morgan, from the algebra notes.
- Ripple delay adds. Lookahead delay does not add one full adder per bit; it adds the depth of the carry equation.
- Active-low pins invert the Boolean level at that pin only. The function you want may need a NAND where an active-high design used an OR.

---

## 8. Solving procedure

1. Name the block from the stem: adder, mux, decoder, encoder. Do not simplify a mux as a random gate network until the select equation is written.
2. For a mux, write \(Y = \sum m_i(S) I_i\) with the stated MSB.
3. For “implement \(F\) with a mux,” cofactors of the select variables are the data ties \(0, 1, x, x'\).
4. For a decoder tree, split the inputs into “these bits form the address inside a block” and “these bits choose the block through enable.” Count enables.
5. For a priority encoder, scan from the high index down. Stop at the first 1.
6. For adder delay, mark the carry path. Sum XORs that are not on that path do not add to the carry-out delay.
7. For Gray, XOR neighbours; do not add the bits as integers.

---

## 9. Traps

| Trap | Correction |
|------|------------|
| Sum and carry of a half adder swapped | Sum is XOR, carry is AND |
| Full-adder carry written as XOR | Carry is majority |
| \(C_{out}=1\) called signed overflow | Different predicate; see fixed-point notes |
| Select width | \(2^n\) data inputs need \(n\) selects, not \(2^n\) |
| Mux count | \(2^n - 1\) copies of a 2-to-1, not \(n\) and not \(2^n\) |
| Decoder output index | The integer value of the inputs, MSB as stated |
| Active-low outputs OR-ed | That does not build the SOP. NAND them |
| Priority ignored | The highest asserted input wins |
| Gray as binary plus one | Gray is XOR of adjacent bits |

---

## 10. Connections

- **Algebra and K-maps.** The data ties of a mux are cofactors. A decoder plus an OR is the canonical SOP.
- **Sequential circuits.** A mux in the feedback of a flip-flop input is still combinational logic between clocks. A counter’s next state is a combinational function of the present state.
- **Fixed-point arithmetic.** The adder and the ALU slice are the circuits behind two’s-complement addition. Overflow detection uses the carries this page defines.
- **Memory interfacing.** A decoder on address bits is chip select. The count of decoders is this topic; the RAM geometry is computer organisation.

# Combinational Circuits — Practice

Original questions. They use mux trees, decoder enables, lookahead carries, Gray conversion, and priority, which are the patterns in the mapped stems and in the existing practice file.

## Level 1 — Conceptual

### Q1 — MCQ

A full adder’s carry output is 1 if and only if

A. an odd number of \(A, B, C_{in}\) are 1

B. at least two of \(A, B, C_{in}\) are 1

C. \(A \oplus B \oplus C_{in} = 1\)

D. exactly one of \(A, B, C_{in}\) is 1

**Answer.** B

**Concept.** Carry is majority; sum is parity.

**Difficulty.** Level 1

**Solution.** The total \(A+B+C_{in}\) is at least 2 exactly when a carry is generated. Odd parity is the sum bit, so A and C describe \(S\), not \(C_{out}\). Exactly one 1 produces sum 1 and carry 0.

---

### Q2 — NAT

The number of select lines of a 64-to-1 multiplexer is ______.

**Answer.** 6

**Concept.** \(2^n\) data inputs need \(n\) selects.

**Difficulty.** Level 1

**Solution.** \(64 = 2^6\).

---

## Level 2 — Standard GATE

### Q3 — NAT

The minimum number of 2-to-1 multiplexers needed to build one 32-to-1 multiplexer is ______.

**Answer.** 31

**Concept.** Mux tree size \(2^n - 1\).

**Difficulty.** Level 2

**Solution.** \(32 = 2^5\), so the tree uses \(16+8+4+2+1 = 31\) muxes.

---

### Q4 — MCQ

The 4-bit Gray code of binary \(1011\), with the left bit the MSB, is

A. \(1011\)

B. \(1110\)

C. \(1101\)

D. \(1001\)

**Answer.** B

**Concept.** \(G_{msb}=B_{msb}\), \(G_i = B_{i+1} \oplus B_i\).

**Difficulty.** Level 2

**Solution.** \(G_3=1\), \(G_2=1\oplus 0=1\), \(G_1=0\oplus 1=1\), \(G_0=1\oplus 1=0\). Result \(1110\).

---

## Level 3 — Multi-step

### Q5 — MSQ

Select all that apply. Generate \(G_i = A_i B_i\) and propagate \(P_i = A_i \oplus B_i\).

A. \(C_1 = G_0 + P_0 C_0\)

B. \(C_2 = G_1 + P_1 G_0 + P_1 P_0 C_0\)

C. \(C_2 = G_1 + P_1 C_0\)

D. \(P_1 G_0\) is the carry generated at bit 0 and passed through bit 1

**Answer.** A, B, D

**Concept.** Unrolled lookahead.

**Difficulty.** Level 3

**Solution.** \(C_2 = G_1 + P_1 C_1\) and \(C_1 = G_0 + P_0 C_0\), so the expansion includes \(P_1 G_0\). Option C drops that term. It would miss the case \(A_0=B_0=1\), \(A_1 \neq B_1\), \(C_0=0\), which must produce \(C_2=1\).

---

### Q6 — NAT

A 4-to-16 decoder is built from 2-to-4 decoders with enable, and no other gates. The number of 2-to-4 decoders required is ______.

**Answer.** 5

**Concept.** One decoder creates the enables; four decode the low bits.

**Difficulty.** Level 3

**Solution.** The high two bits go to one 2-to-4 decoder. Each of its four outputs enables one 2-to-4 decoder. Those four all take the low two bits. Total 5.

---

## Level 4 — Trap

### Q7 — MCQ

An active-low 3-to-8 decoder is enabled. The target is \(F = \sum m(0,3,5)\). Which connection on the pins for \(m_0, m_3, m_5\) produces \(F\)?

A. OR the three pins

B. AND the three pins

C. NAND the three pins

D. NOR the three pins

**Answer.** C

**Concept.** Active-low minterm pins.

**Difficulty.** Level 4

**Solution.** Each chosen pin carries \(m_i'\). NAND of those pins is \((m_0' m_3' m_5')' = m_0 + m_3 + m_5\). OR of the pins is 0 only when all three minterms are 1, which never happens. AND of the pins is the product of complements.

**Trap.** Treating an active-low output as if it were already \(m_i\) and OR-ing it.

---

## Level 5 — Challenge

### Q8 — NAT

\(F(A,B,C) = \sum m(1,2,4,7)\) is implemented by one 4-to-1 multiplexer. The select inputs are \(A\) and \(B\), \(A\) more significant. How many of the four data inputs are tied to \(C'\)? ______.

**Answer.** 2

**Concept.** Cofactors as mux data.

**Difficulty.** Level 5

**Solution.**

| \(AB\) | \(F\) on \(C=0, C=1\) | Tie |
|--------|------------------------|-----|
| 00 | \(m_0=0\), \(m_1=1\) | \(C\) |
| 01 | \(m_2=1\), \(m_3=0\) | \(C'\) |
| 10 | \(m_4=1\), \(m_5=0\) | \(C'\) |
| 11 | \(m_6=0\), \(m_7=1\) | \(C\) |

Two data inputs are tied to \(C'\). None is tied to a constant.

**Trap.** Using \(C\) as a select line, or reading \(AB=01\) as minterms 4 and 5.

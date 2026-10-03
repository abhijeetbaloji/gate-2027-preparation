# Tabular Method — Practice

Original questions. They are not the 2015 prime-implicant stem. The skill is the same: combine distance-1 labels, separate primes from essential primes, and keep don’t-cares out of the chart.

## Level 1 — Conceptual

### Q1 — MCQ

Two implicants may be combined in one step when

A. their strings differ in exactly one bit, and any dashes already occupy the same positions

B. their strings differ in exactly two bits

C. they contain the same number of 1s

D. both are don’t-cares

**Answer.** A

**Concept.** The combine rule \(Px + Px' = P\).

**Difficulty.** Level 1

**Solution.** One bit of difference is one variable appearing both complemented and plain. Two bits of difference are not adjacent. Equal numbers of 1s usually means the strings are in the same bucket and differ in an even number of bits, so they are not combined with each other. Don’t-cares may combine, but that is not the condition for a combine.

---

### Q2 — NAT

Minterms \(m_5 = 0101\) and \(m_{13} = 1101\) combine. How many literals does the resulting product have, on four variables? ______.

**Answer.** 3

**Concept.** A dash deletes one literal.

**Difficulty.** Level 1

**Solution.** The strings differ only in \(A\). The result is \(-101 = BC'D\), three literals.

---

## Level 2 — Standard GATE

### Q3 — NAT

For \(f(A,B,C,D) = \sum m(0,2,8,10,12,14)\), the number of prime implicants is ______.

**Answer.** 2

**Concept.** Combining up to quads and counting unticked terms.

**Difficulty.** Level 2

**Solution.** Every listed minterm has \(D = 0\). The pairs collapse to two quads:

- \(-0-0\), covering \(0,2,8,10\), product \(B'D'\)
- \(1--0\), covering \(8,10,12,14\), product \(AD'\)

Every pair is ticked into one of these quads. The two quads do not combine: their dashes do not line up (\(B\) is fixed in the first and free in the second). Both are prime. So the prime count is 2.

---

### Q4 — MSQ

Select all that apply for the function in Q3.

A. \(B'D'\) is essential

B. \(AD'\) is essential

C. \(D'\) is a prime implicant

D. A minimal sum of products has two product terms

**Answer.** A, B, D

**Concept.** Single-mark columns.

**Difficulty.** Level 2

**Solution.** \(m_0\) is covered only by \(B'D'\). \(m_{12}\) is covered only by \(AD'\). Both primes are essential, so every minimal SOP has those two products. \(D'\) would also cover \(m_4\) and \(m_6\), which are required 0s, so \(D'\) is not an implicant.

---

## Level 3 — Multi-step

### Q5 — NAT

For \(f(A,B,C) = \sum m(0,1,2,5,6,7)\), the number of essential prime implicants is ______.

**Answer.** 0

**Concept.** Every onset minterm lies in two primes.

**Difficulty.** Level 3

**Solution.** The six pairs \(A'B'\), \(A'C'\), \(B'C\), \(BC'\), \(AC\), and \(AB\) are all prime: every quad hits the 0 at \(m_3\) or at \(m_4\). Each onset minterm is in two of those pairs. Example: \(m_0\) is in \(A'B'\) and in \(A'C'\). No column has a single mark, so no prime is essential. A minimal cover still uses three primes, such as \(A'C' + B'C + AB\).

**Trap.** Reporting 6, the prime count, as the essential count.

---

## Level 4 — Trap

### Q6 — MCQ

While building the chart for an onset that includes \(m_0\), the minterm \(m_0\) was combined with another minterm. Which statement is right?

A. \(m_0\) is deleted from the chart because it is ticked

B. \(m_0\) stays as a column; ticking only removes it from the list of primes

C. \(m_0\) becomes a don’t-care

D. The prime that contains \(m_0\) is automatically essential

**Answer.** B

**Concept.** Tick versus cover.

**Difficulty.** Level 4

**Solution.** A tick records that the string is contained in a larger implicant, so the string is not a prime row. The onset column remains until some selected prime covers it. Combination does not change a required 1 into a don’t-care. Containing \(m_0\) is not enough for essential status; \(m_0\) must have no second prime.

---

## Level 5 — Challenge

### Q7 — NAT

\(f(A,B,C,D) = \sum m(0,2,8,10,12,14) + d(4,6)\). Using the don’t-cares in the usual way, the number of literal occurrences in the minimal sum of products is ______.

**Answer.** 1

**Concept.** Don’t-cares completing the subcube \(D'\).

**Difficulty.** Level 5

**Solution.** The onset of Q3 together with \(d(4)\) and \(d(6)\) is every minterm with \(D = 0\). Those eight strings combine to the single prime \(D'\). There is no required 0 with \(D = 0\). One literal. The two-prime cover from Q3 is what you get if the don’t-cares are refused; the stem allows them.

**Trap.** Reporting 4, the literal count of \(B'D' + AD'\) with the don’t-cares ignored.

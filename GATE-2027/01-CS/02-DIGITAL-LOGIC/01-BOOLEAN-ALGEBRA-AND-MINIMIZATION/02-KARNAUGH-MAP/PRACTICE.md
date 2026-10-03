# Karnaugh Map — Practice

Original questions, not previous-year questions. They practise Gray adjacency, power-of-two groups, don’t-cares, POS, and essential primes.

## Level 1 — Conceptual

### Q1 — MCQ

On a 3-variable Karnaugh map, how many cells are adjacent to \(m_0\)?

A. 2

B. 3

C. 4

D. 1

**Answer.** B

**Concept.** Hamming-distance adjacency.

**Difficulty.** Level 1

**Solution.** Three variables give three neighbours. For \(m_0 = 000\) they are \(m_1 = 001\), \(m_2 = 010\), and \(m_4 = 100\). The cell is not adjacent to itself. A 4-variable map is the case with 4 neighbours.

---

### Q2 — MSQ

Select all that apply.

A. A loop of 4 cells can be one product term.

B. A loop of 6 cells can be one product term.

C. The four corner cells of a 4-variable map can be one product term.

D. A loop may wrap from the left edge to the right edge.

**Answer.** A, C, D

**Concept.** Legal subcubes, including wraps.

**Difficulty.** Level 1

**Solution.** Product terms have onset size \(2^k\). Four is allowed; six is not. The corners \(m_0, m_2, m_8, m_{10}\) are the subcube \(B'D'\) in the standard \(AB/CD\) layout, and the Gray labelling is what makes the left and right edges adjacent.

---

## Level 2 — Standard GATE

### Q3 — NAT

\(F(A,B,C,D) = \sum m(0,1,2,3,8,9,10,11)\), with \(A\) the most significant bit. The number of literal occurrences in the minimal sum of products is ______.

**Answer.** 1

**Concept.** One octet, one literal.

**Difficulty.** Level 2

**Solution.** The list is every minterm with \(B = 0\), and no minterm with \(B = 1\). One group of 8 deletes \(A\), \(C\), and \(D\). \(F = B'\).

**Trap.** Splitting the octet into two quads \(A'B'\) and \(AB'\) and reporting two products.

---

### Q4 — MCQ

A minimal sum of products of \(F(A,B,C) = \sum m(0,2,5,7)\) is

A. \(A'C' + AC\)

B. \(B\)

C. \(C\)

D. \(A'B' + AB\)

**Answer.** A

**Concept.** Two disjoint pairs.

**Difficulty.** Level 2

**Solution.** \(m_0, m_2 = 000, 010\) is \(A'C'\). \(m_5, m_7 = 101, 111\) is \(AC\). No larger group exists: \(m_0\) is not adjacent to \(m_5\) or \(m_7\), and \(m_2 = 010\) is not adjacent to \(m_5 = 101\). Options B and C are 1 on rows that are not in the onset. Option D misses \(m_2\) and \(m_5\).

---

## Level 3 — Multi-step

### Q5 — MSQ

Select all that apply. \(F(A,B,C) = \sum m(0,1,2,5)\).

A. \(A'C' + B'C\) is a minimal sum of products.

B. \((A' + C)(B' + C')\) is a minimal product of sums.

C. \(A'B'\) is an essential prime implicant.

D. The canonical SOP has 4 minterms.

**Answer.** A, B, D

**Concept.** SOP, POS, and the difference between prime and essential.

**Difficulty.** Level 3

**Solution.** Pairs: \(m_0 m_1 = A'B'\), \(m_0 m_2 = A'C'\), \(m_1 m_5 = B'C\). The cover \(A'C' + B'C\) uses every onset minterm and no 0, with two products. The 0s are \(m_3, m_4, m_6, m_7\). Grouping \(m_4 m_6\) gives \(A' + C\), and grouping \(m_3 m_7\) gives \(B' + C'\).

\(A'B'\) is prime, but \(m_0\) is also in \(A'C'\) and \(m_1\) is also in \(B'C\), so it is not essential. The onset has four minterms by the list.

---

### Q6 — NAT

\(F(A,B,C) = \sum m(0,1,4) + d(5)\). Using the don’t-care legally, the number of literal occurrences in a minimal sum of products is ______.

**Answer.** 1

**Concept.** A don’t-care that completes a subcube.

**Difficulty.** Level 3

**Solution.** Cells with \(B = 0\) are \(m_0, m_1, m_4, m_5\). The first three are onset and \(m_5\) is don’t-care. No required 0 has \(B = 0\). So \(F = B'\) is legal. One literal.

Without the don’t-care, \(B'\) would include the required 0 at \(m_5\), and the minimal SOP would be the two pairs \(A'B'\) and \(B'C'\), with four literals. The don’t-care is what collapses it.

---

## Level 4 — Trap

### Q7 — MCQ

For \(F(A,B,C) = \sum m(0,2,6) + d(1,7)\), which grouping is legal and minimal?

A. All four cells where \(C = 0\), written \(C'\)

B. All four cells where \(A = 0\), written \(A'\)

C. The pair \(m_0\) with don’t-care \(m_1\), together with the pair \(m_2\) with \(m_6\)

D. The pair \(m_4\) with \(m_6\)

**Answer.** C

**Concept.** A don’t-care may be used; a required 0 may not.

**Difficulty.** Level 4

**Solution.** \(m_4 = 100\) is a required 0, so the \(C'\) octet is illegal. \(m_3 = 011\) is a required 0, so \(A'\) is illegal. \(m_4\) with \(m_6\) includes that same required 0. Option C is \(A'B' + BC'\): it covers \(m_0, m_2, m_6\), uses \(m_1\), and avoids every required 0. Neither product can be deleted.

**Trap.** Treating X as a 1 that fills \(C'\), and not checking \(m_4\).

---

## Level 5 — Challenge

### Q8 — NAT

\(F(A,B,C,D) = \sum m(1,3,4,6,9,11,12,14)\), \(A\) most significant. The number of product terms in the unique minimal sum of products is ______.

**Answer.** 2

**Concept.** Recognising a two-subcube function from the list.

**Difficulty.** Level 5

**Solution.** The onset is exactly the rows where \(B \neq D\):

- \(B = 0, D = 1\): \(m_1, m_3, m_9, m_{11}\)
- \(B = 1, D = 0\): \(m_4, m_6, m_{12}, m_{14}\)

So \(F = B'D + BD' = B \oplus D\). Each product is a group of 4, and the two groups are disjoint, so both are essential. No single product covers both a \(BD\) pattern and its opposite. The minimal SOP has two products.

**Trap.** Counting eight minterms, or four pairs, and reporting 4 or 8.

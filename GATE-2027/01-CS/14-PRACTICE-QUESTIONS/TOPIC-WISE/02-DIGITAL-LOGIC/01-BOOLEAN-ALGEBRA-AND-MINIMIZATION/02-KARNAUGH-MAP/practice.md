# Karnaugh Map — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

How many cells does a 4-variable Karnaugh map contain?

A. 8

B. 12

C. 16

D. 32

---

## Q2 — MSQ

Select all that apply. Which of the following are legal groupings of 1-cells (or allowed don't-care cells) on a Karnaugh map?

A. A group of 3 cells

B. A group of 4 cells

C. A group of 1 cell

D. A group of 8 cells on a 4-variable map

---

## Q3 — NAT

In a 4-variable Karnaugh map, the number of cells adjacent to minterm \(m_0\) is ______. Adjacency includes the wraps of the Gray-code labeling. A cell is not adjacent to itself.

---

## Q4 — MCQ

Which pair of minterms is not adjacent on a 4-variable Karnaugh map?

A. \(m_0\) and \(m_8\)

B. \(m_0\) and \(m_2\)

C. \(m_0\) and \(m_5\)

D. \(m_5\) and \(m_7\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The minimal sum-of-products form of \(F(A, B, C) = \sum m(0, 2, 3, 4, 5, 6)\) is

A. \(C' + A'B + AB'\)

B. \(C' + A\)

C. \(B + C'\)

D. \(A'B' + BC + AC\)

---

## Q6 — NAT

\(F(A, B, C, D) = \sum m(0, 1, 2, 3, 4, 5, 6, 7)\). The number of literal occurrences in the minimal sum of products is ______.

---

## Q7 — MSQ

Select all that apply. For \(F(A, B, C) = \sum m(1, 3, 5, 7)\),

A. the only prime implicant is \(C\)

B. the pair \(m_1 + m_3\) is a prime implicant

C. both a minimal sum of products and a minimal product of sums equal the single literal \(C\)

D. the function has four essential prime implicants

---

## Q8 — MCQ

For \(F(A, B, C) = \sum m(0, 2, 6) + d(1, 7)\), which one of the following is a minimal sum of products?

A. \(A'B' + BC'\)

B. \(A' + BC'\)

C. \(C'\)

D. \(AB + A'C + BC'\)

---

## Q9 — NAT

\(F(A, B, C, D) = \sum m(0, 1, 2, 4, 5, 6, 8, 9, 10, 12, 13, 14)\). The number of product terms in the unique minimal sum of products is ______.

---

## Level 3 — Multi-Step

## Q10 — MCQ

A minimal product-of-sums form of \(F(A, B, C) = \sum m(0, 1, 2, 5)\) is

A. \((A' + C)(B' + C')\)

B. \((A + C)(B + C')\)

C. \(A'C' + B'C\)

D. \((A' + C')(B' + C)\)

---

## Q11 — NAT

\(F(A, B, C, D) = \sum m(1, 3, 7, 9, 11, 15) + d(0, 2, 5)\). The number of essential prime implicants is ______.

---

## Q12 — MSQ

Select all that apply. For \(F(A, B, C) = \sum m(0, 2, 3, 4, 5, 6)\),

A. \(C'\) is an essential prime implicant

B. \(A'C'\) is a prime implicant

C. every prime implicant of \(F\) is essential

D. minterm \(m_1\) must be covered by the chosen groups

---

## Q13 — MCQ

A minimal sum of products of \(F(A, B, C, D) = \sum m(1, 3, 7, 9, 11, 15) + d(0, 2, 5)\) is

A. \(B'D + CD\)

B. \(A'D + CD\)

C. \(D\)

D. \(B'D + A'D\)

---

## Level 4 — Tricky / Trap-Based

## Q14 — MSQ

Select all that apply. The sum \(F = AC + A'B\) is implemented as two-level AND-OR logic, and \(A'\) comes from an inverter.

A. \(AC\) and \(A'B\) are both essential prime implicants of \(F\).

B. The circuit has a static-1 hazard.

C. \(BC\) is a prime implicant of \(F\).

D. Including the product \(BC\) in the sum changes the function.

---

## Q15 — NAT

\(F(A, B, C) = \sum m(1, 5) + d(3, 7)\). The number of literal occurrences in a literal-minimum sum of products, where don't-care cells may be used, is ______.

---

## Q16 — MCQ

For \(F(A, B, C) = \sum m(0, 2, 6) + d(1, 7)\), which grouping is illegal?

A. \(m_0\) with the don't-care cell \(m_1\)

B. \(m_6\) with the don't-care cell \(m_7\)

C. \(m_4\) with \(m_6\)

D. \(m_2\) with \(m_6\)

---

## Level 5 — Challenge

## Q17 — NAT

\(F(A, B, C, D) = \sum m(0, 2, 3, 5, 7, 8, 10, 11, 13, 15)\). The number of distinct minimal sums of products is ______. Two sums that use the same set of product terms are the same expression.

---

## Q18 — MSQ

Select all that apply. For the function in Q17,

A. \(BD\) is an essential prime implicant

B. \(CD\) is an essential prime implicant

C. \(B'D'\) is an essential prime implicant

D. \(B'C + BD + B'D'\) is a minimal sum of products

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MSQ | B, C, D |
| 3 | NAT | 4 |
| 4 | MCQ | C |
| 5 | MCQ | A |
| 6 | NAT | 1 |
| 7 | MSQ | A, C |
| 8 | MCQ | A |
| 9 | NAT | 2 |
| 10 | MCQ | A |
| 11 | NAT | 2 |
| 12 | MSQ | A, C |
| 13 | MCQ | A |
| 14 | MSQ | A, B, C |
| 15 | NAT | 1 |
| 16 | MCQ | C |
| 17 | NAT | 2 |
| 18 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: **C**

A \(k\)-variable map has \(2^k\) cells, one per minterm. For \(k = 4\) that is 16. Option (A) is the 3-variable map. Option (D) counts input combinations of a 5-variable function.

### Q2

Answer: **B, C, D**

A legal group is a rectangle of \(2^k\) cells, so the allowed sizes are 1, 2, 4, 8, and so on, up to the whole map. A block of 3 cells is not a power of two and does not correspond to a single product term. On a 4-variable map a group of 8 is a single literal, and a group of 1 is a full minterm. Both are legal; they are just not always minimal.

### Q3

Answer: **4**

The label of \(m_0\) is \(ABCD = 0000\). Changing exactly one bit produces \(m_8\) (flip \(A\)), \(m_4\) (flip \(B\)), \(m_2\) (flip \(C\)) and \(m_1\) (flip \(D\)). Each variable contributes one neighbour, so a 4-variable cell has four neighbours. The trap is to answer 2 because a printed map shows only the left and upper neighbours and the wraps are forgotten.

### Q4

Answer: **C**

Adjacent cells differ in exactly one bit.

- \(m_0 = 0000\) and \(m_8 = 1000\) differ only in \(A\).
- \(m_0 = 0000\) and \(m_2 = 0010\) differ only in \(C\).
- \(m_5 = 0101\) and \(m_7 = 0111\) differ only in \(C\).
- \(m_0 = 0000\) and \(m_5 = 0101\) differ in \(B\) and in \(D\).

Those two cells lie on a diagonal of the \(B\)-\(D\) change. They must not be grouped as a pair.

### Q5

Answer: **A**

The octet of \(C = 0\) is the quad \(\{m_0, m_2, m_4, m_6\} = C'\). The remaining 1s are \(m_3 = 011\) and \(m_5 = 101\). The largest group around \(m_3\) is the pair \(A'B = \{m_2, m_3\}\). The largest group around \(m_5\) is \(AB' = \{m_4, m_5\}\). All three groups are essential. The minimal sum is \(C' + A'B + AB'\).

Option (B) is 1 at \(m_7 = 111\), a specified 0. Option (C) is also 1 at \(m_7\). Option (D) is 1 at \(m_1 = 001\) because of \(A'B'\), and \(m_1\) is a specified 0; it also fails to cover \(m_4\).

### Q6

Answer: **1**

The listed minterms are exactly the eight cells with \(A = 0\). They form one group of 8, the literal \(A'\). A single literal is one literal occurrence. Writing four separate pairs, or writing \(A'B' + A'B\), is correct but not minimal.

### Q7

Answer: **A, C**

The four minterms are exactly the cells \(C = 1\). That quad cannot be enlarged, so \(C\) is prime, and it is the only prime implicant. The function is identical to the literal \(C\), so the minimal sum and the minimal product of sums are both \(C\).

The pair \(m_1 + m_3 = A'C\) is an implicant, but it is contained in the quad \(C\), so it is not prime. There are not four essential primes; the four minterms are all covered by the single essential prime \(C\).

### Q8

Answer: **A**

Required 1s are \(m_0, m_2, m_6\). Don't cares are \(m_1, m_7\). The cell \(m_4\) is a hard 0, and so is \(m_3\). One minimal cover uses the don't care \(m_1\) to form \(A'B' = \{m_0, m_1\}\) and groups \(m_2\) with \(m_6\) as \(BC'\). Every required 1 is covered, and no hard 0 is covered.

Two other sums are equally small: \(A'C' + BC'\) and \(A'C' + AB\). The question asks for one minimal sum, and only (A) is valid.

Option (B) uses \(A'\), which covers the hard 0 \(m_3\). Option (C) covers the hard 0 \(m_4\). Option (D) contains \(A'C\), which also covers \(m_3\).

### Q9

Answer: **2**

The missing minterms are \(m_3, m_7, m_11, m_15\), exactly the cells \(CD = 11\). Thus \(F = (CD)' = C' + D'\). Both single-literal groups are essential: \(D'\) is the only prime that covers \(m_2\), and \(C'\) is the only prime that covers \(m_1\). The unique minimal sum has two product terms. The product \(C'D'\) is a different function; it is 0 on \(m_1\).

### Q10

Answer: **A**

The 0s of \(F\) are \(m_3, m_4, m_6, m_7\), so \(F' = \sum m(3, 4, 6, 7)\). On that map, \(m_3\) forces the prime \(BC\), and \(m_4\) forces the prime \(AC'\). Their sum \(BC + AC'\) already covers \(m_6\) and \(m_7\). Complementing gives

\[
F = (B' + C')(A' + C).
\]

Option (B) is 0 at \(m_0\), where \(F\) is 1. Option (D) is 0 at \(m_5\), where \(F\) is 1. Option (C) is the minimal sum of products of \(F\), namely \(A'C' + B'C\). It represents the same function, but it is not a product of sums. The question asks for the POS form.

### Q11

Answer: **2**

The required 1s all have \(D = 1\): \(m_1, m_3, m_7, m_9, m_11, m_15\). Don't cares are \(m_0, m_2, m_5\). The quad \(CD = \{m_3, m_7, m_11, m_15\}\) is the only prime that covers \(m_{15}\). The quad \(B'D = \{m_1, m_3, m_9, m_11\}\) is the only prime that covers \(m_9\). So there are exactly two essential prime implicants. The primes \(A'D\) and \(A'B'\) are real but not essential; each of their required minterms is already covered by \(B'D\) or by \(CD\).

### Q12

Answer: **A, C**

This is the function of Q5. The complete prime set is \(\{C',\ A'B,\ AB'\}\), and each one alone covers a minterm the others miss:

- only \(C'\) covers \(m_0\),
- only \(A'B\) covers \(m_3\),
- only \(AB'\) covers \(m_5\).

So every prime implicant is essential. \(A'C' = \{m_0, m_2\}\) is an implicant, but it sits inside \(C'\) and is not prime. Minterm \(m_1\) is a specified 0. Covering it makes the expression wrong. Essential primes are about covering 1s that nobody else covers, not about covering 0s.

### Q13

Answer: **A**

From the chart in Q11, the two essential primes \(B'D\) and \(CD\) together cover every required 1:

- \(B'D\) covers \(m_1, m_3, m_9, m_11\),
- \(CD\) covers \(m_3, m_7, m_11, m_15\).

Option (B) never covers \(m_9 = 1001\). Option (D) never covers \(m_{15} = 1111\). Option (C) covers hard 0s such as \(m_{13}\). Don't cares \(m_0\) and \(m_2\) are used inside \(A'B'\) if one builds that nonessential prime; they are not a reason to replace the essential cover by the single literal \(D\).

### Q14

Answer: **A, B, C**

The onset is \(\{m_2, m_3, m_5, m_7\}\). The primes are \(A'B = \{m_2, m_3\}\), \(AC = \{m_5, m_7\}\) and \(BC = \{m_3, m_7\}\). Only \(A'B\) covers \(m_2\), and only \(AC\) covers \(m_5\), so those two are essential. Their sum is already a complete minimal SOP, so \(BC\) is a nonessential prime. Adding it does not change the function: at every onset cell it is either already 1 or, off the onset, \(BC = 0\). Option (D) is false. In particular at \(m_5 = 101\), \(BC = 0\).

The minimal cover still has a static-1 hazard. With \(B = C = 1\), changing \(A\) moves between \(m_7\) and \(m_3\). Both cells are 1, they are adjacent, and no single product in \(AC + A'B\) contains both. While \(A\) falls and \(A'\) has not yet risen, both products can be 0. The function value is 1 at both ends of the transition. The hazard is a property of this cover, not a change in \(F\). Including the nonessential prime \(BC\) holds the output at 1 during that transition.

### Q15

Answer: **1**

The cells \(m_1, m_3, m_5, m_7\) are \(C = 1\). Two of them are required 1s and two are don't cares, and none of the \(C = 1\) cells is a hard 0. The single implicant \(C\) is legal and uses one literal.

If every don't care is forced to 0, the largest legal group is the pair \(B'C = \{m_1, m_5\}\), which has two literals. That expression meets the specification, because don't cares may be 0, but it is not literal-minimum. The misuse is refusing a don't care that costs nothing and removes a literal. The opposite misuse, covering a hard 0, is also illegal; it just does not arise inside the cube \(C\) for this function.

### Q16

Answer: **C**

\(m_4 = 100\) is neither a required 1 nor a don't care, so it is a hard 0. A group that contains it implements the wrong function on a specified row. The other three pairs are legal:

- \(m_0\) with \(m_1\) is \(A'B'\), using a don't care,
- \(m_6\) with \(m_7\) is \(AB\), using a don't care,
- \(m_2\) with \(m_6\) is \(BC'\), using two required 1s.

Don't cares may enter a group. Specified 0s may not.

### Q17

Answer: **2**

The primes are \(B'D' = \{m_0, m_2, m_8, m_{10}\}\), \(BD = \{m_5, m_7, m_{13}, m_{15}\}\), \(CD = \{m_3, m_7, m_{11}, m_{15}\}\) and \(B'C = \{m_2, m_3, m_{10}, m_{11}\}\).

\(B'D'\) is the only prime covering \(m_0\) and \(m_8\). \(BD\) is the only prime covering \(m_5\) and \(m_{13}\). Both are essential. After they are chosen, the uncovered required minterms are \(m_3\) and \(m_{11}\). Either \(CD\) or \(B'C\) covers both. The two minimal sums are

\[
B'D' + BD + CD, \qquad B'D' + BD + B'C.
\]

There is no two-term cover: \(B'D' + BD\) misses \(m_3\) and \(m_{11}\).

### Q18

Answer: **A, C, D**

From the chart in Q17, \(BD\) and \(B'D'\) are essential, and \(CD\) is not, because the second minimal sum avoids it. Option (B) confuses "appears in some minimal sum" with "essential". A prime is essential only when some minterm has no other prime. Here \(m_3\) can be covered by \(CD\) or by \(B'C\), and \(m_{11}\) likewise.

Option (D) is the second minimal sum. It has three product terms, the minimum, and it covers the whole onset: \(B'D'\) covers \(m_0, m_2, m_8, m_{10}\); \(BD\) covers \(m_5, m_7, m_{13}, m_{15}\); \(B'C\) covers \(m_3\) and \(m_{11}\).

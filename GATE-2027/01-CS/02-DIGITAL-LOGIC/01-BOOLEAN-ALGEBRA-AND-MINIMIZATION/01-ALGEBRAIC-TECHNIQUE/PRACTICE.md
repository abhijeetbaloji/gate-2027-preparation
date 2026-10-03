# Boolean Algebra (Algebraic Technique) — Practice

Original questions. They are not previous-year questions. The mapped stems and the separate practice file in `14-PRACTICE-QUESTIONS` use the same ideas: absorption, covering, consensus, XOR, minterm counts, self-dual functions, and a failed De Morgan step.

## Level 1 — Conceptual

### Q1 — MCQ

Which equation is an identity?

A. \((x+y)' = x' + y'\)

B. \(x + xy = y\)

C. \(x(x+y) = x\)

D. \(xx' = 1\)

**Answer.** C

**Concept.** Absorption / complement laws.

**Difficulty.** Level 1

**Solution.** \(x(x+y) = xx + xy = x + xy = x(1+y) = x\). Option A fails at \((0,1)\). Option B: at \(x=1, y=0\), left side is 1 and right side is 0. Option D is 0, not 1.

**Trap.** Absorption keeps the shorter term. It does not replace \(x\) by \(y\).

---

### Q2 — NAT

The number of distinct Boolean functions of 2 variables is ______.

**Answer.** 16

**Concept.** Truth-table counting.

**Difficulty.** Level 1

**Solution.** Two variables give \(2^2 = 4\) rows. Each row has 2 possible outputs, so \(2^4 = 16\).

---

## Level 2 — Standard GATE

### Q3 — MCQ

The expression \(A + A'BC + A'B'C\) simplifies to

A. \(A + C\)

B. \(A + B\)

C. \(A\)

D. \(C\)

**Answer.** A

**Concept.** Covering, twice.

**Difficulty.** Level 2

**Solution.** \(A'BC + A'B'C = A'C(B+B') = A'C\). Then \(A + A'C = A + C\).

**Trap.** Stopping at \(A + A'C\) and then absorbing \(C\) away, as if the law were \(x+xy = x\) with the complement ignored.

---

### Q4 — NAT

\(F(A,B,C) = (A+B)(A'+C)\). The number of minterms in the canonical SOP of \(F\) is ______.

**Answer.** 5

**Concept.** Expand, then count onset rows.

**Difficulty.** Level 2

**Solution.** \((A+B)(A'+C) = AC + A'B + BC\). The consensus view is the same function as \(AC + A'B\). Rows:

| \(ABC\) | \(AC + A'B\) |
|---------|-------------:|
| 000 | 0 |
| 001 | 0 |
| 010 | 1 |
| 011 | 1 |
| 100 | 0 |
| 101 | 1 |
| 110 | 1 |
| 111 | 1 |

Five rows are 1. The product \(BC\) does not add a sixth row.

---

## Level 3 — Multi-step

### Q5 — MSQ

Select all that apply. Let \(F = (P \oplus Q) \oplus (P \oplus 1)\).

A. \(F = Q'\)

B. \(F = P \oplus Q\)

C. \(F = 1\) on exactly two of the four assignments of \((P,Q)\)

D. \(F = (P \odot Q)'\)

**Answer.** A, C

**Concept.** XOR with a constant.

**Difficulty.** Level 3

**Solution.** \(P \oplus 1 = P'\). So \(F = (P \oplus Q) \oplus P' = P \oplus Q \oplus P' = (P \oplus P') \oplus Q = 1 \oplus Q = Q'\).

\(Q'\) is 1 on \((P,Q) = (0,0)\) and \((1,0)\) only, which is two of the four assignments. \(P \oplus Q\) differs from \(Q'\) on \((0,0)\): the XOR is 0 and \(Q'\) is 1, so B is false. D says \(F = (P \odot Q)'\). That right-hand side is \(P \oplus Q\), already different from \(Q'\).

**Trap.** Cancelling only one \(P\) and forgetting that \(P \oplus 1\) complemented the other copy.

---

### Q6 — MCQ

A minimal sum of products of \(XY + X'Z + YZ + X'YZ\) is

A. \(XY + X'Z\)

B. \(YZ\)

C. \(XY + Z\)

D. \(X'Z + Y\)

**Answer.** A

**Concept.** Consensus plus absorption.

**Difficulty.** Level 3

**Solution.** \(X'YZ\) is absorbed by \(X'Z\). The remaining \(YZ\) is the consensus of \(XY\) and \(X'Z\), so it is redundant. Neither \(XY\) nor \(X'Z\) can be dropped: \(X=Y=1, Z=0\) needs \(XY\), and \(X=0, Z=1, Y=0\) needs \(X'Z\).

---

## Level 4 — Trap

### Q7 — MCQ

A student simplifies \((A + B'C)'\) to \(A' + BC'\). Which statement is correct?

A. The result is right, by De Morgan.

B. The result is wrong. The complement is \(A' + B + C'\).

C. The result is wrong. The complement is \(A'(B + C')\).

D. The result is wrong. The complement is \(A' + BC'\), which is what the student wrote, so the student is right.

**Answer.** C

**Concept.** De Morgan on a sum whose second term is itself a product.

**Difficulty.** Level 4

**Solution.** \((A + B'C)' = A'(B'C)' = A'(B + C')\). That is option C. Expanding gives \(A'B + A'C'\), not \(A' + BC'\).

At \(A=0\), \(B=0\), \(C=1\) the inside is \(B'C = 1\), so the complement is 0. The student’s \(A' + BC'\) equals 1 on that row. Option B, \(A' + B + C'\), is also 1 there, so it is not the complement. Option D repeats the student’s expression.

**Trap.** Flipping the literals of \(B'C\) and leaving the AND in place. \((B'C)' = B + C'\), not \(BC'\).

---

### Q8 — NAT

The number of self-dual Boolean functions of 4 variables is ______.

**Answer.** 256

**Concept.** Pairing each input with its bitwise complement.

**Difficulty.** Level 4

**Solution.** There are \(2^{4-1} = 8\) pairs. Each pair contributes one free bit, so \(2^8 = 256\). The general count is \(2^{2^{n-1}}\). It is not \(2^{n-1} = 8\), and it is not half of all functions.

**Trap.** Halving \(2^{16}\) gives \(2^{15}\), which is the number of functions with \(F(0)=0\) or a similar single-point constraint, not self-duality.

---

## Level 5 — Challenge

### Q9 — MSQ

Select all that apply. \(F = AB + A'C\) and \(G = AB + A'C + BC\) are implemented as two-level AND-OR. The complement \(A'\) comes from an inverter.

A. \(F\) and \(G\) have the same truth table.

B. \(F(1,0,1) = G(1,0,1)\).

C. While \(A\) changes and \(B = C = 1\), the sum \(F\) can have a static-1 hazard.

D. The product \(BC\) is an essential prime implicant of \(F\).

**Answer.** A, B, C

**Concept.** Consensus versus prime implicants.

**Difficulty.** Level 5

**Solution.** \(BC\) is the consensus of \(AB\) and \(A'C\), so \(G = F\) on every stable input. In particular \(F(1,0,1) = 0 = G(1,0,1)\). With \(B = C = 1\), \(F = A + A'\). While \(A\) switches, both products of the sum \(AB + A'C\) can be 0 for an instant, so the OR can glitch to 0 even though the function is 1. That is a static-1 hazard.

The onset is minterms 1, 3, 6, and 7. \(AB\) covers 6 and 7. \(A'C\) covers 1 and 3. \(BC\) covers 3 and 7, and neither literal of \(BC\) can be dropped, so \(BC\) is prime. It is not essential: every onset minterm is already covered by \(AB\) or \(A'C\). Option D is false.

**Trap.** Calling every prime implicant essential, or treating a hazard as a difference of truth tables.

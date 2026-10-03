# Boolean Algebra: Algebraic Technique — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which one of the following is not an identity of Boolean algebra?

A. \(x + xy = x\)

B. \(x(x + y) = x\)

C. \(x + x' = 1\)

D. \(x \cdot x' = 1\)

---

## Q2 — MSQ

Select all that apply. Which of the following expressions equal \(x \oplus y\)?

A. \(x'y + xy'\)

B. \((x + y)(x' + y')\)

C. \((x + y)(xy)'\)

D. \(xy + x'y'\)

---

## Q3 — NAT

The number of distinct Boolean functions of 3 variables is ______.

---

## Q4 — MCQ

The dual of the expression \(x \cdot y + x' \cdot 0\) is

A. \((x + y)(x' + 1)\)

B. \((x + y)(x' + 0)\)

C. \(x' + y' + x \cdot 1\)

D. \((x + y')(x' + 1)\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The expression \((A + B)(A + B')(A' + B)\) simplifies to

A. \(A\)

B. \(B\)

C. \(AB\)

D. \(A + B\)

---

## Q6 — NAT

The minimal sum-of-products form of \(AB'C + AB'C' + A'BC + ABC\) has ______ literal occurrences. Count every occurrence of a complemented or uncomplemented variable. Do not count operators.

---

## Q7 — MSQ

Select all that apply. Which of the following expressions equal \(A + A'B\)?

A. \(A + B\)

B. \((A + B)(A + A')\)

C. \(A + B + AB'\)

D. \(AB + A'B'\)

---

## Q8 — MCQ

By the consensus theorem, which product term is redundant in \(XY + X'Z + YZ\)?

A. \(XY\)

B. \(X'Z\)

C. \(YZ\)

D. None of the three terms is redundant

---

## Q9 — NAT

Let \(F(P, Q) = (P + Q')(P' + Q)\). The number of minterms in the canonical sum-of-products form of \(F\) is ______.

---

## Level 3 — Multi-Step

## Q10 — MCQ

Algebraic simplification of \(A'B + BC' + AC + AB'C'\) gives which minimal sum of products?

A. \(A + B\)

B. \(A + B + C'\)

C. \(AB + AC\)

D. \(A'B + AC\)

---

## Q11 — NAT

For the three-variable function

\[
F(w, x, y) = w'x + wx'y + wxy' + w'x'y + wxy
\]

the number of input combinations at which \(F = 1\) is ______.

---

## Q12 — MSQ

Select all that apply. Let \(F(A, B, C) = AB + A'C\).

A. The cofactors are \(F(1, B, C) = B\) and \(F(0, B, C) = C\).

B. \(F = (A + C)(A' + B)\).

C. \(F' = (A' + B')(A + C')\).

D. \(F' = A'B' + AC'\).

---

## Q13 — MCQ

The minimal product-of-sums form of \(F = x'y + xy'\) is

A. \((x + y)(x' + y')\)

B. \((x + y')(x' + y)\)

C. \(xy + x'y'\)

D. \((x + y)(x + y')\)

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

A student claims that \((x + y)' = x' + y'\) is an identity. Which assignment is a counterexample?

A. \(x = 0,\ y = 0\)

B. \(x = 1,\ y = 1\)

C. \(x = 0,\ y = 1\)

D. The claim is true for every assignment, so no counterexample exists.

---

## Q15 — MSQ

Select all that apply. Compare \(F = xy + x'z\) with \(G = xy + x'z + yz\), both implemented as two-level AND-OR logic. Assume the complement \(x'\) is produced by an inverter, so \(x\) and \(x'\) do not change at the same instant.

A. \(F\) and \(G\) represent the same Boolean function.

B. The implementation of \(F\) has a static-1 hazard when \(x\) changes while \(y = z = 1\).

C. The product \(yz\) removes that static-1 hazard.

D. \(G(1, 1, 0)\) differs from \(F(1, 1, 0)\).

---

## Q16 — NAT

The number of assignments of \((A, B)\) for which \((A \oplus B)(A \oplus B)' = 1\) is ______.

---

## Level 5 — Challenge

## Q17 — MCQ

A Boolean function \(F\) of three variables is self-dual when \(F(x', y', z') = F(x, y, z)'\) for every input. How many self-dual functions of three variables are there?

A. 8

B. 16

C. 32

D. 128

---

## Q18 — NAT

Let \(P = A + B\) and \(Q = C + D\), and let

\[
F = PQ + P'Q'.
\]

The number of minterms of the four-variable function \(F(A, B, C, D)\) is ______.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | D |
| 2 | MSQ | A, B, C |
| 3 | NAT | 256 |
| 4 | MCQ | A |
| 5 | MCQ | C |
| 6 | NAT | 4 |
| 7 | MSQ | A, B, C |
| 8 | MCQ | C |
| 9 | NAT | 2 |
| 10 | MCQ | A |
| 11 | NAT | 6 |
| 12 | MSQ | A, B, C |
| 13 | MCQ | A |
| 14 | MCQ | C |
| 15 | MSQ | A, B, C |
| 16 | NAT | 0 |
| 17 | MCQ | B |
| 18 | NAT | 10 |

## Detailed Solutions

### Q1

Answer: **D**

The complement laws are \(x + x' = 1\) and \(x \cdot x' = 0\). Option (D) swaps the constant. Options (A) and (B) are the two absorption laws. Option (C) is the sum form of the complement law.

### Q2

Answer: **A, B, C**

Expand (B): \((x + y)(x' + y') = xy' + x'y\). Expand (C): \((xy)' = x' + y'\), so \((x + y)(xy)'\) is the same product as (B). Both equal the standard XOR polynomial in (A). Option (D) is \(x \odot y\), the complement of XOR. It is 1 when \(x\) and \(y\) are equal, which is exactly where XOR is 0.

### Q3

Answer: **256**

A function of 3 variables is fixed by an 8-row truth table, and each row may be 0 or 1. The count is \(2^{2^3} = 2^8 = 256\). The trap is to answer \(2^3 = 8\) (the number of minterms) or \(3^2 = 9\).

### Q4

Answer: **A**

Duality interchanges \(+\) with \(\cdot\) and interchanges the constants 0 and 1. It does not complement the variables. Starting from \(x \cdot y + x' \cdot 0\), the dual is \((x + y) \cdot (x' + 1)\).

Option (B) forgets to dualize the constant 0. Option (C) complements variables and also changes the operators incorrectly; that is closer to a mangled complement than to a dual. Option (D) complements \(y\), which duality does not do. As a check, the original expression simplifies to \(xy\), whose dual is \(x + y\), and (A) simplifies to \(x + y\) because \(x' + 1 = 1\).

### Q5

Answer: **C**

First, \((A + B)(A + B') = A + BB' = A\). Then \(A(A' + B) = AB\). Stopping after the first step and answering \(A\) is the usual incomplete simplification. The third factor \(A' + B\) removes the part of \(A\) on which \(B = 0\).

### Q6

Answer: **4**

\(AB'C + AB'C' = AB'(C + C') = AB'\). Also \(A'BC + ABC = BC(A' + A) = BC\). The sum \(AB' + BC\) has four literal occurrences. Neither term absorbs the other: \(AB'\) is needed at \(A = 1, B = 0, C = 0\), and \(BC\) is needed at \(A = 0, B = 1, C = 1\).

### Q7

Answer: **A, B, C**

The factoring identity \(A + A'B = (A + A')(A + B) = A + B\) gives (A) and (B), since \(A + A' = 1\). For (C), \(AB'\) is absorbed by \(A + B\). Option (D) is XNOR. At \(A = 1, B = 0\) the target equals 1, while \(AB + A'B' = 0\).

### Q8

Answer: **C**

The consensus theorem says \(XY + X'Z + YZ = XY + X'Z\). The term \(YZ\) is the consensus of \(XY\) and \(X'Z\), so it may be dropped. Dropping \(XY\) or \(X'Z\) changes the function: \(X = 1, Y = 1, Z = 0\) needs \(XY\), and \(X = 0, Y = 0, Z = 1\) needs \(X'Z\).

### Q9

Answer: **2**

\((P + Q')(P' + Q) = PQ + P'Q'\). The two product terms are minterms \(m_3\) and \(m_0\). The same expression is \(P \odot Q\), which is 1 on exactly two of the four rows. It is not XOR, which would also have two minterms but the other pair, \(m_1\) and \(m_2\).

### Q10

Answer: **A**

Group \(AB'C' + BC' = C'(B + AB')\). The inner sum is \(A + B\), because \(B + AB' = (A + B)(B + B') = A + B\). Thus \(C'(A + B) = AC' + BC'\). The original expression also contributes \(A'B + AC\), so

\[
F = AC + AC' + A'B + BC' = A + A'B + BC'.
\]

Then \(A + A'B = A + B\), and \(B\) absorbs \(BC'\). Hence \(F = A + B\).

Option (B) is 1 at \(A = B = 0, C = 0\), where every original product is 0. Option (C) is 0 at \(A = 0, B = 1, C = 0\), where \(BC' = 1\). Option (D) misses \(A = 1, B = 0, C = 0\), where \(AB'C' = 1\).

### Q11

Answer: **6**

Combine \(wxy' + wxy = wx\). The expression is then

\[
w'x + wx + w'x'y + wx'y = x + x'y(w' + w) = x + x'y = x + y.
\]

Over three variables, \(x + y = 0\) only for the two points \((w, x, y) = (0, 0, 0)\) and \((1, 0, 0)\). The function is therefore 1 on \(8 - 2 = 6\) combinations. Leaving the five-term polynomial unsimplified and trying to count overlapping minterms by hand is what produces off-by-one answers.

### Q12

Answer: **A, B, C**

Substituting \(A = 1\) leaves \(B\). Substituting \(A = 0\) leaves \(C\). That is Shannon's expansion \(F = AF(1) + A'F(0)\).

For (B), \((A + C)(A' + B) = AB + A'C + BC\). The extra product \(BC\) is the consensus of \(AB\) and \(A'C\), so it does not change the function.

For (C), De Morgan's law applied twice gives \((AB + A'C)' = (AB)'(A'C)' = (A' + B')(A + C')\).

Option (D) is the mistake of complementing each product and then OR-ing the results. At \(A = 1, B = 0, C = 1\), one has \(F = 0\), so \(F' = 1\), but \(A'B' + AC' = 0\).

### Q13

Answer: **A**

\(F = x \oplus y\), so \(F' = xy + x'y'\). Complementing that minimal sum, again by De Morgan, produces \((x' + y')(x + y)\).

Option (B) expands to \(xy + x'y'\), which is \(F'\), not \(F\). Option (C) is the same complement written as a sum of products. Option (D) collapses to \(x\), which fails at \(x = 0, y = 1\).

### Q14

Answer: **C**

De Morgan's law is \((x + y)' = x'y'\), not \(x' + y'\). At \(x = 0, y = 1\), the left side is \((0 + 1)' = 0\) and the right side is \(1 + 0 = 1\).

The assignment \(x = 1, y = 0\) is also a counterexample, but it is not one of the listed pairs. The listed pairs in (A) and (B) happen to agree on both sides: both sides are 1 when \(x = y = 0\), and both sides are 0 when \(x = y = 1\). Agreement on those two rows does not make the claim an identity. Option (D) is that false conclusion.

### Q15

Answer: **A, B, C**

\(yz\) is the consensus of \(xy\) and \(x'z\), so \(G = F\) as Boolean functions. Option (D) fails because at \((1, 1, 0)\) one has \(yz = 0\), and both expressions equal \(xy = 1\).

The functions agree at the two static endpoints \(x = 1\) and \(x = 0\) with \(y = z = 1\): both endpoints give output 1. During the change, \(xy\) falls while \(x'z\) has not yet risen, so a two-level implementation of \(F\) can glitch to 0. That is a static-1 hazard. It is not a change in the function. The added product \(yz\) stays 1 throughout that transition and covers the glitch. Functional equality and hazard-freedom are different questions.

### Q16

Answer: **0**

For every Boolean value \(G\), the product \(G \cdot G'\) is 0. Here \(G = A \oplus B\). The expression is the constant 0 on all four rows, so it equals 1 on none of them. A common slip is to answer 2 because XOR itself is 1 on two rows, and then forget that the factor \(G'\) kills those rows.

### Q17

Answer: **B**

The input \(m\) and its total complement \(m \oplus 111_2\) form a pair. Self-duality fixes the output on the complemented input to be the opposite of the output on \(m\). The four pairs are \((0, 7)\), \((1, 6)\), \((2, 5)\) and \((3, 4)\). Each pair contributes one free bit, so there are \(2^4 = 16\) self-dual functions. Equivalently the count is \(2^{2^{n-1}}\) at \(n = 3\).

Option (A) frees only three bits. Option (D), \(2^7 = 128\), is what one gets by freely filling seven truth-table rows and then setting a single remaining row; that does not enforce the condition on every complementary pair. Half of all 256 functions is also 128, and that is a different subset.

### Q18

Answer: **10**

\(F = 1\) exactly when the bits \(P\) and \(Q\) are equal. \(A + B = 0\) for 1 assignment of \((A, B)\) and equals 1 for the other 3. The same counts hold for \((C, D)\). Both zero contributes \(1 \cdot 1 = 1\) minterm. Both one contributes \(3 \cdot 3 = 9\) minterms. The total is 10. The other 6 minterms are the cases where exactly one of \(P, Q\) is 1.

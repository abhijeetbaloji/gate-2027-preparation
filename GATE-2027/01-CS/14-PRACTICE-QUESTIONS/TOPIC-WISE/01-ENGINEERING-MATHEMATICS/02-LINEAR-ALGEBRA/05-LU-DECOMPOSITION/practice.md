# LU Decomposition — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the standard factorization \(A = LU\) used here, \(L\) is unit lower triangular. That means the diagonal entries of \(L\) are

(A) all equal to \(1\)

(B) the pivots produced by elimination

(C) all equal to \(0\)

(D) equal to the corresponding diagonal entries of \(A\)

---

## Q2 — NAT

Let

$$
A = \begin{bmatrix} 3 & 1 \\ 6 & 5 \end{bmatrix} = LU,
$$

with \(L\) unit lower triangular and \(U\) upper triangular, and with no row interchange. The subdiagonal entry \(\ell_{21}\) is ____.

---

## Q3 — MCQ

After a factorization \(A = LU\) has been computed, the system \(Ax = b\) is solved by

(A) solving \(Ux = b\), then solving \(Ly = x\)

(B) solving \(Ly = b\), then solving \(Ux = y\)

(C) solving \(Ux = b\) alone

(D) solving \(Lx = b\) alone

---

## Level 2 — Standard GATE Style

## Q4 — NAT

For the factorization in Q2,

$$
A = \begin{bmatrix} 3 & 1 \\ 6 & 5 \end{bmatrix} = LU
$$

with no row interchange, \(\det(A)\) equals ____.

---

## Q5 — MCQ

Let

$$
A = \begin{bmatrix} 0 & 2 \\ 1 & 3 \end{bmatrix}.
$$

Which one of the following is correct?

(A) \(A\) has an LU factorization with no row interchange

(B) The \((1, 1)\) pivot is \(0\), so a row interchange is required before an LU factorization

(C) \(A\) is singular

(D) Every LU factorization of \(A\) must put \(0\) on the diagonal of \(L\)

---

## Q6 — NAT

Using \(A = LU\) from Q2, solve \(Ax = b\) for

$$
b = \begin{bmatrix} 4 \\ 11 \end{bmatrix}.
$$

The value of \(x_1 + x_2\) is ____.

---

## Level 3 — Multi-Step

## Q7 — NAT

Let

$$
A = \begin{bmatrix} 1 & 2 & 1 \\ 2 & 5 & 3 \\ 3 & 7 & 6 \end{bmatrix} = LU,
$$

with \(L\) unit lower triangular, \(U\) upper triangular, and no row interchange. The diagonal entry \(u_{33}\) is ____.

---

## Q8 — MCQ

A fixed invertible \(n \times n\) matrix \(A\) must be used to solve \(Ax = b\) for many different right-hand sides \(b\). Which statement matches the cost of LU factorization?

(A) Factor \(A = LU\) once, at cubic cost, and then each new \(b\) costs only a forward and a back substitution

(B) Every new \(b\) requires a fresh LU factorization of \(A\)

(C) The factorization itself costs the same as one substitution, namely quadratic in \(n\)

(D) LU factorization can be used for only one right-hand side

---

## Level 4 — Tricky / Trap-Based

## Q9 — NAT

Using the factorization of

$$
A = \begin{bmatrix} 1 & 2 & 1 \\ 2 & 5 & 3 \\ 3 & 7 & 6 \end{bmatrix}
$$

from Q7, solve \(Ax = b\) for

$$
b = \begin{bmatrix} 3 \\ 8 \\ 13 \end{bmatrix}.
$$

The value of \(x_2 + x_3\) is ____.

---

## Q10 — MSQ

Select all that apply to the standard factorization discussed in this topic.

(A) Multipliers used to clear entries below a pivot are stored in \(L\)

(B) In this standard factorization, the diagonal entries of \(L\) are the pivots

(C) If a permutation matrix \(P\) is required and \(PA = LU\), forward substitution is applied to \(Pb\)

(D) When no row interchange is used, \(\det(A)\) equals the product of the diagonal entries of \(U\)

---

## Level 5 — Challenge

## Q11 — MSQ

Let

$$
M = \begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 7 \\ 1 & 1 & 1 \end{bmatrix}.
$$

Select all that apply.

(A) \(\det(M) = 0\)

(B) The leading principal minor of order \(2\) is \(0\)

(C) \(M\) has a factorization \(M = LU\) with \(L\) unit lower triangular and with no row interchange

(D) \(M\) is invertible

---

## Q12 — NAT

Let

$$
A = \begin{bmatrix} 2 & 1 & 0 \\ 4 & 3 & 1 \\ 2 & 2 & 2 \end{bmatrix}, \quad
b = \begin{bmatrix} 4 \\ 10 \\ 8 \end{bmatrix}.
$$

Solve \(Ax = b\) by an LU factorization with no row interchange. The value of \(x_1 + x_3\) is ____.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 2 |
| 3 | MCQ | B |
| 4 | NAT | 9 |
| 5 | MCQ | B |
| 6 | NAT | 2 |
| 7 | NAT | 2 |
| 8 | MCQ | A |
| 9 | NAT | 2 |
| 10 | MSQ | A, C, D |
| 11 | MSQ | B, D |
| 12 | NAT | 4 |

## Detailed Solutions

### Q1

Answer: A

In the Doolittle form used here, \(L\) is unit lower triangular: every diagonal entry equals \(1\), and the entries below the diagonal are the elimination multipliers. The pivots sit on the diagonal of \(U\).

### Q2

Answer: 2

The only multiplier is

$$
\ell_{21} = \frac{a_{21}}{a_{11}} = \frac{6}{3} = 2.
$$

Row 2 minus \(2\) times row 1 is \((0,\ 5 - 2) = (0,\ 3)\). Therefore

$$
L = \begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}, \qquad
U = \begin{bmatrix} 3 & 1 \\ 0 & 3 \end{bmatrix}.
$$

Check:

$$
LU = \begin{bmatrix} 3 & 1 \\ 6 & 2 + 3 \end{bmatrix} = \begin{bmatrix} 3 & 1 \\ 6 & 5 \end{bmatrix} = A.
$$

### Q3

Answer: B

From \(A = LU\), the equation \(LUx = b\) splits into a unit lower-triangular system followed by an upper-triangular system:

$$
Ly = b, \qquad Ux = y.
$$

Forward substitution produces \(y\); back substitution produces \(x\).

### Q4

Answer: 9

From Q2, the diagonal of \(U\) is \(3, 3\). Since \(L\) has unit diagonal, \(\det(L) = 1\), and no row was swapped, so

$$
\det(A) = \det(U) = 3 \cdot 3 = 9.
$$

Directly, \(\det(A) = 3\cdot 5 - 1\cdot 6 = 9\).

### Q5

Answer: B

The \((1, 1)\) entry is \(0\), so elimination cannot form a multiplier \(\ell_{21} = a_{21}/a_{11}\). An LU factorization with no row interchange does not exist. A row interchange gives a factorization of the form \(PA = LU\).

The matrix is not singular:

$$
\det(A) = 0\cdot 3 - 2\cdot 1 = -2 \neq 0.
$$

The standard \(L\) still has ones on its diagonal after pivoting; the pivots belong to \(U\).

### Q6

Answer: 2

Use \(L\) and \(U\) from Q2. Forward substitution \(Ly = b\):

$$
y_1 = 4, \qquad 2y_1 + y_2 = 11 \implies y_2 = 11 - 8 = 3.
$$

Back substitution \(Ux = y\):

$$
3x_2 = 3 \implies x_2 = 1,
$$

$$
3x_1 + x_2 = 4 \implies 3x_1 + 1 = 4 \implies x_1 = 1.
$$

Hence \(x_1 + x_2 = 2\). Check: \(A\begin{bmatrix} 1 \\ 1 \end{bmatrix} = \begin{bmatrix} 4 \\ 11 \end{bmatrix}\).

### Q7

Answer: 2

Column 1 has pivot \(1\). The multipliers are \(\ell_{21} = 2/1 = 2\) and \(\ell_{31} = 3/1 = 3\).

Row 2 minus \(2\) times row 1: \((0,\ 5 - 4,\ 3 - 2) = (0,\ 1,\ 1)\).

Row 3 minus \(3\) times row 1: \((0,\ 7 - 6,\ 6 - 3) = (0,\ 1,\ 3)\).

The matrix is now

$$
\begin{bmatrix} 1 & 2 & 1 \\ 0 & 1 & 1 \\ 0 & 1 & 3 \end{bmatrix}.
$$

Column 2 has pivot \(1\), so \(\ell_{32} = 1/1 = 1\). Row 3 minus row 2 is \((0,\ 0,\ 2)\). Therefore

$$
L = \begin{bmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ 3 & 1 & 1 \end{bmatrix}, \qquad
U = \begin{bmatrix} 1 & 2 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 2 \end{bmatrix}.
$$

The entry \(u_{33}\) is \(2\). Also

$$
LU = \begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 + 1 & 2 + 1 \\ 3 & 6 + 1 & 3 + 1 + 2 \end{bmatrix}
= \begin{bmatrix} 1 & 2 & 1 \\ 2 & 5 & 3 \\ 3 & 7 & 6 \end{bmatrix} = A.
$$

The leading principal minors are \(1\), \(\det\begin{bmatrix} 1 & 2 \\ 2 & 5 \end{bmatrix} = 1\), and \(\det(A) = 1\cdot 1\cdot 2 = 2\), all nonzero, which is why this factorization needs no row swap.

### Q8

Answer: A

Gaussian elimination, stored as \(A = LU\), is done once. Each later right-hand side needs only forward substitution with \(L\) and back substitution with \(U\). The factorization dominates and is cubic in \(n\); each substitution is quadratic in \(n\).

### Q9

Answer: 2

Use \(L\) and \(U\) from Q7. Forward substitution \(Ly = b\):

$$
y_1 = 3,
$$

$$
2y_1 + y_2 = 8 \implies y_2 = 8 - 6 = 2,
$$

$$
3y_1 + y_2 + y_3 = 13 \implies 9 + 2 + y_3 = 13 \implies y_3 = 2.
$$

Back substitution \(Ux = y\):

$$
2x_3 = 2 \implies x_3 = 1,
$$

$$
x_2 + x_3 = 2 \implies x_2 = 1,
$$

$$
x_1 + 2x_2 + x_3 = 3 \implies x_1 + 2 + 1 = 3 \implies x_1 = 0.
$$

Thus \(x_2 + x_3 = 2\). Check:

$$
A\begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}
= \begin{bmatrix} 3 \\ 8 \\ 13 \end{bmatrix}.
$$

### Q10

Answer: A, C, D

(A) is the bookkeeping rule: the multiplier that clears position \((i, k)\) is stored as \(\ell_{ik}\).

(B) is the trap. This standard \(L\) has ones on the diagonal. The pivots are the diagonal entries of \(U\).

(C) If \(PA = LU\), then \(Ax = b\) is equivalent to \(LUx = Pb\). Forward substitution therefore uses \(Pb\), not the original \(b\).

(D) Then \(\det(L) = 1\) and there is no sign from a permutation, so \(\det(A) = \prod_i u_{ii}\). A row interchange would multiply this product by the sign of the permutation.

### Q11

Answer: B, D

The leading principal minor of order \(1\) is \(1 \neq 0\). The leading principal minor of order \(2\) is

$$
\det\begin{bmatrix} 1 & 2 \\ 2 & 4 \end{bmatrix} = 4 - 4 = 0.
$$

Attempt elimination. Row 2 minus \(2\) times row 1 is \((0,\ 0,\ 1)\), and row 3 minus row 1 is \((0,\ -1,\ -2)\):

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & 0 & 1 \\ 0 & -1 & -2 \end{bmatrix}.
$$

The prospective second pivot is \(0\), so there is no LU factorization with unit lower-triangular \(L\) and no row interchange.

These two row operations do not change the determinant. Swap the current row 2 and row 3, which changes the sign:

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & -1 & -2 \\ 0 & 0 & 1 \end{bmatrix}.
$$

The triangular determinant is \(1\cdot(-1)\cdot 1 = -1\). Accounting for the swap,

$$
\det(M) = -(-1) = 1 \neq 0.
$$

So \(M\) is invertible. A zero leading minor blocks this LU form; it does not by itself make the matrix singular.

### Q12

Answer: 4

Column 1 has pivot \(2\). The multipliers are \(\ell_{21} = 4/2 = 2\) and \(\ell_{31} = 2/2 = 1\).

Row 2 minus \(2\) times row 1: \((0,\ 3 - 2,\ 1 - 0) = (0,\ 1,\ 1)\).

Row 3 minus row 1: \((0,\ 2 - 1,\ 2 - 0) = (0,\ 1,\ 2)\).

The second pivot is \(1\), so \(\ell_{32} = 1\). Row 3 minus that new row 2 is \((0,\ 0,\ 1)\). Hence

$$
L = \begin{bmatrix} 1 & 0 & 0 \\ 2 & 1 & 0 \\ 1 & 1 & 1 \end{bmatrix}, \qquad
U = \begin{bmatrix} 2 & 1 & 0 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{bmatrix}.
$$

Check the third row of \(LU\): row 3 of \(L\) times the columns of \(U\) gives

$$
(2,\ 1 + 1,\ 1 + 1) = (2,\ 2,\ 2),
$$

and the other rows likewise recover \(A\). Also \(\det(A) = 2\cdot 1\cdot 1 = 2\).

Forward substitution \(Ly = b\):

$$
y_1 = 4,
$$

$$
2\cdot 4 + y_2 = 10 \implies y_2 = 2,
$$

$$
4 + 2 + y_3 = 8 \implies y_3 = 2.
$$

Back substitution \(Ux = y\):

$$
x_3 = 2,
$$

$$
x_2 + x_3 = 2 \implies x_2 = 0,
$$

$$
2x_1 + x_2 = 4 \implies x_1 = 2.
$$

Therefore \(x_1 + x_3 = 2 + 2 = 4\). Check:

$$
A\begin{bmatrix} 2 \\ 0 \\ 2 \end{bmatrix}
= \begin{bmatrix} 4 \\ 8 + 2 \\ 4 + 4 \end{bmatrix}
= \begin{bmatrix} 4 \\ 10 \\ 8 \end{bmatrix}.
$$

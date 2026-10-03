# Determinants — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — NAT

The determinant of \(\begin{bmatrix} 6 & 1 \\ 2 & 1 \end{bmatrix}\) is ____.

---

## Q2 — MCQ

The determinant of

$$
\begin{bmatrix} 2 & 9 & -1 \\ 0 & 3 & 4 \\ 0 & 0 & -2 \end{bmatrix}
$$

is

(A) \(-12\)

(B) \(12\)

(C) \(-7\)

(D) \(3\)

---

## Q3 — MCQ

Let \(A\) be a square matrix with \(\det(A) = 7\). The matrix \(B\) is obtained from \(A\) by swapping two rows. Then \(\det(B)\) equals

(A) \(7\)

(B) \(-7\)

(C) \(0\)

(D) \(49\)

---

## Q4 — NAT

The determinant of

$$
\begin{bmatrix} 4 & 1 & 2 \\ 0 & -2 & 5 \\ 0 & 0 & 3 \end{bmatrix}
$$

is ____.

---

## Level 2 — Standard GATE Style

## Q5 — MSQ

Let \(A\) and \(B\) be square matrices of the same order. Where an inverse is written, assume it exists. Select all that apply.

(A) \(\det(A^{T}) = \det(A)\)

(B) \(\det(AB) = \det(A)\det(B)\)

(C) \(\det(A + B) = \det(A) + \det(B)\)

(D) \(\det(A^{-1}) = 1/\det(A)\)

---

## Q6 — NAT

Let \(A\) be a \(3 \times 3\) matrix with \(\det(A) = 3\). The value of \(\det(2A)\) is ____.

---

## Q7 — MCQ

Which of the following matrices is singular?

(A) \(\begin{bmatrix} 2 & 0 \\ 0 & 3 \end{bmatrix}\)

(B) \(\begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 2 \end{bmatrix}\)

(C) \(\begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 3 & 1 & 0 \end{bmatrix}\)

(D) \(\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}\)

---

## Q8 — NAT

The determinant of

$$
\begin{bmatrix} 2 & 0 & 1 \\ 3 & 0 & 4 \\ 1 & 5 & 2 \end{bmatrix}
$$

is ____.

---

## Level 3 — Multi-Step

## Q9 — NAT

The system

$$
x + 2y = 5, \qquad 3x + y = 5
$$

has a unique solution. The value of \(y\) is ____.

---

## Q10 — MCQ

The area of the parallelogram in the plane spanned by the vectors \((4, 1)\) and \((2, 3)\) is

(A) \(10\)

(B) \(14\)

(C) \(5\)

(D) \(0\)

---

## Q11 — NAT

The determinant of

$$
\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 10 \end{bmatrix}
$$

is ____.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MSQ

Let \(A\) be a \(3 \times 3\) matrix with \(\det(A) = 6\). Select all that apply.

(A) Replacing row 2 by row 2 plus \(5\) times row 1 does not change the determinant

(B) Multiplying row 3 by \(-2\) multiplies the determinant by \(-2\)

(C) Interchanging row 1 and row 2 multiplies the determinant by \(-1\)

(D) Replacing \(A\) by \(2A\) multiplies the determinant by \(2\)

---

## Q13 — NAT

The determinant of

$$
\begin{bmatrix} 3 & 1 & 4 \\ 0 & 2 & 5 \\ 0 & 1 & 3 \end{bmatrix}
$$

is ____.

---

## Q14 — MCQ

Let

$$
A = \begin{bmatrix} 2 & 0 \\ 0 & 1 \end{bmatrix}, \quad
B = \begin{bmatrix} 1 & 0 \\ 0 & 3 \end{bmatrix}.
$$

Which one of the following is correct?

(A) \(\det(A + B) = \det(A) + \det(B)\)

(B) \(\det(A + B) = 12\) and \(\det(A) + \det(B) = 5\)

(C) \(\det(AB) = 5\)

(D) \(\det(A + B) = \det(A)\det(B)\)

---

## Level 5 — Challenge

## Q15 — NAT

Let \(A\) be a \(3 \times 3\) matrix with \(\det(A) = -2\). The value of \(\det(2A^{-1})\) is ____.

---

## Q16 — MSQ

Let \(A\) be a \(3 \times 3\) invertible matrix with \(\det(A) = 2\). Select all that apply.

(A) \(\det(A^{-1}) = 1/2\)

(B) \(\det(A^{T}A) = 4\)

(C) \(\det(-A) = -2\)

(D) \(\det(2A) = 4\)

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 4 |
| 2 | MCQ | A |
| 3 | MCQ | B |
| 4 | NAT | -24 |
| 5 | MSQ | A, B, D |
| 6 | NAT | 24 |
| 7 | MCQ | C |
| 8 | NAT | -25 |
| 9 | NAT | 2 |
| 10 | MCQ | A |
| 11 | NAT | -3 |
| 12 | MSQ | A, B, C |
| 13 | NAT | 3 |
| 14 | MCQ | B |
| 15 | NAT | -4 |
| 16 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: 4

$$
\det\begin{bmatrix} 6 & 1 \\ 2 & 1 \end{bmatrix} = 6\cdot 1 - 1\cdot 2 = 4.
$$

### Q2

Answer: A

The matrix is upper triangular, so the determinant is the product of the diagonal entries:

$$
2 \cdot 3 \cdot (-2) = -12.
$$

### Q3

Answer: B

Swapping two rows multiplies the determinant by \(-1\). Therefore \(\det(B) = -7\).

### Q4

Answer: -24

The matrix is upper triangular:

$$
\det = 4 \cdot (-2) \cdot 3 = -24.
$$

### Q5

Answer: A, B, D

(A), (B), and (D) are standard identities. For (D), \(AA^{-1} = I\) gives \(\det(A)\det(A^{-1}) = \det(I) = 1\).

(C) is false. Take \(A = \begin{bmatrix} 2 & 0 \\ 0 & 1 \end{bmatrix}\) and \(B = \begin{bmatrix} 1 & 0 \\ 0 & 3 \end{bmatrix}\). Then \(\det(A) + \det(B) = 2 + 3 = 5\), while

$$
A + B = \begin{bmatrix} 3 & 0 \\ 0 & 4 \end{bmatrix}, \qquad \det(A + B) = 12.
$$

### Q6

Answer: 24

For an \(n \times n\) matrix, \(\det(kA) = k^{n}\det(A)\). Here \(n = 3\) and \(k = 2\):

$$
\det(2A) = 2^{3} \cdot 3 = 24.
$$

### Q7

Answer: C

(A) \(\det = 6 \neq 0\).

(B) The matrix is upper triangular with diagonal \(1, 1, 2\), so \(\det = 2 \neq 0\).

(C) Row 2 equals \(2\) times row 1, so the determinant is \(0\). The matrix is singular.

(D) \(\det = 1 \neq 0\).

### Q8

Answer: -25

Column 2 has a single nonzero entry, \(a_{32} = 5\). The cofactor sign is \((-1)^{3+2} = -1\), and the corresponding minor is

$$
\det\begin{bmatrix} 2 & 1 \\ 3 & 4 \end{bmatrix} = 8 - 3 = 5.
$$

$$
\det = 5 \cdot (-1) \cdot 5 = -25.
$$

The same value comes from the first-row expansion:

$$
2\big(0\cdot 2 - 4\cdot 5\big) - 0 + 1\big(3\cdot 5 - 0\cdot 1\big) = 2(-20) + 15 = -25.
$$

### Q9

Answer: 2

$$
\det\begin{bmatrix} 1 & 2 \\ 3 & 1 \end{bmatrix} = 1 - 6 = -5 \neq 0,
$$

so Cramer's rule applies. Replace the second column by the right-hand side:

$$
\det\begin{bmatrix} 1 & 5 \\ 3 & 5 \end{bmatrix} = 5 - 15 = -10.
$$

$$
y = \frac{-10}{-5} = 2.
$$

The companion value is

$$
x = \frac{\det\begin{bmatrix} 5 & 2 \\ 5 & 1 \end{bmatrix}}{-5} = \frac{5 - 10}{-5} = 1.
$$

Check: \(1 + 2\cdot 2 = 5\) and \(3\cdot 1 + 2 = 5\).

### Q10

Answer: A

The absolute value of the determinant is the area of the parallelogram:

$$
\det\begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix} = 12 - 2 = 10.
$$

(The columns may be written in either order; the sign may change, the absolute value does not.) The area is \(10\).

### Q11

Answer: -3

Start with

$$
\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 10 \end{bmatrix}.
$$

Replace row 2 by row 2 minus \(4\) times row 1, and row 3 by row 3 minus \(7\) times row 1. These operations do not change the determinant:

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & -3 & -6 \\ 0 & -6 & -11 \end{bmatrix}.
$$

Replace row 3 by row 3 minus \(2\) times row 2:

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & -3 & -6 \\ 0 & 0 & 1 \end{bmatrix}.
$$

The matrix is now upper triangular, so

$$
\det = 1 \cdot (-3) \cdot 1 = -3.
$$

### Q12

Answer: A, B, C

Adding a multiple of one row to another row does not change the determinant, so (A) holds. Scaling one row by \(k\) multiplies the determinant by \(k\), so (B) holds. A single row swap multiplies the determinant by \(-1\), so (C) holds.

(D) is the trap. Replacing \(A\) by \(2A\) scales all three rows by \(2\), so

$$
\det(2A) = 2^{3}\det(A) = 8 \cdot 6 = 48,
$$

which is not \(2 \cdot 6\).

### Q13

Answer: 3

The matrix is block upper triangular, with blocks \([3]\) and \(\begin{bmatrix} 2 & 5 \\ 1 & 3 \end{bmatrix}\). Therefore

$$
\det = 3 \cdot \det\begin{bmatrix} 2 & 5 \\ 1 & 3 \end{bmatrix} = 3(6 - 5) = 3.
$$

Expanding along the first column gives the same result, because the only nonzero entry in that column is \(3\):

$$
3 \cdot \det\begin{bmatrix} 2 & 5 \\ 1 & 3 \end{bmatrix} = 3.
$$

### Q14

Answer: B

$$
\det(A) = 2, \qquad \det(B) = 3, \qquad \det(A) + \det(B) = 5.
$$

$$
A + B = \begin{bmatrix} 3 & 0 \\ 0 & 4 \end{bmatrix}, \qquad \det(A + B) = 12.
$$

$$
\det(AB) = \det(A)\det(B) = 6,
$$

and \(\det(A)\det(B) = 6 \neq 12\). So only (B) is correct. In particular \(\det(A + B)\) is not \(\det(A) + \det(B)\).

### Q15

Answer: -4

For a \(3 \times 3\) matrix,

$$
\det(2A^{-1}) = 2^{3} \det(A^{-1}) = 8 \cdot \frac{1}{\det(A)} = 8 \cdot \frac{1}{-2} = -4.
$$

### Q16

Answer: A, B, C

(A) \(\det(A^{-1}) = 1/\det(A) = 1/2\).

(B) \(\det(A^{T}A) = \det(A^{T})\det(A) = \det(A)^{2} = 4\).

(C) \(\det(-A) = (-1)^{3}\det(A) = -2\), because the order is odd.

(D) \(\det(2A) = 2^{3}\det(A) = 16\), not \(4\). The value \(4\) is \(\det(A) + \det(A)\), which is a different quantity.

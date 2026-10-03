# Eigenvalues and Eigenvectors — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — NAT

The larger eigenvalue of

$$
\begin{bmatrix} 5 & 2 \\ 1 & 4 \end{bmatrix}
$$

is ____.

---

## Q2 — MCQ

For a square matrix \(A\), the number \(0\) is an eigenvalue of \(A\) if and only if

(A) \(A\) is invertible

(B) \(\det(A) = 0\)

(C) \(\operatorname{tr}(A) = 0\)

(D) \(A\) is symmetric

---

## Q3 — NAT

The sum of the eigenvalues of

$$
\begin{bmatrix} 2 & 5 & 1 \\ 0 & -3 & 4 \\ 0 & 0 & 7 \end{bmatrix}
$$

is ____.

---

## Q4 — MCQ

Eigenvectors corresponding to distinct eigenvalues of a square matrix are

(A) linearly independent

(B) always orthogonal, whether or not the matrix is symmetric

(C) necessarily the zero vector

(D) necessarily equal

---

## Q5 — NAT

The product of the eigenvalues of

$$
\begin{bmatrix} 2 & 1 & 0 \\ 0 & 3 & 4 \\ 0 & 0 & 1 \end{bmatrix}
$$

is ____.

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

The eigenvalues of

$$
\begin{bmatrix} 6 & 2 \\ 2 & 3 \end{bmatrix}
$$

are

(A) \(7\) and \(2\)

(B) \(6\) and \(3\)

(C) \(4\) and \(5\)

(D) \(8\) and \(1\)

---

## Q7 — NAT

For the matrix in Q6, one eigenvector belonging to the eigenvalue \(7\) has the form \(\begin{bmatrix} 2 \\ k \end{bmatrix}\). The value of \(k\) is ____.

---

## Q8 — MSQ

Let \(A\) be a real symmetric matrix. Select all that apply.

(A) Every eigenvalue of \(A\) is real

(B) Eigenvectors belonging to distinct eigenvalues are orthogonal

(C) \(A\) is singular

(D) \(A\) is orthogonally diagonalizable

---

## Q9 — NAT

Let

$$
A = \begin{bmatrix} 2 & 3 \\ 0 & 5 \end{bmatrix}.
$$

The sum of the eigenvalues of \(A^{2}\) is ____.

---

## Q10 — MCQ

The eigenvalues of the inverse of

$$
\begin{bmatrix} 6 & 2 \\ 2 & 3 \end{bmatrix}
$$

are

(A) \(7\) and \(2\)

(B) \(1/7\) and \(1/2\)

(C) \(-7\) and \(-2\)

(D) \(1/7\) and \(2\)

---

## Q11 — NAT

Let

$$
A = \begin{bmatrix} 2 & 3 \\ 0 & 5 \end{bmatrix}.
$$

The value of \(\det(A - 4I)\) is ____.

---

## Level 3 — Multi-Step

## Q12 — MCQ

Let

$$
A = \begin{bmatrix} 5 & 1 \\ 0 & 5 \end{bmatrix}.
$$

Which one of the following is correct?

(A) \(A\) is diagonalizable

(B) \(A\) is not diagonalizable

(C) \(0\) is an eigenvalue of \(A\)

(D) \(\operatorname{tr}(A) = 5\)

---

## Q13 — MSQ

Let

$$
A = \begin{bmatrix} 2 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 5 \end{bmatrix}.
$$

Select all that apply.

(A) \(\operatorname{tr}(A) = 9\)

(B) \(\det(A) = 20\)

(C) \(0\) is an eigenvalue of \(A\)

(D) The eigenvalue \(2\) has algebraic multiplicity \(2\)

---

## Q14 — NAT

Let

$$
A = \begin{bmatrix} 3 & 1 \\ 2 & 2 \end{bmatrix}.
$$

One eigenvector belonging to the eigenvalue \(1\) has the form \(\begin{bmatrix} 1 \\ k \end{bmatrix}\). The value of \(k\) is ____.

---

## Q15 — NAT

Let

$$
B = \begin{bmatrix} 1 & 2 \\ 0 & 4 \end{bmatrix}.
$$

The sum of the eigenvalues of \(2B\) is ____.

---

## Q16 — NAT

The symmetric matrix

$$
\begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}
$$

has eigenvalues \(9\) and \(1\). An eigenvector for eigenvalue \(1\) has the form \(\begin{bmatrix} 1 \\ k \end{bmatrix}\). The value of \(k\) is ____.

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

The product of the eigenvalues of

$$
\begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix}
$$

is

(A) \(7\)

(B) \(10\)

(C) \(5\)

(D) \(4\)

---

## Q18 — MSQ

Let

$$
A = \begin{bmatrix} 3 & 1 \\ 0 & 3 \end{bmatrix}.
$$

Select all that apply.

(A) The algebraic multiplicity of the eigenvalue \(3\) is \(2\)

(B) The geometric multiplicity of the eigenvalue \(3\) is \(2\)

(C) The geometric multiplicity of the eigenvalue \(3\) is \(1\)

(D) \(A\) is diagonalizable

---

## Q19 — NAT

Let

$$
A = \begin{bmatrix} 2 & 4 & 1 \\ 0 & -1 & 5 \\ 0 & 0 & 3 \end{bmatrix}.
$$

The value of \(\det(A + I)\) is ____.

---

## Level 5 — Challenge

## Q20 — NAT

Let

$$
A = \begin{bmatrix} 3 & 1 \\ 2 & 2 \end{bmatrix}.
$$

The \((1, 1)\) entry of \(A^{2}\) is ____.

---

## Q21 — MSQ

Let

$$
A = \begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix}.
$$

Select all that apply.

(A) The eigenvalues of \(A^{2}\) are \(25\) and \(4\)

(B) The eigenvalues of \(A^{-1}\) are \(1/5\) and \(1/2\)

(C) \(\det(A) = 7\)

(D) Eigenvectors belonging to the two eigenvalues are linearly independent

---

## Q22 — NAT

Let

$$
A = \begin{bmatrix} 2 & 1 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 6 \end{bmatrix}.
$$

The geometric multiplicity of the eigenvalue \(2\) is ____.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 6 |
| 2 | MCQ | B |
| 3 | NAT | 6 |
| 4 | MCQ | A |
| 5 | NAT | 6 |
| 6 | MCQ | A |
| 7 | NAT | 1 |
| 8 | MSQ | A, B, D |
| 9 | NAT | 29 |
| 10 | MCQ | B |
| 11 | NAT | -2 |
| 12 | MCQ | B |
| 13 | MSQ | A, B, D |
| 14 | NAT | -2 |
| 15 | NAT | 10 |
| 16 | NAT | -1 |
| 17 | MCQ | B |
| 18 | MSQ | A, C |
| 19 | NAT | 0 |
| 20 | NAT | 11 |
| 21 | MSQ | A, B, D |
| 22 | NAT | 1 |

## Detailed Solutions

### Q1

Answer: 6

$$
\det(A - \lambda I) = (5 - \lambda)(4 - \lambda) - 2 = \lambda^{2} - 9\lambda + 18 = (\lambda - 6)(\lambda - 3).
$$

The eigenvalues are \(6\) and \(3\). The larger one is \(6\).

Check against the trace and determinant: \(6 + 3 = 9 = \operatorname{tr}(A)\) and \(6 \cdot 3 = 18 = \det(A)\).

### Q2

Answer: B

The number \(0\) is an eigenvalue if and only if \(Av = 0\) for some \(v \neq 0\), which is exactly the condition that \(A\) is singular: \(\det(A) = 0\). An invertible matrix cannot have \(0\) as an eigenvalue. A zero trace, or symmetry, does not force a zero eigenvalue.

### Q3

Answer: 6

The matrix is upper triangular, so its eigenvalues are the diagonal entries \(2\), \(-3\), and \(7\). Their sum is

$$
2 + (-3) + 7 = 6,
$$

which is also the trace.

### Q4

Answer: A

Eigenvectors belonging to distinct eigenvalues are linearly independent. They are orthogonal when the matrix is real and symmetric; orthogonality is not guaranteed for a general matrix. An eigenvector is nonzero by definition, so (C) and (D) fail.

### Q5

Answer: 6

The matrix is upper triangular. The product of the eigenvalues equals the product of the diagonal entries, and also equals the determinant:

$$
2 \cdot 3 \cdot 1 = 6.
$$

### Q6

Answer: A

$$
\det\begin{bmatrix} 6 - \lambda & 2 \\ 2 & 3 - \lambda \end{bmatrix}
= (6 - \lambda)(3 - \lambda) - 4
= \lambda^{2} - 9\lambda + 14
= (\lambda - 7)(\lambda - 2).
$$

The eigenvalues are \(7\) and \(2\). Their sum is the trace \(9\), and their product is the determinant \(18 - 4 = 14\).

### Q7

Answer: 1

$$
A - 7I = \begin{bmatrix} -1 & 2 \\ 2 & -4 \end{bmatrix}.
$$

The second row is \(-2\) times the first, so the system is \(-x + 2y = 0\), or \(x = 2y\). Taking \(x = 2\) gives \(y = 1\). Thus \(k = 1\), and \(\begin{bmatrix} 2 \\ 1 \end{bmatrix}\) is an eigenvector:

$$
\begin{bmatrix} 6 & 2 \\ 2 & 3 \end{bmatrix}
\begin{bmatrix} 2 \\ 1 \end{bmatrix}
= \begin{bmatrix} 14 \\ 7 \end{bmatrix}
= 7\begin{bmatrix} 2 \\ 1 \end{bmatrix}.
$$

### Q8

Answer: A, B, D

A real symmetric matrix has only real eigenvalues, eigenvectors for distinct eigenvalues may be taken orthogonal, and the matrix is orthogonally diagonalizable.

(C) is not always true. The identity matrix is symmetric and invertible.

### Q9

Answer: 29

The matrix is upper triangular, so its eigenvalues are \(2\) and \(5\). The eigenvalues of \(A^{2}\) are \(2^{2} = 4\) and \(5^{2} = 25\). Their sum is \(29\).

Directly,

$$
A^{2} = \begin{bmatrix} 2 & 3 \\ 0 & 5 \end{bmatrix}
\begin{bmatrix} 2 & 3 \\ 0 & 5 \end{bmatrix}
= \begin{bmatrix} 4 & 21 \\ 0 & 25 \end{bmatrix},
$$

and \(\operatorname{tr}(A^{2}) = 4 + 25 = 29\).

### Q10

Answer: B

From Q6, the eigenvalues are \(7\) and \(2\), neither of which is \(0\), so the matrix is invertible. If \(Av = \lambda v\) with \(v \neq 0\) and \(\lambda \neq 0\), then

$$
A^{-1}v = \frac{1}{\lambda}v.
$$

The eigenvalues of the inverse are \(1/7\) and \(1/2\).

### Q11

Answer: -2

The eigenvalues of \(A\) are \(2\) and \(5\), so the eigenvalues of \(A - 4I\) are \(2 - 4 = -2\) and \(5 - 4 = 1\). Their product is

$$
\det(A - 4I) = (-2)(1) = -2.
$$

Directly,

$$
A - 4I = \begin{bmatrix} -2 & 3 \\ 0 & 1 \end{bmatrix}, \qquad \det(A - 4I) = -2.
$$

### Q12

Answer: B

The characteristic polynomial is \((5 - \lambda)^{2}\), so \(\lambda = 5\) is the only eigenvalue and its algebraic multiplicity is \(2\). Also \(\operatorname{tr}(A) = 10\) and \(\det(A) = 25 \neq 0\), so \(0\) is not an eigenvalue.

$$
A - 5I = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}
$$

has rank \(1\). The geometric multiplicity is

$$
2 - \operatorname{rank}(A - 5I) = 1,
$$

which is strictly smaller than the algebraic multiplicity. A full set of linearly independent eigenvectors does not exist, so \(A\) is not diagonalizable.

### Q13

Answer: A, B, D

The matrix is diagonal, so the eigenvalues are the diagonal entries \(2\), \(2\), and \(5\).

$$
\operatorname{tr}(A) = 2 + 2 + 5 = 9, \qquad \det(A) = 2 \cdot 2 \cdot 5 = 20.
$$

The factor \((\lambda - 2)\) appears twice, so the algebraic multiplicity of \(2\) is \(2\). The product of the eigenvalues is \(20 \neq 0\), so \(0\) is not an eigenvalue.

### Q14

Answer: -2

First confirm the eigenvalue. The characteristic polynomial is

$$
(3 - \lambda)(2 - \lambda) - 2 = \lambda^{2} - 5\lambda + 4 = (\lambda - 4)(\lambda - 1).
$$

So \(1\) is an eigenvalue. Then

$$
A - I = \begin{bmatrix} 2 & 1 \\ 2 & 1 \end{bmatrix},
$$

and \(2x + y = 0\). With \(x = 1\), one gets \(y = -2\). Check:

$$
\begin{bmatrix} 3 & 1 \\ 2 & 2 \end{bmatrix}
\begin{bmatrix} 1 \\ -2 \end{bmatrix}
= \begin{bmatrix} 1 \\ -2 \end{bmatrix}.
$$

### Q15

Answer: 10

\(B\) is upper triangular with eigenvalues \(1\) and \(4\). The eigenvalues of \(2B\) are \(2\cdot 1 = 2\) and \(2\cdot 4 = 8\). Their sum is \(10\), which is also

$$
\operatorname{tr}(2B) = 2\operatorname{tr}(B) = 2(1 + 4) = 10.
$$

### Q16

Answer: -1

The eigenvalues were given; they match the characteristic polynomial

$$
(5 - \lambda)^{2} - 16 = \lambda^{2} - 10\lambda + 9 = (\lambda - 9)(\lambda - 1).
$$

For \(\lambda = 1\),

$$
A - I = \begin{bmatrix} 4 & 4 \\ 4 & 4 \end{bmatrix},
$$

so \(4x + 4y = 0\), hence \(y = -x\). With \(x = 1\), one gets \(k = -1\).

The companion eigenvector for \(\lambda = 9\) is \(\begin{bmatrix} 1 \\ 1 \end{bmatrix}\), from \(A - 9I = \begin{bmatrix} -4 & 4 \\ 4 & -4 \end{bmatrix}\). Their dot product is \(1 + (-1) = 0\), as required for distinct eigenvalues of a real symmetric matrix. Check:

$$
\begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}
\begin{bmatrix} 1 \\ -1 \end{bmatrix}
= \begin{bmatrix} 1 \\ -1 \end{bmatrix}.
$$

### Q17

Answer: B

$$
\operatorname{tr}(A) = 7, \qquad \det(A) = 12 - 2 = 10.
$$

The product of the eigenvalues equals the determinant, so it is \(10\). The sum equals the trace, so \(7\) is the sum, not the product.

The characteristic polynomial is \(\lambda^{2} - 7\lambda + 10 = (\lambda - 5)(\lambda - 2)\). The eigenvalues are \(5\) and \(2\), and \(5 \cdot 2 = 10\).

### Q18

Answer: A, C

The characteristic polynomial is \((3 - \lambda)^{2}\), so the only eigenvalue is \(3\) and its algebraic multiplicity is \(2\).

$$
A - 3I = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}
$$

has rank \(1\), so the geometric multiplicity is \(2 - 1 = 1\). Geometric multiplicity is strictly smaller than algebraic multiplicity, so \(A\) is not diagonalizable.

### Q19

Answer: 0

\(A\) is upper triangular with diagonal entries \(2\), \(-1\), and \(3\). The eigenvalues of \(A + I\) are \(3\), \(0\), and \(4\). The product is \(0\), so

$$
\det(A + I) = 0.
$$

Directly,

$$
A + I = \begin{bmatrix} 3 & 4 & 1 \\ 0 & 0 & 5 \\ 0 & 0 & 4 \end{bmatrix}.
$$

Column operations are unnecessary: the second column of the lower-right \(2 \times 2\) block is a zero column after expansion along the first column pattern, or expand along the first column and use

$$
\det\begin{bmatrix} 0 & 5 \\ 0 & 4 \end{bmatrix} = 0.
$$

Note that \(\det(A) + 1 = 2\cdot(-1)\cdot 3 + 1 = -5\), which is not \(\det(A + I)\).

### Q20

Answer: 11

From Q14, the characteristic polynomial is \(\lambda^{2} - 5\lambda + 4\). Cayley–Hamilton says

$$
A^{2} - 5A + 4I = O, \qquad A^{2} = 5A - 4I.
$$

$$
5A - 4I = \begin{bmatrix} 15 & 5 \\ 10 & 10 \end{bmatrix} - \begin{bmatrix} 4 & 0 \\ 0 & 4 \end{bmatrix}
= \begin{bmatrix} 11 & 5 \\ 10 & 6 \end{bmatrix}.
$$

The \((1, 1)\) entry is \(11\). The same matrix is obtained by multiplying directly:

$$
A^{2} = \begin{bmatrix} 3 & 1 \\ 2 & 2 \end{bmatrix}
\begin{bmatrix} 3 & 1 \\ 2 & 2 \end{bmatrix}
= \begin{bmatrix} 9 + 2 & 3 + 2 \\ 6 + 4 & 2 + 4 \end{bmatrix}
= \begin{bmatrix} 11 & 5 \\ 10 & 6 \end{bmatrix}.
$$

The trace \(17\) equals \(4^{2} + 1^{2}\), the sum of the squares of the eigenvalues \(4\) and \(1\).

### Q21

Answer: A, B, D

From Q17, the eigenvalues are \(5\) and \(2\), and \(\det(A) = 10\). The trace is \(7\), so (C) confuses the trace with the determinant.

Eigenvalues of \(A^{2}\) are \(5^{2} = 25\) and \(2^{2} = 4\). Eigenvalues of \(A^{-1}\) are \(1/5\) and \(1/2\). The two eigenvalues are distinct, so any corresponding eigenvectors are linearly independent, and \(A\) is diagonalizable.

As a check of the square,

$$
A^{2} = \begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix}
\begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix}
= \begin{bmatrix} 18 & 14 \\ 7 & 11 \end{bmatrix}.
$$

Its trace is \(29 = 25 + 4\), and its determinant is \(18\cdot 11 - 14\cdot 7 = 198 - 98 = 100 = 25\cdot 4\).

### Q22

Answer: 1

The matrix is upper triangular, so the eigenvalues are \(2\), \(2\), and \(6\). The algebraic multiplicity of \(2\) is \(2\).

$$
A - 2I = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 4 \end{bmatrix}.
$$

The nonzero rows \((0, 1, 0)\) and \((0, 0, 4)\) are independent, so the rank is \(2\). The geometric multiplicity is

$$
3 - 2 = 1.
$$

The eigenspace is spanned by \(\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}\): the equations are \(y = 0\) and \(4z = 0\), with \(x\) free. Because the geometric multiplicity is smaller than the algebraic multiplicity, \(A\) is not diagonalizable.

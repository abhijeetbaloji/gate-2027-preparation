# System of Linear Equations — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

For a homogeneous system \(Ax = 0\), which one of the following is always true?

(A) The system has no solution

(B) The zero vector is the only solution, for every coefficient matrix \(A\)

(C) The zero vector is always a solution

(D) The system always has infinitely many solutions

---

## Q2 — NAT

The system

$$
3x + y = 7, \qquad x + y = 3
$$

has a unique solution. The value of \(x\) is ____.

---

## Q3 — MCQ

Let \(A\) be an \(m \times n\) coefficient matrix and \([A \mid b]\) the augmented matrix of \(Ax = b\). If

$$
\operatorname{rank}(A) = \operatorname{rank}([A \mid b]) = n,
$$

then the system has

(A) a unique solution

(B) infinitely many solutions

(C) no solution

(D) exactly two solutions

---

## Q4 — NAT

Consider the homogeneous system \(Ax = 0\) with

$$
A = \begin{bmatrix} 1 & 2 & 3 & 4 \\ 2 & 4 & 6 & 8 \end{bmatrix}.
$$

The number of free variables is ____.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

The system

$$
x + 2y = 3, \qquad 2x + 4y = 6
$$

has

(A) a unique solution

(B) infinitely many solutions

(C) no solution

(D) exactly two solutions

---

## Q6 — MCQ

The system

$$
x + 2y = 3, \qquad 2x + 4y = 7
$$

has

(A) a unique solution

(B) infinitely many solutions

(C) no solution

(D) exactly two solutions

---

## Q7 — NAT

The homogeneous system

$$
\begin{aligned}
x + y + z &= 0, \\
2x + 2y + 2z &= 0, \\
x - y &= 0
\end{aligned}
$$

has solution space of dimension ____.

---

## Q8 — MSQ

Let \(A\) be an \(n \times n\) real matrix. Select all statements that are equivalent to “\(Ax = b\) has a unique solution for every \(b \in \mathbb{R}^{n}\)”.

(A) \(\det(A) \neq 0\)

(B) \(\operatorname{rank}(A) = n\)

(C) \(Ax = 0\) has a nontrivial solution

(D) \(A\) is invertible

---

## Level 3 — Multi-Step

## Q9 — NAT

Consider

$$
x + 2y = 4, \qquad \lambda x + 6y = 10.
$$

The value of \(\lambda\) for which the system has no solution is ____.

---

## Q10 — MCQ

The system

$$
x + y + z = 1, \qquad 2x + 2y + 2z = 3
$$

has

(A) infinitely many solutions, because there are fewer equations than unknowns

(B) no solution

(C) a unique solution

(D) exactly three solutions

---

## Q11 — NAT

The system

$$
\begin{aligned}
x + y &= 3, \\
2x - y &= 0, \\
3x &= 3
\end{aligned}
$$

is consistent. The value of \(x\) is ____.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MSQ

Select all that apply.

(A) If a linear system has fewer equations than unknowns, then it has infinitely many solutions

(B) In a consistent system \(Ax = b\) with \(n\) unknowns, the number of free variables is \(n - \operatorname{rank}(A)\)

(C) If \(\operatorname{rank}(A) < \operatorname{rank}([A \mid b])\), then \(Ax = b\) has no solution

(D) Every homogeneous system \(Ax = 0\) is consistent

---

## Q13 — NAT

For the system

$$
\begin{aligned}
x + 2y + 3z &= 6, \\
2x + 4y + 6z &= 12, \\
x + y + z &= 3,
\end{aligned}
$$

the number of free variables is ____.

---

## Q14 — MCQ

Consider

$$
x + y = 2, \qquad 2x + 2y = 4.
$$

Which one of the following is correct?

(A) Cramer's rule produces the unique solution

(B) The coefficient determinant is \(0\), so the system has no solution

(C) The coefficient determinant is \(0\), and the system has infinitely many solutions

(D) The coefficient determinant is \(0\), and the system is inconsistent

---

## Level 5 — Challenge

## Q15 — NAT

The system

$$
\begin{aligned}
x + y + z &= 6, \\
2x - y + z &= 3, \\
x + 2y - z &= 2
\end{aligned}
$$

has a unique solution \((x, y, z)\). The value of \(x + z\) is ____.

---

## Q16 — MSQ

Let

$$
A = \begin{bmatrix} 1 & 2 & -1 \\ 2 & 4 & -2 \\ 3 & 6 & -3 \end{bmatrix}, \quad
b = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}.
$$

Select all that apply to \(Ax = b\).

(A) The system is inconsistent

(B) The system has infinitely many solutions

(C) The number of free variables is \(2\)

(D) The only solution is the zero vector

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | NAT | 2 |
| 3 | MCQ | A |
| 4 | NAT | 3 |
| 5 | MCQ | B |
| 6 | MCQ | C |
| 7 | NAT | 1 |
| 8 | MSQ | A, B, D |
| 9 | NAT | 3 |
| 10 | MCQ | B |
| 11 | NAT | 1 |
| 12 | MSQ | B, C, D |
| 13 | NAT | 1 |
| 14 | MCQ | C |
| 15 | NAT | 4 |
| 16 | MSQ | B, C |

## Detailed Solutions

### Q1

Answer: C

Substituting the zero vector gives \(A0 = 0\), so the zero vector is always a solution. It is the only solution precisely when \(\operatorname{rank}(A)\) equals the number of unknowns. If the rank is smaller, there are nontrivial solutions as well, hence infinitely many. A homogeneous system is never inconsistent.

### Q2

Answer: 2

Subtract the second equation from the first:

$$
(3x + y) - (x + y) = 7 - 3 \implies 2x = 4 \implies x = 2.
$$

Then \(2 + y = 3\), so \(y = 1\). Check: \(3\cdot 2 + 1 = 7\).

The coefficient determinant is \(3\cdot 1 - 1\cdot 1 = 2 \neq 0\), which confirms uniqueness.

### Q3

Answer: A

By the rank criterion: if \(\operatorname{rank}(A) = \operatorname{rank}([A \mid b]) = n\), every unknown is fixed by a pivot and the right-hand side introduces no contradiction. The solution is unique.

### Q4

Answer: 3

Row 2 equals \(2\) times row 1, and row 1 is nonzero, so \(\operatorname{rank}(A) = 1\). There are \(n = 4\) unknowns. The number of free variables in \(Ax = 0\) is the nullity

$$
n - \operatorname{rank}(A) = 4 - 1 = 3.
$$

### Q5

Answer: B

The augmented matrix is

$$
\begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \end{bmatrix}.
$$

Row 2 equals \(2\) times row 1, including the right-hand side \(6 = 2\cdot 3\). So

$$
\operatorname{rank}(A) = \operatorname{rank}([A \mid b]) = 1 < 2.
$$

The system is consistent with \(2 - 1 = 1\) free variable, hence infinitely many solutions: \(x + 2y = 3\).

### Q6

Answer: C

The augmented matrix is

$$
\begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 7 \end{bmatrix}.
$$

Replace row 2 by row 2 minus \(2\) times row 1:

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & 0 & 1 \end{bmatrix}.
$$

The last row says \(0 = 1\). Thus \(\operatorname{rank}(A) = 1\) and \(\operatorname{rank}([A \mid b]) = 2\). The system is inconsistent.

### Q7

Answer: 1

The coefficient matrix is

$$
\begin{bmatrix} 1 & 1 & 1 \\ 2 & 2 & 2 \\ 1 & -1 & 0 \end{bmatrix}.
$$

Row 2 minus \(2\) times row 1 is a zero row. Row 3 minus row 1 is \((0, -2, -1)\). The nonzero rows \((1, 1, 1)\) and \((0, -2, -1)\) are independent, so the rank is \(2\).

With \(n = 3\),

$$
\text{nullity} = 3 - 2 = 1.
$$

Explicitly, \(x = y\) and \(z = -2y\), with \(y\) free. The solution space is one-dimensional.

### Q8

Answer: A, B, D

For a square matrix, the following are equivalent: \(\det(A) \neq 0\), \(\operatorname{rank}(A) = n\), \(A\) is invertible, and \(Ax = b\) has a unique solution for every \(b\).

(C) is the opposite of uniqueness for the homogeneous system. A nontrivial solution of \(Ax = 0\) means \(\operatorname{rank}(A) < n\), so \(A\) is singular.

### Q9

Answer: 3

The coefficient determinant is

$$
\det\begin{bmatrix} 1 & 2 \\ \lambda & 6 \end{bmatrix} = 6 - 2\lambda = 2(3 - \lambda).
$$

If \(\lambda \neq 3\), the determinant is nonzero and the solution is unique.

If \(\lambda = 3\), the second equation is \(3x + 6y = 10\). Three times the first equation is \(3x + 6y = 12\). These cannot hold together, so the augmented rank is \(2\) while \(\operatorname{rank}(A) = 1\). The system has no solution exactly when \(\lambda = 3\).

### Q10

Answer: B

There are fewer equations than unknowns, but that does not decide consistency. The augmented matrix is

$$
\begin{bmatrix} 1 & 1 & 1 & 1 \\ 2 & 2 & 2 & 3 \end{bmatrix}.
$$

Row 2 minus \(2\) times row 1 is \((0, 0, 0, 1)\), which is the contradiction \(0 = 1\). So \(\operatorname{rank}(A) = 1 < 2 = \operatorname{rank}([A \mid b])\). There is no solution.

### Q11

Answer: 1

The third equation gives \(3x = 3\), so \(x = 1\). The first equation then gives \(y = 2\). The second equation checks: \(2\cdot 1 - 2 = 0\).

The coefficient matrix of the first two equations already has determinant \(1\cdot(-1) - 1\cdot 2 = -3 \neq 0\), and the third equation is their sum, so it adds no new constraint. The ranks of \(A\) and \([A \mid b]\) are both \(2\), equal to the number of unknowns. The solution \(x = 1\), \(y = 2\) is unique.

### Q12

Answer: B, C, D

(B) is the count of non-pivot columns: free variables \(= n - \operatorname{rank}(A)\), once the system is consistent.

(C) is the inconsistency test: a pivot in the augmented column means the right-hand side is not in the column space.

(D) holds because \(x = 0\) always satisfies \(Ax = 0\).

(A) is false. An underdetermined system can be inconsistent, as in the system of Q10.

### Q13

Answer: 1

Augmented matrix:

$$
\begin{bmatrix} 1 & 2 & 3 & 6 \\ 2 & 4 & 6 & 12 \\ 1 & 1 & 1 & 3 \end{bmatrix}.
$$

Row 2 minus \(2\) times row 1 is a zero row, and \(12 = 2\cdot 6\), so there is no contradiction. Row 3 minus row 1 is

$$
(0,\ -1,\ -2 \mid -3).
$$

Two pivots appear, in columns 1 and 2, and none in the augmented column. Thus

$$
\operatorname{rank}(A) = \operatorname{rank}([A \mid b]) = 2 < 3.
$$

The number of free variables is \(3 - 2 = 1\).

Back-substitution: \(y + 2z = 3\) and \(x + 2y + 3z = 6\). With \(z\) free,

$$
y = 3 - 2z, \qquad x = z.
$$

### Q14

Answer: C

$$
\det\begin{bmatrix} 1 & 1 \\ 2 & 2 \end{bmatrix} = 0,
$$

so Cramer's rule does not apply. The second equation is exactly twice the first, and \(4 = 2\cdot 2\), so the system is consistent. The rank is \(1 < 2\), and the solutions are all pairs with \(x + y = 2\). There are infinitely many solutions.

A zero determinant does not, by itself, mean the system is inconsistent.

### Q15

Answer: 4

Augmented matrix:

$$
\begin{bmatrix} 1 & 1 & 1 & 6 \\ 2 & -1 & 1 & 3 \\ 1 & 2 & -1 & 2 \end{bmatrix}.
$$

Row 2 minus \(2\) times row 1, and row 3 minus row 1:

$$
\begin{bmatrix} 1 & 1 & 1 & 6 \\ 0 & -3 & -1 & -9 \\ 0 & 1 & -2 & -4 \end{bmatrix}.
$$

Replace row 2 by row 2 plus \(3\) times row 3:

$$
\begin{bmatrix} 1 & 1 & 1 & 6 \\ 0 & 0 & -7 & -21 \\ 0 & 1 & -2 & -4 \end{bmatrix}.
$$

From row 2, \(-7z = -21\), so \(z = 3\). From row 3,

$$
y - 2\cdot 3 = -4 \implies y = 2.
$$

From row 1,

$$
x + 2 + 3 = 6 \implies x = 1.
$$

Therefore \(x + z = 1 + 3 = 4\).

The coefficient determinant is \(7 \neq 0\), which agrees with uniqueness. Check: \(1 + 2 + 3 = 6\), \(2 - 2 + 3 = 3\), and \(1 + 4 - 3 = 2\).

### Q16

Answer: B, C

Every row of \(A\) is a multiple of \((1, 2, -1)\):

$$
\text{row 2} = 2\cdot\text{row 1}, \qquad \text{row 3} = 3\cdot\text{row 1}.
$$

The same multiples match \(b\): \(2 = 2\cdot 1\) and \(3 = 3\cdot 1\). Row reduction of the augmented matrix therefore produces two zero rows and no pivot in the \(b\) column. Hence

$$
\operatorname{rank}(A) = \operatorname{rank}([A \mid b]) = 1 < 3.
$$

The system is consistent, with

$$
3 - 1 = 2
$$

free variables, so there are infinitely many solutions. The zero vector satisfies \(Ax = 0\), not \(Ax = b\), because \(b \neq 0\). One particular solution is \((1, 0, 0)\), since the first column of \(A\) equals \(b\).

# Matrices — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Let \(A\) be a \(3 \times 4\) matrix and \(B\) a \(4 \times 2\) matrix. The product \(AB\) is

(A) a \(3 \times 2\) matrix

(B) a \(4 \times 4\) matrix

(C) a \(3 \times 4\) matrix

(D) not defined

---

## Q2 — NAT

Let

$$
A = \begin{bmatrix} 4 & -2 & 7 \\ 1 & 5 & -3 \end{bmatrix}.
$$

The entry in row 3, column 1 of \(A^{T}\) is ____.

---

## Q3 — MCQ

Let \(A\) be a real square matrix satisfying \(A^{T} = -A\). Which of the following is always true?

(A) Every diagonal entry of \(A\) is \(0\)

(B) \(A\) is invertible

(C) \(A^{T} = A\)

(D) Every entry of \(A\) is \(0\)

---

## Q4 — NAT

The rank of

$$
\begin{bmatrix} 2 & -4 & 6 \\ 1 & -2 & 3 \\ -3 & 6 & -9 \end{bmatrix}
$$

is ____.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Let \(A\) and \(B\) be invertible matrices of the same order. Then \((AB)^{-1}\) equals

(A) \(A^{-1}B^{-1}\)

(B) \(B^{-1}A^{-1}\)

(C) \(AB\)

(D) \(A^{T}B^{T}\)

---

## Q6 — NAT

Let

$$
A = \begin{bmatrix} 1 & 4 \\ 2 & -1 \end{bmatrix}, \quad
B = \begin{bmatrix} 3 & 0 \\ 1 & 2 \end{bmatrix}.
$$

The value of \(\operatorname{tr}(AB)\) is ____.

---

## Q7 — MCQ

Which of the following matrices \(M\) satisfies \(M^{2} = M\)?

(A) \(\begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}\)

(B) \(\begin{bmatrix} 2 & -1 \\ 2 & -1 \end{bmatrix}\)

(C) \(\begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}\)

(D) \(\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}\)

---

## Q8 — MSQ

Let

$$
A = \begin{bmatrix} 0 & -2 \\ 2 & 0 \end{bmatrix}.
$$

Select all that apply.

(A) \(A^{T} = -A\)

(B) \(A^{2} = -4I\)

(C) \(\operatorname{tr}(A) = 0\)

(D) \(\det(A) = 0\)

---

## Q9 — NAT

Let

$$
A = \begin{bmatrix} 5 & 2 \\ 2 & 1 \end{bmatrix}.
$$

The sum of all four entries of \(A^{-1}\) is ____.

---

## Level 3 — Multi-Step

## Q10 — NAT

The rank of

$$
\begin{bmatrix}
1 & 0 & 2 & 1 \\
2 & 1 & 4 & 3 \\
3 & 1 & 6 & 4
\end{bmatrix}
$$

is ____.

---

## Q11 — MCQ

Let

$$
A = \begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & 3 \\ 0 & 0 & 0 \end{bmatrix}.
$$

The smallest positive integer \(k\) such that \(A^{k}\) is the zero matrix is

(A) \(1\)

(B) \(2\)

(C) \(3\)

(D) \(4\)

---

## Q12 — NAT

Let

$$
A = \begin{bmatrix} 0 & 0 & 1 \\ 1 & 0 & 0 \\ 0 & 1 & 0 \end{bmatrix}.
$$

The value of \(\det(A)\) is ____.

---

## Q13 — MSQ

Let \(A\) and \(B\) be real square matrices of the same order, and assume every inverse below exists when it is written. Select all that apply.

(A) \(\operatorname{tr}(AB) = \operatorname{tr}(BA)\)

(B) \((AB)^{T} = B^{T}A^{T}\)

(C) \(AB = BA\)

(D) If \(A\) is invertible, then \(\det(A) \neq 0\)

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Let

$$
A = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}, \quad
B = \begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}.
$$

Which one of the following is correct?

(A) \(AB = BA\)

(B) \(AB - BA = \begin{bmatrix} 2 & 0 \\ 0 & -2 \end{bmatrix}\)

(C) Both \(A\) and \(B\) are singular

(D) \(\operatorname{tr}(AB) \neq \operatorname{tr}(BA)\)

---

## Q15 — MSQ

Let

$$
A = \begin{bmatrix} 1 & 3 & -2 \\ 2 & 6 & -4 \\ 4 & 12 & -8 \end{bmatrix}.
$$

Select all that apply.

(A) \(\operatorname{rank}(A) = 1\)

(B) \(\operatorname{rank}(A) = 3\), because \(A\) has three rows

(C) \(A\) is singular

(D) Every row of \(A\) is a scalar multiple of one nonzero row

---

## Q16 — NAT

Let

$$
A = \begin{bmatrix} 1 & 2 \\ 2 & 4 \end{bmatrix}, \quad
B = \begin{bmatrix} 2 & -1 \\ -1 & 2 \end{bmatrix}.
$$

The rank of \(AB\) is ____.

---

## Level 5 — Challenge

## Q17 — MSQ

Let

$$
A = \begin{bmatrix} 1 & 3 \\ 0 & 1 \end{bmatrix}.
$$

Select all that apply.

(A) \(A\) is nilpotent

(B) For every positive integer \(n\), \(A^{n} = \begin{bmatrix} 1 & 3n \\ 0 & 1 \end{bmatrix}\)

(C) \(\det(A^{n}) = 1\) for every positive integer \(n\)

(D) \(A^{-1} = \begin{bmatrix} 1 & -3 \\ 0 & 1 \end{bmatrix}\)

---

## Q18 — NAT

Let

$$
A = \begin{bmatrix} 1 & -2 & 3 \\ 4 & 0 & 1 \end{bmatrix}.
$$

The value of \(\operatorname{tr}(AA^{T})\) is ____.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | NAT | 7 |
| 3 | MCQ | A |
| 4 | NAT | 1 |
| 5 | MCQ | B |
| 6 | NAT | 5 |
| 7 | MCQ | B |
| 8 | MSQ | A, B, C |
| 9 | NAT | 2 |
| 10 | NAT | 2 |
| 11 | MCQ | C |
| 12 | NAT | 1 |
| 13 | MSQ | A, B, D |
| 14 | MCQ | B |
| 15 | MSQ | A, C, D |
| 16 | NAT | 1 |
| 17 | MSQ | B, C, D |
| 18 | NAT | 31 |

## Detailed Solutions

### Q1

Answer: A

\(A\) is \(3 \times 4\) and \(B\) is \(4 \times 2\). The inner dimensions are both \(4\), so \(AB\) is defined and has size \(3 \times 2\).

### Q2

Answer: 7

By definition, \((A^{T})_{ij} = a_{ji}\). Hence

$$
(A^{T})_{31} = a_{13} = 7.
$$

Explicitly,

$$
A^{T} = \begin{bmatrix} 4 & 1 \\ -2 & 5 \\ 7 & -3 \end{bmatrix}.
$$

### Q3

Answer: A

The condition \(A^{T} = -A\) means \(a_{ji} = -a_{ij}\) for every \(i, j\). On the diagonal, \(i = j\), so \(a_{ii} = -a_{ii}\), hence \(2a_{ii} = 0\) and \(a_{ii} = 0\).

(B) fails for the zero matrix, which is skew-symmetric and singular. (C) would force \(A = -A\), so \(A = O\), which is stronger than the given hypothesis. (D) fails for \(\begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix}\).

### Q4

Answer: 1

Denote the rows by \(R_1, R_2, R_3\).

$$
R_2 = \tfrac{1}{2} R_1, \qquad R_3 = -\tfrac{3}{2} R_1,
$$

since

$$
\tfrac{1}{2}(2, -4, 6) = (1, -2, 3), \qquad -\tfrac{3}{2}(2, -4, 6) = (-3, 6, -9).
$$

Row 1 is nonzero, so there is exactly one linearly independent row. The rank is \(1\).

### Q5

Answer: B

If \(AB\) is invertible, the inverse reverses the order:

$$
(AB)(B^{-1}A^{-1}) = A(BB^{-1})A^{-1} = AIA^{-1} = I.
$$

The same check on the left gives \(B^{-1}A^{-1}(AB) = I\). So \((AB)^{-1} = B^{-1}A^{-1}\).

### Q6

Answer: 5

$$
AB = \begin{bmatrix} 1 & 4 \\ 2 & -1 \end{bmatrix}
\begin{bmatrix} 3 & 0 \\ 1 & 2 \end{bmatrix}
= \begin{bmatrix} 1\cdot 3 + 4\cdot 1 & 1\cdot 0 + 4\cdot 2 \\ 2\cdot 3 + (-1)\cdot 1 & 2\cdot 0 + (-1)\cdot 2 \end{bmatrix}
= \begin{bmatrix} 7 & 8 \\ 5 & -2 \end{bmatrix}.
$$

$$
\operatorname{tr}(AB) = 7 + (-2) = 5.
$$

The same trace is obtained from \(BA\):

$$
BA = \begin{bmatrix} 3 & 0 \\ 1 & 2 \end{bmatrix}
\begin{bmatrix} 1 & 4 \\ 2 & -1 \end{bmatrix}
= \begin{bmatrix} 3 & 12 \\ 5 & 2 \end{bmatrix},
\quad \operatorname{tr}(BA) = 3 + 2 = 5.
$$

### Q7

Answer: B

(A)

$$
\begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}^{2}
= \begin{bmatrix} 1 & 4 \\ 0 & 1 \end{bmatrix} \neq \begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}.
$$

(B)

$$
\begin{bmatrix} 2 & -1 \\ 2 & -1 \end{bmatrix}^{2}
= \begin{bmatrix} 4 - 2 & -2 + 1 \\ 4 - 2 & -2 + 1 \end{bmatrix}
= \begin{bmatrix} 2 & -1 \\ 2 & -1 \end{bmatrix}.
$$

So this matrix is idempotent.

(C)

$$
\begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}^{2}
= \begin{bmatrix} 2 & 1 \\ 1 & 1 \end{bmatrix} \neq \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}.
$$

(D)

$$
\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}^{2}
= \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \neq \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}.
$$

### Q8

Answer: A, B, C

$$
A^{T} = \begin{bmatrix} 0 & 2 \\ -2 & 0 \end{bmatrix} = -A,
$$

so (A) holds, and the diagonal entries are \(0\), so \(\operatorname{tr}(A) = 0\). Thus (C) holds.

$$
A^{2} = \begin{bmatrix} 0 & -2 \\ 2 & 0 \end{bmatrix}
\begin{bmatrix} 0 & -2 \\ 2 & 0 \end{bmatrix}
= \begin{bmatrix} -4 & 0 \\ 0 & -4 \end{bmatrix} = -4I.
$$

So (B) holds.

$$
\det(A) = 0\cdot 0 - (-2)\cdot 2 = 4 \neq 0,
$$

so (D) does not hold. In particular \(A\) is invertible.

### Q9

Answer: 2

$$
\det(A) = 5\cdot 1 - 2\cdot 2 = 1.
$$

The \(2 \times 2\) inverse formula gives

$$
A^{-1} = \begin{bmatrix} 1 & -2 \\ -2 & 5 \end{bmatrix}.
$$

The sum of the entries is \(1 + (-2) + (-2) + 5 = 2\).

Check:

$$
\begin{bmatrix} 5 & 2 \\ 2 & 1 \end{bmatrix}
\begin{bmatrix} 1 & -2 \\ -2 & 5 \end{bmatrix}
= \begin{bmatrix} 5 - 4 & -10 + 10 \\ 2 - 2 & -4 + 5 \end{bmatrix}
= I.
$$

### Q10

Answer: 2

Row-reduce. \(R_2 \leftarrow R_2 - 2R_1\) and \(R_3 \leftarrow R_3 - 3R_1\):

$$
\begin{bmatrix}
1 & 0 & 2 & 1 \\
0 & 1 & 0 & 1 \\
0 & 1 & 0 & 1
\end{bmatrix}.
$$

Then \(R_3 \leftarrow R_3 - R_2\):

$$
\begin{bmatrix}
1 & 0 & 2 & 1 \\
0 & 1 & 0 & 1 \\
0 & 0 & 0 & 0
\end{bmatrix}.
$$

There are two nonzero rows, so the rank is \(2\).

### Q11

Answer: C

$$
A^{2} = \begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & 3 \\ 0 & 0 & 0 \end{bmatrix}
\begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & 3 \\ 0 & 0 & 0 \end{bmatrix}
= \begin{bmatrix} 0 & 0 & 6 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix} \neq O.
$$

$$
A^{3} = A^{2}A = \begin{bmatrix} 0 & 0 & 6 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}
\begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & 3 \\ 0 & 0 & 0 \end{bmatrix}
= O.
$$

The smallest such positive integer is \(3\). The matrix is nilpotent of index \(3\).

### Q12

Answer: 1

Expand along the first row. The only nonzero entry is \(a_{13} = 1\), and the cofactor sign is \((-1)^{1+3} = +1\):

$$
\det(A) = 1 \cdot \det\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = 1.
$$

As a check, \(A^{T}A = I\), so \(A\) is orthogonal and \(\det(A) = \pm 1\). The expansion selects the sign \(+1\).

### Q13

Answer: A, B, D

(A) holds because

$$
\operatorname{tr}(AB) = \sum_i \sum_j a_{ij} b_{ji} = \operatorname{tr}(BA).
$$

(B) is the reversal rule for transpose of a product. (D) is the invertibility criterion: a square matrix has an inverse if and only if its determinant is nonzero.

(C) is false in general. For a concrete counterexample,

$$
\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 0 \\ 1 & 1 \end{bmatrix}
= \begin{bmatrix} 2 & 1 \\ 1 & 1 \end{bmatrix},
\quad
\begin{bmatrix} 1 & 0 \\ 1 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}
= \begin{bmatrix} 1 & 1 \\ 1 & 2 \end{bmatrix}.
$$

### Q14

Answer: B

$$
AB = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}
= \begin{bmatrix} 1 + 2 & 1 \\ 2 & 1 \end{bmatrix}
= \begin{bmatrix} 3 & 1 \\ 2 & 1 \end{bmatrix}.
$$

$$
BA = \begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}
= \begin{bmatrix} 1 & 1 \\ 2 & 3 \end{bmatrix}.
$$

$$
AB - BA = \begin{bmatrix} 2 & 0 \\ 0 & -2 \end{bmatrix}.
$$

So (B) is correct and (A) is not. Also \(\det(A) = 1\) and \(\det(B) = 1\), so neither matrix is singular. Finally \(\operatorname{tr}(AB) = 4 = \operatorname{tr}(BA)\).

### Q15

Answer: A, C, D

Row 2 is \(2\) times row 1, and row 3 is \(4\) times row 1:

$$
2(1, 3, -2) = (2, 6, -4), \qquad 4(1, 3, -2) = (4, 12, -8).
$$

Row 1 is nonzero, so the rank is \(1\), not \(3\). A square matrix of rank less than its order is singular. Equivalently, two rows are scalar multiples of the first, so \(\det(A) = 0\).

### Q16

Answer: 1

$$
AB = \begin{bmatrix} 1 & 2 \\ 2 & 4 \end{bmatrix}
\begin{bmatrix} 2 & -1 \\ -1 & 2 \end{bmatrix}
= \begin{bmatrix} 2 - 2 & -1 + 4 \\ 4 - 4 & -2 + 8 \end{bmatrix}
= \begin{bmatrix} 0 & 3 \\ 0 & 6 \end{bmatrix}.
$$

The second row is twice the first, and the first row is nonzero, so \(\operatorname{rank}(AB) = 1\).

For comparison, \(\operatorname{rank}(A) = 1\) and

$$
\det(B) = 4 - 1 = 3 \neq 0,
$$

so \(\operatorname{rank}(B) = 2\). The rank of a product is at most the smaller of the two ranks; it is not their product.

### Q17

Answer: B, C, D

(A) fails because the diagonal entries of every power stay equal to \(1\), so no power is the zero matrix. Directly, \(A \neq O\).

(B) For \(n = 1\) the formula is \(A\) itself. If \(A^{n} = \begin{bmatrix} 1 & 3n \\ 0 & 1 \end{bmatrix}\), then

$$
A^{n+1} = \begin{bmatrix} 1 & 3n \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 3 \\ 0 & 1 \end{bmatrix}
= \begin{bmatrix} 1 & 3 + 3n \\ 0 & 1 \end{bmatrix}
= \begin{bmatrix} 1 & 3(n+1) \\ 0 & 1 \end{bmatrix}.
$$

By induction the formula holds for every positive integer \(n\). In particular

$$
\det(A^{n}) = 1 \cdot 1 - 3n \cdot 0 = 1,
$$

which is (C). Since \(\det(A) = 1\),

$$
A^{-1} = \begin{bmatrix} 1 & -3 \\ 0 & 1 \end{bmatrix},
$$

and

$$
\begin{bmatrix} 1 & -3 \\ 0 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 3 \\ 0 & 1 \end{bmatrix}
= I.
$$

So (D) holds.

### Q18

Answer: 31

$$
A^{T} = \begin{bmatrix} 1 & 4 \\ -2 & 0 \\ 3 & 1 \end{bmatrix}.
$$

$$
AA^{T} = \begin{bmatrix} 1 & -2 & 3 \\ 4 & 0 & 1 \end{bmatrix}
\begin{bmatrix} 1 & 4 \\ -2 & 0 \\ 3 & 1 \end{bmatrix}
= \begin{bmatrix} 1 + 4 + 9 & 4 + 0 + 3 \\ 4 + 0 + 3 & 16 + 0 + 1 \end{bmatrix}
= \begin{bmatrix} 14 & 7 \\ 7 & 17 \end{bmatrix}.
$$

$$
\operatorname{tr}(AA^{T}) = 14 + 17 = 31.
$$

The same number is the sum of the squares of the entries of \(A\):

$$
1^{2} + (-2)^{2} + 3^{2} + 4^{2} + 0^{2} + 1^{2} = 1 + 4 + 9 + 16 + 0 + 1 = 31,
$$

because the diagonal entries of \(AA^{T}\) are the squared Euclidean norms of the rows.

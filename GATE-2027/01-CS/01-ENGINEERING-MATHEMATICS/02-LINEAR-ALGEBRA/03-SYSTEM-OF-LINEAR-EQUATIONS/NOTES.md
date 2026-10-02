# System of Linear Equations — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What are linear systems in GATE?

A **system of linear equations** asks: find x such that several linear constraints hold simultaneously. In matrix form:

**Ax = b**

where A is m×n, x is n×1, b is m×1.

**Prerequisites:** `01-MATRICES` (operations, rank), `02-DETERMINANTS` (invertibility).

**Connections:** Gaussian elimination underlies `05-LU-DECOMPOSITION`; solution structure links to `04-EIGENVALUES` (null space of A).

---

## 2. Matrix and augmented matrix

### Concept

Equations:
a₁₁x₁ + … + a₁ₙxₙ = b₁
…
aₘ₁x₁ + … + aₘₙxₙ = bₘ

**Coefficient matrix A**, **augmented matrix [A|b]**.

### Worked Example 1

2x + y = 5; x − y = 1.

A = [[2,1],[1,−1]], b = [5,1]^T → x=2, y=1.

---

## 3. Rank and solution classification

### Definitions

- **rank(A)** = number of pivot columns in RREF of A.
- **rank([A|b])** = pivots in augmented matrix.

### Rouché–Capelli theorem (GATE essential)

| Condition | Solution |
|-----------|----------|
| rank(A) = rank([A|b]) = n | **Unique** solution |
| rank(A) = rank([A|b]) < n | **Infinitely many** |
| rank(A) < rank([A|b]) | **No** solution (inconsistent) |

### Derivation intuition

Each pivot equation fixes one independent variable. If rank < n, free variables remain → infinite solutions. If b introduces a new independent equation incompatible with A → no solution.

### Worked Example 2

A = [[1,2],[2,4]], b = [3,6]^T. rank(A)=1, rank([A|b])=1 < n=2 → **infinite** solutions: x₁ + 2x₂ = 3.

A = [[1,2],[2,4]], b = [3,7]^T. rank(A)=1, rank([A|b])=2 → **no** solution.

### GATE Connection

GATE often asks "how many solutions?" without full solve — compute ranks only.

---

## 4. Homogeneous systems Ax = 0

### Concept

Always has **trivial solution** x = 0.

**Non-trivial solutions exist** ⟺ rank(A) < n ⟺ det(A)=0 for square A.

### Solution space

Set of all solutions forms a **vector space** (null space) of dimension **n − rank(A)** = number of **free variables**.

### Worked Example 3

x + y + z = 0; x − y = 0 → 2x=0, so x=0, y=0, z free → **1 free variable**, infinite solutions (line through origin).

---

## 5. Gaussian elimination

### Procedure

1. Form augmented matrix [A|b].
2. Use elementary row operations to reach **row echelon form** (REF): pivots move right; zeros below pivots.
3. Back-substitute.

### Elementary operations (preserve solution set)

- Swap rows
- Multiply row by nonzero scalar
- Add multiple of one row to another

### Worked Example 4

[[1,1,2|4],[2,3,1|7],[1,2,0|3]]

R₂−2R₁, R₃−R₁ → REF → back-substitute → unique solution.

---

## 6. Gauss–Jordan (RREF)

Continue elimination until **reduced row echelon form**: pivots are 1; only 0 above and below each pivot.

Advantage: directly read solution with free variables identified.

### Free variables

Columns without pivots → free parameters t, s, … Express pivots in terms of free vars.

---

## 7. Consistency for over/under-determined systems

### m < n (underdetermined)

More unknowns than equations → if consistent, usually **infinite** solutions (unless rank = n, rare).

### m > n (overdetermined)

More equations than unknowns → may be **inconsistent** even if each pair looks fine.

### Trap

"Underdetermined" does **not** guarantee infinite solutions — check rank([A|b]).

---

## 8. Inverse method (square, invertible)

If A is n×n and det(A) ≠ 0:

**x = A^{-1} b**

Practical only for small n; elimination preferred.

---

## 9. Cramer's rule (small systems)

x_i = det(A_i)/det(A). See `02-DETERMINANTS/NOTES.md`.

---

## 10. Linear independence and span

Columns of A are **linearly independent** ⟺ Ax=0 has only trivial solution ⟺ rank(A)=n (when A is m×n with n columns).

**Span of columns** = set of all b for which Ax=b consistent.

---

## 11. Worked Example 5 — Parameter problems

For what λ does the system have no solution?

x + y = 1; λx + 2y = 3.

Augmented: rank 2 unless λ=2 (dependent rows). If λ=2: 2x+2y=3 with x+y=1 → inconsistent → **λ=2, no solution**. λ≠2 → unique.

---

## 12. Worked Example 6 — Count free variables

3 equations, 5 unknowns, rank(A)=2 → free variables = 5−2 = **3**; solution space dimension 3.

---

## 13. Connection to LU decomposition

Gaussian elimination without row swaps factors A = LU (`05-LU-DECOMPOSITION`). Solve Ax=b via Ly=b, Ux=y — efficient for multiple b.

---

## 14. GATE checklist

1. Write [A|b]; row-reduce to find ranks.
2. Homogeneous: always x=0; non-trivial iff rank < n.
3. Free vars = n − rank(A).
4. Do not assume underdetermined ⇒ infinite solutions.
5. Parameter λ: track when rows become dependent.

---

## 15. Concept map

```
Systems ← Matrices, Determinants (rank, det)
        → LU (efficient solving)
        → Eigenvalues (null space, Av=0 for λ=0)
```

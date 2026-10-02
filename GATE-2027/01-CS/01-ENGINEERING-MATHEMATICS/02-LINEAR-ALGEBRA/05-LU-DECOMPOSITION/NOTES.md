# LU Decomposition — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is LU decomposition in GATE?

**LU decomposition** factors a square matrix A into:

**A = LU**

where:
- **L** is **lower triangular** with **1s on the diagonal** (unit lower triangular).
- **U** is **upper triangular**.

When row swaps are needed during elimination:

**PA = LU**

where P is a **permutation matrix** recording row interchanges.

**Prerequisites:** `01-MATRICES`, `03-SYSTEM-OF-LINEAR-EQUATIONS` (Gaussian elimination).

**Connections:** Efficient solution of Ax=b for many b; determinant via U; foundation for numerical linear algebra.

---

## 2. Why LU exists — link to Gaussian elimination

### Concept

Gaussian elimination (without row swaps) applies elementary row operations: subtract multiples of row k from rows below to zero entries below the pivot in column k.

Each such operation is multiplication on the left by a **lower triangular** matrix with 1s on the diagonal.

### Formal idea

E_{n−1} … E₁ A = U

where each E_k is unit lower triangular. Then:

A = (E_{n−1} … E₁)⁻¹ U = LU

with L = (E_{n−1} … E₁)⁻¹ — also unit lower triangular.

### Intuition

L **remembers** the multipliers used during elimination; U is the **final upper triangular** form.

### Existence (no pivoting)

LU without swaps exists iff all **leading principal minors** are nonzero (every pivot position a_{kk} ≠ 0 during elimination).

---

## 3. Structure of L and U

### L (lower triangular, unit diagonal)

- ℓ_{ij} = 0 for j > i
- ℓ_{ii} = **1** for all i
- ℓ_{ij} for j < i = **multiplier** used to eliminate entry (i,j) using pivot in column j

### U (upper triangular)

- u_{ij} = 0 for j < i
- u_{ii} = **pivot** after elimination in column i
- u_{ij} for j > i = entries above diagonal after elimination

### Worked Example 1 — 2×2

A = [[2, 1], [4, 3]]

Eliminate below pivot 2 in column 1: multiplier ℓ₂₁ = 4/2 = **2**.

Row 2 ← Row 2 − 2·Row 1 → U = [[2, 1], [0, 1]]

L = [[1, 0], [2, 1]]

Verify: LU = [[2,1],[4,3]] ✓

---

## 4. Algorithm to compute LU (hand calculation)

### For k = 1 to n−1:

1. Pivot u_{kk} = a_{kk} (after previous steps).
2. For i = k+1 to n: ℓ_{ik} = a_{ik} / a_{kk}.
3. Row i ← Row i − ℓ_{ik} · Row k (updates A toward U).

Store multipliers in L; final upper part is U.

### Worked Example 2 — 3×3

A = [[1, 2, 3], [2, 5, 7], [4, 9, 10]]

**Column 1:** ℓ₂₁=2/1=2, ℓ₃₁=4/1=4.

After step: [[1,2,3],[0,1,1],[0,1,−2]]

**Column 2:** ℓ₃₂=1/1=1.

U = [[1,2,3],[0,1,1],[0,0,−3]]

L = [[1,0,0],[2,1,0],[4,1,1]]

Check A = LU by multiplication.

---

## 5. Solving Ax = b with LU

### Two-step process

Since A = LU, solve Ax = b as:

1. **Forward substitution:** Ly = b  → find y
2. **Back substitution:** Ux = y  → find x

### Why reuse?

- Factor A **once:** O(n³) arithmetic (≈ 2n³/3 flops).
- Each new b: O(n²) only.

Gaussian elimination from scratch each time costs O(n³) per b.

### Worked Example 3

Using A = [[2,1],[4,3]], b = [3, 7]ᵀ.

**Ly = b:** y₁ = 3; y₂ = 7 − 2·3 = **1**.

**Ux = y:** 2x₁ + x₂ = 3, x₂ = 1 → x₁ = **1**, x₂ = **1**.

Solution x = [1, 1]ᵀ.

---

## 6. PA = LU (partial pivoting)

### Concept

When pivot a_{kk} = 0 (or very small for numerical stability), **swap rows** to bring a nonzero pivot to position (k,k).

P records the permutation: PA = LU.

### Solving with pivoting

1. Compute Pb (permute RHS same as A).
2. Ly = Pb
3. Ux = y

### Worked Example 4 — Need pivot

A = [[0, 1], [1, 0]]

No LU without swap — zero pivot at (1,1).

Swap rows: P = [[0,1],[1,0]], PA = [[1,0],[0,1]] = I.

L = I, U = I. Trivial but illustrates pivot necessity.

### Common Trap

Not every matrix has LU **without** pivoting. [[0,1],[1,0]] is the standard example.

---

## 7. Determinant from LU

### Formula

det(L) = 1 (unit diagonal).

det(U) = ∏_{i=1}^{n} u_{ii}  (product of diagonal of U).

**det(A) = det(P) · ∏ u_{ii}**

det(P) = (−1)^{number of row swaps}.

### Worked Example 5

If U has diagonal entries 2, 3, 5 and P = I:

det(A) = 2 × 3 × 5 = **30**.

With one row swap: det(A) = **−30**.

### GATE Connection

Faster than cofactor expansion for conceptual 3×3 after LU.

---

## 8. Complexity and when to use LU

### Complexity

| Task | Cost |
|------|------|
| LU factorization | O(n³) ≈ 2n³/3 flops |
| Forward + back substitution | O(n²) per b |
| k different b vectors | O(n³) + k·O(n²) |

### When LU wins

- **Multiple RHS** with same A.
- Need **det(A)** after factorization.
- Building block for matrix inverse (solve AX = I column-wise — not preferred for hand work).

### Comparison

| Method | Best for |
|--------|----------|
| LU | Multiple b, det |
| Gauss–Jordan | RREF, explicit inverse |
| Cramer's rule | Tiny n only |
| Cholesky A=LLᵀ | Symmetric positive definite |

---

## 9. Uniqueness

### Doolittle LU

For **invertible** A with LU existing **without** row swaps, factorization A = LU with L unit lower and U upper is **unique**.

### Worked Example 6 — Conceptual

If two factorizations A = L₁U₁ = L₂U₂, then L₂⁻¹L₁ = U₂U₁⁻¹ — left side lower triangular, right side upper triangular → both must be I → L₁=L₂, U₁=U₂.

---

## 10. LDU variant (awareness)

Sometimes A = LDU where:
- L unit lower, U unit upper, D diagonal.

Useful in theory; GATE usually uses standard LU (pivots on U diagonal).

---

## 11. When LU fails conceptually

### Singular matrix

If A is singular, elimination produces **zero on diagonal of U** → det(A) = 0.

LU may still be computed with pivoting but U is singular.

### Numerical stability

Even when exact LU exists, partial pivoting improves stability (avoid dividing by tiny pivots).

---

## 12. Relation to matrix inverse

To find A⁻¹, solve AX = I — each column of X is a system Ax = e_j.

Use LU once, solve n times → O(n³) total after factorization.

GATE rarely asks full inverse via LU by hand; prefers conceptual questions.

---

## 13. Worked Example 7 — Full 3×3 solve

A = [[1,2,3],[2,5,7],[4,9,10]], b = [6, 15, 17]ᵀ.

From Example 2: L, U known.

**Ly = b:** y₁=6; y₂=15−2·6=3; y₃=17−4·6−1·3=−10.

**Ux = y:** −3x₃=−10 → x₃=10/3; x₂+x₃=3 → x₂=−1/3; x₁+2x₂+3x₃=6 → solve x₁.

(Practice arithmetic in `PRACTICE.md`.)

---

## 14. Worked Example 8 — GATE conceptual

**Q:** Why store multipliers in L instead of storing all row operation history?

**A:** L compactly encodes elimination steps; given L and U, reproduce U from A without separate operation log. Same arithmetic as Gaussian elimination, better for reuse.

---

## 15. Worked Example 9 — Upper triangular A

If A is already upper triangular:

L = **I**, U = **A**.

If A is lower triangular, may need different factorization view — standard LU still applies with appropriate pivoting.

---

## 16. Permutation matrices

P is obtained by swapping rows of I.

Properties: P⁻¹ = Pᵀ, det(P) = ±1.

Left-multiplying A by P swaps rows of A.

---

## 17. GATE checklist

1. L unit lower (diagonal 1s); U upper triangular; A = LU.
2. Solve: **Ly = b** then **Ux = y** (forward then back).
3. det(A) = sign(P) · ∏ u_{ii}.
4. Zero pivot → use **PA = LU**.
5. Factor once, solve many b cheaply.
6. Same arithmetic as Gaussian elimination.
7. Do not confuse with Cholesky (symmetric A = LLᵀ).

---

## 18. Concept map

```
LU ← Gaussian elimination (Systems of equations)
   ← Matrices (triangular structure)
   → Determinants (product of U diagonal)
   → Efficient Ax=b (multiple RHS)
   → Numerical methods (pivoting, stability)
```

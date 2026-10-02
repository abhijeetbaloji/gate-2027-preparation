# Determinants

## Concept links
- **Matrices** define the array; **determinant** is a scalar attached to square matrices.
- det(A) ≠ 0 ⇔ A invertible ⇔ unique solution to Ax = b.
- **Eigenvalues**: det(A − λI) = 0 is the characteristic equation.
- **LU**: det(A) = product of diagonal of U.

---

## 1. Definition

For 2×2: det [[a,b],[c,d]] = **ad − bc**.

For n×n: expand along any row/column using **cofactors**:

det(A) = Σⱼ aᵢⱼ Cᵢⱼ  where Cᵢⱼ = (−1)ⁱ⁺ʲ Mᵢⱼ

Mᵢⱼ = minor (det of submatrix after deleting row i, col j).

**Worked example.** det [[2,1],[4,3]] = 2·3 − 1·4 = **2**.

---

## 2. Properties (derivation sketches)

| Operation | Effect on det |
|-----------|---------------|
| Swap two rows | Sign flips |
| Multiply row by k | det × k |
| Add multiple of one row to another | Unchanged |
| Two proportional/equal rows | det = 0 |
| det(Aᵀ) | = det(A) |
| det(AB) | = det(A)·det(B) |
| det(A⁻¹) | = 1/det(A) |
| det(kA) | = kⁿ det(A) |

**Why det(AB) = det(A)det(B)?** Determinant measures volume scaling of linear map; composition scales by product.

**Worked example.** det(A) = 3, det(B) = −2 ⇒ det(AB) = **−6**.

---

## 3. Triangular matrices

Upper or lower triangular: **det = product of diagonal entries**.

**Worked example.** det [[1,2,3],[0,4,5],[0,0,6]] = 1·4·6 = **24**.

---

## 4. Cofactor expansion strategy

Expand along row/column with most zeros to minimize work.

**Worked example.** det [[0,2,1],[0,0,3],[4,0,0]] — expand along col 1:

= 4 · (−1)⁴ · det [[2,1],[0,3]] = 4 · 6 = **24**.

---

## 5. Cramer's rule

For Ax = b with det(A) ≠ 0: xᵢ = det(Aᵢ)/det(A), where Aᵢ replaces column i of A with b.

GATE uses this for 2×2/3×3 only.

---

## GATE Connection

- **Singular vs non-singular** questions reduce to det = 0 or not.
- **Eigenvalue product** = det(A) — fast check.
- **Row operation tracking** in elimination preserves/changes det predictably.
- det(A + B) ≠ det(A) + det(B) in general — classic trap.

## Common traps

- Applying determinant to non-square matrices.
- Forgetting sign on row swap.
- Using det(A + B) = det(A) + det(B).

---

## 6. Derivation: det(A⁻¹) = 1/det(A)

If AA⁻¹ = I, then det(A)·det(A⁻¹) = det(I) = 1.

Hence det(A⁻¹) = **1/det(A)** when det(A) ≠ 0.

**Worked example.** det(A)=5 ⇒ det(A⁻¹)=**1/5**.

---

## 7. Derivation: det(kA) = kⁿ det(A)

Each of n rows of A is multiplied by k; each row scaling multiplies det by k.

n rows ⇒ factor **kⁿ**.

**Worked example.** A is 3×3, det(A)=2 ⇒ det(3A) = 3³·2 = **54**.

---

## 8. Why det(A+B) ≠ det(A)+det(B)

Counterexample: A = I₂, B = I₂.

det(A+B) = det(2I) = 4; det(A)+det(B) = 1+1 = **2**.

**GATE Connection:** MSQs testing determinant identities — only multiplicative rules are safe.

---

## 9. Block triangular determinant

If A = [[B, C],[0, D]] with B, D square blocks:

**det(A) = det(B)·det(D)**.

**Worked example.** B=[[2]], D=[[3,1],[0,4]] ⇒ det(A)=2·12=**24**.

---

## 10. Eigenvalue connection (preview)

Characteristic polynomial: p(λ) = det(A − λI).

- Constant term p(0) = det(A).
- Sum of roots = tr(A); product of roots = det(A).

Full treatment: `04-EIGENVALUES-AND-EIGENVECTORS/NOTES.md`.

**Worked example.** Eigenvalues 1,2,3 ⇒ det(A)=**6**, tr(A)=**6**.

---

## 11. Row reduction to compute det

Track operations: count row swaps (sign), row scalings (factor), then multiply diagonal of triangular form.

**Worked example.** [[1,1,1],[1,2,3],[1,4,9]] → upper triangular with diagonal 1,1,2 ⇒ det=**2**.

---

## 12. Geometric meaning

|det(A)| = factor by which area (2D) or volume (3D) scales under x ↦ Ax.

- det > 0: orientation preserved.
- det < 0: orientation reversed.
- det = 0: dimension collapses (singular).

---

## 13. Worked example — GATE expression

det(A)=4, A is 3×3. Find det(2A), det(A⁻¹), det(AᵀA).

- det(2A) = 8·4 = **32**
- det(A⁻¹) = **1/4**
- det(AᵀA) = det(A)² = **16**

---

## 14. Concept map

```
02-DETERMINANTS ← 01-MATRICES
                → 03-SYSTEMS (Cramer, consistency)
                → 04-EIGENVALUES (characteristic poly)
                → 05-LU (det = Π uᵢᵢ)
```

# Eigenvalues and Eigenvectors — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What are eigenvalues in GATE?

For square matrix A, if **Av = λv** for nonzero vector v, then λ is an **eigenvalue** and v is an **eigenvector**.

Eigenanalysis answers: how does the linear transformation A stretch/rotate special directions?

**Prerequisites:** `01-MATRICES`, `02-DETERMINANTS`, `03-SYSTEM-OF-LINEAR-EQUATIONS`.

**Connections:** Diagonalization, matrix powers, symmetric matrices (PCA spirit), Markov chains, LU stability.

---

## 2. Finding eigenvalues

### Characteristic equation

**det(A − λI) = 0**

Roots λ₁, λ₂, … are eigenvalues.

### Worked Example 1

A = [[4,1],[2,3]].

det [[4−λ,1],[2,3−λ]] = (4−λ)(3−λ)−2 = λ²−7λ+10 = 0 → **λ=5, λ=2**.

---

## 3. Finding eigenvectors

For each λ, solve **(A − λI)v = 0** (homogeneous system).

### Worked Example 2

λ=5: [[−1,1],[2,−2]]v=0 → v = t[1,1]^T → eigenvector **(1,1)** (any scalar multiple).

λ=2: [[2,1],[2,1]]v=0 → v = t[1,−2]^T.

---

## 4. Why sum of eigenvalues = trace(A)

### Derivation

det(A − λI) is degree-n polynomial:

det(A − λI) = (−1)^n λ^n + c_{n−1} λ^{n−1} + … + c₀.

Expand det(A − λI): the λ^{n−1} term comes from choosing n−1 diagonal (−λ) entries and one off-diagonal a_{ii}:

Coefficient of λ^{n−1} is **−(a₁₁ + a₂₂ + … + aₙₙ) = −tr(A)** (with sign convention (−1)^n).

For monic form λ^n − tr(A)λ^{n−1} + … + (−1)^n det(A) = 0:

**λ₁ + λ₂ + … + λₙ = tr(A)**.

**λ₁ λ₂ … λₙ = det(A)** (constant term).

### Worked Example 3

A 3×3 with eigenvalues 1,2,3: tr(A)=**6**, det(A)=**6**.

### GATE Connection

Compute trace/det without finding eigenvalues when only sum/product needed.

---

## 5. Algebraic vs geometric multiplicity

- **Algebraic multiplicity:** exponent in characteristic polynomial factor (λ−λᵢ)^k.
- **Geometric multiplicity:** dimension of eigenspace = n − rank(A−λᵢI) = number of independent eigenvectors for λᵢ.

Always: **1 ≤ geometric ≤ algebraic**.

### Diagonalizability

A is **diagonalizable** ⟺ geometric = algebraic for **every** eigenvalue ⟺ A = PDP^{-1} with D diagonal.

### Worked Example 4

A = [[2,1],[0,2]] — only one eigenvalue λ=2 (algebraic mult 2), one eigenvector direction → **not diagonalizable** (Jordan block).

---

## 6. Eigenvectors for distinct eigenvalues

**Theorem:** Eigenvectors corresponding to **distinct** eigenvalues are **linearly independent**.

### Proof sketch

If c₁v₁ + … + c_kv_k = 0 with distinct λᵢ, apply A repeatedly and use Vandermonde-like argument → all cᵢ=0.

---

## 7. Symmetric real matrices (GATE favorite)

If A is real and **A^T = A**:

1. All eigenvalues are **real**.
2. Eigenvectors for distinct eigenvalues are **orthogonal**.
3. A is **orthogonally diagonalizable**: **A = QΛQ^T** with Q orthogonal (Q^{-1}=Q^T).

### Why eigenvalues are real (sketch)

λv = Av, λ̄v̄ = Av̄. Then λ v^T v̄ = v^T A v̄ = v^T A^T v̄ = (Av)^T v̄ = λ̄ v^T v̄ → λ=λ̄.

---

## 8. Powers and exponentials

If Av = λv, then **A^k v = λ^k v**.

If A = PDP^{-1}, **A^k = PD^k P^{-1}**.

### Worked Example 5

A = [[1,1],[0,2]], P=[[1,1],[0,1]], D=[[1,0],[0,2]] → A^{10} = P[[1,0],[0,1024]]P^{-1}.

---

## 9. Zero eigenvalue

**λ=0 is eigenvalue** ⟺ Av=0 for nonzero v ⟺ A is **singular** ⟺ det(A)=0.

Links to `03-SYSTEM-OF-LINEAR-EQUATIONS` (non-trivial null space).

---

## 10. Cayley–Hamilton theorem (awareness)

A satisfies its own characteristic equation: if p(λ)=det(A−λI), then **p(A)=0**.

GATE may use for quick matrix polynomial simplification.

---

## 11. Worked Example 6 — GATE trace/det

3×3 matrix A has eigenvalues −1,0,2. Find det(A), tr(A), det(A−3I).

- det(A) = (−1)(0)(2) = **0**.
- tr(A) = **1**.
- Eigenvalues of A−3I: −4,−3,−1 → det = **−12**.

---

## 12. Worked Example 7 — Orthogonal diagonalization setup

Symmetric A = [[2,1],[1,2]]. Eigenvalues 3,1; eigenvectors [1,1]^T, [1,−1]^T → normalize → Q, Λ.

---

## 13. Applications in CS

- **PageRank / Markov:** dominant eigenvalue 1, eigenvector = steady state.
- **Graph spectra:** adjacency matrix eigenvalues.
- **Stability:** largest |λ| governs growth of A^k.

---

## 14. GATE checklist

1. Characteristic polynomial from det(A−λI).
2. tr(A) = sum λᵢ; det(A) = product λᵢ.
3. Solve (A−λI)v=0 per eigenvalue.
4. Symmetric ⇒ real λ, orthogonal eigenvectors.
5. Distinct λ ⇒ independent eigenvectors; check mult for diagonalization.

---

## 15. Concept map

```
Eigenvalues ← Determinants (characteristic poly)
            ← Systems (null space)
            → Diagonalization / powers
            → LU (conditioning, not core)
```

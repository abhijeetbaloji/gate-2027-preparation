# Matrices — GATE-STYLE PRACTICE

## Level 1

**1.** If A is 3×2 and B is 2×4, what is the size of AB?

**2.** Compute tr(A) for A = [[1,0,2],[0,3,1],[4,0,5]].

**3.** Is [[1,0],[0,1]] orthogonal?

### Level 1 — Solutions

1. **3×4** — inner dimension 2 matches.
2. **tr(A) = 1 + 3 + 5 = 9**.
3. **Yes** — IᵀI = I.

## Level 2

**1.** (AB)ᵀ equals? (a) AᵀBᵀ (b) BᵀAᵀ (c) AB (d) BA

**2.** If Aᵀ = A and Aᵀ = −A simultaneously, find A.

**3.** det(3A) for 2×2 A with det(A) = 4.

### Level 2 — Solutions

1. **(b) BᵀAᵀ**.
2. **Zero matrix** — only matrix both symmetric and skew-symmetric.
3. **3² × 4 = 36**.

## Level 3

**1.** A = [[2,1],[5,3]]. Find A⁻¹.

**2.** If A is 4×3 with rank 2, can AAᵀ be invertible?

**3.** Prove (AB)ᵀ = BᵀAᵀ for 2×2 matrices.

### Level 3 — Solutions

1. det = 1 ⇒ **A⁻¹ = [[3,−1],[−5,2]]**.
2. **No** — AAᵀ is 4×4 rank ≤ 2, not full rank.
3. (AB)ᵢⱼ = Σₖ aᵢₖbₖⱼ ⇒ (AB)ᵀⱼᵢ = Σₖ bₖⱼaᵢₖ = (BᵀAᵀ)ⱼᵢ.

## Level 4

**1.** A, B are n×n invertible. Simplify (A⁻¹Bᵀ)⁻¹.

**2.** If A is orthogonal, what is det(A)?

**3.** rank(AB) ≤ ? when A is m×n, B is n×p.

### Level 4 — Solutions

1. **(Bᵀ)⁻¹A = (B⁻¹)ᵀA**.
2. **±1** — det(A)² = det(AᵀA) = det(I) = 1.
3. **min(rank(A), rank(B))**.

## Level 5

**1.** A is 3×3, rank 2. Maximum rank of AᵀA?

**2.** If tr(A) = 7, det(A) = 10 for 2×2 A, find eigenvalues.

**3.** Show idempotent matrix (A² = A) has eigenvalues only 0 or 1.

### Level 5 — Solutions

1. **2** — rank(AᵀA) = rank(A) for real A.
2. **λ² − 7λ + 10 = 0 ⇒ λ = 2, 5**.
3. If Av = λv, then A²v = Av ⇒ λ²v = λv ⇒ λ(λ−1) = 0.

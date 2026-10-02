# Determinants — GATE-STYLE PRACTICE

## Level 1

**1.** det [[3,1],[2,4]]?

**2.** det [[1,0,0],[0,2,0],[0,0,5]]?

**3.** If two rows of A are equal, det(A) = ?

### Level 1 — Solutions

1. **12 − 2 = 10**.
2. **1·2·5 = 10**.
3. **0**.

## Level 2

**1.** det(A) = 5, det(B) = 2. Find det(AB).

**2.** det(2A) for 3×3 A with det(A) = 4.

**3.** Is det(A + B) = det(A) + det(B) always true?

### Level 2 — Solutions

1. **10**.
2. **2³ × 4 = 32**.
3. **No** — counterexample: A = I, B = I gives det(A+B) = 4 ≠ 2.

## Level 3

**1.** det [[1,2,3],[0,4,5],[0,0,6]] via triangular form.

**2.** det(A) = 0. Is A invertible?

**3.** Expand det [[2,0,1],[3,0,0],[1,4,2]] along column 2.

### Level 3 — Solutions

1. **24**.
2. **No** — singular.
3. Column 2 has one nonzero: −4 · det [[2,1],[3,0]] = −4·(−3) = **12**.

## Level 4

**1.** det(A) = −3. Find det(A⁻¹) and det(3A) for 2×2 A.

**2.** Eigenvalues 1, 2, 3. Find det(A).

**3.** A is orthogonal 3×3. Possible values of det(A)?

### Level 4 — Solutions

1. det(A⁻¹) = **−1/3**; det(3A) = 9·(−3) = **−27**.
2. **1·2·3 = 6**.
3. **+1 or −1**.

## Level 5

**1.** Prove det(Aᵀ) = det(A) for 2×2.

**2.** If A has a zero row, prove det(A) = 0.

**3.** det(A) = 1, det(B) = 2. Can det(AB) = 5?

### Level 5 — Solutions

1. det(Aᵀ) = ad − bc = det(A).
2. Expand along zero row — all cofactors give 0.
3. **No** — det(AB) = det(A)det(B) = **2**.

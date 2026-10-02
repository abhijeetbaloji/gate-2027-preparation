# Eigenvalues and Eigenvectors — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Solve det(A−λI)=0 for A=[[5,0],[0,2]].

**2.** If Av=3v, what is A²v?

**3.** Sum of eigenvalues of A equals what matrix function?

**4.** det(A)=0 implies which eigenvalue exists?

**5.** Is v=0 ever an eigenvector?

---

## Level 2 — Standard GATE Style

**6.** Find eigenvalues of [[2,1],[1,2]].

**7.** Eigenvector for λ=3 in Q6.

**8.** tr(A)=7, det(A)=12 for 2×2 A. Find eigenvalues.

**9.** Eigenvalues 1,−1,2. Find tr(A) and det(A) for 3×3 A.

**10.** Is [[1,1],[0,1]] diagonalizable?

---

## Level 3 — Multi-Step

**11.** Full eigenanalysis of [[4,1],[2,3]].

**12.** det(A−5I) if eigenvalues of A are 2,3,5,5.

**13.** Symmetric A=[[3,1],[1,3]]. Orthogonal eigenvectors?

**14.** If A³=I for 3×3 A, what can you say about |λ| for eigenvalues?

---

## Level 4 — Trap Questions

**15.** Distinct eigenvalues always imply diagonalizable?

**16.** Real matrix must have real eigenvalues?

**17.** Algebraic mult 2 always means two independent eigenvectors?

**18.** tr(AB) = tr(A)tr(B)?

---

## Level 5 — Challenge

**19.** Prove eigenvectors for distinct eigenvalues are independent (2 eigenvalues case).

**20.** A is 3×3 with char poly λ³−6λ²+11λ−6. Factor and find eigenvalues if A is upper triangular with positive diagonal.

---

## Answers and Explanations

**1.** **λ=5,2**.

**2.** **9v**.

**3.** **tr(A)**.

**4.** **λ=0**.

**5.** **No** (must be nonzero).

**6.** λ²−4λ+3=0 → **1,3**.

**7.** (A−3I)v=0 → **t[1,1]^T**.

**8.** λ²−7λ+12=0 → **3,4**.

**9.** tr=**2**, det=**−2**.

**10.** **No** — one eigenvalue 1, one eigenvector direction.

**11.** λ=5,2; v∝(1,1), v∝(1,−2).

**12.** (2−5)(3−5)(5−5)(5−5)=**0**.

**13.** **(1,1)/√2, (1,−1)/√2**.

**14.** λ³=1 → |λ|=**1**.

**15.** **Yes** for n×n with n distinct eigenvalues.

**16.** **No** — e.g. [[0,−1],[1,0]] has λ=±i.

**17.** **No** — Jordan block counterexample.

**18.** **No**.

**19.** If c₁v₁+c₂v₂=0, A gives c₁λ₁v₁+c₂λ₂v₂=0; subtract λ₁×first → c₂(λ₂−λ₁)v₂=0 → c₂=0 → c₁=0.

**20.** (λ−1)(λ−2)(λ−3)=0 → **1,2,3** on diagonal of upper triangular.

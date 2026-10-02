# LU Decomposition — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** In A = LU, what appears on the diagonal of L?

**2.** What is the first triangular solve after factorizing A = LU?

**3.** U has diagonal 2, 3, 5. What is det(A) if L is unit lower and P = I?

**4.** What does P represent in PA = LU?

**5.** Is L the inverse of U?

---

## Level 2 — Standard GATE Style

**6.** Why does LU fail without pivoting for [[0,1],[1,0]]?

**7.** If A is upper triangular, what are L and U in A = LU?

**8.** What are the sizes of L and U for a 4×4 matrix A?

**9.** Find LU for A = [[2,1],[4,3]] without pivoting.

**10.** Using Q9, solve [[2,1],[4,3]]x = [3,7]ᵀ.

---

## Level 3 — Multi-Step

**11.** Find LU for A = [[1,2,3],[2,5,7],[4,9,10]].

**12.** Compute det(A) from U in Q11.

**13.** Solve Ax = b for b = [6,15,17]ᵀ using LU from Q11.

**14.** After one row swap in 3×3 elimination, how does det(A) change?

**15.** Cost of solving 5 systems with same A but different b after one LU?

---

## Level 4 — Trap Questions

**16.** Advantage of LU over computing A⁻¹ explicitly for 10 different b?

**17.** Is LU unique for every invertible matrix (standard L unit diagonal)?

**18.** Can singular matrix have PA = LU with U having zero diagonal entry?

**19.** det(L) for unit lower triangular L?

**20.** Cholesky A = LLᵀ applies to any square A. True or false?

---

## Level 5 — Challenge

**21.** Prove det(A) = ∏ u_{ii} when A = LU and L is unit lower.

**22.** Factor [[1,1],[1,1.0001]] — discuss pivoting need (conceptual).

**23.** Write L and U for A = [[3,0],[6,2]] and verify A = LU.

**24.** If A = LU and b changes k times, compare flop count to k Gaussian eliminations.

**25.** 3×3 A needs 2 row swaps. U diagonal product is 12. Find |det(A)|.

---

## Answers and Explanations

**1.** **All 1s** (unit lower triangular).

**2.** **Ly = b** (forward substitution on L).

**3.** 2 × 3 × 5 = **30**.

**4.** **Row permutation** / swap record from pivoting.

**5.** **No** — L and U are triangular factors, not inverses of each other.

**6.** **Zero pivot** at position (1,1); cannot divide by 0 for multiplier.

**7.** **L = I**, **U = A**.

**8.** Both **4×4**.

**9.** **L = [[1,0],[2,1]]**, **U = [[2,1],[0,1]]**.

**10.** Ly=b: y=[3,1]; Ux=y: x₂=1, 2x₁+x₂=3 → **x=[1,1]ᵀ**.

**11.** **L = [[1,0,0],[2,1,0],[4,1,1]]**, **U = [[1,2,3],[0,1,1],[0,0,−3]]**.

**12.** 1×1×(−3) = **−3**.

**13.** Ly=b: y=[6,3,−10]; Ux=y: x₃=10/3, x₂=−1/3, x₁=**1** (complete: x=[1,−1/3,10/3]ᵀ).

**14.** det multiplies by **−1** per swap.

**15.** One O(n³) factor + 5·O(n²) solves vs 5·O(n³) — **LU wins**.

**16.** **Reuse factorization** — O(n²) per b vs O(n³) for inverse or full elimination each time.

**17.** **Yes** for invertible A with fixed convention (no pivoting ambiguity); pivoting adds P.

**18.** **Yes** — singular ⇒ zero pivot on U diagonal; det = 0.

**19.** **1** (product of diagonal 1s).

**20.** **False** — Cholesky requires symmetric **positive definite** A.

**21.** det(A)=det(L)det(U)=1·∏u_{ii}.

**22.** Nearly equal rows → small pivot without swap hurts stability; **partial pivoting** recommended.

**23.** ℓ₂₁=6/3=2; U=[[3,0],[0,2]]; L=[[1,0],[2,1]]; verify LU=A.

**24.** LU: ~2n³/3 + k·2n²; k eliminations: k·2n³/3 — LU better when k>1.

**25.** |det(A)| = 2² × 12 = **48** (two swaps → det(P)=1).

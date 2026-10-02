# System of Linear Equations — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Write Ax=b for x+2y=3, 3x−y=1.

**2.** Ax=0 always has which solution?

**3.** If rank(A)=3 and n=3 for square A, how many solutions to Ax=b if consistent?

**4.** What is nullity if rank(A)=2, n=5?

**5.** Can an overdetermined system (m>n) have a unique solution?

---

## Level 2 — Standard GATE Style

**6.** Classify: [[1,2|3],[2,4|6]].

**7.** Classify: [[1,2|3],[2,4|7]].

**8.** Solve: x+y=4, x−y=2.

**9.** Homogeneous: x−2y=0, 2x−4y=0. Describe all solutions.

**10.** rank(A)=2, rank([A|b])=3. Conclusion?

---

## Level 3 — Multi-Step

**11.** Solve by elimination: x+y+z=6, 2y+z=5, z=2.

**12.** For λ, system x+λy=1, λx+y=λ. For which λ unique / infinite / none?

**13.** 3 equations, 4 unknowns, rank=2. How many free variables if consistent?

**14.** Express general solution: x₁+x₂+x₃=0, x₁−x₂=0.

---

## Level 4 — Trap Questions

**15.** 2 equations, 5 unknowns. Must there be infinite solutions?

**16.** det(A)=0 for 3×3 A. Ax=b always has infinite solutions?

**17.** If Ax=b has unique solution, must A be square?

**18.** Same rank(A) for two systems implies same solution set?

---

## Level 5 — Challenge

**19.** Prove: if rank(A)=rank([A|b])=n, solution is unique.

**20.** Find all solutions to [[1,1,1],[2,2,2],[1,2,3]]x = [3,6,6]^T.

---

## Answers and Explanations

**1.** A=[[1,2],[3,−1]], b=[3,1]^T.

**2.** **Trivial x=0**.

**3.** **Unique**.

**4.** **5−2=3**.

**5.** **Yes** if consistent and rank=n (e.g. 3 eqns, 2 unknowns, rank 2).

**6.** rank=1, rank aug=1, n=2 → **infinite**.

**7.** rank=1, rank aug=2 → **no solution**.

**8.** **x=2, y=2**.

**9.** Second eq redundant; x=2y → **all (2t,t)**.

**10.** **No solution** (inconsistent).

**11.** z=2, y=3/2, x=5/2.

**12.** det=1−λ²; λ≠±1 unique; λ=1 infinite; λ=−1 none.

**13.** **4−2=2**.

**14.** x₁=x₂, 2x₁+x₃=0 → **(t,t,−2t)**.

**15.** **No** — may be inconsistent.

**16.** **No** — may be inconsistent if rank([A|b])>rank(A).

**17.** **No** — e.g. full row rank 2×3 with rank=2, n=3 gives unique along consistent b in special cases; actually unique with n columns means rank=n so columns=n; A can be m×n with m>n. Unique ⇒ rank(A)=n; A need not be square (e.g. 3×2 with rank 2 gives unique if consistent).

**18.** **No** — different b.

**19.** n pivot columns ⇒ each x_i determined.

**20.** Row2=2×row1; system consistent; rank=2, n=3 → **x₁=3−t, x₂=t−3, x₃=t** (one free param).

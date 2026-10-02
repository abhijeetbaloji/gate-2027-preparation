# Graphs: Matching — GATE-STYLE PRACTICE

---

## Level 1 — Basic definitions

**Q1.** In K_{4,4}, what is the size of a maximum matching?

**Q2.** How many edges in a perfect matching of a 10-vertex graph?

**Q3.** Maximum matching size in P_5 (path on 5 vertices)?

**Q4.** Is every maximal matching also a maximum matching? (Yes/No + example if No.)

**Q5.** Can K_{1,7} (star with 8 vertices) have a perfect matching?

### Solutions — Level 1

**S1.** min(4,4) = **4**.

**S2.** Perfect matching covers all 10 vertices with disjoint edges → **5 edges**.

**S3.** ⌊5/2⌋ = **2**.

**S4.** **No.** P_4: edge (b,c) alone is maximal but size 1; maximum is 2.

**S5.** **No.** |V| = 8 (even) but only one edge can be in any matching (centre used once) → max size 1.

---

## Level 2 — Bipartite bounds

**Q1.** Bipartite graph with |A| = 5, |B| = 7. Upper bound on maximum matching?

**Q2.** How many perfect matchings in K_{3,3} if vertices on left are labelled and on right labelled?

**Q3.** Maximum matching in K_6 (complete, not bipartite unless stated)?

**Q4.** In K_{2,5}, is the maximum matching also perfect (for the smaller part)?

**Q5.** Matching size in graph with 9 vertices all of degree 1 (disjoint edges only)?

### Solutions — Level 2

**S1.** **5** (min of part sizes).

**S2.** Bijections from 3 left to 3 right → **3! = 6**.

**S3.** K_6: **3** (n/2 for even complete).

**S4.** Max matching size 2; saturates A (size 2) but not all of B → perfect for A side yes, not for whole graph (7 vertices).

**S5.** 9 vertices degree 1 → disjoint edges cover all? 9 odd → cannot perfect; max = **4** edges (8 vertices covered, one isolated).

---

## Level 3 — Hall's theorem

**Q1.** Bipartite: A = {a1,a2,a3}, B = {b1,b2,b3}. Edges: a1–b1, a2–b1, a2–b2, a3–b3. Does a matching saturating A exist?

**Q2.** Same setup but only edges a1–b1, a2–b1, a3–b2. Does matching saturating A exist?

**Q3.** If |A| = |B| = n and Hall holds, what is size of maximum matching?

**Q4.** K_{n,n} always satisfies Hall for left set A. Why?

**Q5.** Give a subset S that violates Hall when a2, a3 share only b1 as neighbour.

### Solutions — Level 3

**S1.** Check S = {a1,a2}: N(S) = {b1,b2}, |N(S)| = 2 ≥ 2 ✓. Full matching exists → **yes**, size 3.

**S2.** S = {a2,a3}: N(S) = {b1,b2}, |N(S)| = 2 < 3? Wait S = {a2,a3}, N = {b1,b2} size 2 < 3 → **Hall fails** → no matching saturating A.

**S3.** **n** (perfect matching).

**S4.** For any S ⊆ A, N(S) = all of B when |S| = n? Actually N(S) has at least |S| because complete to B → |N(S)| = |B| = n ≥ |S|.

**S5.** S = {a2, a3}, N(S) = {b1} → |N(S)| = 1 < 2.

---

## Level 4 — König and vertex cover

**Q1.** Bipartite graph has maximum matching of size 4. Minimum vertex cover size?

**Q2.** In C_4 (cycle of 4), maximum matching size and minimum vertex cover size?

**Q3.** Construct bipartite graph where max matching = 2 and min cover = 2.

**Q4.** Why doesn't König apply to C_3?

**Q5.** If every vertex in A has degree ≥ k, can we conclude matching size ≥ k?

### Solutions — Level 4

**S1.** König → **4**.

**S2.** C_4 is bipartite. Max matching **2**; min cover **2** (take opposite vertices).

**S3.** Example: two disjoint edges K_{2,2} style or 4-cycle — many examples.

**S4.** C_3 not bipartite; max matching 1, min cover 2 — **not equal**.

**S5.** **No.** Star-like from A: all connect to one b ∈ B → matching size 1 only.

---

## Level 5 — Counting and structure

**Q1.** Number of perfect matchings in P_6 (path 1–2–3–4–5–6)?

**Q2.** For n even, does P_n always have a perfect matching?

**Q3.** Maximum matching in complete graph K_n for odd n?

**Q4.** In a tree with 2k vertices, necessary condition for perfect matching?

**Q5.** Jobs J1,J2,J3 and workers W1,W2,W3; J1→W1,W2; J2→W2; J3→W1,W3. Maximum assignment count?

### Solutions — Level 5

**S1.** Only one way to pair along path: (1,2)(3,4)(5,6)? That shares vertex 2. Perfect matching on P_6: **only** {(1,2),(3,4),(5,6)} invalid. Valid: (2,1)(3,4)(5,6) — actually edges (1,2),(3,4),(5,6) are disjoint → **1** perfect matching? Also (1,2),(3,4),(5,6) works. Alternative (2,3),(4,5) leaves 1,6 — no. Only **1** perfect matching: edges 1–2, 3–4, 5–6.

**S2.** **Yes** for n even — pair consecutive vertices.

**S3.** **(n−1)/2**.

**S4.** |V| even necessary; also no **unsaturated** structure — in practice, no leaf attached to degree-1 chain issues; necessary: **|V| even** (not sufficient).

**S5.** Maximum matching size **3** if full assignment exists: J1→W2, J2→W2 conflict. Try J1→W1, J2→W2, J3→W3 → **3** assignments.

---

## GATE Connection recap

- Hall + König: classic bipartite MCQ pair with **Connectivity** (bipartite test).
- K_{n,n} perfect matchings = **n!** links to **Counting** permutations.
- Path matching recurrence connects to **Recurrence Relations**.

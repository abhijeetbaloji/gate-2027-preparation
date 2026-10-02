# Graphs: Colouring — GATE-STYLE PRACTICE

---

## Level 1 — Direct χ values

**Q1.** χ(K_7) = ?

**Q2.** χ(C_6) = ?

**Q3.** χ(C_7) = ?

**Q4.** A tree with 20 vertices (connected acyclic). χ = ?

**Q5.** Empty graph on 5 vertices (no edges). χ = ?

### Solutions — Level 1

**S1.** **7** (complete).

**S2.** Even cycle → bipartite → **2**.

**S3.** Odd cycle → **3**.

**S4.** Tree with n ≥ 2 → **2**.

**S5.** No edges → all same colour → **1**.

---

## Level 2 — Bounds from Δ and cliques

**Q1.** G contains K_5 as subgraph. Lower bound on χ(G)?

**Q2.** Δ(G) = 4. Can χ(G) = 2? Can χ(G) = 5?

**Q3.** For K_n, what is Δ and χ?

**Q4.** Is χ(G) ≤ Δ(G) always?

**Q5.** Greedy colouring uses at most how many colours?

### Solutions — Level 2

**S1.** **χ ≥ 5**.

**S2.** χ = 2 possible if G bipartite (e.g. subgraph of K_{2,2}). χ = 5 possible (e.g. K_5 subgraph forces χ ≥ 5; if G = K_5 then χ = 5).

**S3.** Δ = n−1, χ = **n**.

**S4.** **No** — C_5: Δ = 2, χ = 3.

**S5.** **Δ + 1**.

---

## Level 3 — Bipartite and Brooks

**Q1.** Which have χ = 2? (a) K_{2,3}  (b) C_8  (c) C_9  (d) P_10

**Q2.** Connected graph, Δ = 3, not K_4, not odd cycle. Maximum χ by Brooks?

**Q3.** Why is K_4 an exception to Brooks (Δ = 3 but χ = 4)?

**Q4.** Graph is tree. Is it 2-colourable for n ≥ 2?

**Q5.** ω(G) = 3 means what about χ?

### Solutions — Level 3

**S1.** (a), (b), (d) yes; (c) C_9 odd → χ = 3. Answer: **(a), (b), (d)**.

**S2.** Brooks → **χ ≤ 3**.

**S3.** K_4 is **complete graph** — listed exception in Brooks.

**S4.** **Yes** — trees are bipartite.

**S5.** **χ ≥ 3** (clique of 3 needs 3 colours).

---

## Level 4 — Edge colouring and structure

**Q1.** χ'(K_3) = ? (minimum edge colours)

**Q2.** Δ(K_3) and χ'(K_3) — verify Vizing.

**Q3.** If G is 3-regular and not bipartite, can χ = 2?

**Q4.** Planar graph: maximum χ guaranteed?

**Q5.** Graph: triangle plus one pendant edge attached to a triangle vertex. χ = ?

### Solutions — Level 4

**S1.** Triangle edges pairwise share vertices → **3** colours.

**S2.** Δ = 2? K_3 each vertex degree 2. χ' = **3** = Δ + 1. Vizing allows Δ or Δ+1.

**S3.** **No** — 3-regular connected bipartite would be 2-regular on each part; odd cycle impossible for χ = 2 with odd triangle subgraph.

**S4.** **4** (Four Colour Theorem).

**S5.** Triangle needs 3 colours; pendant edge from one vertex — that vertex already coloured; pendant neighbour gets different colour → still **χ = 3**.

---

## Level 5 — Multi-concept

**Q1.** Construct graph with Δ = 3 and χ = 4.

**Q2.** χ(G) = 2 iff ? (Fill standard iff condition for connected G with edges.)

**Q3.** How many colours needed for K_{2,2,2} (complete tripartite, all parts size 2)?

**Q4.** If χ(G) = k, is G k-regular?

**Q5.** Prove χ(C_{2k+1}) = 3 using odd-cycle argument.

### Solutions — Level 5

**S1.** **K_4** works: Δ = 3, χ = 4.

**S2.** G is **bipartite** (equivalently: **no odd cycle**).

**S3.** Complete tripartite: every part independent, edges between parts → proper 3-colouring (one colour per part) → **χ = 3**.

**S4.** **No** — C_4 has χ = 2, degrees 2; K_4 has χ = 4, not all degree 4 required.

**S5.** Not 2-colourable (odd cycle argument in NOTES). Three colours suffice: colour cycle 1,2,3 around; closes properly. Hence **χ = 3**.

---

## GATE Connection recap

- Bipartite/tree χ = 2 links **Connectivity** and **Matching**.
- Clique bound χ ≥ ω links to subgraph search in MCQs.
- Counting colourings → **Generating Functions** / **Recurrence** for paths and cycles.

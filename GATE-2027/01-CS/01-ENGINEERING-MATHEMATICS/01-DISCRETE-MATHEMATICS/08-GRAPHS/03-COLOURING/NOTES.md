# Graphs: Colouring

## Vertex colouring

A **proper vertex k-colouring** assigns colours {1,…,k} to vertices so **adjacent vertices get different colours**.

- **Chromatic number χ(G):** minimum k for which a proper k-colouring exists.
- **k-colourable:** χ(G) ≤ k.

**Worked example:** C_4 (square): 2-colourable (alternate corners) → **χ = 2**. C_5 (pentagon): not 2-colourable (odd cycle) → need 3 → **χ = 3**.

---

## Lower and upper bounds

**Lower bound:** If G contains clique K_r as subgraph, then **χ(G) ≥ r** (all clique vertices pairwise adjacent).

**Upper bound (greedy):** Order vertices arbitrarily; colour each with smallest available colour. Uses at most **Δ(G) + 1** colours, where **Δ(G)** = maximum degree.

**Worked example:** K_4 has Δ = 3 but **χ = 4** — greedy bound is not always tight; clique gives exact χ = 4 here.

---

## Bipartite graphs and 2-colouring

**Theorem:** Non-empty G is bipartite **iff** χ(G) = 2 **iff** G has no odd cycle.

**Trees** (with ≥ 2 vertices): bipartite → **χ = 2**. Single isolated vertex: **χ = 1**.

**Connection to Matching:** 2-colouring partitions V into two independent sets — same partition used in bipartite matching.

---

## Brooks' theorem

If G is connected, simple, not complete, and not an odd cycle, then:

> **χ(G) ≤ Δ(G)**

**Exceptions where χ = Δ + 1:**
- Complete graphs K_n: χ = n = Δ + 1 (for n ≥ 2, Δ = n−1)
- Odd cycles C_{2k+1}: Δ = 2, χ = 3 = Δ + 1

**Worked example:** Δ = 3, not K_4, connected → Brooks → χ ≤ 3. Could be 2 or 3 depending on structure.

---

## Special graph families

| Graph | χ(G) |
|-------|------|
| K_n | n |
| Bipartite (|E| > 0) | 2 |
| Odd cycle C_{2k+1} | 3 |
| Even cycle C_{2k} | 2 |
| Tree (n ≥ 2 vertices) | 2 |
| Empty (no edges), n vertices | 1 |

---

## Edge colouring (awareness)

**Edge k-colouring:** adjacent edges get different colours.

**Chromatic index χ'(G):** minimum colours for edges.

**Vizing's theorem:** For simple G, χ'(G) is **Δ(G)** or **Δ(G) + 1**.

GATE may ask: "Can edges of K_3 be coloured with 2 colours?" No — triangle needs **3** = Δ + 1.

---

## Planar graphs

**Four Colour Theorem:** Every planar graph is **4-colourable** (χ ≤ 4). GATE: know the statement; proofs not required.

---

## Greedy vs optimal

Greedy order affects colour count. **χ may be less than Δ + 1** (e.g. odd cycle: Δ = 2, χ = 3).

**Trap:** χ ≤ Δ always? **False** — C_5 has Δ = 2, χ = 3.

---

## GATE Connection

| Link | Idea |
|------|------|
| **Connectivity → Colouring** | Bipartite ⇔ no odd cycle ⇔ χ = 2 |
| **Colouring → Counting** | Number of proper colourings with k colours relates to **chromatic polynomial** (awareness); k-colourings of tree often via **recurrence** |
| **χ + clique** | ω(G) = clique number; χ ≥ ω |
| **Trees** | χ = 2 (except single vertex) — fast MCQ |

**Combinatorics link:** Counting proper 2-colourings of a path uses **2 × 2^(n−1)** for connected path with fixed ends — ties to **Generating Functions** for constrained assignments.

---

## Derivation sketch: odd cycle needs 3 colours

C_{2k+1}: assume 2-colouring. Walk around cycle; colours must alternate A,B,A,B,… Returning to start after odd length forces same colour as start on adjacent vertex — contradiction. Hence **χ ≥ 3**; 3 colours suffice → **χ = 3**.

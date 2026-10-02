# Graphs: Matching

## What is a matching?

A **matching** M ⊆ E is a set of edges such that **no two edges share a vertex** (vertex-disjoint edges).

- **Matching number ν(G):** size of a **maximum matching** (largest possible).
- **Maximal matching:** cannot add any edge without violating disjointness — **not necessarily maximum**.
- **Perfect matching:** every vertex is incident to exactly one edge in M ⇒ |M| = |V|/2, so **|V| must be even**.

**Worked example:** In P_4 (path a–b–c–d), M = {(a,b), (c,d)} is perfect matching of size 2. M = {(b,c)} is maximal of size 1 but not maximum.

---

## Bipartite graphs

**Bipartite graph:** V = A ∪ B, A ∩ B = ∅, every edge connects A to B.

- **Complete bipartite K_{m,n}:** every vertex in A connected to every vertex in B; |E| = mn.
- **Bipartite test:** G is bipartite iff it has **no odd cycle** (from Connectivity).

**Why bipartite matters for matching:** Many assignment problems are naturally "left = jobs, right = workers" → bipartite.

---

## Hall's Marriage Theorem

For bipartite graph with parts A (left) and B (right), a matching that **saturates A** (covers every vertex of A) exists **iff**:

> For every subset S ⊆ A: |N(S)| ≥ |S|

where **N(S)** = neighbours of S in B.

**Perfect matching in K_{n,n}:** |N(S)| = n ≥ |S| for all S → always exists; size **n**.

**Worked example:** A has 3 vertices, B has 3. Edges: a1→b1, a1→b2, a2→b2, a3→b3. For S = {a1, a2}, N(S) = {b1, b2}, |N(S)| = 2 ≥ 2 ✓. Hall holds → matching saturating A exists (size 3).

**Failure example:** S = {a1, a2} but N(S) = {b1} only → |N(S)| = 1 < 2 → **no** matching saturating A.

---

## König's theorem (bipartite)

In a bipartite graph:

> Size of **maximum matching** = size of **minimum vertex cover**

**Vertex cover:** set of vertices touching every edge.

This dual relationship is classic in GATE "min cover / max matching" questions on small bipartite drawings.

---

## Matching bounds

| Graph | Maximum matching size |
|-------|----------------------|
| K_{m,n} | min(m, n) |
| P_n (path) | ⌊n/2⌋ |
| K_n (n even) | n/2 |
| K_n (n odd) | (n−1)/2 |
| Star K_{1,k} | 1 |

**Perfect matching necessary condition:** |V| even and |M| = |V|/2. **Not sufficient** (e.g. star on 6 vertices: max matching = 1).

---

## Augmenting paths (concept)

A matching is **maximum** iff there is **no augmenting path** — an alternating path (matched/unmatched edges) from an unmatched vertex to another unmatched vertex. GATE rarely requires full algorithm; small graphs: draw and try.

---

## GATE Connection

| Link | Idea |
|------|------|
| **Connectivity → Bipartite** | No odd cycle characterisation |
| **Matching → Counting** | Number of perfect matchings in K_{n,n} is **n!** (assign bijection A → B) |
| **Matching → Algorithms** | Assignment problem, Hopcroft–Karp (awareness) |
| **Matching ↔ Cover (König)** | Min cover size = max matching in bipartite |

**Graphs → Trees → Counting:** A tree on 2k vertices may or may not have a perfect matching; counting matchings in structured graphs uses **recurrence** (path P_n: Fibonacci-type).

---

## Common GATE traps

- **Maximum ≠ maximal** — always read which is asked.
- Perfect matching requires **|V| even**; also structural constraints (star fails).
- In K_{m,n}, max matching = **min(m,n)**, not always perfect unless m = n.
- Hall's condition: check **worst subset S**, not just total degrees.

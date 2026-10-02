# Graphs: Connectivity — GATE-STYLE PRACTICE

---

## Level 1 — Definitions and direct formulas

**Q1.** A simple undirected graph has 8 vertices and degree sequence 4, 4, 3, 3, 2, 2, 2, 2. How many edges does it have?

**Q2.** How many edges does a tree with 15 vertices have?

**Q3.** A graph on 6 vertices has no edges. How many connected components?

**Q4.** Which of the following degree sequences is impossible for a simple graph?
(a) 2, 2, 2, 2  (b) 3, 3, 2, 2, 2  (c) 3, 3, 3, 1, 1  (d) 4, 2, 2, 2, 2, 2

**Q5.** A connected acyclic graph on n vertices has how many edges? (Express in n.)

### Solutions — Level 1

**S1.** Sum of degrees = 4+4+3+3+2+2+2+2 = 22. Handshaking: 2|E| = 22 → **|E| = 11**.

**S2.** Tree: |E| = |V| − 1 = 15 − 1 = **14**.

**S3.** No edges → every vertex isolated → **6 components**.

**S4.** (c): three odd degrees (3,3,3,1,1 → four odd) — wait count: 3,3,3,1,1 = five odd numbers → **impossible**. (b) has two odd (3,3) → OK. Answer: **(c)**.

**S5.** Connected acyclic = tree → **n − 1**.

---

## Level 2 — Tree and forest reasoning

**Q1.** A simple graph has 10 vertices and 15 edges. Can it be a tree? Can it be a forest?

**Q2.** A graph has 7 vertices, 6 edges, and is acyclic. Is it necessarily a tree?

**Q3.** Prove or disprove: every tree with at least 2 vertices has at least 2 leaves.

**Q4.** How many edges must be added to connect 5 isolated vertices into one connected graph (minimum)?

**Q5.** A forest on 12 vertices has 9 edges. How many connected components?

### Solutions — Level 2

**S1.** Tree needs 9 edges → **not a tree**. Forest on 10 vertices has at most 10 − 1 = 9 edges if connected; with 15 edges it must have a cycle → **not a forest** either (forest = acyclic).

**S2.** Acyclic with 6 = 7 − 1 edges. If disconnected, edges ≤ |V| − (#components) < 6. So must be connected → **yes, it is a tree**.

**S3.** **True.** In any tree n ≥ 2, sum of degrees = 2(n−1). If at most 1 leaf, all other n−1 vertices have degree ≥ 2, so sum ≥ 1 + 2(n−1) = 2n − 1 > 2(n−1) for n ≥ 2. Contradiction.

**S4.** Need spanning tree on 5 vertices → **4 edges** minimum.

**S5.** Forest: |E| = |V| − k → 9 = 12 − k → k = **3 components**.

---

## Level 3 — Paths, cycles, bipartite

**Q1.** Which graphs are bipartite: (a) C_4  (b) C_5  (c) K_2  (d) K_3?

**Q2.** A graph is connected and has 20 vertices and 19 edges. Must it be a tree?

**Q3.** Can a simple graph with 5 vertices have 10 edges?

**Q4.** If a graph has exactly one cycle and is connected, how many edges in terms of vertices n?

**Q5.** A tree is bipartite. What is its chromatic number if it has at least 2 vertices?

### Solutions — Level 3

**S1.** (a) C_4 even cycle → **bipartite**. (b) C_5 odd → **not**. (c) K_2 → **bipartite**. (d) K_3 odd cycle → **not**. Answer: **(a), (c)**.

**S2.** Connected with |E| = |V| − 1 → **yes, always a tree** (unique characterisation).

**S3.** Max edges = 5×4/2 = 10 → **yes**, K_5.

**S4.** Connected + one cycle: unicyclic. |E| = |V| (n edges, n vertices — one extra edge beyond tree).

**S5.** Bipartite non-empty → **χ = 2**.

---

## Level 4 — Euler trails, degree sequences, spanning trees

**Q1.** Does K_5 have an Euler circuit?

**Q2.** A connected graph has exactly two vertices of odd degree. What type of Euler trail exists?

**Q3.** How many labelled spanning trees does K_3 have? (Use Cayley or count directly.)

**Q4.** Degree sequence 5, 3, 3, 3, 2, 2, 2 — is it realisable by a simple graph?

**Q5.** A bridge in a connected graph: can it belong to a cycle?

### Solutions — Level 4

**S1.** K_5: each vertex degree 4 (even), connected → **Euler circuit exists**.

**S2.** Connected + exactly 2 odd degrees → **Euler trail** (open, not circuit) starting at one odd vertex, ending at the other.

**S3.** Cayley on 3 labels: 3^(3−2) = **3**. Direct: three possible edges in span tree of K_3.

**S4.** Sum = 5+3+3+3+2+2+2 = 20 → 10 edges. Odd count: 5,3,3,3 = four odd → **realisable** (even number of odd degrees).

**S5.** **No.** Removing a bridge disconnects; cycle edge removal keeps graph connected — bridge cannot lie on a cycle.

---

## Level 5 — Multi-concept GATE style

**Q1.** Let T be a tree with n ≥ 2 vertices. Maximum possible diameter (longest shortest path) for a fixed n occurs for which tree shape? For n = 7, what is that diameter?

**Q2.** A simple graph on 8 vertices has 7 edges and is connected. How many cycles can it have at minimum and maximum?

**Q3.** Prove: if G is bipartite and |E| > 0, then χ(G) = 2.

**Q4.** Number of non-isomorphic **unlabelled** trees on 4 vertices?

**Q5.** A connected graph has all degrees even except vertices a and b. Describe an Euler trail and its endpoints.

### Solutions — Level 5

**S1.** Maximum diameter for fixed n is **path graph P_n** (linear chain). For n = 7, diameter = **6**.

**S2.** Connected, 8 vertices, 7 edges → **tree** (|E| = |V| − 1). Trees have **0 cycles** (min = max = 0).

**S3.** Bipartite V = A ∪ B: colour A with colour 1, B with colour 2. Adjacent vertices in different parts → valid 2-colouring. Need ≥ 2 colours if edge exists. So **χ = 2**.

**S4.** Four vertices: only two shapes — **path P_4** and **star K_{1,3}** → **2** non-isomorphic trees.

**S5.** Graph has Euler **trail** (not circuit). Trail uses every edge once, starts at **a** (odd degree) and ends at **b** (other odd degree). All other vertices even → traversable in one trail.

---

## GATE Connection recap

- Level 1–2: handshaking, trees, components — foundation for algorithm analysis (DFS/BFS).
- Level 3: bipartite ↔ no odd cycle — bridges to **Matching** and **Colouring**.
- Level 4–5: Euler conditions, Cayley n^(n−2) — links to **Combinatorics / Counting**.

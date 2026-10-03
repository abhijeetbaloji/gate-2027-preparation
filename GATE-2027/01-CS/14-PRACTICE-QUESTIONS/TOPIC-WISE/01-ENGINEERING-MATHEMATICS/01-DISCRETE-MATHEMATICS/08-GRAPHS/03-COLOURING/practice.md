# Graphs: Colouring — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The chromatic number of the complete graph K_5 is

A. 4
B. 5
C. 6
D. 10

---

## Q2 — MCQ

The chromatic number of the cycle C_7 is

A. 2
B. 3
C. 4
D. 7

---

## Q3 — MSQ

Select all that apply.

A. Every tree with at least 2 vertices has chromatic number 2
B. A graph with 5 vertices and no edges has chromatic number 1
C. Every bipartite graph with at least one edge has chromatic number 2
D. The cycle C_4 has chromatic number 3

---

## Level 2 — Standard GATE Style

## Q4 — NAT

What is the sum of the chromatic numbers of the cycles C_5 and C_6?

---

## Q5 — MCQ

Let G be a connected simple graph that is neither a complete graph nor an odd cycle, and suppose the maximum degree of G is 4. Which one of the following follows?

A. The chromatic number of G is at most 4
B. The chromatic number of G is exactly 5
C. The chromatic number of G is at most 3
D. The chromatic number of G is exactly Δ(G) + 1

---

## Q6 — MSQ

Select all that apply.

A. The chromatic number of a graph is at least the number of vertices in a largest clique
B. Every graph G satisfies χ(G) ≤ Δ(G) + 1, where Δ(G) is the maximum degree
C. Every connected simple graph G satisfies χ(G) ≤ Δ(G)
D. Every planar graph has chromatic number at most 4

---

## Level 3 — Multi-Step

## Q7 — MCQ

Suppose a simple graph G contains a triangle. Which one of the following must be true?

A. χ(G) ≥ 3
B. χ(G) = 2
C. G is bipartite
D. χ(G) = 1

---

## Q8 — NAT

Let G be a connected simple graph on 8 vertices with maximum degree 3, and suppose G contains a triangle. What is χ(G)?

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Which one of the following is true?

A. Every graph G satisfies χ(G) ≤ Δ(G)
B. The cycle C_5 satisfies χ(C_5) = Δ(C_5)
C. The cycle C_5 satisfies χ(C_5) = Δ(C_5) + 1
D. Every tree on at least 2 vertices satisfies χ = Δ

---

## Q10 — MSQ

Select all that apply.

A. Every run of the greedy colouring algorithm uses exactly χ(G) colours
B. The complete graph K_n needs n colours in a proper vertex colouring
C. A single vertex has chromatic number 1
D. The Four Colour Theorem says that every planar graph has chromatic number at most 3

---

## Level 5 — Challenge

## Q11 — NAT

Let W be the graph whose vertices are c, v1, v2, v3, v4, and v5. The edges are the cycle v1—v2—v3—v4—v5—v1 together with an edge from c to each vi. What is χ(W)?

---

## Q12 — MCQ

The chromatic index (edge-chromatic number) of the simple graph K_4 is

A. 2
B. 3
C. 4
D. 6

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | MSQ | A, B, C |
| 4 | NAT | 5 |
| 5 | MCQ | A |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 3 |
| 9 | MCQ | C |
| 10 | MSQ | B, C |
| 11 | NAT | 4 |
| 12 | MCQ | B |

## Detailed Solutions

### Q1

Answer: B

In K_5 every pair of vertices is adjacent, so all five vertices need different colours. Five colours are also enough: give each vertex its own colour. Thus χ(K_5) = 5. In general χ(K_n) = n. The number 4 is Δ(K_5), since each vertex has degree 4, and it is one colour too few. The number 6 is Δ + 2. The number 10 is the number of edges, 5 × 4 / 2 = 10, which is not a vertex-colour count.

### Q2

Answer: B

The cycle C_7 has odd length. Suppose two colours alternated around the cycle. After seven steps the colour required next to the start would equal the colour of the start, but those two vertices are adjacent. So C_7 is not 2-colourable, and χ(C_7) ≥ 3. Three colours suffice for any odd cycle: alternate two colours along a path of length 6, and use the third colour on the remaining vertex. Thus χ(C_7) = 3. The degree is Δ = 2, so this is the case χ = Δ + 1. The cycle is not complete, so the chromatic number is not 7.

### Q3

Answer: A, B, C

A tree with at least two vertices is connected and has no cycle, so it has no odd cycle. It is bipartite and has an edge, and therefore χ = 2. A graph with no edges has no adjacency restriction. One colour is a proper colouring, and zero colours do not colour the vertices, so χ = 1.

A bipartite graph with at least one edge is 2-colourable by definition of the two parts, and it is not 1-colourable because that edge has two endpoints. Thus its chromatic number is 2. The cycle C_4 is an even cycle, hence bipartite, and χ(C_4) = 2, not 3.

### Q4

Answer: 5

The cycle C_5 has odd length, so χ(C_5) = 3. The cycle C_6 has even length, so it is bipartite and χ(C_6) = 2. The required sum is

3 + 2 = 5.

Swapping the two values, or treating every cycle as 2-colourable, gives 4. Treating both as odd cycles gives 6. The lengths 5 and 6 are not themselves the chromatic numbers.

### Q5

Answer: A

Brooks’ theorem says that a connected simple graph which is not complete and not an odd cycle satisfies χ(G) ≤ Δ(G). Here Δ(G) = 4, so χ(G) ≤ 4.

The bound is not forced to be an equality. A tree of maximum degree 4 meets the hypotheses and has chromatic number 2, so χ(G) need not be 5 and need not equal Δ(G) + 1.

It also need not be at most 3. Delete one edge from K_5. The graph remains connected and simple, it is not complete, and it is not a cycle. The two endpoints of the deleted edge have degree 3, and the other three vertices keep degree 4, so the maximum degree is 4. Any four vertices that include at most one endpoint of the deleted edge still induce a copy of K_4, so χ ≥ 4. Hence χ = 4, which is greater than 3.

### Q6

Answer: A, B, D

Every pair of vertices in a clique is adjacent, so those vertices all receive different colours. If the largest clique has r vertices, then χ(G) ≥ r.

The greedy algorithm colours the vertices in some order and gives each vertex the smallest colour not used on an already coloured neighbour. A vertex has at most Δ(G) neighbours, so at most Δ(G) colours are forbidden and a colour among 1, 2, …, Δ(G) + 1 is available. Hence χ(G) ≤ Δ(G) + 1.

The stronger bound χ ≤ Δ fails for complete graphs and for odd cycles. For K_2, Δ = 1 and χ = 2. The Four Colour Theorem states that every planar graph is 4-colourable, so χ ≤ 4. It does not claim the sharper bound 3.

### Q7

Answer: A

A triangle is a clique K_3. All three of its vertices are pairwise adjacent, so they need three different colours. Therefore χ(G) ≥ 3. The graph may need more than 3 colours, so equality with 3 is not guaranteed, and equality with 1 or 2 is impossible. A graph with a triangle has an odd cycle, so it is not bipartite.

### Q8

Answer: 3

The graph contains a triangle, so χ(G) ≥ 3, as in the clique bound for K_3.

Brooks’ theorem gives the matching upper bound. The graph is connected and simple. It is not an odd cycle: an odd cycle has maximum degree 2, while Δ(G) = 3, and 8 is even anyway. It is not a complete graph: the complete graph on 8 vertices has degree 7, not 3. Brooks’ theorem therefore yields χ(G) ≤ Δ(G) = 3.

Combining the two bounds, χ(G) = 3. The greedy estimate Δ + 1 = 4 is only an upper bound. The presence of a triangle rules out 2, which would be the chromatic number of a bipartite graph.

### Q9

Answer: C

Every vertex of C_5 has degree 2, so Δ(C_5) = 2. An odd cycle is not 2-colourable, and three colours are enough, so χ(C_5) = 3. That is exactly Δ(C_5) + 1 = 2 + 1 = 3, and it is not equal to Δ(C_5).

The same cycle is a counterexample to A: χ = 3 > 2 = Δ. A tree on at least two vertices has χ = 2, but its maximum degree can be larger. The star K_{1,4} is a tree with Δ = 4 and χ = 2, so χ and Δ need not be equal.

### Q10

Answer: B, C

In K_n every vertex is adjacent to every other vertex, so χ(K_n) = n. A single vertex has no incident edge. Colouring it with one colour is proper, so its chromatic number is 1. The empty graph on more than one vertex also has chromatic number 1; the one-vertex case is included.

Greedy colouring depends on the order of the vertices. It never uses more than Δ + 1 colours, but a poor order can use more colours than χ(G). It is an upper bound, not an exact computation of the chromatic number.

The Four Colour Theorem says that every planar graph satisfies χ ≤ 4. Replacing 4 by 3 is false: K_4 is planar and has chromatic number 4.

### Q11

Answer: 4

The outer cycle v1—v2—v3—v4—v5—v1 is a copy of C_5, so it is not 2-colourable. In any proper colouring of W, the five outer vertices therefore use at least three colours. The centre c is adjacent to every outer vertex, so c is adjacent to at least one vertex of each of those three colours. The centre needs a fourth colour. Hence χ(W) ≥ 4.

Four colours are enough. Colour the outer C_5 properly with colours 1, 2, and 3, which is possible, and colour c with colour 4. The new colour differs from every neighbour of c. Thus χ(W) = 4.

Three colours are enough for C_5 alone and are not enough once the centre is added. The graph is not complete: v1 is not adjacent to v3, for example, so the chromatic number is not 6.

### Q12

Answer: B

The graph K_4 has 4 vertices and 4 × 3 / 2 = 6 edges. Each vertex has degree 3, so Δ = 3. Vizing’s theorem says that the edge-chromatic number of a simple graph is either Δ or Δ + 1, so it is 3 or 4. A single colour class is a matching. In K_4 a matching has at most 2 edges, because 4 vertices give at most two disjoint edges. Covering 6 edges therefore needs at least 6 / 2 = 3 colours.

Three colours are achievable by this partition into perfect matchings, with vertices labelled 1, 2, 3, 4:

- colour 1: {1—2, 3—4}
- colour 2: {1—3, 2—4}
- colour 3: {1—4, 2—3}

These six edges are all the edges of K_4. At each vertex the three incident edges receive colours 1, 2, and 3, so adjacent edges have different colours. The edge-chromatic number is exactly 3. It is not the vertex chromatic number 4, and it is not the number of edges.

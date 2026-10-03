# Graphs: Connectivity — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which one of the following is correct for an undirected graph?

A. A path may repeat vertices, but it may not repeat edges
B. A trail may repeat edges
C. A path has no repeated vertex
D. A cycle in a simple graph may have length 2

---

## Q2 — MCQ

A tree on 9 vertices has

A. 8 edges
B. 9 edges
C. 10 edges
D. 36 edges

---

## Q3 — MSQ

Select all that apply.

A. In every undirected graph, the sum of the vertex degrees equals twice the number of edges
B. In every undirected graph, the number of odd-degree vertices is even
C. Every connected graph on n vertices, with n ≥ 1, has at least n edges
D. The complete graph K_n has n(n − 1)/2 edges

---

## Level 2 — Standard GATE Style

## Q4 — NAT

A simple undirected graph has degree sequence 4, 3, 3, 2, 2, 2. How many edges does it have?

---

## Q5 — MCQ

A simple undirected graph has 6 vertices and 5 edges, and it contains no cycle. Which one of the following is true?

A. The graph is a tree
B. The graph is disconnected
C. The graph contains a cycle
D. The graph has exactly two connected components

---

## Q6 — MSQ

A connected simple undirected graph has degree sequence 1, 1, 2, 2, 2. Select all that apply.

A. The graph has an Euler trail
B. The graph has an Euler circuit
C. The graph has exactly two vertices of odd degree
D. The graph is a tree

---

## Level 3 — Multi-Step

## Q7 — NAT

A forest has 20 vertices and 4 connected components. How many edges does it have?

---

## Q8 — MCQ

Let T be a tree on 6 vertices. Which one of the following is true?

A. T has exactly one bridge
B. Every edge of T is a bridge
C. T has no cut vertex
D. T contains a cycle

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Let G be a simple undirected graph with 8 vertices and 7 edges. Which one of the following is true?

A. G is necessarily a tree
B. If G is connected, then G is a tree
C. G necessarily contains a cycle
D. G is necessarily disconnected

---

## Q10 — MSQ

Select all that apply.

A. Every undirected graph in which all vertex degrees are even has an Euler circuit
B. No bridge of an undirected graph lies on a cycle
C. The star K_{1,5} has exactly five vertices of degree 1
D. Every weakly connected directed graph is strongly connected

---

## Level 5 — Challenge

## Q11 — NAT

How many distinct trees are there on 5 labelled vertices?

---

## Q12 — MCQ

Which one of the following graphs is bipartite?

A. A cycle of length 7
B. A cycle of length 6
C. The complete graph K_3
D. A graph that contains a triangle

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MCQ | A |
| 3 | MSQ | A, B, D |
| 4 | NAT | 8 |
| 5 | MCQ | A |
| 6 | MSQ | A, C, D |
| 7 | NAT | 16 |
| 8 | MCQ | B |
| 9 | MCQ | B |
| 10 | MSQ | B, C |
| 11 | NAT | 125 |
| 12 | MCQ | B |

## Detailed Solutions

### Q1

Answer: C

A walk may repeat vertices and edges. A trail is a walk with no repeated edge, so vertices may still repeat; B reverses that restriction. A path is a trail with no repeated vertex. In a simple graph a cycle is a closed path of length at least 3. Length 2 would require two distinct edges between the same pair, which a simple graph does not have, or a repeated edge, which a path does not use.

### Q2

Answer: A

A tree on n vertices is connected and acyclic, and it has exactly n − 1 edges. For n = 9 the edge count is 8. The count n = 9 is one edge too many and would force a cycle in a connected graph. The count 10 is n + 1. The count 36 is the number of edges in K_9, since 9 × 8 / 2 = 36, which is the maximum for a simple graph on 9 vertices, not the tree count.

### Q3

Answer: A, B, D

Each edge contributes 2 to the degree sum, once at each end, so the sum of degrees is 2|E|. A sum of integers is even if and only if an even number of the summands are odd, so the number of odd-degree vertices is even.

A connected graph on n vertices has at least n − 1 edges, with equality for trees. It does not need n edges. The complete graph K_n joins every unordered pair of distinct vertices, and there are n(n − 1)/2 such pairs.

### Q4

Answer: 8

Add the degrees:

4 + 3 + 3 + 2 + 2 + 2 = 16.

By the handshaking lemma, 2|E| = 16, so |E| = 8. The two degrees equal to 3 are the only odd degrees, and two is even, so the sequence is not immediately impossible. Dividing by 2 only once is required; reporting the degree sum 16 as the number of edges counts each edge twice.

### Q5

Answer: A

The graph is acyclic and has |E| = 6 − 1 = 5. An acyclic graph is a forest, and a forest with k components and n vertices has n − k edges. Here 5 = 6 − k, so k = 1. The graph is connected and acyclic, which is the definition of a tree. The same conclusion is the characterisation “acyclic and |E| = |V| − 1”.

Option C contradicts the hypothesis that there is no cycle. A tree has one component, so B and D are false.

### Q6

Answer: A, C, D

The sequence has five entries, so the graph has 5 vertices. The degree sum is 1 + 1 + 2 + 2 + 2 = 8, and therefore |E| = 4. A connected graph with |E| = |V| − 1 is a tree. The two vertices of degree 1 are the leaves, and the other three vertices have degree 2, so the tree is a path of length 4.

That path uses every edge exactly once and has different endpoints, so it is an Euler trail. It is not closed. Equivalently, a connected graph has an Euler circuit only when every degree is even. Here exactly two degrees are odd, so there is an Euler trail and there is no Euler circuit. All-even degrees are what B would need, and this sequence does not have them.

### Q7

Answer: 16

A forest is an acyclic graph. If it has n vertices and k components, each component is a tree, so the components with n_i vertices contribute n_i − 1 edges. Summing gives

|E| = (n_1 − 1) + … + (n_k − 1) = n − k.

Here n = 20 and k = 4, so |E| = 20 − 4 = 16. Using n − 1 = 19 would be correct for a single tree, not for four components. Using k − 1, or n + k, answers a different counting problem.

### Q8

Answer: B

In a tree there is a unique simple path between any two vertices. Removing an edge destroys the unique path between its endpoints, so the tree falls into two components. Every edge is therefore a bridge. A tree on 6 vertices has 5 edges, so it has five bridges, not one.

A tree with at least three vertices has a vertex that is not a leaf. Removing such a vertex disconnects the tree, so T has a cut vertex. Option C would be appropriate only for a single vertex or a single edge. Option D contradicts the definition of a tree.

### Q9

Answer: B

One characterisation of a tree is “connected, with |E| = |V| − 1”. This graph has 8 vertices and 7 edges. If it is connected, that characterisation says it is a tree.

Connectedness was not given, so A is false. A concrete disconnected example is a 7-vertex graph consisting of a triangle with trees attached so that the component has 7 edges, together with an isolated vertex: 8 vertices, 7 edges, one cycle, and two components. Thus C and D are also not forced. The connected case and the disconnected case are both possible; only the implication in B holds for every such G.

### Q10

Answer: B, C

If an edge lies on a cycle, deleting it leaves the rest of that cycle as a path between its endpoints, so the number of components does not rise. A bridge is an edge whose deletion does increase the number of components. Therefore a bridge lies on no cycle.

The star K_{1,5} has one central vertex joined to five leaves and no other edges. Those five leaves are exactly the vertices of degree 1, and the centre has degree 5.

All degrees even is not enough for an Euler circuit: the graph must also be connected. Two disjoint copies of a triangle have all degrees equal to 2 and no single trail that uses every edge of both components. A directed path a → b → c is weakly connected, but there is no directed path from c back to a, so it is not strongly connected.

### Q11

Answer: 125

Cayley’s formula says that the number of distinct trees on n labelled vertices is n^(n − 2). For n = 5,

5^(5 − 2) = 5^3 = 125.

The count 5 − 1 = 4 is the number of edges in each such tree, not the number of trees. The count 5! = 120 is the number of ways to order five labels, which is close to 125 but is not the tree count. The formula is for labelled vertices; unlabelled trees on 5 vertices are fewer.

### Q12

Answer: B

A graph is bipartite if and only if it has no odd cycle. A cycle of length 6 is itself an even cycle, so it is bipartite: the two colour classes alternate around the cycle, and they are independent sets. A cycle of length 7 is an odd cycle. The graph K_3 is a triangle, which is an odd cycle. Any graph that contains a triangle contains an odd cycle, so it is not bipartite.

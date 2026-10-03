# Graphs: Matching — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which one of the following is the definition of a matching in an undirected graph?

A. A set of edges in which some vertex may lie on two of the edges
B. A set of edges in which no two edges share a vertex
C. A set of edges that together touch every vertex
D. A cycle that passes through every vertex

---

## Q2 — MSQ

Select all that apply.

A. If a graph has a perfect matching, then it has an even number of vertices
B. Every maximal matching is a maximum matching
C. The path on 4 vertices has a perfect matching
D. The star K_{1,3} has a perfect matching

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

The size of a maximum matching in the complete bipartite graph K_{4,7} is

A. 4
B. 7
C. 11
D. 28

---

## Q4 — NAT

Let P_9 be the path graph on 9 vertices. What is the size of a maximum matching in P_9?

---

## Q5 — MCQ

The number of perfect matchings in the complete bipartite graph K_{3,3} is

A. 3
B. 6
C. 9
D. 27

---

## Level 3 — Multi-Step

## Q6 — MSQ

Let G be the bipartite graph with parts {p, q, r} and {x, y, z} and edges p—x, q—x, r—y, and r—z. Select all that apply.

A. The set {p, q} violates Hall’s condition
B. G has a matching that saturates {p, q, r}
C. A maximum matching in G has size 2
D. A minimum vertex cover of G has size 2

---

## Q7 — NAT

Let H be the bipartite graph with parts {1, 2, 3} and {a, b} and edges 1—a, 2—a, 2—b, and 3—b. What is the size of a minimum vertex cover of H?

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

The size of a maximum matching in the complete graph K_5 is

A. 2
B. 3
C. 5
D. 10

---

## Q9 — MSQ

Select all that apply.

A. K_{3,5} has a perfect matching
B. A maximum matching in K_{3,5} has size 3
C. In every undirected graph, the size of a maximum matching equals the size of a minimum vertex cover
D. There exists a graph with a maximal matching that is strictly smaller than some maximum matching

---

## Level 5 — Challenge

## Q10 — MCQ

Let G be the bipartite graph with parts {1, 2, 3} and {a, b, c} and edges 1—a, 1—b, 2—a, 2—b, 2—c, and 3—c. The number of perfect matchings in G is

A. 0
B. 1
C. 2
D. 6

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C |
| 3 | MCQ | A |
| 4 | NAT | 4 |
| 5 | MCQ | B |
| 6 | MSQ | A, C, D |
| 7 | NAT | 2 |
| 8 | MCQ | A |
| 9 | MSQ | B, D |
| 10 | MCQ | C |

## Detailed Solutions

### Q1

Answer: B

A matching is a set of edges with no two sharing a vertex. The edges are vertex-disjoint; they do not have to cover every vertex. A matching that does cover every vertex is the special case of a perfect matching. A cycle through every vertex is a Hamilton cycle, which uses two edges at every vertex and is not a matching.

### Q2

Answer: A, C

A perfect matching pairs the vertices, so each edge accounts for two vertices and no vertex is left over. The number of vertices must be even.

Label the path on 4 vertices a—b—c—d. The set {a—b, c—d} is a matching, and it covers every vertex, so it is a perfect matching of size 2.

A maximal matching cannot be extended by another edge, but a different matching may still be larger. On this same path, {b—c} is maximal: both a—b and c—d touch b—c, so neither can be added. Its size is 1, which is less than 2. Thus maximal does not mean maximum.

The star K_{1,3} has 4 vertices, an even number, but every edge uses the centre. A matching can contain only one edge, while a perfect matching would need 4/2 = 2 edges. Even order is necessary and not sufficient.

### Q3

Answer: A

In K_{m,n} every vertex on the left is joined to every vertex on the right, and a matching can take at most one edge at each vertex. Its size is therefore at most the smaller part:

min(4, 7) = 4.

That size is achieved by matching the four vertices of the small part to four distinct vertices of the large part. The number 7 is the larger part, 11 is the sum of the part sizes, and 28 = 4 × 7 is the number of edges, not the matching number.

### Q4

Answer: 4

On a path, a maximum matching takes every other edge. With 9 vertices the largest number of vertex-disjoint edges is

floor(9 / 2) = 4.

Four edges cover 8 vertices and leave one vertex exposed. A fifth edge would need two fresh vertices, but only one vertex remains. A perfect matching would need 9/2 edges, which is impossible because 9 is odd. Taking floor(n / 2) − 1 = 3 undercounts a maximum matching.

### Q5

Answer: B

A perfect matching in K_{3,3} assigns to each of the three vertices on the left a distinct vertex on the right, and every such assignment is present because the graph is complete bipartite. The number of bijections from a 3-element set to a 3-element set is

3! = 3 × 2 × 1 = 6.

The count 3 = min(3, 3) is the size of each perfect matching, not the number of them. The count 9 = 3 × 3 is the number of edges. The count 27 = 3^3 allows the three left vertices to choose right vertices independently, including collisions, so it counts assignments that are not matchings.

### Q6

Answer: A, C, D

Hall’s condition for a matching that saturates {p, q, r} requires |N(S)| ≥ |S| for every S contained in that part. For S = {p, q} the neighbourhood is {x}, so |N(S)| = 1 < 2. The condition fails, and no matching saturates {p, q, r}.

The matching {p—x, r—y} has size 2. Size 3 is impossible by the Hall failure, and it is also impossible because p and q have only one neighbour between them, so at most one of p and q is matched. Thus the maximum size is exactly 2.

König’s theorem applies because G is bipartite: the size of a minimum vertex cover equals the size of a maximum matching, which is 2. One such cover is {x, r}. It touches p—x, q—x, r—y, and r—z. No single vertex touches both p—x and r—y, so the minimum is not 1.

### Q7

Answer: 2

The matching {1—a, 3—b} has size 2. There is no larger matching, because the part {a, b} has only two vertices. So a maximum matching has size 2.

The graph is bipartite, so König’s theorem says a minimum vertex cover also has size 2. The set {a, b} is a vertex cover: every listed edge has an end in {a, b}. It is minimum because the two edges 1—a and 3—b share no vertex, so one vertex cannot cover both.

Using the number of edges, which is 4, or the larger part size 3, does not give the cover size.

### Q8

Answer: A

K_5 has 5 vertices. A matching of size k covers 2k vertices, so k ≤ floor(5 / 2) = 2. The same bound is (5 − 1) / 2 = 2 because n is odd. Two disjoint edges exist in K_5, so the maximum size is exactly 2. It is not a perfect matching.

Option B rounds the odd order upward. Option C would cover every vertex and would require a fractional edge. Option D is the number of edges, 5 × 4 / 2 = 10, not the size of a matching.

### Q9

Answer: B, D

In K_{3,5} the maximum matching has size min(3, 5) = 3. A perfect matching would have size |V| / 2 = 8 / 2 = 4 and would cover the part of size 5. At most 3 edges can leave the part of size 3, so at least two vertices on the large side stay exposed. There is no perfect matching.

König’s equality is a bipartite theorem. In the triangle K_3 a maximum matching has size 1, while a minimum vertex cover has size 2, because each edge needs its own witness and one vertex covers only the two edges incident with it, leaving the opposite edge. So C is false outside bipartite graphs.

On the path a—b—c—d, the matching {b—c} is maximal of size 1, while {a—b, c—d} is a maximum matching of size 2. A maximal matching can be strictly smaller than a maximum matching.

### Q10

Answer: C

A perfect matching must cover 3, and the only edge at 3 is 3—c. Thus c is used, and the remaining vertices {1, 2} must be matched to {a, b}. Both of the bijections use edges that exist:

- 1—a, 2—b, 3—c
- 1—b, 2—a, 3—c

Any other assignment sends 3 somewhere other than c, and that edge is absent. There is no third perfect matching. The number 6 = 3! counts perfect matchings of K_{3,3}, which has the extra edges 1—c, 3—a, and 3—b that G does not have. The number 0 would be right only if Hall’s condition failed. For the whole left part, N({1, 2, 3}) = {a, b, c}, and the critical pair {1, 2} has neighbourhood {a, b}. The condition holds, in agreement with the two matchings above.

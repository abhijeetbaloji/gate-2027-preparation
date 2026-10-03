# Graphs (Data Structures) — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Vertices of an undirected graph may be stored in an adjacency matrix or in adjacency lists. A simple undirected graph has no self-loops and no repeated edge. Its matrix is symmetric and has zeros on the diagonal. In an adjacency list for an undirected graph, each edge `{u, v}` appears once in `u`’s list and once in `v`’s list.

In a directed graph, the adjacency list of `u` stores the heads of edges that leave `u`. Each directed edge contributes one list entry.

When a traversal must choose among several neighbors, it tries them in increasing vertex number. BFS uses a queue. A vertex is marked when it is enqueued, and the source is enqueued before the scan begins. DFS is recursive: the vertex is marked when its call begins, and then its unmarked neighbors are explored in increasing order. The DFS depth counts the active calls, including the call on the source.

## Level 1 — Conceptual

## Q1 — NAT

An undirected graph has 5 vertices and 6 edges. Its adjacency lists contain how many neighbor entries in total?

---

## Q2 — NAT

The adjacency matrix of an undirected graph on vertices 0, 1, 2, 3 is

```text
0 1 1 0
1 0 1 1
1 1 0 0
0 1 0 0
```

The degree of vertex 1 is ____.

---

## Q3 — MCQ

In a directed graph, the number of entries in the adjacency list of vertex `u` equals

A. the in-degree of `u`

B. the out-degree of `u`

C. the number of vertices

D. the number of undirected edges incident on `u`

---

## Q4 — MCQ

An adjacency matrix for 5 vertices stores one integer for every ordered pair of vertex indices, including the diagonal. How many integers is that?

A. 5

B. 10

C. 25

D. 32

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

An undirected graph has adjacency lists

```text
0: 1, 2
1: 0, 3, 4
2: 0, 5
3: 1
4: 1, 5
5: 2, 4
```

BFS starting at 0 visits vertices in the order

A. 0, 1, 2, 3, 4, 5

B. 0, 1, 3, 4, 5, 2

C. 0, 2, 1, 5, 4, 3

D. 0, 1, 2, 5, 3, 4

---

## Q6 — NAT

A directed graph has 6 vertices and 9 directed edges. Its adjacency lists contain how many neighbor entries in total?

---

## Q7 — NAT

The complete undirected graph `K_4` has an edge between every pair of distinct vertices. How many 1s are in its adjacency matrix?

---

## Q8 — MCQ

An isolated vertex is included in an adjacency-list representation. Which statement is correct?

A. The vertex is omitted, because it has no edges.

B. The vertex is present and its neighbor list is empty.

C. The vertex is stored as a self-loop.

D. The vertex increases the edge count by 1.

---

## Level 3 — Multi-Step

## Q9 — NAT

Using the graph and BFS rules of Q5, the maximum number of vertices in the BFS queue at one time is ____.

---

## Q10 — MCQ

DFS on the graph in Q5, starting at 0, visits vertices in the order

A. 0, 1, 2, 3, 4, 5

B. 0, 1, 3, 4, 5, 2

C. 0, 2, 5, 4, 1, 3

D. 0, 1, 4, 5, 2, 3

---

## Q11 — MSQ

Select all that apply. Which matrices are adjacency matrices of simple undirected graphs?

A. ```text
0 1 0
1 0 1
0 1 0
```

B. ```text
0 1 0
0 0 1
0 1 0
```

C. ```text
1 1
1 0
```

D. ```text
0 1 1
1 0 0
1 0 0
```

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Vertices are numbered 1, 2, 3, 4. Their adjacency matrix is stored with row 0 for vertex 1, row 1 for vertex 2, row 2 for vertex 3, and row 3 for vertex 4. The four row sums are 1, 2, 2, 1 in that order. The degree of vertex 3 is

A. 1

B. 2

C. 3

D. 0

---

## Q13 — NAT

An undirected graph has 10 vertices and 15 edges. Its adjacency lists contain how many neighbor entries?

---

## Q14 — MCQ

In the handshaking convention for an undirected graph, one self-loop at vertex `v` contributes

A. 1 to the degree of `v`

B. 2 to the degree of `v`

C. 0 to the degree of `v`

D. 1 to the degree of every vertex

---

## Level 5 — Challenge

## Q15 — NAT

Using the graph and DFS rules of Q5, the maximum number of active DFS calls at one time, counting the call on vertex 0, is ____.

---

## Q16 — MSQ

Select all that apply.

A. An adjacency matrix answers whether a particular pair of vertices is an edge in `Θ(1)` time.

B. An adjacency-list representation uses `Θ(n^2)` space for every graph on `n` vertices.

C. Walking through the neighbors of one vertex takes time proportional to the length of that vertex’s list.

D. The adjacency matrix of an undirected simple graph is symmetric.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 12 |
| 2 | NAT | 3 |
| 3 | MCQ | (B) |
| 4 | MCQ | (C) |
| 5 | MCQ | (A) |
| 6 | NAT | 9 |
| 7 | NAT | 12 |
| 8 | MCQ | (B) |
| 9 | NAT | 3 |
| 10 | MCQ | (B) |
| 11 | MSQ | (A), (D) |
| 12 | MCQ | (B) |
| 13 | NAT | 30 |
| 14 | MCQ | (B) |
| 15 | NAT | 5 |
| 16 | MSQ | (A), (C), (D) |

## Detailed Solutions

### Q1

Answer: 12

Each undirected edge is stored at both endpoints. Six edges produce `2 * 6 = 12` neighbor entries. The five list headers are also present, but the question asks for neighbor entries, not headers.

### Q2

Answer: 3

Row 1 is `1 0 1 1`. It has three 1s, in columns 0, 2, and 3. The degree of vertex 1 is 3. The sum of all row sums is `2 + 3 + 2 + 1 = 8`, which is twice the number of edges, so the graph has 4 edges. That check agrees with the matrix being symmetric and having a zero diagonal.

### Q3

Answer: (B)

The list written for a directed graph in this set stores outgoing edges. Its length is the out-degree of `u`. The in-degree is the number of lists in which `u` appears as a neighbor, not the length of `u`’s own list.

### Q4

Answer: (C)

A 5 by 5 matrix has `5 * 5 = 25` entries. The diagonal is included even when a simple graph puts zeros there. The number of entries does not depend on how many pairs are edges; the zeros occupy space as well.

### Q5

Answer: (A)

The source 0 is enqueued first and marked. Dequeue 0 and enqueue its neighbors 1 and 2. Dequeue 1 and enqueue 3 and 4; the neighbor 0 is already marked. Dequeue 2 and enqueue 5; the neighbor 0 is already marked. Dequeue 3, then 4, then 5. Vertex 5 is already marked when 4 is processed, so it is not enqueued again. The visit order is 0, 1, 2, 3, 4, 5.

Option (B) is the DFS order from Q10. BFS finishes both neighbors of 0 before it goes deeper, so 2 appears before 3.

### Q6

Answer: 9

Each directed edge is stored once, in the list of its tail. Nine directed edges produce 9 neighbor entries. The undirected doubling in Q1 does not apply.

### Q7

Answer: 12

`K_4` has `4 * 3 / 2 = 6` undirected edges. Each edge puts a 1 in two symmetric positions, so the matrix contains 12 ones. The four diagonal entries are 0 because the graph is simple.

### Q8

Answer: (B)

The representation has one list header for every vertex, including a vertex whose list is empty. Omitting it would make that vertex disappear from the vertex set. An empty list is not a self-loop and does not add an edge.

### Q9

Answer: 3

Count the queue after the initial enqueue and after every dequeue’s additions.

- Enqueue 0. The queue is `0`, size 1.
- Dequeue 0 and enqueue 1, 2. The queue is `1 2`, size 2.
- Dequeue 1 and enqueue 3, 4. The queue is `2 3 4`, size 3.
- Dequeue 2 and enqueue 5. The queue is `3 4 5`, size 3.
- The later dequeues only shrink the queue.

The maximum is 3.

### Q10

Answer: (B)

DFS marks a vertex when the call starts, then tries neighbors in increasing order.

Call 0. Its first unmarked neighbor is 1. Call 1. The neighbor 0 is marked; the next is 3. Call 3, whose only neighbor is already marked, and return. The next neighbor of 1 is 4. Call 4. Its neighbor 1 is marked; the next is 5. Call 5. Its first unmarked neighbor is 2. Call 2. Both of its neighbors, 0 and 5, are marked, so return. Then 5, 4, 1, and 0 return. Vertex 2 was reached from 5 before the call on 0 could explore 2 directly.

The visit order is 0, 1, 3, 4, 5, 2.

### Q11

Answer: (A), (D)

A simple undirected adjacency matrix is symmetric, contains only 0s and 1s, and has a zero diagonal.

(A) is symmetric, with zeros on the diagonal. It is a path on three vertices.

(D) is symmetric, with zeros on the diagonal. Vertex 0 is connected to 1 and 2, and there is no edge between 1 and 2.

(B) is not symmetric: position `(0, 1)` is 1, while position `(1, 0)` is 0. It could represent a directed graph, not this undirected convention.

(C) has a 1 on the diagonal, which is a self-loop, so it is not a simple graph under the definition in the header.

### Q12

Answer: (B)

Vertex 3 is the third vertex in the list 1, 2, 3, 4, so it occupies row index 2, not row index 3. The row sums are stored in order for vertices 1, 2, 3, 4, and the third sum is 2. Reading row index 3 instead answers 1, which is the degree of vertex 4. The degree of vertex 3 is 2.

### Q13

Answer: 30

Each of the 15 undirected edges contributes two neighbor entries. The total is 30. The matrix for these 10 vertices would contain `10 * 10 = 100` integers, most of them zero. The list entry count is not 15, and it is not 100.

### Q14

Answer: (B)

The handshaking lemma sums degrees to twice the number of edge ends. A self-loop is incident with `v` at both ends, so it contributes 2 to the degree of `v`. An ordinary edge from `v` to one other vertex contributes 1. This question is about that degree convention; the header’s simple graphs exclude self-loops, but the contribution is still 2 when a loop is present.

### Q15

Answer: 5

From the DFS trace in Q10, the deepest chain of active calls is 0, then 1, then 4, then 5, then 2. That is five calls. The call on 3 happens earlier and returns before 4 is called, so 3 and 4 are not active together. The BFS queue in Q9 peaks at 3; the DFS recursion depth is a different number because DFS follows one branch to vertex 2 before backtracking.

### Q16

Answer: (A), (C), (D)

(A) is true: the matrix entry at the row and column of the two vertices is read directly. (C) is true: the list of `u` can be scanned from its first neighbor to its last, and that scan does not inspect the other vertices’ lists. (D) is true for an undirected simple graph because `{u, v}` is the same edge as `{v, u}`, and the diagonal is zero.

(B) is false. Adjacency lists use space proportional to `n` plus the number of neighbor entries. For a sparse graph that is `Θ(n + m)`, which need not be `Θ(n^2)`. The matrix is the representation whose size stays quadratic for every graph on `n` vertices.

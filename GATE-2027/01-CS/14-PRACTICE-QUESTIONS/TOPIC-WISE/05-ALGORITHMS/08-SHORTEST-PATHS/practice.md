# Shortest Paths — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Every edge weight is 1. A minimum-weight path is a path with the fewest edges. The algorithm and its time on adjacency lists are

A. Dijkstra’s binary-heap version, \(\Theta(E \log V)\), and BFS is incorrect even for equal weights

B. BFS, \(\Theta(V + E)\)

C. Floyd–Warshall, and no linear algorithm exists

D. Kruskal’s algorithm, because a minimum spanning tree preserves distances

---

## Q2 — MSQ

Select all that apply. Dijkstra grows a set \(S\) of vertices whose distances are treated as final. The next vertex added to \(S\) is the unsettled vertex of smallest tentative distance, and its outgoing edges are then relaxed.

A. The proof that this vertex is final uses the hypothesis that every edge weight is at least 0.

B. A negative edge weight, even on a graph with no negative cycle, is enough to make the finalised distance wrong.

C. The tentative distance is initialised to 0 at every vertex, so every vertex looks like a source.

D. With a binary heap the time is \(\Theta((V + E) \log V)\). With an array scan of unsettled vertices the time is \(\Theta(V^2)\).

---

## Q3 — MCQ

Bellman–Ford allows negative edges and detects a negative cycle reachable from the source. On a graph with \(V\) vertices and \(E\) edges the running time of the standard implementation is

A. \(\Theta(V + E)\)

B. \(\Theta(E \log V)\)

C. \(\Theta(VE)\)

D. \(\Theta(V^3)\) on every graph, including a graph with \(E = \Theta(V)\)

---

## Q4 — MCQ

Floyd–Warshall fills a \(V \times V\) matrix. The loop structure that matches the state “intermediates restricted to \(\{1, \ldots, k\}\)” is

A. \(k\) outermost, then \(i\), then \(j\), with \(D[i][j] = \min(D[i][j],\ D[i][k] + D[k][j])\)

B. \(i\) outermost, then \(j\), then \(k\)

C. one relaxation pass over the edge list

D. a BFS from each vertex

---

## Level 2 — Standard GATE Style

## Q5 — NAT

The directed graph has source \(S\) and edges

\[
\begin{align*}
&S \to A\ (3),\ S \to B\ (8),\ A \to B\ (2),\ A \to C\ (5),\\
&B \to C\ (1),\ B \to D\ (7),\ C \to D\ (4),\ A \to D\ (12).
\end{align*}
\]

Every weight is positive. Dijkstra finalises the unsettled vertex of smallest distance and does not reopen a finalised vertex. What is the distance from \(S\) to \(D\)?

---

## Q6 — NAT

On the graph of Q5, the distance from \(S\) to \(B\) is

---

## Q7 — NAT

The directed graph has source \(P\) and edges, listed in this relaxation order,

\[
P \to Q\ (5),\ P \to R\ (6),\ R \to Q\ (-3),\ Q \to S\ (4),\ R \to S\ (8).
\]

There is no negative cycle. Bellman–Ford performs \(V - 1\) full passes over this edge list and then one detection pass. What is the distance from \(P\) to \(S\)?

---

## Q8 — MCQ

Dijkstra is run on the graph of Q7. A vertex is never reopened after it is finalised. The distance it reports from \(P\) to \(S\) is

A. 7, the same value Bellman–Ford reports

B. 9, which is wrong: the path \(P \to R \to Q \to S\) has weight \(6 + (-3) + 4 = 7\), and \(Q\) was finalised at 5 before the edge \(R \to Q\) could repair it

C. 5, the direct edge into \(Q\)

D. undefined, because a negative edge means no shortest path exists

---

## Q9 — MSQ

Select all that apply. A DAG has vertices \(1, 2, 3, 4\) in topological order and edges

\[
1 \to 2\ (4),\ 1 \to 3\ (10),\ 2 \to 3\ (-2),\ 2 \to 4\ (1),\ 3 \to 4\ (3).
\]

Distances are relaxed once, in that topological order, from source 1.

A. The distance to 3 is 2, by the path \(1 \to 2 \to 3\).

B. The distance to 4 is 5.

C. The running time of this one pass, on adjacency lists, is \(\Theta(V + E)\), and a negative edge is allowed because a DAG has no cycle to walk repeatedly.

D. The same distances can be obtained by negating the weights and running Dijkstra.

---

## Q10 — NAT

Floyd–Warshall is run on four vertices. The initial matrix, with \(\infty\) where no edge exists and 0 on the diagonal, is

\[
\begin{bmatrix}
0 & 3 & \infty & 7 \\
\infty & 0 & 2 & \infty \\
1 & \infty & 0 & 4 \\
\infty & 5 & \infty & 0
\end{bmatrix}
\]

After the algorithm finishes, the shortest-path weight from vertex 1 to vertex 3 (1-based labels, matching the matrix order) is

---

## Level 3 — Multi-Step

## Q11 — NAT

On the Floyd–Warshall instance of Q10, the shortest-path weight from vertex 4 to vertex 1 is

---

## Q12 — MSQ

Select all that apply. Bellman–Ford’s detection pass is the extra pass after \(V - 1\) rounds.

A. If some distance still decreases, a negative cycle is reachable from the source.

B. A negative edge by itself, with no negative cycle, makes every distance undefined.

C. On a DAG the topological one-pass algorithm is \(\Theta(V + E)\) and is asymptotically faster than \(\Theta(VE)\) Bellman–Ford when the graph is sparse.

D. Initialising every distance to 0 makes unreachable vertices look reachable at distance 0. Unreachable vertices should stay at \(\infty\).

---

## Q13 — MCQ

The directed edges \(S \to A\ (1)\), \(A \to B\ (2)\), \(B \to A\ (-4)\), and \(S \to C\ (5)\) are relaxed in that order. Bellman–Ford runs a fourth pass on this four-vertex graph and the distance of \(A\) still falls. Which conclusion is correct?

A. A negative cycle is reachable from \(S\), namely \(A \to B \to A\) of weight \(2 + (-4) = -2\). No shortest path to \(A\) exists.

B. The distance to \(A\) is \(-4\), the single negative edge.

C. Dijkstra would report the same distances and would also detect the cycle.

D. The distance to \(C\) is undefined, because some other vertex lies on a negative cycle.

---

## Q14 — MCQ

An undirected triangle has edge weights 4, 7, and 8. The MST has weight \(4 + 7 = 11\). The two endpoints of the unused edge are connected by a tree path of weight 11 and by a direct edge of weight 8. Which statement is correct?

A. The shortest-path distance between those endpoints is 11, because the MST deleted the heavier edge.

B. The shortest-path distance is 8. The MST objective is a different sum, and the rejected edge is the shorter path.

C. The shortest-path distance is 19, the sum of all three weights.

D. Prim’s key and Dijkstra’s key are the same number on this triangle, so both algorithms delete the weight-8 edge from the distance answer.

---

## Level 4 — Tricky / Trap-Based

## Q15 — MCQ

A graph has a negative edge and no negative cycle. A solution runs Dijkstra from the source and returns the finalised labels. Which judgement is correct?

A. Absence of a negative cycle is exactly Dijkstra’s hypothesis, so the labels are shortest paths.

B. Existence of a shortest path needs no negative cycle. Dijkstra’s proof needs non-negative tails. The labels can be wrong, and Bellman–Ford is the single-source algorithm that remains correct.

C. BFS repairs the negative edge, because a negative edge is shorter in hop count.

D. Kruskal, run on the underlying undirected graph, returns the same distance labels.

---

## Q16 — MSQ

Select all that apply.

A. Subtracting a positive constant from every edge weight preserves shortest paths, because every path loses the same amount.

B. Johnson’s reweighting \(w'(u, v) = w(u, v) + h(u) - h(v)\), with \(h\) taken from a Bellman–Ford potential, changes every \(s\)-to-\(t\) path by the same \(h(s) - h(t)\) and can make every new weight non-negative.

C. Floyd–Warshall reports a negative cycle somewhere in the graph when some diagonal entry becomes negative.

D. The \(k\) loop of Floyd–Warshall may be placed innermost without changing the state, because addition is commutative.

---

## Q17 — MCQ

Longest paths in a DAG are required. Which method is correct?

A. Negate the weights and run Dijkstra.

B. Negate the weights and relax edges in topological order, or replace \(\min\) by \(\max\) in that same topological pass and initialise distances to \(-\infty\).

C. Run BFS and negate the hop counts.

D. Compute an MST of the underlying undirected graph and read the tree path.

---

## Level 5 — Challenge

## Q18 — MCQ

On the Dijkstra run of Q5, the order in which \(A, B, C, D\) are finalised, after the source, is

A. \(A, B, C, D\)

B. \(B, A, C, D\)

C. \(A, C, B, D\)

D. \(A, B, D, C\)

---

## Q19 — NAT

After Floyd–Warshall on the matrix of Q10, the shortest-path weight from vertex 2 to vertex 4 is

---

## Q20 — MSQ

Select all that apply.

A. One-source Bellman–Ford on a sparse graph is \(\Theta(VE)\). Quoting \(\Theta(V^3)\) as the tight bound replaces \(E\) by its dense maximum.

B. Dijkstra from every vertex, with an array, is \(\Theta(V^3)\) and requires non-negative weights. Floyd–Warshall is also \(\Theta(V^3)\) and allows negative edges that do not form a negative cycle.

C. An undirected edge of weight \(w < 0\), treated as two directed arcs, forms a 2-cycle of weight \(2w < 0\). In the usual walk model that pair has no shortest path.

D. A zero-weight cycle makes distances undefined. Detection must report it, because a strict decrease is not required.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | C |
| 4 | MCQ | A |
| 5 | NAT | 10 |
| 6 | NAT | 5 |
| 7 | NAT | 7 |
| 8 | MCQ | B |
| 9 | MSQ | A, B, C |
| 10 | NAT | 5 |
| 11 | NAT | 8 |
| 12 | MSQ | A, C, D |
| 13 | MCQ | A |
| 14 | MCQ | B |
| 15 | MCQ | B |
| 16 | MSQ | B, C |
| 17 | MCQ | B |
| 18 | MCQ | A |
| 19 | NAT | 6 |
| 20 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: B

With every weight equal to 1, the weight of a path is its number of edges. BFS dequeues vertices in increasing hop count, and the first time a vertex is discovered its distance is final. On adjacency lists that scan is \(\Theta(V + E)\). Dijkstra is correct too, but it is not the bound the equal weights allow, and a binary heap would add an unnecessary \(\log V\). Floyd–Warshall computes all pairs in \(\Theta(V^3)\), which is the wrong tool for one unweighted source. An MST minimises a sum of tree edges. On a triangle of equal weights it happens to look like a shortest-path tree, and that coincidence fails as soon as the weights differ.

### Q2

Answer: A, B, D

Let \(u\) be the unsettled vertex of smallest tentative distance, and suppose that value was produced by a path that stays in \(S\) until the last hop. Any competing path must leave \(S\) at some first vertex \(x\). The prefix up to \(x\) already weighs at least \(\mathrm{dist}[u]\), because \(u\) was the closest unsettled vertex. The tail from \(x\) to \(u\) weighs at least 0 only when every edge is non-negative, and that is what prevents the tail from repairing a worse prefix. A negative edge on a tail removes the inequality. Q7 and Q8 are a four-vertex case where the finalised label is already wrong, and that graph has no negative cycle, so (B) is true. Only the source starts at distance 0. Every other vertex starts at \(\infty\); starting them at 0 creates a false path of weight 0 from nowhere. The heap bound counts \(O(\log V)\) per extract and per decrease-key. The array bound spends \(\Theta(V)\) time finding the next vertex and does this \(V\) times.

### Q3

Answer: C

Each of \(V - 1\) rounds relaxes every edge once, and the detection pass is one more round of the same scan. The product is \(\Theta(VE)\). Early exit when a round changes nothing is correct if there is no negative cycle, but a negative cycle never settles, so the algorithm must still cap the rounds. On a sparse graph \(E = \Theta(V)\) and the time is \(\Theta(V^2)\), not \(\Theta(V^3)\). The cubic figure is what remains when \(E = \Theta(V^2)\). BFS is the linear unweighted algorithm. The heap bound is Dijkstra’s, and it is not valid once a weight is negative.

### Q4

Answer: A

The state \(D_k[i][j]\) is the best path from \(i\) to \(j\) whose intermediate vertices lie in \(\{1, \ldots, k\}\). Such a path either avoids \(k\), which is the previous state, or it visits \(k\) and splits into a best path from \(i\) to \(k\) plus a best path from \(k\) to \(j\), both using only lower-numbered intermediates. That recurrence is one new \(k\) at a time, so \(k\) is the outer loop. Placing \(k\) inside uses a vertex as an intermediate before the state has allowed it, and the in-place update is then unjustified. One edge-list pass is a single round of Bellman–Ford, not all pairs. BFS ignores unequal weights.

### Q5

Answer: 10

| Finalised | Distances \(S, A, B, C, D\) | Relaxations that change a label |
|-----------|----------------------------|----------------------------------|
| start | \(0, 3, 8, \infty, \infty\) | edges out of \(S\) |
| \(A\) at 3 | \(0, 3, 5, 8, 15\) | \(B \leftarrow 3+2\), \(C \leftarrow 3+5\), \(D \leftarrow 3+12\) |
| \(B\) at 5 | \(0, 3, 5, 6, 12\) | \(C \leftarrow \min(8, 5+1)\), \(D \leftarrow \min(15, 5+7)\) |
| \(C\) at 6 | \(0, 3, 5, 6, 10\) | \(D \leftarrow \min(12, 6+4)\) |
| \(D\) at 10 | unchanged | no outgoing edge |

The distance to \(D\) is 10. The path \(S \to A \to B \to C \to D\) weighs \(3+2+1+4 = 10\). The path \(S \to A \to B \to D\) weighs 12, \(S \to A \to C \to D\) weighs 12, and \(S \to B \to C \to D\) weighs 13. No other route is lighter. Finalising \(C\) before \(D\) is safe because every weight is positive: a path that reached \(D\) first and then came back toward \(C\) could not undercut a distance that was already the smallest unsettled label.

### Q6

Answer: 5

From the same table, \(B\) is set to 8 by \(S \to B\) and then decreased to \(3+2 = 5\) when \(A\) is finalised. It is finalised at 5, before \(C\) and \(D\). The direct edge of weight 8 is a feasible path and not a shortest path.

### Q7

Answer: 7

There are 4 vertices, so Bellman–Ford uses 3 rounds plus a detection pass. In the first round the edges fire as follows.

- \(P \to Q\) sets \(Q = 5\).
- \(P \to R\) sets \(R = 6\).
- \(R \to Q\) sets \(Q = \min(5,\ 6-3) = 3\).
- \(Q \to S\) sets \(S = 3+4 = 7\).
- \(R \to S\) offers \(6+8 = 14\), which does not improve 7.

Later rounds find no stricter improvement, and the detection pass is quiet, which agrees with the absence of a negative cycle. The distance 7 is the path \(P \to R \to Q \to S\). The path \(P \to Q \to S\) weighs \(5+4 = 9\) and is worse. The negative edge is used, and it does not make the distance undefined.

### Q8

Answer: B

Dijkstra from \(P\) starts with \(Q = 5\) and \(R = 6\). The smaller unsettled label is \(Q\), so \(Q\) is finalised at 5. Its edge sets \(S = 9\). Then \(R\) is finalised at 6. The edge \(R \to Q\) would offer \(6-3 = 3\), which is better than 5, but \(Q\) is already final and is not reopened. The edge \(R \to S\) offers 14, which does not beat 9. The algorithm reports 9 for \(S\). The true distance computed in Q7 is 7. The gap is exactly the negative tail: at the moment \(Q\) was finalised, the path through \(R\) looked worse (6 against 5) and only became better after the edge of weight \(-3\). Non-negativity is what would have forbidden that repair. A negative edge is not by itself a negative cycle. This graph’s only cycle-free routes are simple paths, and a shortest path exists.

### Q9

Answer: A, B, C

Process vertices in the order \(1, 2, 3, 4\).

- From 1: \(2 \leftarrow 4\), \(3 \leftarrow 10\).
- From 2: \(3 \leftarrow \min(10,\ 4 + (-2)) = 2\), \(4 \leftarrow 4+1 = 5\).
- From 3: \(4 \leftarrow \min(5,\ 2+3) = 5\).

The distance to 3 is 2 and the distance to 4 is 5. Both \(2 \to 4\) and \(2 \to 3 \to 4\) weigh 5. One pass is enough because every edge goes forward in the topological order, so when a vertex is processed every predecessor is finished. A negative edge cannot be repeated: there is no cycle. The scan of the lists is \(\Theta(V + E)\). Negating the weights and calling Dijkstra is not this algorithm. Negation creates the negative edge \(-4\) on \(1 \to 2\) in the negated instance, or, on the original negative edge, Dijkstra was already the wrong tool. The topological pass is what may be run on the negated DAG.

### Q10

Answer: 5

Number the vertices \(1, 2, 3, 4\) in the order of the rows. The outer loop adds intermediate \(k = 1\), then \(2\), then \(3\), then \(4\).

After \(k = 1\), vertex 3 can reach vertex 2: \(D[3][2] = \min(\infty,\ 1+3) = 4\). Other finite entries are unchanged.

After \(k = 2\), vertex 1 reaches vertex 3 through vertex 2: \(D[1][3] = \min(\infty,\ 3+2) = 5\). Vertex 4 reaches vertex 3: \(D[4][3] = 5+2 = 7\).

After \(k = 3\), vertex 1 reaches vertex 4 by \(5+4 = 9\), which does not beat the direct edge of weight 7. Vertex 2 reaches vertex 4: \(D[2][4] = 2+4 = 6\). Vertex 2 reaches vertex 1: \(D[2][1] = 2+1 = 3\). Vertex 4 reaches vertex 1: \(D[4][1] = 7+1 = 8\).

After \(k = 4\), the offer \(D[1][4] + D[4][3] = 7+7 = 14\) does not beat 5, and the other new routes are similarly worse.

The finished matrix is

\[
\begin{bmatrix}
0 & 3 & 5 & 7 \\
3 & 0 & 2 & 6 \\
1 & 4 & 0 & 4 \\
8 & 5 & 7 & 0
\end{bmatrix}
\]

The entry in row 1, column 3 is 5, the path \(1 \to 2 \to 3\) of weight \(3+2\). There is no direct edge from 1 to 3.

### Q11

Answer: 8

The finished matrix of Q10 has row 4, column 1 equal to 8. One path is \(4 \to 2 \to 3 \to 1\), of weight \(5+2+1 = 8\). No edge leaves 4 for 1 directly. The intermediate sequence matters: vertex 2 is allowed before vertex 3, and vertex 3’s edge into 1 was already present at \(k = 0\). A reading of the initial matrix would have reported \(\infty\).

### Q12

Answer: A, C, D

A simple path has at most \(V-1\) edges. If a \(V\)-th relaxation still decreases a distance, the walk that produced the decrease repeats a vertex, and the cycle it closed has negative weight and is reachable from the source. A negative edge that lies on no negative cycle is a legal part of a shortest path; Q7 uses one and the detection pass stays quiet. The DAG promise gives a topological order, and one relaxation of each edge in that order is \(\Theta(V + E)\), which is \(o(VE)\) when \(E\) is linear in \(V\). Distance 0 is the distance of the source from itself, not the distance of a vertex the search never reached. Those vertices remain \(\infty\).

### Q13

Answer: A

Relax the four edges in the listed order, starting from \(S = 0\) and every other distance \(\infty\).

| Pass | \(A\) after the pass | \(B\) after the pass | \(C\) |
|-----:|---------------------:|---------------------:|------:|
| 1 | \(0+1 = 1\), then \(3 + (-4) = -1\) | \(1+2 = 3\) | 5 |
| 2 | \(-3\) | \(-1+2 = 1\) | 5 |
| 3 | \(-5\) | \(-3+2 = -1\) | 5 |
| 4 | \(-7\) | \(-5+2 = -3\) | 5 |

The cycle \(A \to B \to A\) weighs \(2 + (-4) = -2\). Once \(A\) is reachable, each full pass decreases \(A\) by 2. Pass \(V = 4\) still decreases \(A\), which is the detection criterion. No shortest path to \(A\) exists, because another trip around the cycle is always cheaper. Dijkstra neither accepts the negative edge in its proof nor runs a detection pass. Vertex \(C\) is reached only by \(S \to C\) of weight 5, and nothing on the cycle has an edge to \(C\), so repeated relaxation does not change \(C\). The distance to \(C\) exists and equals 5. The distance to \(A\) does not.

### Q14

Answer: B

The MST selects the edges of weights 4 and 7 and rejects 8, because 8 is the heaviest edge on the triangle. The sum of the tree is 11, and that answer is correct for the spanning-tree objective. Between the endpoints of the rejected edge, the direct path has weight 8 and the tree path has weight 11. The distance is 8. Prim’s key, while the tree contains one endpoint and not the other, is the weight of a single leaving edge. Dijkstra’s key is the best path weight from a chosen source. On this triangle those numbers disagree as soon as the source is one endpoint of the weight-8 edge and the tree path has already been built: Dijkstra keeps 8, Prim never needed that edge for the sum.

### Q15

Answer: B

“No negative cycle” is the condition under which shortest paths exist and under which Bellman–Ford’s \(V-1\) rounds are enough. It is not the condition under which the greedy finalisation is safe. Q8 has no negative cycle and Dijkstra reports 9 where the distance is 7. The failed sentence in the proof is the claim that the tail beyond the cut has weight at least 0. BFS does not read the negative weight at all. Kruskal builds a tree of minimum total weight, not distance labels from a source, and the graph in Q7 is directed.

### Q16

Answer: B, C

Subtracting a constant \(c\) from every edge decreases a path of \(k\) edges by \(kc\). Paths with different numbers of edges change by different amounts, so the identity of the shortest path can change. Johnson’s correction depends only on the endpoints. On every \(s\)-to-\(t\) path the intermediate potentials cancel, and the whole path changes by \(h(s) - h(t)\). If \(h(v)\) is a feasible shortest-path distance from an added super-source, every reweighted edge satisfies \(w'(u, v) \ge 0\), and Dijkstra may then be run from each vertex. A negative diagonal after Floyd–Warshall means a walk from \(i\) back to \(i\) beats the empty path, which is a negative cycle through \(i\). The \(k\) loop is not free to move. The state adds one intermediate vertex per outer iteration; an inner \(k\) mixes those sets.

### Q17

Answer: B

Negating weights turns a longest-path problem into a shortest-path problem and turns at least one non-negative edge negative whenever a path of positive length existed. Dijkstra cannot be run on that negated instance. On a DAG the topological pass can. Negate, initialise the source to 0 and everyone else to \(\infty\), and relax \(\min\), or keep the original weights, initialise non-sources to \(-\infty\), and relax \(\max\). Both are one \(\Theta(V+E)\) pass. BFS hop counts are not weighted lengths. An MST path is not a longest path either; Q14 already shows that it is not even a shortest path.

### Q18

Answer: A

From the table in Q5, the unsettled minima are \(A\) at 3, then \(B\) at 5, then \(C\) at 6, then \(D\) at 10. Vertex \(B\) becomes smaller than the original edge \(S \to B\) only after \(A\) is finalised, and \(B\) is still finalised before \(C\), because \(5 < 6\). Finalising \(D\) before \(C\) would require \(D\)’s label to undercut \(C\) while \(C\) was unsettled. After \(B\) is finalised, \(D\) sits at 12 and \(C\) at 6, so \(C\) is next. The order is \(A, B, C, D\).

### Q19

Answer: 6

The finished matrix in Q10 has row 2, column 4 equal to 6. The path is \(2 \to 3 \to 4\), weight \(2+4\). This entry appears when \(k = 3\) is allowed as an intermediate. Before that iteration the direct distance from 2 to 4 was \(\infty\). The path \(2 \to 3 \to 1 \to 4\) weighs \(2+1+7 = 10\) and is worse, which is why the later intermediate \(k = 4\) does not reduce the 6.

### Q20

Answer: A, B, C

Bellman–Ford’s tight bound keeps both \(V\) and \(E\). Replacing it by \(\Theta(V^3)\) is valid only as a loose upper bound on simple graphs, where \(E = O(V^2)\), and it is not tight for a path or a tree. Array Dijkstra from each of \(V\) sources costs \(V \cdot \Theta(V^2) = \Theta(V^3)\) and still requires non-negative weights. Floyd–Warshall matches that cubic time, uses \(\Theta(V^2)\) memory, and tolerates negative edges until a diagonal goes negative. An undirected negative edge traversed in both directions is a closed walk of weight \(2w < 0\). Shortest paths between its endpoints are undefined in the walk model; a question that wants that edge to be legal has to say that the graph is directed. A zero-weight cycle does not produce a strict decrease, so the detection test does not fire. Distances remain well defined, and a shortest path can be chosen simple.

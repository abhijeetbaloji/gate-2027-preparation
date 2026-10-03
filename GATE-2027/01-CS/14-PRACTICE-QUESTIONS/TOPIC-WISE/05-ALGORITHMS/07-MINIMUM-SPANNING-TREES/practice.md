# Minimum Spanning Trees — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A connected undirected graph has \(V\) vertices. Every spanning tree has

A. \(V\) edges

B. \(V - 1\) edges

C. \(V + 1\) edges

D. \(E\) edges, one for every edge of the graph

---

## Q2 — MSQ

Select all that apply.

A. If \(A\) is contained in some MST and no edge of \(A\) crosses a cut, then a lightest edge across that cut can be added to \(A\) and the result is still contained in some MST.

B. On any cycle, a heaviest edge is excluded from some MST. If that heaviest edge is strictly heavier than every other edge on the cycle, it is in no MST.

C. Kruskal and Prim require every weight to be positive.

D. The path in an MST between two vertices is a shortest path in the graph.

---

## Q3 — MCQ

Kruskal’s algorithm sorts edges by increasing weight and adds an edge when its endpoints lie in different Union-Find components. On a connected simple graph the running time is

A. \(\Theta(E \log E)\), which is the same class as \(\Theta(E \log V)\) because \(\log E = \Theta(\log V)\)

B. \(\Theta(V^2)\) for every graph, including a tree

C. \(\Theta(E)\), because Union-Find is the only cost and \(\alpha(V)\) dominates the sort

D. \(\Theta(V^3)\)

---

## Q4 — MCQ

Prim’s algorithm grows one tree. With a binary heap and adjacency lists, each decrease-key and extract costs \(O(\log V)\). The time is

A. \(\Theta(V^2)\) for the heap version

B. \(\Theta(E \log V)\)

C. \(\Theta(E + V \log V)\) only, and only the binary heap achieves that bound

D. \(\Theta(E)\), the same as BFS, because Prim is a traversal

---

## Level 2 — Standard GATE Style

## Q5 — NAT

An undirected graph has vertices \(\{A, B, C, D, E\}\) and edge list

\[
\begin{align*}
&(A,B,4),\ (A,C,9),\ (B,C,2),\ (B,D,7),\ (C,D,5),\\
&(C,E,8),\ (D,E,3),\ (A,E,11),\ (B,E,6).
\end{align*}
\]

Kruskal scans edges from lightest to heaviest and rejects an edge whose endpoints are already connected. What is the weight of the MST?

---

## Q6 — NAT

On the graph of Q5, how many edges does the MST contain?

---

## Q7 — MSQ

Select all that apply. The graph of Q5 has distinct edge weights.

A. The MST is unique.

B. The edge \(B-C\) of weight 2 is in the MST.

C. The edge \(A-C\) of weight 9 is in the MST.

D. Prim, started at \(A\), using the lightest edge that leaves the current tree, selects the same set of four edges as Kruskal.

---

## Q8 — MCQ

A second undirected graph has vertices \(\{P, Q, R, S\}\) and edge list

\[
(P,Q,3),\ (P,R,3),\ (Q,R,4),\ (Q,S,5),\ (R,S,5).
\]

Which additional statement is true?

A. \(Q-R\) belongs to every MST, because it is the lightest edge on the triangle \(PQR\).

B. \(Q-R\) belongs to no MST. Both weight-3 edges belong to every MST, and exactly one of the two weight-5 edges belongs to each MST.

C. Every spanning tree has weight 11, so the MST is the whole graph.

D. The repeated weights make every edge optional, and the minimum weight is 4.

---

## Level 3 — Multi-Step

## Q9 — NAT

Edge weights may be negative. The undirected edge list on \(\{A, B, C, D\}\) is

\[
(A,B,6),\ (A,C,-2),\ (B,C,4),\ (B,D,1),\ (C,D,-5),\ (A,D,8).
\]

Kruskal’s algorithm is run exactly as on positive weights. What is the MST weight?

---

## Q10 — MCQ

The triangle \(A-B\), \(B-C\), \(A-C\) has weights 5, 6, and 9 respectively. The MST uses the two lighter edges. The unique path in that MST between \(A\) and \(C\) has weight

A. 9, the direct edge, because an MST preserves shortest paths

B. 11, which is larger than the direct edge of weight 9, so the tree path is not a shortest path

C. 5

D. 30, the product of the weights

---

## Q11 — MSQ

Select all that apply.

A. The array implementation of Prim, scanning all vertices to find the next minimum key, runs in \(\Theta(V^2)\) and is the better of the two classical bounds when the graph is dense.

B. Kruskal on a complete graph is \(\Theta(V^2 \log V)\). Array Prim is asymptotically faster on that graph.

C. A Fibonacci heap improves Prim’s theoretical bound to \(\Theta(E + V \log V)\). The binary-heap bound to use in a hand simulation is still \(\Theta(E \log V)\).

D. A disconnected graph has a spanning tree on all vertices. Kruskal is required to add \(V\) edges.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Prim and Kruskal are run on the graph of Q5. Which comparison is correct?

A. Prim’s key for a vertex outside the tree is the weight of one edge leaving the tree. Kruskal accepts a globally lightest edge that joins two components. On this graph both return the same weight.

B. Prim’s key is a path distance from the start, so Prim is Dijkstra.

C. Kruskal rejects \(B-C\) because that edge is the heaviest on a cycle.

D. Because the weights are distinct, Prim and Kruskal must add the edges in the same chronological order.

---

## Q13 — MSQ

Select all that apply.

A. A negative edge is a reason to abandon Kruskal. The cut property divides by the weight.

B. A negative edge is a reason to abandon Dijkstra, not Kruskal or Prim.

C. Reverse-delete sorts edges from heavy to light and deletes an edge when it is not a bridge. The surviving edges form an MST, by the cycle property.

D. A maximum spanning tree is obtained by negating every weight and running Kruskal, or by adding the heaviest edge that does not close a cycle.

---

## Q14 — MCQ

All edge weights on a connected undirected graph are distinct. Which statement follows from the exchange argument?

A. The MST need not be unique, because distinctness does not constrain the lightest edge of a cut.

B. The MST is unique. If two trees differed, the lightest edge that lies in one and not the other could replace a heavier edge in the other tree and strictly decrease its weight.

C. Distinct weights imply that the MST is also the shortest-path tree from every source.

D. Distinct weights imply that the graph has no cycle.

---

## Level 5 — Challenge

## Q15 — MCQ

On the graph of Q8, a student adds \(Q-R\) of weight 4 and then the two weight-3 edges, and reports a “tree” of weight \(4+3+3 = 10\) on four vertices using three edges \(Q-R\), \(P-Q\), and \(P-R\). What is wrong?

A. Nothing is wrong. Weight 10 beats weight 11, so Q8’s MST is not minimum.

B. Those three edges form a cycle on \(\{P, Q, R\}\) and leave \(S\) uncovered. They are not a spanning tree. Every real spanning tree that includes \(Q-R\) has weight at least 12.

C. Union-Find would accept all three edges, because they have small weights.

D. Four vertices need four edges, so the construction is short by one edge and the weight 10 is only a partial sum.

---

## Q16 — MSQ

Select all that apply.

A. An MST minimises the sum of selected edge weights. A shortest-path tree minimises distances from one source. Swapping the two keys solves the wrong problem.

B. If the graph is directed, undirected Kruskal still computes a minimum spanning arborescence. Directions can be ignored.

C. Union by rank with path compression costs \(\alpha(V)\) amortised per operation, the inverse Ackermann function. The \(\Theta(E \log E)\) sort still dominates Kruskal.

D. When weights are allowed to tie, two MSTs may differ as sets of edges and must still share the same minimum weight. Marking a second correct tree wrong is a comparison of shapes, not of the objective.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B |
| 3 | MCQ | A |
| 4 | MCQ | B |
| 5 | NAT | 14 |
| 6 | NAT | 4 |
| 7 | MSQ | A, B, D |
| 8 | MCQ | B |
| 9 | NAT | -6 |
| 10 | MCQ | B |
| 11 | MSQ | A, B, C |
| 12 | MCQ | A |
| 13 | MSQ | B, C, D |
| 14 | MCQ | B |
| 15 | MCQ | B |
| 16 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: B

A tree on \(V\) vertices is connected and acyclic, and those two properties are equivalent to having exactly \(V - 1\) edges and being connected. A \(V\)-th edge joins two vertices that are already connected and closes a cycle, so the result is not a tree. A spanning tree is a subset of the edges, not the full edge set, unless the graph was already a tree.

### Q2

Answer: A, B

The cut property is the exchange that justifies both Kruskal and Prim. Take an MST that already contains \(A\). If it misses the chosen light edge \(e\), add \(e\). The cycle that appears must leave the cut again by some other edge \(e'\). That edge is at least as heavy as \(e\), so deleting it does not raise the weight. The cycle property is the same fact read in the other direction: a heaviest edge on a cycle is the one the exchange would delete. A strict heaviest edge is deleted from every MST. Neither argument divides by a weight or assumes the weight is positive. A negative edge that does not close a cycle only helps the sum. The tree path is not a shortest path. Q10 is a three-edge counterexample.

### Q3

Answer: A

Sorting \(E\) edges is \(\Theta(E \log E)\). Each edge then performs a constant number of Union-Find operations. With union by rank and path compression those operations are \(\alpha(V)\) amortised, and \(\alpha(V)\) grows so slowly that the sort dominates. In a connected simple graph \(V - 1 \le E < V^2\), so \(\log E = \Theta(\log V)\), and \(\Theta(E \log E)\) may be written \(\Theta(E \log V)\). The \(\Theta(V^2)\) bound is array Prim, not Kruskal. A tree has \(E = V - 1\), and Kruskal on it is far from quadratic in \(V\) only in the sense that \(E\) is linear; the general answer in terms of \(E\) is still the sorting bound.

### Q4

Answer: B

The binary heap stores vertices outside the tree, keyed by the lightest edge that reaches them from the tree. There are \(V\) extracts and at most one decrease-key per edge, each \(O(\log V)\), which is \(\Theta(E \log V)\) on a connected graph. The \(\Theta(V^2)\) bound is the implementation that finds the minimum key by scanning an array, with no heap. A Fibonacci heap is what reaches \(\Theta(E + V \log V)\); a binary heap does not. Prim is not BFS. BFS would be correct only if every weight were equal, and even then its output is a shortest-path tree in hop count, not a proof about the sum of selected weights.

### Q5

Answer: 14

Sorted order, lightest first: \(B-C\ (2)\), \(D-E\ (3)\), \(A-B\ (4)\), \(C-D\ (5)\), \(B-E\ (6)\), \(B-D\ (7)\), \(C-E\ (8)\), \(A-C\ (9)\), \(A-E\ (11)\).

- \(B-C\) joins two components. Take it.
- \(D-E\) joins two components. Take it.
- \(A-B\) joins \(A\) to \(\{B, C\}\). Take it.
- \(C-D\) joins \(\{A, B, C\}\) to \(\{D, E\}\). Take it. The forest is now one tree, weight \(2+3+4+5 = 14\).
- \(B-E\) has both ends in that tree. Reject it. The same rejection removes \(B-D\), \(C-E\), \(A-C\), and \(A-E\).

The accepted edges \(B-C\), \(D-E\), \(A-B\), and \(C-D\) connect all five vertices and contain no cycle. There are \(V-1 = 4\) of them, so they form a spanning tree. Every rejected edge was considered only after a lighter connection between its endpoints already existed, which is Kruskal’s use of the cut property: the accepted edge was a lightest edge across the cut between the two components it joined. The weight 14 is therefore minimum.

### Q6

Answer: 4

Five vertices require \(5 - 1 = 4\) tree edges. The trace in Q5 stops when the fourth edge, \(C-D\), is accepted. Adding any further edge from the list closes a cycle.

### Q7

Answer: A, B, D

All nine weights are different. Suppose two MSTs differed. Let \(e\) be the lightest edge that belongs to one and not the other. The exchange of Q2 would move \(e\) into the tree that lacks it and strictly decrease that tree, because the edge it replaces is heavier. So the MST is unique. The edge \(B-C\) was the first edge accepted. The edge \(A-C\) was rejected; it is also the strict heaviest edge on the triangle \(A-B-C\) (weights 4, 2, 9), so the cycle property excludes it from every MST.

Prim from \(A\) grows a different sequence and the same set. Start with \(\{A\}\). The lightest leaving edge is \(A-B\) of weight 4. From \(\{A, B\}\) the lightest new edge is \(B-C\) of weight 2, which improves on \(A-C\) of weight 9. From \(\{A, B, C\}\) the lightest new edge is \(C-D\) of weight 5, which improves on \(B-D\) of weight 7. From \(\{A, B, C, D\}\) the lightest new edge is \(D-E\) of weight 3, which improves on \(B-E\) of weight 6 and on \(C-E\) of weight 8. The edges are \(A-B\), \(B-C\), \(C-D\), and \(D-E\), weight 14. Kruskal had added \(D-E\) before \(A-B\); the chronological order differs and the set does not.

### Q8

Answer: B

The triangle \(P-Q-R\) has weights 3, 3, and 4. The edge \(Q-R\) is the unique heaviest edge on that cycle, so it lies in no MST. The two weight-3 edges must both lie in every MST: a spanning tree that omits \(P-Q\) and still connects \(Q\) has to use \(Q-R\) or the path through \(S\), and the resulting trees weigh at least \(3+4+5 = 12\). The same lower bound holds if \(P-R\) is the omitted edge. After both weight-3 edges are taken, \(P\), \(Q\), and \(R\) are connected, and exactly one edge of weight 5 is needed to bring in \(S\). Either \(Q-S\) or \(R-S\) works, and both trees weigh \(3+3+5 = 11\). The graph has five edges, so it is not itself a tree, and a tree that includes the weight-4 edge is not minimum.

### Q9

Answer: -6

Sorted order: \(C-D\ (-5)\), \(A-C\ (-2)\), \(B-D\ (1)\), \(B-C\ (4)\), \(A-B\ (6)\), \(A-D\ (8)\).

- Take \(C-D\).
- Take \(A-C\). The component is \(\{A, C, D\}\).
- Take \(B-D\). Vertex \(B\) was isolated from that component, and weight 1 is the lightest edge that reaches it. \(B-C\) and \(A-B\) are heavier.
- \(B-C\) now closes \(B-D-C\). Reject it. \(A-B\) and \(A-D\) close cycles as well.

The tree edges are \(C-D\), \(A-C\), and \(B-D\). The weight is \(-5 + (-2) + 1 = -6\). The negative edges were accepted because they do not form a cycle with the edges already chosen. Rejecting them for being negative would have forced a heavier tree, for example \(A-B\), \(B-D\), \(D-C\) of weight \(6+1-5 = 2\).

### Q10

Answer: B

The MST edges are \(A-B\) and \(B-C\), total weight \(5+6 = 11\). The only \(A\)-to-\(C\) path that uses tree edges is \(A-B-C\), of weight 11. The direct edge \(A-C\) has weight 9 and was correctly rejected by Kruskal, because it is the heaviest edge on the triangle and taking it would not reduce the tree’s total. That rejection is right for the MST objective and wrong if the objective is the \(A\)-to-\(C\) distance. Dijkstra, with every weight positive, would keep 9 as the distance from \(A\) to \(C\). An MST and a shortest-path tree answer different questions.

### Q11

Answer: A, B, C

Array Prim does \(V\) selection scans, each looking at up to \(V\) keys, which is \(\Theta(V^2)\), and the edge relaxations are absorbed when the graph is dense. Kruskal must sort \(\Theta(V^2)\) edges of a simple complete graph and costs \(\Theta(V^2 \log V)\), so array Prim is the faster dense-graph algorithm. A Fibonacci heap makes decrease-key amortised constant and extract \(O(\log V)\), giving \(\Theta(E + V \log V)\). Hand simulation and the usual sparse-graph answer use the binary heap, \(\Theta(E \log V)\). A disconnected graph has no spanning tree of the whole vertex set. Kruskal returns a minimum spanning forest and stops short of \(V-1\) edges. It never adds \(V\) edges to a forest: that would include a cycle in some component.

### Q12

Answer: A

Prim’s key is the weight of the single best edge from the grown tree to that vertex. It is not a path sum from the source; using a path sum is Dijkstra. Kruskal’s key is global lightness among edges that still join different components. Q5 and Q7 show both algorithms returning weight 14 on this edge list. Kruskal does not reject \(B-C\). That edge is the lightest in the graph and is accepted first. Distinct weights make the final set unique, not the order in which the two algorithms discover it. Prim’s order was \(A-B\), \(B-C\), \(C-D\), \(D-E\). Kruskal’s order was \(B-C\), \(D-E\), \(A-B\), \(C-D\).

### Q13

Answer: B, C, D

The cut exchange compares weights with \(\le\). A negative number is a legal weight, and Kruskal’s sort places it first, which is what happened in Q9. Dijkstra is the algorithm whose proof breaks, because a negative tail can undercut a distance that has already been finalised. Reverse-delete is the cycle property used as a destruction rule: while the edge being considered is the heaviest so far, deleting it whenever the graph stays connected removes a heaviest edge of some cycle. The edges that remain are an MST. Negating weights turns a maximum spanning tree into a minimum one, so the same cut property applies. Equivalently, scan edges from heavy to light and add an edge when it does not form a cycle.

### Q14

Answer: B

Distinctness makes the lightest edge across a cut unique whenever the cut is the one used by the exchange. If two optimal trees differed, the lightest symmetric difference edge would be a strict improvement of the tree that omitted it, contradicting optimality of that tree. So the MST is unique. It is still not a shortest-path tree: the triangle in Q10 can be given three distinct weights and the same gap between tree-path weight and direct-edge weight remains. Distinct weights also say nothing about whether a cycle exists. A triangle with weights 1, 2, and 3 has both a cycle and a unique MST.

### Q15

Answer: B

The edges \(P-Q\), \(P-R\), and \(Q-R\) are the triangle. Their three endpoints are only \(\{P, Q, R\}\), so \(S\) is not connected, and the three edges contain a cycle. Either defect is enough to show that they are not a spanning tree. Union-Find would reject the third of them: after \(P-Q\) and \(P-R\) are united, \(Q\) and \(R\) have the same root. The weight 10 is the weight of a cyclic subgraph, not a competitor of 11. Every spanning tree that includes the weight-4 edge must still connect four vertices with three acyclic edges. One such tree is \(Q-R\), \(P-Q\), \(Q-S\), of weight \(4+3+5 = 12\), and the other combinations that keep \(Q-R\) are at least 12 as well. The true minimum remains 11, achieved only by trees that exclude \(Q-R\).

### Q16

Answer: A, C, D

Prim and Dijkstra both grow a set and extract a minimum key. Prim’s key is one edge. Dijkstra’s key is a path weight from a source. Substituting one key into the other algorithm computes the other objective. The syllabus MST is undirected. A minimum spanning tree of a directed graph, an arborescence, is a different problem; throwing away directions and running Kruskal can accept an edge the wrong way and can also accept a structure that is not an arborescence. Path compression with union by rank is the \(\alpha(V)\) bound. It does not remove the need to sort. Ties, as in Q8, produce more than one optimal edge set and only one optimal weight. A solution that lists the other weight-5 edge is correct if the question asked for the weight or for any MST, and incorrect only if the question asked for a specific tie break.

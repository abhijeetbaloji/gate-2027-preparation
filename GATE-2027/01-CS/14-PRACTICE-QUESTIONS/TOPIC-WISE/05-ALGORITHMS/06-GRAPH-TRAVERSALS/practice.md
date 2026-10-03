# Graph Traversals — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Breadth-first search and depth-first search are run from a source on a graph stored as adjacency lists. A full traversal that also restarts on every unvisited vertex costs

A. \(\Theta(E)\) even when the graph has isolated vertices and \(E = 0\)

B. \(\Theta(V + E)\)

C. \(\Theta(V^2)\) for every list representation

D. \(\Theta(V \log V)\)

---

## Q2 — MSQ

Select all that apply.

A. BFS stores the wavefront in a queue. The vertex that has been waiting longest is expanded next.

B. DFS stores the frontier in a stack, often the call stack. The most recently discovered unfinished vertex is expanded next.

C. On an unweighted graph, the BFS distance from the source is the minimum number of edges on a path.

D. The DFS parent pointers are minimum-edge distances, because DFS also paints vertices in a layer order.

---

## Q3 — MCQ

An undirected graph is stored as an adjacency matrix. A BFS or DFS that scans every row to find neighbours costs

A. \(\Theta(V + E)\)

B. \(\Theta(V^2)\)

C. \(\Theta(E \log V)\)

D. \(\Theta(V)\)

---

## Q4 — MCQ

In a directed DFS, an edge \(u \to v\) is examined. Which classification is correct?

A. \(v\) white: tree edge. \(v\) grey: back edge. \(v\) black and \(\mathrm{disc}[u] < \mathrm{disc}[v]\): forward edge. \(v\) black and \(\mathrm{disc}[v] < \mathrm{disc}[u]\): cross edge.

B. Every edge to a black vertex is a back edge.

C. A back edge goes to a white vertex.

D. Undirected graphs use all four names, tree, back, forward, and cross, as four disjoint cases.

---

## Level 2 — Standard GATE Style

## Q5 — NAT

The undirected graph has adjacency lists in alphabetical order:

\[
\begin{align*}
A&: B, C \\
B&: A, C, D \\
C&: A, B, E \\
D&: B, F \\
E&: C, F \\
F&: D, E
\end{align*}
\]

BFS starts at \(A\). In the order vertices are first discovered, including the source, what is the third vertex? Encode \(A=1, B=2, C=3, D=4, E=5, F=6\).

---

## Q6 — NAT

On the same BFS as Q5, what is the distance of \(F\) from \(A\), measured in number of edges?

---

## Q7 — NAT

The directed graph has adjacency lists in the order written:

\[
\begin{align*}
1&: 2,\ 3 \\
2&: 4,\ 5 \\
3&: 4 \\
4&: 5 \\
5&: 3
\end{align*}
\]

DFS starts at 1. Discovery times are assigned by the usual preorder increment, starting at 1. What is \(\mathrm{disc}[3]\)?

---

## Q8 — MSQ

Select all that apply. The DFS of Q7 uses colours white, grey, and black, and classifies each edge when it is first examined.

A. \(3 \to 4\) is a back edge.

B. \(2 \to 5\) is a forward edge.

C. \(1 \to 3\) is a tree edge.

D. A directed cycle exists, because a back edge exists.

---

## Q9 — MCQ

A second directed graph has edges \(1 \to 2\), \(1 \to 3\), \(2 \to 4\), \(3 \to 4\), and adjacency lists in increasing order. DFS from 1 produces finish times \(\mathrm{fin}[1] = 8\), \(\mathrm{fin}[2] = 5\), \(\mathrm{fin}[3] = 7\), \(\mathrm{fin}[4] = 4\). Decreasing finish time is a topological order. Which sequence is that order?

A. \(1, 2, 4, 3\)

B. \(1, 3, 2, 4\)

C. \(4, 2, 3, 1\)

D. \(1, 2, 3, 4\), the increasing discovery order

---

## Level 3 — Multi-Step

## Q10 — MCQ

The undirected graph with edges \(\{1-2,\ 2-3,\ 3-1,\ 3-4\}\) is 2-coloured by BFS, starting at 1 with colour 0 and giving each newly discovered vertex the other colour. Which statement is correct?

A. The colouring succeeds, so the graph is bipartite.

B. Vertices 2 and 3 both receive colour 1, and the edge \(2-3\) joins two vertices of the same colour, so the graph is not bipartite.

C. A triangle is bipartite because it has three vertices.

D. The pendant edge \(3-4\) is what destroys the colouring.

---

## Q11 — MSQ

Select all that apply. A directed graph is searched by DFS.

A. The graph is acyclic if and only if this DFS, restarted on every white vertex, produces no back edge.

B. On a DAG, decreasing finish time is a topological order. Increasing discovery time need not be.

C. Kahn’s algorithm repeatedly removes a vertex of indegree 0. If the process stops before every vertex is removed, a cycle remains.

D. An undirected edge back to the DFS parent is a cycle.

---

## Q12 — MCQ

Kosaraju’s algorithm computes strongly connected components. Which account is correct?

A. One DFS, on the original graph, in increasing discovery order. Each tree is a component.

B. DFS for finish times, transpose every edge, then DFS on the transpose in decreasing finish order. Each tree of the second pass is one component. Both passes are \(\Theta(V + E)\) on adjacency lists.

C. The second pass runs on the original graph in decreasing finish order.

D. The second pass runs on the transpose in increasing finish order.

---

## Q13 — MSQ

Select all that apply. The BFS tree of Q5 is compared with a DFS that starts at \(A\) and always tries the alphabetically first unused neighbour.

A. The BFS distance of \(C\) is 1. A DFS that walks \(A \to B \to C\) gives \(C\) a tree-path length of 2.

B. Reading the DFS parent depth as a fewest-edge distance is valid, because every spanning tree preserves distances.

C. In an undirected BFS, a non-tree edge joins two vertices on the same level or on adjacent levels.

D. The edge \(B-C\) in Q5 joins two vertices at distance 1 from \(A\), so it is a same-level non-tree edge.

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

A directed edge \(u \to v\) has weight 5, and another \(u\)-to-\(v\) route uses four edges of weight 1. BFS from \(u\), ignoring weights and counting edges, reports the distance of \(v\) as 1. Which conclusion is correct?

A. BFS has computed the minimum-weight path.

B. BFS has computed the minimum number of edges. The weight-4 route is shorter in weight, so a weighted algorithm is required.

C. DFS would have minimised the weight, because it explores long paths first.

D. BFS minimises weight whenever every weight is positive, even if the weights are unequal.

---

## Q15 — MSQ

Select all that apply.

A. The parenthesis property says that if \(v\) is a descendant of \(u\) in the DFS forest, then the interval \([\mathrm{disc}[v], \mathrm{fin}[v]]\) lies inside \([\mathrm{disc}[u], \mathrm{fin}[u]]\).

B. A grey vertex is on the current recursion stack. A back edge into a grey vertex closes a directed cycle.

C. A black vertex has finished. An edge to a black vertex is not, by itself, a back edge.

D. Forgetting to restart DFS or BFS on a disconnected graph still visits every component, because the first source can see isolated vertices through missing edges.

---

## Q16 — MCQ

An undirected DFS is used only to test for a cycle. The edge from a vertex back to its parent is ignored, and any other edge to a visited vertex is reported as a cycle. Which statement is correct?

A. The parent edge must be reported, because every tree edge is a cycle of length 1.

B. The parent edge is the same undirected edge that was just walked. A cycle needs a different visited neighbour.

C. Undirected graphs have forward edges that are not cycles.

D. The test is valid only on directed graphs.

---

## Level 5 — Challenge

## Q17 — NAT

On the DFS of Q7, the finish time of vertex 4 is

---

## Q18 — MSQ

Select all that apply.

A. Articulation points and bridges can be found from one DFS that maintains discovery times and low-link values, in \(\Theta(V + E)\) time on lists.

B. A non-root vertex \(u\) is an articulation point when some child \(c\) has \(\mathrm{low}[c] \ge \mathrm{disc}[u]\): no edge from \(c\)’s subtree reaches an ancestor of \(u\).

C. The root is an articulation point exactly when it has two or more children in the DFS forest.

D. BFS layer numbers compute weighted shortest paths as soon as the adjacency lists are sorted.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, C |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | NAT | 3 |
| 6 | NAT | 3 |
| 7 | NAT | 5 |
| 8 | MSQ | A, B, D |
| 9 | MCQ | B |
| 10 | MCQ | B |
| 11 | MSQ | A, B, C |
| 12 | MCQ | B |
| 13 | MSQ | A, C, D |
| 14 | MCQ | B |
| 15 | MSQ | A, B, C |
| 16 | MCQ | B |
| 17 | NAT | 8 |
| 18 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: B

Each vertex is started once, either as the source of a restart or when it is first discovered. Each adjacency-list edge is scanned a constant number of times. The sum of the list lengths is \(\Theta(E)\) for a directed graph and \(\Theta(E)\) for an undirected graph stored in both directions. Isolated vertices contribute to \(V\) even when \(E = 0\), so the bound is \(\Theta(V + E)\), not \(\Theta(E)\). The quadratic bound is the cost of scanning a matrix. Nothing in BFS or DFS sorts, so a \(\log V\) factor is not part of the plain traversal.

### Q2

Answer: A, B, C

The queue is first-in first-out, which is why BFS finishes every vertex at distance \(d\) before it finishes vertices at distance \(d+1\). The stack is last-in first-out, which is why DFS dives to a dead end before it tries the next neighbour. On unit weights, or on an unweighted graph, “fewer edges” is the path length, and the first time BFS discovers a vertex it discovers it along a minimum-edge path. DFS parent pointers do not have that meaning. The tree path can be a long route around a short edge that DFS happened to walk later.

### Q3

Answer: B

Finding the neighbours of one vertex scans that vertex’s entire row, which has \(V\) entries, whether or not the vertex has degree 1. Over \(V\) vertices the scans cost \(\Theta(V^2)\). A sparse graph does not make the matrix scan sparse: the zeros are stored and are examined. Adjacency lists are what produce \(\Theta(V + E)\).

### Q4

Answer: A

White means undiscovered, so the edge becomes a tree edge and the search recurses. Grey means the vertex is an ancestor on the stack, so the edge goes backward along the current path. Black means the vertex has finished. If it was discovered after \(u\), it is a descendant and the edge is a forward edge that is not the tree edge. If it was discovered before \(u\) and is not an ancestor, the edge jumps to another branch and is a cross edge. Calling every black target a back edge merges three different situations. An undirected graph, once each edge is seen from both ends, uses only tree edges and back edges.

### Q5

Answer: 3

The queue starts as \([A]\).

- Dequeue \(A\). Discover \(B\) and then \(C\). Queue: \(B, C\).
- Dequeue \(B\). \(A\) is visited, \(C\) is visited, \(D\) is new. Queue: \(C, D\).
- The third vertex in discovery order is \(C\), encoded as 3. Discovery order, including the source, is \(A, B, C, D, E, F\).

Distances do not depend on this tie break. The order of \(B\) before \(C\) does, and it is fixed by the adjacency list of \(A\).

### Q6

Answer: 3

Continue the BFS of Q5.

- Dequeue \(C\). Discover \(E\). Queue: \(D, E\).
- Dequeue \(D\). Discover \(F\). Distance \(1 + \mathrm{dist}[D] = 1 + 2 = 3\).
- Dequeue \(E\). \(F\) is already grey, so the edge \(E-F\) is not a second discovery.

One shortest path is \(A-B-D-F\). Another, \(A-C-E-F\), also has three edges. BFS reports 3 the first time \(F\) is reached, and a later edge cannot reduce it. The parent of \(F\) is \(D\), because \(D\) was dequeued before \(E\).

### Q7

Answer: 5

DFS from 1 follows the first unused neighbour.

- Discover 1 at time 1. Recurse to 2 at time 2.
- From 2, recurse to 4 at time 3.
- From 4, recurse to 5 at time 4.
- From 5, the only neighbour is 3, still white. Discover 3 at time 5.

So \(\mathrm{disc}[3] = 5\). The edge \(1 \to 3\) is not the edge that discovers 3. By the time DFS returns to 1, vertex 3 has already been reached through \(2 \to 4 \to 5 \to 3\).

### Q8

Answer: A, B, D

Finish times on this run: 3 finishes at 6, 5 at 7, 4 at 8, 2 at 9, and 1 at 10. The edge classification is:

| Edge | Colour of the head when examined | Class |
|------|----------------------------------|-------|
| \(1 \to 2\) | white | tree |
| \(2 \to 4\) | white | tree |
| \(4 \to 5\) | white | tree |
| \(5 \to 3\) | white | tree |
| \(3 \to 4\) | grey | back |
| \(2 \to 5\) | black, and \(\mathrm{disc}[2] < \mathrm{disc}[5]\) | forward |
| \(1 \to 3\) | black, and \(\mathrm{disc}[1] < \mathrm{disc}[3]\) | forward |

Vertex 4 is still grey when \(3 \to 4\) is examined, because 3 is a descendant of 4 and 4 has not finished. That edge closes the directed cycle \(4 \to 5 \to 3 \to 4\). A directed graph has a cycle if and only if a DFS produces a back edge, so (D) follows from (A). The edge \(1 \to 3\) is forward, not a tree edge: 3 was already black.

### Q9

Answer: B

Decreasing finish time sorts the vertices as \(1\) (8), \(3\) (7), \(2\) (5), \(4\) (4). The order is \(1, 3, 2, 4\). Every edge goes forward in this order: \(1\) precedes \(2\) and \(3\), and both \(2\) and \(3\) precede \(4\). Increasing discovery time is \(1, 2, 4, 3\). That sequence places 4 before 3 even though the edge \(3 \to 4\) exists, so it is not a topological order. The parenthesis property is what makes decreasing finish time work on a DAG: when \(u \to v\) is examined, \(v\) cannot be grey, or the edge would be a back edge and the graph would not be a DAG. If \(v\) is white it becomes a descendant and finishes before \(u\). If \(v\) is black it has already finished.

### Q10

Answer: B

BFS from 1 colours 1 with 0, then 2 with 1, then 3 with 1, because 3 is also a neighbour of 1. The edge \(2-3\) is examined when both ends already have colour 1. An edge inside a colour class is an odd cycle; here the cycle is the triangle \(1-2-3\). A graph is bipartite if and only if it has no odd cycle, so the colouring’s failure is the whole test. The edge \(3-4\) is fine: 4 receives colour 0. Deleting the triangle edge \(2-3\) would make the colouring succeed. Three vertices do not make a triangle bipartite.

### Q11

Answer: A, B, C

If a directed cycle exists, the first vertex of that cycle to finish still has its successor on the cycle grey, and the edge to that successor is a back edge. Conversely every back edge to a grey ancestor closes a cycle. So absence of back edges, over a DFS of the whole graph, is exactly acyclicity. On a DAG the argument in Q9 turns decreasing finish time into a topological order, while discovery order can emit a vertex before a predecessor that is still unexplored in another branch. Kahn’s algorithm is the queue version of the same fact: a vertex of indegree 0 can be first, and deleting it exposes later vertices. A leftover vertex of positive indegree means every remaining vertex has a predecessor inside the remainder, which produces a cycle. In an undirected graph the edge back to the parent is the tree edge already used. It is not a second route.

### Q12

Answer: B

The first DFS records finish times on the original graph. The second DFS follows edges of the transpose, and it starts vertices in decreasing order of those finish times. Each tree grown by the second pass is one strongly connected component. Both passes scan every vertex and every edge a constant number of times, so the time on lists is \(\Theta(V + E)\). Running the second pass on the original graph, or starting it from the earliest finisher instead of the latest, does not follow the condensation in topological order, and the trees need not be the components.

### Q13

Answer: A, C, D

BFS discovers \(C\) from \(A\), so the BFS distance is 1 and the BFS tree contains the edge \(A-C\). DFS that prefers \(B\) walks \(A\) to \(B\) to \(C\) before it ever uses \(A-C\) as a tree edge. The DFS tree path has two edges. That parent depth is not a shortest-path length. Only the BFS tree, on an unweighted graph, has a shortest path along every root-to-node tree path. In that BFS, a non-tree edge cannot jump over a level. If it joined a vertex at level \(d\) to a vertex at level \(d+2\) or more, the farther vertex would have been discovered earlier, from the nearer end, and the distance would be smaller than the level BFS assigned. The edge \(B-C\) joins two vertices that Q5 placed at level 1, so it is a same-level non-tree edge. The edge \(E-F\) joins level 2 to level 3, which is the adjacent-level case.

### Q14

Answer: B

BFS never reads the weight 5 or the weights 1. It reports that \(v\) is one edge away, which is the correct hop count and the wrong weight: the four-edge route has weight 4, less than 5. Unequal positive weights need Dijkstra. Negative weights need Bellman–Ford, or the topological scan if the graph is a DAG. DFS does not minimise either hops or weight. Its tree path is an artefact of adjacency order.

### Q15

Answer: A, B, C

DFS assigns discovery time on entry and finish time on exit. Every recursive call made from \(u\) happens between those two assignments, so a descendant’s interval is nested. That is the parenthesis property. Grey is exactly “entered and not finished”, which is the stack. An edge to such a vertex returns to an ancestor and closes a cycle. Black means the recursive call has returned; an edge to a finished vertex is forward or cross, decided by comparing discovery times, and is not a back edge. A source reaches only its own reachable set. An isolated vertex, or another component, stays white unless the outer loop starts a new search there. Missing edges do not carry the search across.

### Q16

Answer: B

The search arrived at \(u\) along the edge \(\{parent, u\}\). Seeing that same edge from \(u\) back to the parent is not a second path. A cycle is an edge from \(u\) to some visited vertex that is not the parent: that vertex was reached by another route, and the two routes plus this edge close a circuit. Undirected DFS does not keep a separate forward or cross class. The parent test is precisely the undirected cycle test; the directed test uses grey vertices instead, because a directed parent edge is not traversable backward.

### Q17

Answer: 8

From the trace in Q7 and Q8: vertex 4 is discovered at time 3, its child 5 is discovered at time 4 and finishes at time 7, and 4 then finishes at time 8. The later forward edge \(2 \to 5\) does not reopen 4. Finish time 8 is the moment the entire descendant interval of 4, namely vertices 5 and 3, has closed.

### Q18

Answer: A, B, C

One DFS computes \(\mathrm{disc}\) and

\[
\mathrm{low}[u] = \min\bigl(\mathrm{disc}[u],\ \mathrm{low}[c]\text{ over children},\ \mathrm{disc}[w]\text{ over back-edge targets}\bigr).
\]

If a child’s subtree has no edge reaching strictly above \(u\), then \(\mathrm{low}[c] \ge \mathrm{disc}[u]\), and removing \(u\) separates that subtree from the rest of the graph. The root has no parent to bypass. It is a cut vertex exactly when two or more DFS subtrees hang from it, because those subtrees have no edges between them. The whole computation scans each list a constant number of times and is \(\Theta(V + E)\). BFS levels are hop counts. Sorting an adjacency list does not turn those levels into weighted distances.

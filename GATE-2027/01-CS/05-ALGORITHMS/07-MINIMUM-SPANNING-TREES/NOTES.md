# Minimum Spanning Trees — Learning Notes

A spanning tree connects all vertices with no cycle. Among all spanning trees, a minimum spanning tree has the smallest total edge weight. Kruskal and Prim are greedy algorithms whose safety comes from one fact: the lightest edge across a cut is always safe to include. Shortest-path trees are a different object. An MST does not claim that the path inside the tree between two vertices is a shortest path.

---

## 1. Definitions

**Spanning tree.** An undirected graph `G = (V, E)` is connected. A spanning tree is a subset of `V − 1` edges that connects every vertex. Equivalently: connected and acyclic, on all vertices. If `G` is disconnected, the same ideas produce a **spanning forest**, one tree per component, and a minimum spanning forest.

**Weight.** Each edge `e` has a real weight `w(e)`. The weight of a tree is the sum of its edge weights. An MST is a spanning tree of minimum weight.

**Why negative weights are allowed.** The sum does not care whether a term is negative. Adding a negative edge, when it does not close a cycle, only helps. Nothing in the cut property divides by a weight or assumes a weight is positive. This is the opposite of Dijkstra.

**Uniqueness.** If all edge weights are distinct, the MST is unique. Proof idea: if two trees differed, the lightest edge that lies in one and not the other would be a safe swap that strictly decreases the heavier tree, a contradiction. If weights repeat, several MSTs can share the same optimal weight. Do not mark a different correct tree as wrong when ties exist; compare weights.

**What an MST is not.**

- Not a shortest-path tree. Between two vertices the tree path can be longer, in weight, than some path that uses a non-tree edge.
- Not the travelling salesman tour. TSP is a minimum Hamiltonian cycle, which is NP-hard. An MST is a lower bound idea used in approximations, not the tour itself.
- Not a Steiner tree. Steiner trees may add extra vertices. That problem is NP-hard. MST uses only the given vertices.

---

## 2. The cut property

**Cut.** A partition of `V` into two non-empty sets `S` and `V − S`. An edge **crosses** the cut if one end is in `S` and the other is not.

**Statement.** Suppose a set `A` of edges is contained in some MST. Let `(S, V − S)` be a cut that no edge of `A` crosses. Let `e` be a lightest edge that crosses the cut. Then `A ∪ {e}` is still contained in some MST.

**Why it works (exchange).** Take an MST `T` that contains `A`. If `T` already contains `e`, done. If not, add `e` to `T`. A cycle appears. That cycle must cross the cut an even number of times, so it contains another edge `e'` that also crosses the cut. Then `e'` is not lighter than `e`, because `e` was a lightest crossing edge. Delete `e'`. The result is still a spanning tree, its weight is at most the weight of `T`, and it contains `A ∪ {e}`. So `e` is safe.

**The cycle property, the twin fact.** On any cycle, a heaviest edge is excluded from some MST. If every edge on the cycle were in the tree you would have a cycle in the tree. If a heaviest edge were forced in while a lighter cycle edge was out, the cut/exchange argument swaps them.

**GATE use.** “Is this edge in some MST?” If it is the unique lightest edge across some cut, yes. If it is the unique heaviest edge on some cycle, no. If weights tie, say “some” rather than “every”.

---

## 3. Kruskal’s algorithm

**Rule.** Sort edges by increasing weight. Walk the sorted list. Add an edge if its ends lie in different components. Reject it if they are already connected (it would close a cycle).

**Why this is the cut property.** When an edge is accepted, the two components it joins define a cut: one component versus the rest. No lighter edge can still be waiting to connect those two components, because lighter edges were considered first and did not connect them. So the accepted edge is a lightest edge across that cut, and it is safe.

**How to test “different components”.** Union-Find (disjoint sets). Each vertex starts in its own set. `Find` returns the representative. `Union` merges two sets. Path compression and union by rank make each operation almost `O(1)`: the inverse Ackermann function `α(V)`, which is at most 4 for every graph you will ever see. The sort still dominates.

```
sort E by increasing weight
make a set for each vertex
T = empty
for each edge u—v in that order:
    if Find(u) ≠ Find(v):
        add the edge to T
        Union(u, v)
stop when T has V − 1 edges
```

**Example.** Vertices `{1, 2, 3, 4}`. Edges `(1—2, 1), (2—3, 2), (1—3, 2), (3—4, 3), (1—4, 10)`.

- Take `1—2` (weight 1).
- Take `2—3` (weight 2). Now `1—3` has both ends in the same component. Reject, even though its weight equals 2.
- Take `3—4` (weight 3).
- Tree weight `1 + 2 + 3 = 6`. The edge of weight 10 is never needed.

**Complexity.**

| Piece | Cost | Why |
|-------|------|-----|
| Sort | `Θ(E log E) = Θ(E log V)` | `E < V²`, so `log E = Θ(log V)` when `E ≥ V` in a connected simple graph; more carefully `log E ≤ 2 log V` |
| Union-Find | `Θ(E α(V))` | One find-pair per edge |
| Total | `Θ(E log E)` | The sort dominates `α` |
| Extra space | `Θ(V)` | Parent and rank arrays, plus the output tree |

Best, average, and worst time are the same: you sort every edge. The algorithm is correct with negative weights. It does not need the graph to be complete. If the graph is disconnected, you obtain a minimum spanning forest and you never reach `V − 1` edges.

**When to use.** The natural form when the graph is given as an edge list, especially when it is sparse. Also the form that makes the “next lightest edge that does not form a cycle” story obvious.

**When not to use.** You already have a dense adjacency matrix and you want the `Θ(V²)` Prim variant below, which avoids an `E log E` sort with `E = Θ(V²)`.

---

## 4. Prim’s algorithm

**Rule.** Grow one tree. Start at any vertex. Repeatedly add the lightest edge that leaves the current tree and enters a new vertex.

**Why this is the cut property.** The cut is “vertices in the tree” versus “vertices outside”. The edge you add is a lightest edge across that cut, and no tree edge crosses it yet. Safe.

**Array implementation.** `key[v]` is the lightest edge weight known from the tree to `v`. Each step scans all vertices to find the smallest key outside the tree, then scans that vertex’s neighbours. Time `Θ(V² + E) = Θ(V²)` with a matrix, because the `V` selection scans dominate. This is the right Prim for a dense graph.

**Binary-heap implementation.** The priority queue holds vertices outside the tree, keyed by `key[v]`. Each edge may cause a decrease-key. Time `Θ((V + E) log V)`, often written `Θ(E log V)` for connected graphs. A Fibonacci heap brings the theoretical bound to `Θ(E + V log V)`. GATE expects you to know the binary-heap and the `Θ(V²)` bounds; the Fibonacci bound is the “best known comparison-style” figure, not the one to simulate by hand.

**Example.** Same graph, start at 1.

- Tree `{1}`. Best leaving edges: `1—2` weight 1, `1—3` weight 2, `1—4` weight 10. Add `1—2`.
- Tree `{1, 2}`. Edge `2—3` weight 2 updates vertex 3 (equal to the direct edge). Add `2—3` or `1—3`; both weight 2.
- Then add `3—4` weight 3.
- Same weight 6. If both weight-2 edges are available, either may be chosen; with the rejected-cycle story of Kruskal you saw `1—3` dropped, while Prim might take `1—3` and drop `2—3`. Both trees weigh 6.

**Complexity summary.**

| Implementation | Time | When it is attractive | Extra space |
|----------------|------|------------------------|-------------|
| Array / matrix | `Θ(V²)` | Dense graphs, `E` near `V²` | `Θ(V)` |
| Binary heap + lists | `Θ(E log V)` | Sparse graphs | `Θ(V)` |
| Fibonacci heap | `Θ(E + V log V)` | Theoretical sparse bound | `Θ(V)` |

All three are correct on every weight assignment, including negatives. Best and worst do not depend on the weight values, only on `V` and `E` and the heap.

**Comparison with Kruskal.**

| | Kruskal | Prim |
|--|---------|------|
| Grows | A forest, many components | One tree |
| Order | Global edge sort | Lightest edge out of one set |
| Sparse | `Θ(E log E)` | `Θ(E log V)` with a binary heap |
| Dense | `Θ(V² log V)` because `E = Θ(V²)` | `Θ(V²)` with the array version |
| Needs | Edge list, Union-Find | A way to scan neighbours of one vertex |

---

## 5. Reverse-delete and a maximum spanning tree

**Reverse-delete.** Sort edges heavy to light. Delete an edge if it is not a bridge (the graph stays connected without it). The edges that remain form an MST. This is the cycle property: you drop a heaviest edge on some cycle whenever deleting it does not disconnect the graph. Time depends on the bridge tests; it is correct but usually slower to implement than Kruskal. Know the idea, not a clever data structure, unless the question asks.

**Maximum spanning tree.** Negate every weight and run Kruskal or Prim, or sort edges from heaviest to lightest and add an edge when it does not form a cycle. The cut property applies to the negated weights. Do not run a shortest-path algorithm for this.

---

## 6. A shortest-path trap on the same graph

Take a triangle, weights `1, 1, 100`. The MST uses the two edges of weight 1, total 2. The path in the MST between the two vertices joined by the weight-100 edge has weight 2, which happens to be shorter than 100. Change the weights to `3, 3, 4`. The MST uses `3` and `3`, total 6. The two endpoints of one weight-3 edge have tree-path... they are directly connected. The endpoints of the unused edge of weight 4 are connected by a tree path of weight `3+3 = 6`, which is **longer** than the direct edge 4. So the MST path is not a shortest path. Dijkstra on non-negative weights would keep the direct edge of weight 4 as the shortest path.

---

## 7. Common GATE traps

1. Dijkstra or BFS used to build an MST. The objectives differ.
2. Kruskal edge added even though `Find` returns the same root. That edge is a cycle.
3. Prim’s `Θ(V²)` bound quoted together with a binary heap, or `Θ(E log V)` quoted for the array scan.
4. Negative weight used as a reason to reject Kruskal. It is a reason to reject Dijkstra.
5. “The MST is unique” when two edges share a weight.
6. Tree path treated as a shortest path.
7. `V` edges in the answer. A tree has `V − 1` edges. `V` edges force a cycle.
8. Disconnected graph: no spanning tree exists. The algorithm should report a forest.
9. Directed MST (minimum arborescence) solved with undirected Kruskal. The syllabus problem is the undirected one. Arborescence is a different algorithm.
10. Forgetting that `log E = Θ(log V)` is why Kruskal is written both ways. They are the same class for simple graphs.

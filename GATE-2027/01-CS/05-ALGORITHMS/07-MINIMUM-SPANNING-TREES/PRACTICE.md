# Minimum Spanning Trees — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** How many edges does a spanning tree on `V` vertices have?

**2.** State the cut property.

**3.** Why may an MST algorithm accept a negative edge?

**4.** When is the MST unique?

**5.** Why is a path inside the MST not automatically a shortest path?

### Level 2 — Standard

**6.** Edges `(1—2, 1), (2—3, 2), (1—3, 2), (3—4, 3), (1—4, 10)`. Kruskal’s tree and its weight?

**7.** Time of Kruskal on a connected simple graph, in terms of `E` and `V`.

**8.** Time of Prim with an adjacency matrix and a linear scan for the next vertex.

**9.** Time of Prim with a binary heap and adjacency lists.

**10.** All weights distinct. Can two different spanning trees both be minimum?

### Level 3 — Multi-step

**11.** Triangle edges 3, 3, and 4. MST weight? Weight of the tree path between the endpoints of the unused edge, and the true shortest-path weight between them?

**12.** Kruskal sees edge `u—v` and `Find(u) = Find(v)`. What does it do, and which property explains why?

**13.** A complete graph has `V = 200`. Which of array-Prim and Kruskal has the better asymptotic time?

**14.** You want a *maximum* spanning tree. How do you reuse Kruskal?

**15.** The graph has two components. What should Kruskal return, and why is “spanning tree” the wrong name?

### Level 4 — Trap-based

**16.** A student refuses Kruskal because one weight is `−2`, and runs Dijkstra from an arbitrary source to build a tree. Two separate mistakes: name them.

**17.** Prim with a binary heap is given time `Θ(V²)`. For which implementation is that bound right?

**18.** “Every MST edge is a lightest edge in the whole graph.” Counterexample with four vertices?

**19.** Two edges have weight 5, and either can complete an MST. A solution marks one tree wrong. What was assumed?

**20.** Someone includes `V` edges and still calls the result an MST. What structure do they actually have if it is connected?

### Level 5 — Challenge

**21.** Prove the exchange step: if `e` is a lightest edge across a cut and `T` is an MST that avoids `e`, then swapping `e` for another cut edge on the cycle does not increase the weight.

**22.** Why does Kruskal’s accepted edge meet the cut property at the moment it is accepted?

**23.** Show that distinct edge weights imply a unique MST, using the lightest edge that belongs to one candidate and not the other.

**24.** Fibonacci-heap Prim is `Θ(E + V log V)`. For a sparse connected graph `E = Θ(V)`, compare this with binary-heap Prim. For a complete graph, compare it with array Prim.

**25.** Edge weights `1, 1, 100` on a triangle. MST weight? Is the expensive edge in every MST, some MST, or none?

---

## Answers and explanations

**1.** `V − 1`.

**2.** If a set of edges is inside some MST, and a cut is not yet crossed by that set, then a lightest edge across the cut can be added and some MST still contains the enlarged set.

**3.** The objective is a sum of chosen edges. A negative term decreases the sum. The exchange proof never requires a weight to be positive.

**4.** When all edge weights are distinct. Equal weights can leave a choice between two safe edges of the same weight.

**5.** The tree minimises the sum of its edges, not the path weight between a given pair. A direct edge that was rejected as a cycle edge can still be a shorter route than the long way around the tree.

**6.** Take weight 1 (`1—2`), then one of the weight-2 edges (`2—3` if it comes first), reject the other weight-2 edge, take weight 3 (`3—4`). Weight 6. Reject 10.

**7.** `Θ(E log E)`, which is `Θ(E log V)`.

**8.** `Θ(V²)`.

**9.** `Θ(E log V)`.

**10.** No. Distinct weights force a unique MST.

**11.** MST uses the two edges of weight 3, total 6. The unused edge has weight 4. Its endpoints are connected in the tree by the other two edges, path weight 6. The shortest path between them is the direct edge, weight 4.

**12.** Reject the edge. Its ends are already connected, so the edge is the extra edge of a cycle. The cycle property lets you leave out a heaviest edge of that cycle; Kruskal’s order has already connected the ends by lighter or equal edges considered earlier, so this edge is safe to skip. If it were strictly heavier than some cycle edge, skipping it is mandatory for every MST.

**13.** Array Prim, `Θ(V²) = Θ(40000)`. Kruskal sorts `Θ(V²)` edges, `Θ(V² log V)`, which is worse.

**14.** Sort heavy to light and add an edge when it joins different components. Equivalently, negate all weights and run ordinary Kruskal.

**15.** A minimum spanning forest: one tree per component. A single spanning tree does not exist, because no edge connects the components.

**16.** Kruskal is correct with weight `−2`. Dijkstra is the algorithm that cannot handle a negative edge, and a shortest-path tree from one source is not defined to be an MST.

**17.** The adjacency-matrix Prim that scans all vertices to find the next minimum key. The binary heap is `Θ(E log V)`.

**18.** Vertices 1, 2, 3, 4. Edges `1—2` weight 1, `2—3` weight 3, `3—4` weight 4, and no cheaper way to reach 4. The MST must include `3—4` of weight 4, which is not a lightest edge of the graph. The lightest edge is weight 1. An MST contains the lightest edge of the *graph* when that edge is the unique lightest, but later edges are only lightest across their own cuts.

**19.** Uniqueness. Equal weights allow both trees. Compare total weight; both are optimal.

**20.** A connected graph with `V` edges contains exactly one cycle (if it is unicyclic). It is not a tree, so it is not an MST. Dropping the heaviest edge on that cycle returns to a tree, which is the reverse-delete idea on the last extra edge.

**21.** Adding `e` to `T` creates one cycle. The cycle leaves the cut and must re-enter, so some other edge `e'` on the cycle crosses the cut. `w(e) ≤ w(e')` because `e` is a lightest crossing edge. Delete `e'`. The graph stays connected and has `V − 1` edges, and the weight change is `w(e) − w(e') ≤ 0`.

**22.** The two Union-Find components of the endpoints form a cut. No lighter edge connected them, because every lighter edge was already processed and would have united them. So the edge is a lightest edge across that cut, and the forest built so far does not cross it.

**23.** Suppose `T1` and `T2` are distinct MSTs. Let `e` be the lightest edge that lies in one of them, say `T1`, and not in `T2`. Add `e` to `T2` and delete the other cut-crossing edge `e'` on the created cycle. Then `w(e) < w(e')` because all weights differ and `e` was the lightest disagreement, so `e'` is heavier. The new tree is lighter than `T2`, which contradicts optimality of `T2`.

**24.** Sparse: Fibonacci `Θ(V + V log V) = Θ(V log V)`, same class as binary-heap `Θ(V log V)`. Complete: Fibonacci `Θ(V² + V log V) = Θ(V²)`, same class as array Prim. The asymptotic win of Fibonacci heaps shows up between those extremes, for example `E = Θ(V log V)`, where `E log V` is larger than `E + V log V` by a log factor. For the usual sparse and dense exam cases the classes match the simpler implementations.

**25.** MST weight `1 + 1 = 2`. The edge of weight 100 is in no MST. Any tree that uses it has weight at least `100 + 1 = 101`.

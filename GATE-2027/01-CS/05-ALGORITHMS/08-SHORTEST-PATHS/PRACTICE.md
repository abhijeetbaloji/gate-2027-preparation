# Shortest Paths — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Why does a negative cycle reachable from `s` destroy shortest paths?

**2.** Which weight condition does Dijkstra need, and which algorithm replaces it when the condition fails?

**3.** Why is BFS correct when every weight is 1?

**4.** How many full relaxation passes does Bellman–Ford use before the detection pass?

**5.** Where does `k` sit in the Floyd–Warshall loops?

### Level 2 — Standard

**6.** Edges `s→a` weight 2, `s→b` weight 5, `a→b` weight 1, `b→c` weight 1, `a→c` weight 4. Dijkstra distances from `s`?

**7.** Time of binary-heap Dijkstra and of array Dijkstra.

**8.** Time of Bellman–Ford, and what the extra pass decides.

**9.** A DAG has a negative edge. Best single-source time?

**10.** After Floyd–Warshall, `D[3][3] = −2`. What does that mean?

### Level 3 — Multi-step

**11.** Edges `s→a` weight 1, `s→b` weight 100, `b→a` weight `−100`. What does Dijkstra report for `a`, and what is the true distance?

**12.** Edges `s→a` 4, `s→b` 5, `b→a` −2, no other edges. Trace Bellman–Ford’s first round if the edge list is `s→a`, `s→b`, `b→a`. Can a later round improve anything?

**13.** Triangle MST weights 3, 3, 4. Shortest-path weight between the endpoints of the weight-4 edge?

**14.** You negate every weight on a DAG and run Dijkstra. Why is that not a correct longest-path algorithm? What do you run instead?

**15.** All-pairs on a sparse graph with a few negative edges and no negative cycle. Why might Johnson be preferred to Floyd–Warshall?

### Level 4 — Trap-based

**16.** “There is a negative edge but no negative cycle, so Dijkstra is correct.” What is wrong?

**17.** Every `dist[v]` is initialised to 0. What distances do you get on a graph of positive edges?

**18.** Bellman–Ford on a graph with `V = 1000`, `E = 3000` is quoted as `Θ(V³)`. Give the tight class.

**19.** An undirected edge of weight `−3` is fed to Bellman–Ford as two arcs. Does a shortest path between its endpoints exist?

**20.** Floyd is coded `for i, for j, for k`. Why can that disagree with `for k, for i, for j`?

### Level 5 — Challenge

**21.** Explain Dijkstra’s safe-finalise argument, and mark the step that uses `w ≥ 0`.

**22.** Why do `V − 1` rounds of Bellman–Ford suffice when there is no negative cycle?

**23.** Show that replacing `w(u, v)` by `w(u, v) + h(u) − h(v)` adds the same constant `h(s) − h(t)` to every `s`-to-`t` path. Why does that preserve the identity of a shortest path?

**24.** A directed graph is a DAG. Give the longest-path procedure and its time.

**25.** Compare one-source array Dijkstra from every vertex with Floyd–Warshall. Same time class, different weight hypotheses: state both.

---

## Answers and explanations

**1.** Each trip around the cycle reduces the total weight. Repeating it produces arbitrarily small walk weights, so no minimum exists.

**2.** Every edge weight must be at least 0. If any weight is negative, use Bellman–Ford (or the DAG algorithm if there is no cycle).

**3.** Path weight equals the number of edges. BFS visits vertices in increasing hop count, so the first time a vertex is reached it is reached by a minimum hop count.

**4.** `V − 1`. Pass `V` is the detection pass.

**5.** Outermost. The middle and inner loops run over the pair `(i, j)`.

**6.** `s: 0`, `a: 2`, `b: 3`, `c: 4`. The path `s-a-b-c` beats `s-a-c`.

**7.** Binary heap `Θ((V + E) log V)`. Array `Θ(V²)`.

**8.** `Θ(V E)`. The extra pass reports a negative cycle reachable from the source if any distance can still fall.

**9.** `Θ(V + E)`, by relaxing edges in topological order. A negative edge does not change that bound, because a DAG has no cycle to repair later.

**10.** Vertex 3 lies on a negative cycle. Shortest paths through that cycle are undefined.

**11.** Dijkstra finalises `a` at distance 1 and never applies `b→a`. The true distance is `100 − 100 = 0`.

**12.** After `s→a` and `s→b`, distances are `a = 4`, `b = 5`. Then `b→a` sets `a = 5 + (−2) = 3`. Another full round sees `b→a` again: `5 + (−2) = 3`, no improvement. Later rounds do nothing.

**13.** 4, the direct edge. The MST path around the other two edges weighs 6 and is not the shortest path.

**14.** Negated weights are negative, so Dijkstra may finalise a vertex too early. On a DAG, relax in topological order with the negated weights (or with `max` on the original weights). Time stays `Θ(V + E)`.

**15.** Floyd is `Θ(V³)`. Johnson is one Bellman–Ford plus `V` heap Dijkstras, `Θ(V E log V)` with a binary heap. When `E` is much smaller than `V²`, that product is smaller than `V³`.

**16.** Dijkstra’s proof needs every leftover tail to have non-negative weight. A negative edge can improve a vertex after it has been finalised. No negative cycle means shortest paths exist; Bellman–Ford will find them. Dijkstra’s hypothesis is still false.

**17.** The source is fine, but every other vertex already has distance 0, which is smaller than any positive path, so relaxations never raise a distance and the algorithm reports 0 everywhere it fails to overwrite. Unreachable vertices stay 0 instead of `∞`. Even reachable vertices can keep a bogus 0 if you implemented relaxation only in one direction. Initialise non-sources to `∞`.

**18.** `Θ(V E) = Θ(1000 · 3000) = Θ(3 · 10^6)`, which is `Θ(V E)`, not `Θ(V³) = Θ(10^9)`.

**19.** No. The two arcs form a cycle of weight `−6`. Distances are undefined.

**20.** The recurrence needs paths into `k` and out of `k` that only use intermediates below `k`. Those values are ready only after the previous `k` iteration has finished for all pairs. An inner `k` uses intermediate values from the same sweep, which are not the `D_{k−1}` table.

**21.** Take the unsettled vertex `u` of smallest tentative distance. Any other path to `u` first exits the finalised set at some vertex `x`. The prefix to `x` already weighs at least `dist[u]`, because `x` was unsettled and `u` was the closest such vertex. The suffix from `x` to `u` weighs at least 0 only because every edge weighs at least 0. That is the step which fails if a negative edge sits on the suffix.

**22.** If a shortest path exists, some shortest path is simple: a cycle that is not negative can be removed without increasing the weight, and a negative cycle was assumed absent. A simple path has at most `V − 1` edges. Round `k` has correctly considered every path of at most `k` edges.

**23.** A path `s = v0 → v1 → … → vt` changes by `Σ (h(v_i) − h(v_{i+1})) = h(s) − h(t)`. The telescoping sum depends only on the endpoints. Every competing path from `s` to `t` shifts by the same amount, so the minimum stays on the same path. Adding `h(t) − h(s)` (the sign depends on how you defined the reweighting; with `w + h(u) − h(v)` the new path weight is old weight `+ h(s) − h(t)`) translates the number back.

**24.** Topologically sort, initialise the source to 0 and other vertices to `−∞`, and relax with `max` and the original weights: `dist[v] = max(dist[v], dist[u] + w(u, v))`. Time `Θ(V + E)`. Equivalently, negate weights, run the shortest-path DAG pass, and negate the results.

**25.** Both are `Θ(V³)` when Dijkstra uses an array. Array Dijkstra from every source requires non-negative weights. Floyd–Warshall allows negative edges and reports a negative cycle on the diagonal.

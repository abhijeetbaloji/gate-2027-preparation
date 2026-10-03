# Shortest Paths — Learning Notes

A shortest path from `s` to `t` is a path whose total edge weight is minimum. The right algorithm depends on the sign of the weights, on whether you want one source or all pairs, and on whether the graph is a DAG. Minimum spanning trees solve a different problem: they minimise a sum of tree edges, not a path between two vertices.

---

## 1. The problem, and when a shortest path exists

**Input.** A directed or undirected graph with weights `w(e)`. Undirected edges are usually treated as two directed edges of the same weight. A path’s weight is the sum of its edge weights, not the number of edges, unless every weight is 1.

**Single source.** Distances from one `s` to every vertex.

**Single pair.** One `s` and one `t`. In the worst case the standard algorithms still compute a single-source result. There is no asymptotic shortcut in the general comparison model that is worth a different syllabus entry.

**All pairs.** Distances between every ordered pair.

**Optimal substructure.** A shortest path from `s` to `t` that goes through `u` is a shortest path from `s` to `u` plus a shortest path from `u` to `t`. If the first piece were not shortest, splicing a better one would improve the whole path. This is why the algorithms relax edges: `dist[v] = min(dist[v], dist[u] + w(u, v))`.

**Negative cycles.** If a cycle reachable from `s` has negative total weight, walking around it decreases the distance forever. No shortest path exists from `s` to vertices that can reach that cycle’s aftermath. Algorithms must either assume there is no negative cycle or detect one. A negative *edge* is not the same thing as a negative *cycle*.

**Unreachable vertices.** Their distance is defined as `∞`, not 0. Initialising every distance to 0 makes every vertex look like a source.

---

## 2. Unweighted graphs: BFS

If every edge has weight 1, breadth-first search computes distances. The queue order is the order of increasing hop count, and hop count is the weight. Time `Θ(V + E)` on adjacency lists, `Θ(V²)` on a matrix. Auxiliary space `Θ(V)`.

Why a weighted edge breaks it: one hop of weight 100 can lose to two hops of weight 1. BFS never sees the weights. Full traversal properties are in the graph-traversal notes.

Use BFS only when the statement is “minimum number of edges” or every relevant weight is equal and positive.

---

## 3. Dijkstra’s algorithm

**What it is.** Single source, every weight `≥ 0`. Grow a set `S` of vertices whose distances are final. Each step moves into `S` the unsettled vertex `u` with the smallest tentative `dist[u]`, then relaxes every edge out of `u`.

**Why the greedy choice is safe.** Suppose `u` is the unsettled vertex of smallest tentative distance, and the tentative value was set by some path that stays inside `S` until the last hop. Any other path from `s` to `u` must at some point leave `S`. Let `x` be the first vertex on that path outside `S`. The path weight up to `x` is already at least `dist[u]`, because `u` was the closest unsettled vertex, and the rest of the path from `x` to `u` has weight `≥ 0`. So that path cannot beat `dist[u]`. Non-negativity is the sentence that makes the tail of the path unable to repair a bad prefix.

**Why a negative edge breaks it.** The tail can have negative weight, so a path that looks worse at `x` can become better by the time it reaches `u`. Dijkstra will already have finalised `u` and will not reopen it.

**Example.** Vertices `s, a, b`. Edges `s→a` weight 1, `s→b` weight 100, `b→a` weight `−100`. True distance to `a` is `100 + (−100) = 0`, via `b`. Dijkstra finalises `a` at distance 1 first, because 1 < 100, and never uses the negative edge to repair `a`. With all weights positive the same graph shape is fine.

**A correct small run.** Edges `s→a` 2, `s→b` 5, `a→b` 1, `a→c` 4, `b→c` 1. Source `s`.

| Step | Finalise | dist s, a, b, c |
|------|----------|-----------------|
| start | — | 0, 2, 5, ∞ |
| 1 | s | relaxes to a=2, b=5 |
| 2 | a (dist 2) | b becomes `min(5, 2+1)=3`, c becomes 6 |
| 3 | b (dist 3) | c becomes `min(6, 3+1)=4` |
| 4 | c | 4 |

**Complexity.**

| Implementation | Time | Why | Extra space |
|----------------|------|-----|-------------|
| Array scan of unsettled vertices | `Θ(V² + E) = Θ(V²)` | `V` selections, each scanning `V` keys; each edge relaxed once | `Θ(V)` |
| Binary heap | `Θ((V + E) log V)` | Each decrease-key and extract is `O(log V)` | `Θ(V)` |
| Fibonacci heap | `Θ(E + V log V)` | Decrease-key amortised `O(1)`, extract `O(log V)` | `Θ(V)` |

Best, average, and worst follow `V` and `E`, not the numeric weights, as long as weights stay non-negative so the algorithm is valid. A binary heap is the usual sparse-graph bound. The array is the usual dense-graph bound.

**When to use.** One source, non-negative weights, a shortest-path tree or distances.

**When not to use.** Any negative weight. All-pairs on a dense graph may be simpler as Floyd–Warshall, `Θ(V³)`, which matches running the array Dijkstra from every vertex and also allows negative edges that do not form a negative cycle. A DAG has a faster linear algorithm below.

**Comparison with Prim.** Both grow a set and pick a minimum key. Prim’s key is the weight of a single edge leaving the tree. Dijkstra’s key is a path weight from the source. Swapping the two keys solves the wrong problem.

---

## 4. Bellman–Ford

**What it is.** Single source. Negative edges allowed. Detects a negative cycle reachable from the source.

**Why `V − 1` rounds.** A simple path has at most `V − 1` edges. Relax *every* edge once per round. After round `k`, `dist[v]` is the minimum weight of a path from `s` to `v` that uses at most `k` edges, provided no negative cycle has been feeding it. This is DP on the number of edges. After `V − 1` rounds every simple path has been considered. A further round that still decreases some `dist[v]` can only be using a cycle, and that cycle’s weight is negative.

```
dist[s] = 0
dist[v] = ∞ for v ≠ s
repeat V − 1 times:
    for each edge u→v with weight w:
        if dist[u] + w < dist[v]:
            dist[v] = dist[u] + w
one more pass:
    if any edge can still relax: report a negative cycle reachable from s
```

**Example.** Edges `s→a` weight 4, `s→b` weight 5, `b→a` weight `−2`. There is no cycle.

Round 1, edge order `s→a`, `s→b`, `b→a`: `a` becomes 4, `b` becomes 5, then `b→a` improves `a` to 3. Later rounds do not change either distance. The shortest path to `a` is `s→b→a`, weight 3, not the direct edge.

A negative cycle is a different picture. Add `a→b` of weight 1. The cycle `a→b→a` weighs `1 − 2 = −1`. Distances keep falling, and the detection pass reports the cycle.

**Complexity.** Each of `Θ(V)` rounds scans `E` edges. Time `Θ(V E)`. Space `Θ(V)` for distances. On a simple graph `E = O(V²)`, so this is `O(V³)`, matching Floyd’s order but only for one source. Best and worst are the same unless you stop early when a round changes nothing. Early stop is correct when there is no negative cycle; a negative cycle never settles, so you must still cap the rounds at `V`.

**When to use.** Negative edges, or you must prove there is no negative cycle reachable from `s`.

**When not to use.** Non-negative sparse graphs, where Dijkstra’s heap is `Θ(E log V)`, faster than `Θ(V E)`. Unweighted graphs, where BFS is linear.

**GATE trap.** Stopping at `V − 1` and ignoring the detection pass when the question asks “does a negative cycle exist?”. Also running only one round.

---

## 5. Single source on a DAG

**Rule.** Topologically sort the vertices, which takes `Θ(V + E)`. Process vertices in that order and relax each outgoing edge when the vertex is processed.

**Why one pass works.** Every path respects the topological order, so when you process `u`, every predecessor of `u` is finished and `dist[u]` is final. There is no cycle to reopen a vertex. Negative weights are allowed. A negative *cycle* cannot exist in a DAG.

**Complexity.** `Θ(V + E)` time, `Θ(V)` extra space. This is strictly better than both Dijkstra and Bellman–Ford, but only because the DAG promise gives you an order.

**When not to use.** The graph has a cycle, even a positive one. Topological order does not exist. Use Dijkstra or Bellman–Ford according to the signs.

**Longest path in a DAG.** Negate the weights and run the same algorithm, or replace `min` by `max` and initialise distances to `−∞`. Longest paths in general graphs are NP-hard; the DAG promise is what makes this legal. Do not “negate and run Dijkstra”: negation creates negative edges, which Dijkstra cannot take. Negate and run the DAG algorithm, or Bellman–Ford.

---

## 6. Floyd–Warshall (all pairs)

**State.** `D_k[i][j]` is the shortest-path weight from `i` to `j` using only intermediate vertices in `{1, …, k}`.

```
D_0[i][j] = w(i, j) if the edge exists, 0 if i = j, ∞ otherwise
D_k[i][j] = min( D_{k−1}[i][j],  D_{k−1}[i][k] + D_{k−1}[k][j] )
```

**Why the recurrence is correct.** A best path that is allowed to use vertex `k` either does not use it, or it goes from `i` to `k` and from `k` to `j` using only lower-numbered intermediates. Optimal substructure glues those two pieces. There is no third shape.

**In-place update.** One matrix is enough if you update carefully: when computing `k`, the cells `D[i][k]` and `D[k][j]` are already final for this `k` because a path through `k` twice would only help if a negative cycle touched `k`. The standard triple loop

```
for k in 1..V:
    for i in 1..V:
        for j in 1..V:
            D[i][j] = min(D[i][j], D[i][k] + D[k][j])
```

is correct for the no-negative-cycle case. The `k` loop must be outermost. Swapping loops changes the meaning and can be wrong.

**Negative cycle detection.** After the algorithm, some `D[i][i] < 0`. A vertex on a negative cycle can return to itself more cheaply than the empty path.

**Complexity.** `Θ(V³)` time, always. Three nested loops, no early exit that changes the class. Space `Θ(V²)`. Best, average, and worst coincide.

**Comparison.**

| Need | Algorithm | Time |
|------|-----------|------|
| All pairs, dense, possibly negative edges, no negative cycle | Floyd–Warshall | `Θ(V³)` |
| All pairs, non-negative, sparse | Dijkstra from each vertex | `Θ(V E log V)` with binary heaps |
| All pairs, negative edges, sparse | Johnson’s algorithm | `Θ(V E + V E log V)` typical binary-heap form |

Johnson: add a new source with zero-weight edges to every vertex, run Bellman–Ford to get potentials `h(v)`, reweight each edge `u→v` to `w(u, v) + h(u) − h(v)`, which makes every new weight non-negative and preserves path comparisons, then run Dijkstra from each vertex and translate distances back by `dist'(u, v) − h(u) + h(v)`. If Bellman–Ford finds a negative cycle, stop. This is the sparse all-pairs algorithm. Floyd is simpler when `E` is `Θ(V²)`.

---

## 7. Choosing an algorithm

| Graph | Algorithm | Time (lists, binary heap where relevant) |
|-------|-----------|------------------------------------------|
| Unweighted | BFS | `Θ(V + E)` |
| Non-negative, one source, sparse | Dijkstra, heap | `Θ(E log V)` |
| Non-negative, one source, dense | Dijkstra, array | `Θ(V²)` |
| Negative edges, one source | Bellman–Ford | `Θ(V E)` |
| DAG, one source, any signs | Topological relaxation | `Θ(V + E)` |
| All pairs, general dense | Floyd–Warshall | `Θ(V³)` |
| Negative cycle question from one source | Bellman–Ford extra pass | `Θ(V E)` |
| Negative cycle anywhere | Floyd diagonal, or Bellman–Ford from a super-source | `Θ(V³)` or `Θ(V E)` |

**Do not use.**

- Dijkstra with a negative edge.
- BFS with unequal weights.
- An MST algorithm, when the question asks for a path length.
- Bellman–Ford on a DAG when the linear topological algorithm is available and the question asks for the best bound.
- Floyd’s loop order with `k` inside.

---

## 8. A few more exam facts

**Shortest-path tree.** Parent pointers from Dijkstra or Bellman–Ford form a tree of shortest paths from `s`, if no negative cycle exists. It is not an MST.

**Zero-weight cycles.** Distances stay well defined. A shortest path can be chosen simple. Detection of a negative cycle looks for a *strict* decrease, so a zero cycle does not trigger it.

**Undirected negative edge.** Treated as two arcs, it is already a negative cycle of length 2 if you can traverse the edge both ways (`w + w = 2w < 0`). An undirected graph with a negative edge has no shortest path between its endpoints in the usual walk model. Questions that want undirected negative weights are rare; read whether the graph is directed.

**Difference constraints.** A system `x_i − x_j ≤ c_k` is a graph with an edge `j→i` of weight `c_k`. The system is feasible if and only if there is no negative cycle. Bellman–Ford decides it. This is the constraint-graph application of the same algorithm.

**Reweighting does not let you run Dijkstra on the original negative edges without potentials.** Subtracting a constant from every edge changes path weights by a multiple of the number of edges, which can reorder paths of different lengths. Johnson’s `h(u) − h(v)` correction depends on the endpoints only, so every `s`-to-`t` path changes by the same `h(s) − h(t)`, and the shortest path stays the shortest path.

---

## 9. Common GATE traps

1. Dijkstra on a graph that contains a negative edge, even if you “know” there is no negative cycle. Correctness needs non-negativity, not merely the absence of a negative cycle. Bellman–Ford is the algorithm that survives a negative edge.
2. BFS on weighted input.
3. `dist` initialised to 0 for every vertex.
4. Floyd with `k` not outermost.
5. Negative cycle declared because a negative edge exists.
6. MST weight reported as a distance.
7. `Θ(V³)` for one-source Bellman–Ford on a sparse graph. The tight bound is `Θ(V E)`.
8. Longest path by negating weights and calling Dijkstra.
9. Early-exit Bellman–Ford used as a negative-cycle test without a `V`-th pass cap. A cycle keeps changing forever; you need the extra pass, not an unlimited loop.
10. Unreachable vertex printed as distance 0.

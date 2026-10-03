# Graph Traversals — Learning Notes

A traversal visits every vertex and every edge in a controlled order. BFS and DFS are the two orders. Almost every later graph algorithm is one of them plus a rule about what to do when you see an edge. Graph *representation* is also taught under Programming and Data Structures; the facts needed to price a traversal are repeated here.

---

## 1. Representation, because it sets the time bound

**Adjacency list.** For each vertex, a list of its neighbours. Space `Θ(V + E)`. Finding all neighbours of `u` takes time proportional to `deg(u)`.

**Adjacency matrix.** A `V × V` table, 1 if the edge exists. Space `Θ(V²)`. Testing one edge is `Θ(1)`. Listing all neighbours of `u` is `Θ(V)`, even if `u` has one neighbour.

**Why traversals are quoted as `Θ(V + E)`.** With lists, each vertex is enqueued or started once, and each edge is examined a constant number of times (twice in an undirected graph if you store both directions). Sum of degrees is `2E` undirected and `E` directed. Total `Θ(V + E)`.

With a matrix, scanning every row costs `Θ(V²)` even when the graph is a tree (`E = V − 1`). Say which representation the question uses.

**GATE trap.** `O(E)` with no `V`. An isolated vertex still needs to be noticed, so a forest of isolated vertices costs `Θ(V)`. The safe bound is `Θ(V + E)`.

---

## 2. Breadth-first search

**What it is.** From a source `s`, visit vertices in order of increasing number of edges from `s`.

**Intuition.** Expand a wave. Everyone at distance `d` is finished before anyone at distance `d + 1` starts.

**How it works.** A queue holds the wavefront. A colour or a distance array stops you from enqueueing a vertex twice.

```
colour[*] = white
dist[s] = 0
enqueue s
while the queue is not empty:
    u = dequeue
    for each neighbour v of u:
        if colour[v] is white:
            colour[v] = grey
            dist[v] = dist[u] + 1
            parent[v] = u
            enqueue v
    colour[u] = black
```

Vertices not reached keep an infinite distance. On a disconnected graph, restart from each unvisited vertex if you need every component. That full traversal is still `Θ(V + E)`.

**Example.** Undirected edges `{1—2, 1—3, 2—4, 3—4, 4—5}`, source 1.

- Dequeue 1, discover 2 and 3. Distances 1.
- Dequeue 2, discover 4. Distance 2.
- Dequeue 3, 4 is already grey, skip.
- Dequeue 4, discover 5. Distance 3.

Queue order of first discovery: 1, 2, 3, 4, 5. Another valid order discovers 3 before 2 if 3 appears first in the adjacency list. The distances do not change.

**Why distances are shortest-path lengths in an unweighted graph.** By induction on the dequeue order: when `v` is first discovered from `u`, every closer vertex has already been enqueued. If a shorter path to `v` existed, its second-to-last vertex would have been dequeued earlier and would have discovered `v` sooner. Edge weights of 1 are what make “fewer edges” the same as “smaller weight”. A weight of 5 on an edge breaks the argument: BFS would still count edges, not weight.

**Complexity.**

| Representation | Time | Why | Auxiliary space |
|----------------|------|-----|-----------------|
| Lists | `Θ(V + E)` | Each vertex once, each edge once | `Θ(V)` queue and colours |
| Matrix | `Θ(V²)` | Each row scanned fully | `Θ(V)` besides the matrix |

Best, average, and worst match for a given graph: BFS does not stop early unless you are searching for one target and you find it. A single-source shortest path in an unweighted graph still looks at the whole reachable component in the worst case.

**Properties.**

- The BFS tree (parent pointers) contains a shortest path from `s` to every reachable vertex, measured in number of edges.
- The first time you see a vertex, you see it along a shortest path.
- Cross edges in an undirected BFS tree connect vertices on the same level or on adjacent levels, never a level difference of 2 or more. That is a useful check, and it is why a back edge to a non-parent detects an odd cycle when you are 2-colouring.

**When to use.** Unweighted distances, fewest hops, level order, bipartiteness, shortest path in a maze with unit steps.

**When not to use.** Weighted edges, unless every weight is identical. Negative weights. All-pairs distances on a dense weighted graph (Floyd–Warshall). A weighted non-negative graph needs Dijkstra.

**Comparison with DFS.** DFS uses a stack (often the call stack) and dives down one branch. Its tree paths are not shortest. DFS uses less auxiliary memory in some implementations only in the sense that the recursion depth may be smaller than the widest BFS level; in the worst case both are `Θ(V)`. BFS queue can hold `Θ(V)` vertices (a star’s leaves). DFS stack can hold `Θ(V)` vertices (a long path).

---

## 3. Depth-first search

**What it is.** From `u`, recursively visit an unvisited neighbour, and only then try the next neighbour. Equivalently, use an explicit stack.

**Intuition.** Walk until you are stuck, then backtrack to the last choice you have not tried.

```
time = 0
DFS-all:
    for each vertex u:
        if u is white: DFS(u)

DFS(u):
    colour[u] = grey
    time = time + 1
    disc[u] = time
    for each neighbour v of u:
        if v is white:
            parent[v] = u
            DFS(v)
    colour[u] = black
    time = time + 1
    fin[u] = time
```

`disc` is the discovery time. `fin` is the finish time, when the entire reachable unvisited neighbourhood has been explored. The interval `[disc[u], fin[u]]` contains the intervals of all descendants of `u` in the DFS forest. This parenthesis theorem is the reason finish times give a topological order.

**Example.** Directed edges `1→2, 1→3, 2→4, 3→4`, start at 1, adjacency order 2 then 3.

- Discover 1, go to 2, go to 4. Finish 4, finish 2.
- Back at 1, go to 3. 4 is already black, so 3 does not recurse. Finish 3, finish 1.

One possible timing: `disc = {1:1, 2:2, 4:3, 3:6}`, `fin = {4:4, 2:5, 3:7, 1:8}`. Another adjacency order swaps the roles of 2 and 3. Times depend on the adjacency order; the parenthesis property does not.

**Complexity.** Same as BFS: `Θ(V + E)` on lists, `Θ(V²)` on a matrix. Auxiliary space `Θ(V)` for colours and, in the worst case, `Θ(V)` stack frames. Best and worst are the same for a full traversal of a given graph.

**Edge classification (directed graphs), relative to one DFS forest.**

| Class | Meaning | Colour of `v` when edge `u→v` is examined |
|-------|---------|-------------------------------------------|
| Tree | `v` was white; the edge enters the forest | white |
| Back | `v` is an ancestor of `u`, including a self-loop | grey |
| Forward | `v` is a descendant, and the edge is not a tree edge | black, and `disc[u] < disc[v]` |
| Cross | `v` is in another branch | black, and `disc[v] < disc[u]` |

**Undirected graphs** only have tree edges and back edges. A back edge is an edge to a visited vertex that is not the parent. Forward and cross are not a separate category once each undirected edge is seen from both ends; the usual statement is “non-tree edges are back edges”.

**Why a directed back edge means a cycle.** A grey vertex on the stack is an ancestor. An edge to an ancestor closes a cycle. Conversely, a directed cycle forces some back edge in every DFS: the first vertex of the cycle to finish has a successor on the cycle that is still grey. So a directed graph is acyclic if and only if DFS produces no back edge.

**Undirected cycle test.** A back edge to a vertex other than the parent means a cycle. The parent edge is not a cycle; it is the same edge you just walked.

---

## 4. What the two orders are for

**Connected components (undirected).** Each restart of BFS or DFS is one component. Count restarts. Time `Θ(V + E)`.

**Bipartite test.** BFS (or DFS) 2-colours the graph. An edge with both ends the same colour means an odd cycle, so the graph is not bipartite. If every edge joins different colours, it is bipartite. Why BFS works: levels are the colours. An edge inside a level is an odd cycle.

**Topological order (directed acyclic graph).** Finish times in decreasing order are a topological order: if there is an edge `u→v`, then `v` finishes before `u`. Reason: when the edge is examined, `v` cannot be grey (that would be a back edge and a cycle). If `v` is white, it becomes a descendant and finishes before `u`. If `v` is black, it has already finished. Kahn’s algorithm is the BFS version: repeatedly remove a vertex of indegree 0. If you run out of vertices before the graph is empty, a cycle remains.

**Strongly connected components.** Kosaraju: DFS for finish times, reverse every edge, DFS in decreasing finish order on the reversed graph. Each tree in the second DFS is one SCC. Both passes are `Θ(V + E)`. Tarjan’s one-pass algorithm computes the same partition with a stack and low-link values; either algorithm is enough for the exam if the question asks for the components rather than a specific implementation detail.

**Path existence.** Either traversal. DFS is natural for “is there a path”, BFS for “shortest unweighted path”.

**Articulation points and bridges** can be computed with DFS discovery times and low values in `Θ(V + E)`. Know that they are DFS applications. The low-value formulas are worth deriving only if you are implementing them: `low[u] = min(disc[u], low[child], disc[back-edge target])`. A root is an articulation point if it has two or more DFS children. A non-root `u` is one if some child has `low[child] ≥ disc[u]`.

---

## 5. BFS tree versus DFS tree

On the same graph the trees can differ.

- BFS tree: each tree path from the source is a fewest-edge path. The tree is short and wide when the graph is.
- DFS tree: tree paths can be long even when a short path exists. From source 1 with edges `1—2, 1—3, 2—3`, DFS might walk `1—2—3` and never use `1—3` as a tree edge. The BFS tree uses `1—2` and `1—3` and leaves `2—3` as a non-tree edge. Distance of 3 from 1 is 1, which DFS’s tree path overstates as 2.

**GATE trap.** Reading a DFS parent pointer as a shortest path. Only the BFS parent (on an unweighted graph) or a shortest-path tree from Dijkstra or Bellman–Ford has that meaning.

---

## 6. Choosing a traversal

| Question | Tool | Time on lists |
|----------|------|----------------|
| Fewest edges from `s` | BFS | `Θ(V + E)` |
| Any path, maze with a pencil | DFS | `Θ(V + E)` |
| Directed cycle | DFS back edges, or Kahn stops early | `Θ(V + E)` |
| Undirected cycle | DFS back edge to a non-parent, or Union-Find while adding edges | `Θ(V + E)` |
| Topological order | Decreasing finish time, or Kahn | `Θ(V + E)` |
| Bipartite | 2-colour BFS or DFS | `Θ(V + E)` |
| SCCs | Kosaraju or Tarjan | `Θ(V + E)` |
| Weighted non-negative distance | Dijkstra, not plain BFS | see shortest paths |
| Weighted with negatives | Bellman–Ford | `Θ(V E)` |

---

## 7. Common GATE traps

1. BFS used on weighted edges as if it minimised weight.
2. Time `O(E)` forgetting isolated vertices, or `O(V²)` quoted for a list representation.
3. DFS finish order reversed: topological order is **decreasing** finish time, not increasing discovery time.
4. An undirected parent edge reported as a cycle.
5. Grey versus black: a back edge goes to grey, not to every black vertex.
6. Restart forgotten on a disconnected graph, so only one component is visited.
7. Queue and stack swapped: BFS is the queue, DFS is the stack.
8. Shortest path read off DFS parents.
9. Kosaraju’s second pass run on the original graph instead of the transpose, or in increasing finish order.
10. Matrix-scan time left as `O(V + E)`.

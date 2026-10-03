# Graph Traversals — Shortcuts

### Unit weights → BFS; real weights → a shortest-path algorithm

**Shortcut.** If every edge counts as one hop, BFS distances are optimal. If edges have different weights, stop.

**Why it works.** The BFS proof inducts on the number of edges. A heavy edge can be one hop and still be a bad path.

**When to use.** Maze grids, unweighted social graphs, “minimum number of edges”.

**Example.** Edges of weight 1 and 100. BFS may return the weight-100 edge because it is one hop.

**Limitation.** Equal positive weights can be scaled to 1 and then BFS applies. A zero-weight edge is not a problem for “number of edges”, but it is a different question from “weight”.

---

### Decreasing finish time is the topological order

**Shortcut.** Run DFS. Output vertices from latest finish to earliest finish.

**Why it works.** An edge `u→v` cannot run from a finished vertex back to a grey ancestor in a DAG, so `v` finishes first.

**When to use.** “A valid order of courses / tasks” on a DAG.

**Example.** Finish times 4, 3, 2, 1 for vertices A, B, C, D means the order A, B, C, D only if those are the finish times in that decreasing sense: the vertex with finish 4 comes first.

**Limitation.** If DFS reports a back edge, no topological order exists. Do not sort discovery times and call that topological.

---

### Grey means “on the stack”, and that is the cycle test

**Shortcut.** In a directed graph, an edge into a grey vertex is a back edge and a cycle. An edge into a black vertex is forward or cross, not automatically a cycle by that one test.

**Why it works.** Grey vertices are exactly the current root-to-node path.

**When to use.** Cycle detection while you DFS.

**Example.** A cross edge into a finished branch does not by itself tell you to abort; the cycle, if any, shows up as some back edge somewhere.

**Limitation.** In an undirected graph, the edge back to the parent is grey and is not a cycle. Exclude the parent.

---

### `V + E`, not `E` alone, and not `V²` on a list

**Shortcut.** List traversal is `Θ(V + E)`. Matrix traversal is `Θ(V²)`.

**Why it works.** You must look at every vertex to know it is isolated, and at every list entry to know the edges. A matrix has no sparse representation to exploit.

**When to use.** Complexity options for BFS or DFS.

**Example.** `V` isolated vertices: `E = 0`, time `Θ(V)`, not `Θ(1)`.

**Limitation.** A search that stops at a target can be faster on some inputs. The standard exam bound is the full traversal of the reachable graph.

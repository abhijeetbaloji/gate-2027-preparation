# Minimum Spanning Trees — Shortcuts

### Lightest safe edge, not shortest path

**Shortcut.** Add a lightest edge across a cut that the forest does not yet cross. Do not compute distances from a source.

**Why it works.** The exchange argument swaps that edge into some MST without increasing weight.

**When to use.** “Which edge can be added next?” in Kruskal or Prim.

**Example.** Components `{1, 2}` and `{3}`, crossing edges of weight 4 and 9. Take 4 even if some path inside a component is long.

**Limitation.** The lightest edge *inside* a component closes a cycle. Same Find-root means reject.

---

### Distinct weights → one MST

**Shortcut.** If no two edges share a weight, the MST is unique. If they do, compute the weight and allow more than one tree.

**Why it works.** The lightest disagreeing edge would strictly improve the tree that omitted it.

**When to use.** “The MST is unique. True or false?”

**Example.** Two edges of weight 2 between the same pair of components: either can be chosen.

**Limitation.** Uniqueness of the *weight* always holds by definition of minimum. Uniqueness of the *edge set* needs distinctness or a separate argument.

---

### Dense → Prim `V²`. Sparse → Kruskal or heap Prim

**Shortcut.** `E` near `V²`: Prim’s array scan is `Θ(V²)`, better than sorting `Θ(V² log V)` edges. `E` near `V`: both Kruskal and binary-heap Prim are `Θ(V log V)`.

**Why it works.** The sort pays `log E` per edge. The array Prim pays `V` per vertex and does not sort.

**When to use.** Complexity comparison questions.

**Example.** Complete graph, `V = 500`: prefer `Θ(V²)` Prim over Kruskal’s sort.

**Limitation.** The Fibonacci bound `Θ(E + V log V)` beats `Θ(V²)` only in theory for sparse graphs; it is not a reason to avoid `Θ(V²)` Prim on a dense matrix. Also, negative weights do not change this table.

---

### A negative edge does not disqualify an MST algorithm

**Shortcut.** Run Kruskal or Prim unchanged if some weights are negative. Do not switch to Dijkstra.

**Why it works.** Safety is an exchange of edges, not a sum of a path that could be undercut later.

**When to use.** The stem includes a minus sign and asks for an MST.

**Example.** Edge weight `−5` is simply the lightest edge in most cuts it crosses, so it is taken unless it closes a cycle.

**Limitation.** A negative edge does not mean the tree path is a shortest path. If the question asks for distances, leave this shortcut.

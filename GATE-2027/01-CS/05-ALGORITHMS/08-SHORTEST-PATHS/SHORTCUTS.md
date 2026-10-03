# Shortest Paths — Shortcuts

### Read the signs, then the shape

**Shortcut.** Non-negative: Dijkstra. Some negative edge: Bellman–Ford. A DAG: one topological pass, even if weights are negative. All pairs, dense: Floyd–Warshall. Unweighted: BFS.

**Why it works.** Each algorithm’s proof uses exactly that promise. Dijkstra needs a non-negative tail. The DAG pass needs an order with all predecessors first. Floyd tries every intermediate. BFS counts hops.

**When to use.** The first line of a shortest-path question.

**Example.** One negative edge and a cycle elsewhere: Bellman–Ford, not Dijkstra, even if you suspect the cycle is positive.

**Limitation.** “No negative cycle” does not restore Dijkstra. Absence of a negative cycle is Bellman–Ford’s and Floyd’s operating condition. Dijkstra’s condition is stronger: no negative edge at all.

---

### A negative edge is not a negative cycle

**Shortcut.** One edge of weight `−1` does not by itself make distances undefined. A reachable cycle whose weights sum to a negative number does.

**Why it works.** A simple path can use the edge once and stop. A negative cycle can be repeated.

**When to use.** “Does a shortest path exist?”

**Example.** `s→a` weight `−1`, and no way back to `s`. Distance to `a` is `−1`.

**Limitation.** In an undirected graph, storing the edge in both directions creates the cycle `−1 + −1`. Check directed versus undirected before you declare the distance defined.

---

### `k` is the outer loop

**Shortcut.** Floyd–Warshall iterates the intermediate vertex outside the pair `(i, j)`.

**Why it works.** The state is “intermediates among the first `k` vertices”. When you use `k`, the paths `i→k` and `k→j` must already be optimal for intermediates below `k`. That is true only if those pairs were finished in earlier `k` rounds.

**When to use.** Any triple-loop pseudocode.

**Example.** `for k, for i, for j`, update by `D[i][k] + D[k][j]`.

**Limitation.** The in-place loop is justified when you are not simultaneously depending on a half-updated higher intermediate. Do not reorder to `for i, for j, for k` and expect the same fills.

---

### Negating weights is safe only for the DAG (or Bellman–Ford) longest path

**Shortcut.** Longest path in a DAG: flip the sign and run the topological shortest-path pass, then flip the sign of the answer. Do not feed the negated graph to Dijkstra.

**Why it works.** Negation turns a maximum into a minimum and creates negative edges. The DAG algorithm allows those edges. Dijkstra does not.

**When to use.** “Longest path” together with “directed acyclic”.

**Example.** A chain of two edges, weights 3 and 1. Longest path weight 4. Negated shortest path is `−4`, which you negate back.

**Limitation.** In a graph with cycles, longest simple path is NP-hard. Negation plus Bellman–Ford finds a shortest path in the negated graph, which is a longest path only if you allow the algorithm to stop; a positive cycle in the original graph is a negative cycle after negation and means the longest walk is unbounded.

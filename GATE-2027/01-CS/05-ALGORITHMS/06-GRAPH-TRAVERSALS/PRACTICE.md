# Graph Traversals — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Why is a list-based BFS `Θ(V + E)` rather than `Θ(E)`?

**2.** Which data structure implements BFS, and which implements DFS?

**3.** Why are BFS distances optimal only for unweighted graphs?

**4.** What is a directed back edge, in terms of colour?

**5.** How do you read a topological order off DFS times?

### Level 2 — Standard

**6.** Undirected graph, vertices 1..4, edges `1—2, 1—3, 2—4`. BFS from 1 with adjacency lists sorted numerically. Give distances.

**7.** Time of DFS on a matrix representation of a graph with `V = 100` and `E = 100`.

**8.** Directed edges `1→2, 2→3, 3→1`. Does DFS report a back edge if it starts at 1 and follows the only outgoing edge each time?

**9.** An undirected DFS walks `1—2` and then sees the edge `2—1`. Is there a cycle?

**10.** Kosaraju’s two passes: which graph is the second pass on, and in what order are starts chosen?

### Level 3 — Multi-step

**11.** DAG edges `A→B, A→C, B→D, C→D`. One DFS from A visits B before C. Give one valid finish-time order and the topological order it produces.

**12.** Edges `1—2, 2—3, 3—1`. Run a 2-colouring from 1. Where does it fail?

**13.** A directed graph’s DFS yields no back edge. What else is true, and which algorithm then produces a linear order?

**14.** Star graph: one centre, `n − 1` leaves, source = centre. Size of the BFS queue after the centre is dequeued? Size of a DFS stack if the implementation recurses into a leaf and returns immediately?

**15.** You have an adjacency matrix and you need one shortest unweighted path. Time?

### Level 4 — Trap-based

**16.** “DFS parent pointers from `s` give fewest-edge paths.” Give a three-vertex counterexample.

**17.** Edges `A→C`, `B→C`, `A→B`. DFS from A follows C before B. Discovery order is A, C, B. Why is that not a topological order? Which order do the finish times give instead?

**18.** Undirected triangle, parent edge counted as a cycle, so a tree is also “cyclic” under that bug. Explain the false positive on a single edge `1—2`.

**19.** BFS complexity on lists is answered `Θ(V²)` because the graph might be complete. When is `Θ(V²)` the right simplified form, and when is it not?

**20.** Second Kosaraju pass walks decreasing finish times on the original, unreversed graph. What invariant is lost?

### Level 5 — Challenge

**21.** Prove that if `u→v` is an edge in a DAG, then `v` finishes before `u` in a DFS that classifies edges as usual. Consider the colour of `v` when the edge is first examined.

**22.** Why does an odd cycle prevent a 2-colouring, and why does a failed BFS colouring produce an odd cycle?

**23.** Show that BFS with all weights equal to `c > 0` still gives a minimum-weight path. What goes wrong if one weight is `2c` and another is `c`?

**24.** A graph is stored as lists. You run DFS from every vertex without a global colour array, each time on a fresh colour array, to test reachability of every pair. Time?

**25.** Kahn’s algorithm stops with a vertex left and indegree still positive. Why does the remaining graph contain a cycle?

---

## Answers and explanations

**1.** Vertices with degree 0 still take time to recognise. The vertex loop is `Θ(V)` and the edge scans sum to `Θ(E)`. Either term can dominate.

**2.** BFS uses a queue. DFS uses a stack, often the call stack.

**3.** The inductive proof orders vertices by hop distance. A single high-weight edge is one hop and can be worse than a two-hop light path.

**4.** An edge from the current vertex to a grey vertex. Grey means the vertex is an ancestor on the recursion stack.

**5.** Sort vertices by finish time, largest first. That order is topological if and only if the graph has no back edge.

**6.** `dist(1)=0`, `dist(2)=1`, `dist(3)=1`, `dist(4)=2`.

**7.** `Θ(V²) = Θ(10000)`. Sparsity does not help a matrix scan. `E` is irrelevant once you have decided to scan rows.

**8.** Yes. The path discovers 1, 2, 3 while 1 is still grey, and `3→1` is a back edge.

**9.** No. That is the parent edge, the same undirected edge already in the tree.

**10.** On the transposed graph. Source vertices for the second DFS are tried in decreasing finish time of the first DFS.

**11.** One run: discover A, B, D, finish D, finish B, then C, finish C, finish A. Finish order from earliest to latest: D, B, C, A. Decreasing finish: A, C, B, D. Check edges: A before B, A before C, B before D, C before D. All hold. (If C’s finish and B’s finish swap, A, B, C, D is the other typical order.)

**12.** Colour 1 red, 2 blue, 3 red. The edge `3—1` joins two red vertices. The cycle has length 3.

**13.** The graph is a DAG. Decreasing finish time is a topological order. Kahn’s algorithm also produces one.

**14.** The queue holds all `n − 1` leaves, so `Θ(n)`. DFS from the centre into a leaf returns immediately, so the stack depth is `Θ(1)` above the centre (the leaf frame). The star is wide, not deep.

**15.** `Θ(V²)` to BFS using a matrix, even if the path is short, in the standard bound that scans an adjacency row fully. You can stop when the target is dequeued, but a late target or a matrix row scan still costs `Θ(V²)` in the worst case.

**16.** Vertices 1, 2, 3. Edges `1—2`, `2—3`, `1—3`. DFS from 1 that walks to 2 first then to 3 sets parent of 3 to 2. The DFS-tree distance is 2. The true hop distance is 1, via `1—3`.

**17.** Edges `A→C`, `B→C`, `A→B`. Adjacency list of A is C then B. DFS from A discovers A, then C, then later B. Discovery order A, C, B places C before B, but the edge `B→C` requires B before C. So discovery order is not topological. Decreasing finish time finishes C before B before A, and the order A, B, C is valid.

**18.** From 1 the only neighbour is 2. From 2 the only neighbour is 1, which is the parent. There is no second edge. Marking the parent as a cycle says a tree edge is a cycle. A single edge is a tree, which is acyclic.

**19.** If the graph is complete, `E = Θ(V²)`, so `Θ(V + E) = Θ(V²)`. If the graph is a tree, `E = V − 1` and the list bound is `Θ(V)`, not `Θ(V²)`. Completeness is an extra assumption.

**20.** The second pass must follow edges of the transpose so that a finished source component is a sink in the reversed graph and does not leak into other components. On the original graph, decreasing finish order does not isolate SCCs.

**21.** When `u→v` is examined, `v` is not grey: a grey `v` would mean a back edge and a cycle, contradicting the DAG. If `v` is white, the recursive call finishes `v` before it returns, so `fin[v] < fin[u]`. If `v` is black, `v` has already finished, so again `fin[v] < fin[u]`.

**22.** Around an odd cycle the colours must alternate, and an odd length forces the last vertex to match the first vertex’s colour, which is a contradiction. So no 2-colouring exists. Conversely, if BFS assigns two ends of an edge the same colour, those two vertices are on the same level or the colour rule failed along a path; the standard BFS argument builds an odd closed walk from the two paths back to the first vertex where the paths diverged, and a same-colour edge means that closed walk has odd length. An undirected graph is bipartite exactly when this colouring succeeds.

**23.** Every path with `k` edges has weight `c k`. Minimising weight is the same as minimising `k`, which BFS does. If weights may be `c` or `2c`, a one-edge path of weight `2c` loses to a two-edge path of weight `c + c = 2c` only as a tie, and loses strictly to two edges of weight `c` if you compare `2c` with `c + c`. A cleaner break: one direct edge of weight `3` and a two-edge path of weights `1` and `1`. BFS returns the direct edge, weight 3, which is worse than weight 2.

**24.** Each DFS is `Θ(V + E)`, and you start `V` of them, so `Θ(V(V + E))`. A global colour array is what keeps a single full traversal at `Θ(V + E)`. All-pairs reachability is better done from a transpose or from `V` searches that share nothing; the bound above is the naive one. Floyd–Warshall is `Θ(V³)` and also answers reachability.

**25.** Every remaining vertex has indegree at least 1, so each has an incoming edge from another remaining vertex. Follow those edges backward. A finite graph must eventually repeat a vertex. The repeated vertex closes a directed cycle.

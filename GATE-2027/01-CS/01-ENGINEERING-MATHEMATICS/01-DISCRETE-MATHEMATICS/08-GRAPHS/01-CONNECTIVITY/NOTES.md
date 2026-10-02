# Graphs: Connectivity

## Graph basics

A **graph** G = (V, E) has a vertex set V and edge set E. Unless stated otherwise, assume a **simple undirected graph**: no loops, no multiple edges between the same pair.

- **Adjacent**: u and v share an edge.
- **Incident**: edge e touches vertex v.
- **Neighbourhood N(v)**: all vertices adjacent to v.

### Degree and the handshaking lemma

**deg(v)** = number of edges incident to v (loop counts twice if allowed).

**Handshaking lemma:** Σ_{v∈V} deg(v) = 2|E|.

**Derivation:** Each edge contributes exactly 2 to the total degree sum (one at each endpoint).

**Worked example:** A graph has degree sequence 3, 3, 2, 2, 2. Sum = 12, so |E| = 6. Number of odd-degree vertices must be **even** (each odd degree contributes oddly to the sum; total is even).

### Simple graph edge bounds

- Minimum |E| for connected graph on n vertices: **n − 1** (a tree).
- Maximum |E| for simple graph on n vertices: **n(n−1)/2** (complete graph K_n).

---

## Paths, walks, cycles

| Term | Definition |
|------|------------|
| **Walk** | Sequence of vertices with edges between consecutive pairs; vertices/edges may repeat |
| **Trail** | Walk with no repeated **edges** |
| **Path** | Trail with no repeated **vertices** |
| **Cycle** | Closed path of length ≥ 3 (start = end, no other repeat) |
| **Length** | Number of edges in the walk/path/cycle |

**Simple path** between u and v: path with distinct vertices.

**Worked example:** In a tree on 5 vertices, the unique simple path between any two vertices has length equal to the number of edges on that tree path. A tree with 5 vertices has exactly **4** edges.

---

## Connectedness

**Connected (undirected):** There is a path between every pair of vertices.

**Connected component:** A maximal connected subgraph. Components partition V.

**Disconnected graph:** More than one component.

**Counting components:** With no edges on n vertices → **n** components (all isolated). Adding one edge merges at most two components.

### Directed graphs

- **Weakly connected:** Connected when all directions are ignored.
- **Strongly connected:** Directed path **both ways** between every ordered pair (u, v) and (v, u).

A directed graph can be weakly connected but not strongly connected (e.g. a → b → c with no return paths).

---

## Trees and forests

**Tree:** Connected + acyclic (no cycles).

**Forest:** Acyclic graph (disjoint union of trees).

### Tree characterisations (equivalent for finite graphs)

1. Connected and |E| = |V| − 1
2. Acyclic and |E| = |V| − 1
3. Connected; removing any edge disconnects
4. Acyclic; adding any non-edge creates exactly one cycle
5. Unique simple path between every pair of vertices

**Proof sketch (|E| = |V| − 1):** Induction on n. A tree has a leaf (vertex of degree 1). Delete leaf and its edge → smaller tree with (n−1) vertices and (n−2) edges.

**Spanning tree:** Subgraph that is a tree and includes all vertices of G. Exists iff G is connected.

**Leaves:** Every tree with n ≥ 2 has at least **2 leaves** (vertices of degree 1).

**Worked example:** Prove a 7-vertex graph with 6 edges and no cycle is a tree. Acyclic + 6 = 7−1 → if connected, it is a tree. If disconnected, each component is a tree with n_i − 1 edges; sum = |V| − (#components) < |V| − 1 — contradiction. So it must be connected → **tree**.

---

## Bipartite graphs (connectivity link)

**Bipartite:** V = A ∪ B, A ∩ B = ∅, every edge goes between A and B (none inside A or B).

**Characterisation:** G is bipartite **iff** it has **no odd cycle**.

**2-colourability:** Can assign two colours so adjacent vertices differ ↔ bipartite (for non-empty G).

This connects directly to **Matching** (assignments across two parts) and **Colouring** (χ = 2 when bipartite and non-empty).

---

## Cut vertices and bridges

- **Cut vertex (articulation point):** Removing it increases the number of components.
- **Bridge (cut edge):** Removing it increases the number of components.

In a tree, **every edge is a bridge**; there is no cut vertex only if the tree is a single edge or one vertex.

---

## Euler trails and circuits

- **Euler trail:** Uses every edge exactly once.
- **Euler circuit:** Euler trail that starts and ends at the same vertex.

**Undirected existence (connected graph):**
- Euler circuit ⇔ every vertex has **even** degree.
- Euler trail (not circuit) ⇔ exactly **0 or 2** odd-degree vertices.

**Trap:** All degrees even does **not** guarantee an Euler circuit if the graph is disconnected.

---

## GATE Connection

| Idea | Where it appears |
|------|------------------|
| \|E\| = \|V\| − 1 for trees | Counting edges/vertices; spanning trees in networks |
| Handshaking lemma | Feasibility of degree sequences |
| Components | DFS/BFS in algorithms; reliability |
| Bipartite ⇔ no odd cycle | Links to **Matching** and **Colouring** |
| Tree counting (Cayley: n^(n−2) labelled trees) | Connects to **Combinatorics / Counting** |

**Graphs → Trees → Counting:** Number of labelled trees on n vertices is **n^(n−2)** (Cayley's formula). Number of edges in any tree on n vertices is **n − 1** — a constant used in many counting arguments.

---

## Common GATE traps

- Confusing **path** (no repeated vertices) with **walk** (vertices may repeat).
- Assuming a graph with |E| = |V| − 1 is a tree without checking **connectedness**.
- Forgetting odd-degree count must be even.
- Euler circuit needs **connected + all even degrees**, not even degrees alone.

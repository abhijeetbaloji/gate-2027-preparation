# Graphs: Connectivity — Quick Revision

- Handshaking: Σ deg(v) = 2|E|; odd-degree vertices come in pairs.
- Path = no repeated vertices; cycle length ≥ 3.
- Connected: path between every pair; components = maximal connected pieces.
- Tree ⇔ connected + acyclic ⇔ |E| = |V| − 1 (connected case).
- Forest: acyclic; |E| = |V| − (#components).
- Spanning tree: n − 1 edges; every tree has ≥ 2 leaves (n ≥ 2).
- Bipartite ⇔ no odd cycle ⇔ χ = 2 (non-empty).
- Bridge/cut vertex: removal increases component count.
- Euler circuit: connected + all degrees even; trail: 0 or 2 odd degrees.
- Max edges simple undirected: n(n−1)/2; min connected: n − 1.
- Cayley: n^(n−2) labelled trees on n vertices.

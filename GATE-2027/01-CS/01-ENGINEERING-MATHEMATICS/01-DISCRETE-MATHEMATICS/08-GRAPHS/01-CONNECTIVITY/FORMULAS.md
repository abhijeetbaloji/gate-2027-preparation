# Graphs: Connectivity — Formulas

| Formula | Meaning | Conditions | GATE use | Common mistake |
|---------|---------|------------|----------|----------------|
| Σ deg(v) = 2\|E\| | Handshaking lemma | Any graph, loops count twice | Find \|E\| from degrees; check feasibility | Forgetting loops count twice |
| \|E\| = \|V\| − 1 | Tree edge count | Tree (connected acyclic) | "Is this a tree?" counting | Using without checking connected |
| \|E\| = \|V\| − k | Forest edge count | k components, acyclic | Disconnected acyclic graphs | Confusing k with n |
| Min \|E\| connected | n − 1 | n vertices, undirected connected | Lower bound on edges | — |
| Max \|E\| simple | n(n−1)/2 | Simple undirected, n vertices | Complete graph K_n | Including loops/multiedges |
| Leaves ≥ 2 | Tree leaf bound | Tree, n ≥ 2 | Pigeonhole on degrees | Thinking star is exception (star has 2 leaves if n=2 only) |
| Euler circuit | All degrees even | **And** connected | Trail existence | Even degrees only, ignore connectivity |
| Euler trail | 0 or 2 odd degrees | **And** connected | Open trail | Same trap |
| n^(n−2) | Labelled trees (Cayley) | n labelled vertices | Counting trees | Confusing with spanning trees in a fixed G |
| Bipartite ⇔ no odd cycle | 2-partition exists | Finite graph | Links to χ = 2 | Checking only one odd cycle |

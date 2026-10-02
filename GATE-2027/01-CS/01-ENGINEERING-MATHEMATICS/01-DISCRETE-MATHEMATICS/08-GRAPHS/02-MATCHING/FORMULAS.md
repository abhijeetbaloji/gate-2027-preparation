# Graphs: Matching — Formulas

| Formula / theorem | Meaning | Conditions | GATE use | Common mistake |
|-------------------|---------|------------|----------|----------------|
| \|M\| ≤ min(\|A\|, \|B\|) | Upper bound bipartite | Bipartite parts A, B | Quick bound on matching | Assuming equality always |
| Perfect matching size | \|V\|/2 edges | Covers all vertices | "Does perfect matching exist?" | Ignoring \|V\| odd |
| Hall: \|N(S)\| ≥ \|S\| | Matching saturating A | Bipartite, all S ⊆ A | Existence proofs | Checking only \|A\| vs \|B\| |
| König | max matching = min cover | Bipartite | Dual problems | Applying to non-bipartite |
| K_{m,n} matching | min(m, n) | Complete bipartite | Direct MCQ | Confusing with \|E\| = mn |
| P_n matching | ⌊n/2⌋ | Path graph | Small graph counting | Off-by-one on floor |
| K_{n,n} perfect matchings | n! | Labelled parts size n | Counting assignments | Using C(n,n) instead of n! |
| Star K_{1,k} | max = 1 | Any k | Perfect matching fails for k ≥ 2 | Thinking leaves help |

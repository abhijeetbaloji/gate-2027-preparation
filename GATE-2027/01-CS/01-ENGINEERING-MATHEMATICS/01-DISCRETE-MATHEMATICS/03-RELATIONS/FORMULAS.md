# Relations — Formulas

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| Total relations | 2^(n²) | n=\|A\| | Finite A | Subset of A×A | Count all relations | Using 2^n |
| Reflexive relations | 2^(n²−n) | n=\|A\| | Must include diagonal | n diagonal fixed | Count with property | Forgetting diagonal |
| Symmetric relations | 2^(n(n+1)/2) | n=\|A\| | Pair (i,j),(j,i) together | Upper triangle + diag | Symmetric count | Double-count pairs |
| Equivalence classes | Partition of A | E.R. R | — | aRb ↔ same class | Classify elements | Overlap classes |
| Transitive closure | Reachability | Digraph | — | Warshall idea | Minimal transitive superset | Confuse with reflexive |
| Composition | (a,c) via ∃b | R,S | Order as stated | Matrix multiply | Compose relations | Reverse order |

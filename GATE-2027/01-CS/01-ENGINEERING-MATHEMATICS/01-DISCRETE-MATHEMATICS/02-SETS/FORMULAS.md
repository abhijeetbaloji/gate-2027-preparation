# Sets — Formulas

| Formula | Meaning | Variables | Conditions | Derivation (see NOTES) | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------------------|------------------|----------------|
| \(\|\mathcal{P}(A)\| = 2^{\|A\|}\) | Number of subsets | \(n=\|A\|\) | A finite | Binary choice per element (NOTES §2) | Subset counting | Using n instead of 2^n |
| \(\|A \cup B\| = \|A\|+\|B\|-\|A \cap B\|\) | Union size (2 sets) | Finite A,B | — | Partition A∪B into disjoint regions (NOTES §5) | Survey / overlap problems | Forgetting subtract overlap |
| 3-set I–E formula | Union of three sets | \|A∩B∩C\| known | Finite | Inclusion–exclusion principle (NOTES §5) | Divisibility 2,3,5 type | Missing triple term or wrong sign |
| \(\|A \times B\| = \|A\|\cdot\|B\|\) | Product size | Finite A,B | — | Multiplication principle (NOTES §6) | Counting pairs, strings | Treating as union size |
| \((A \cup B)^c = A^c \cap B^c\) | De Morgan (union) | A,B ⊆ U | U fixed | Element-wise logic (NOTES §4) | Simplify set expressions | Wrong intersection/union flip |
| \((A \cap B)^c = A^c \cup B^c\) | De Morgan (intersection) | A,B ⊆ U | U fixed | Dual of union law (NOTES §4) | Complement of overlap | Same as above |
| \(\|A \triangle B\| = \|A\|+\|B\|-2\|A \cap B\|\) | Symmetric difference size | Finite A,B | — | Exclude double-counted intersection twice (NOTES §7) | XOR-style counting | Using \|A∪B\| instead |
| Subsets containing fixed \(x\): \(2^{n-1}\) | Constrained subset count | n=\|A\|, x∈A | — | Fix x, free rest (NOTES §8) | "Must include 7" problems | Using 2^n |
| \(\binom{n}{k}\) | k-subsets of n-set | n≥k≥0 | — | Combinatorics (NOTES §8) | Size-k subsets | Confusing with 2^n |


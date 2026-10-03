# Greedy — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Example as proof | One successful run is treated as correctness | Prove an exchange, or give a counterexample to reject | Ask “does this hold for every input?” |
| Wrong interval key | Sort by start or by duration | Unweighted interval scheduling sorts by finish time | The exchange uses `f_g ≤ f_a` |
| Weighted intervals | Earliest finish still used | Weights need DP | Check whether intervals have values |
| 0/1 ratio sort | Fractional rule copied onto indivisible items | Ratio greedy can score 160 where 220 is feasible on the standard triple | Read “fraction” versus “take or leave” |
| Coins always greedy | Largest coin first on every set | `{1,3,4}`, amount 6, is a counterexample; DP is the general algorithm | Test a non-canonical set |
| Huffman direction | Two heaviest merged | Two lightest, parent re-inserted | The rare symbols must sit deep |
| Job sort key | Sorted by deadline for a profit objective | Sort by profit; deadline only limits the slot | EDF is a different problem |
| Earliest slot | High-profit job placed in slot 1 | Place it in the latest slot that meets the deadline | Early slots must stay available |
| Dijkstra and negatives | Greedy shortest paths with a negative edge | Non-negative weights only; otherwise Bellman–Ford | Scan the weight signs |
| “No greedy if negative” | Kruskal rejected because of a negative edge | MST cut property allows negative weights | Separate MST from shortest paths |
| Time bound | Activity selection answered `Θ(n)` from an unordered list | Sorting costs `Θ(n log n)` unless the question says the list is sorted | Include the sort |
| Unique optimum | A different optimal tree marked wrong | Huffman, file merge, and MST need not be unique; the cost is | Compare values, not shapes, unless the question asks for the tree |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

# Dynamic Programming — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Recursion called DP | Fibonacci tree left unmemoised | DP stores each state; otherwise time is `Θ(φ^n)` | Say where the answer is cached |
| 0/1 uses the same row | One item taken many times | Take-branch reads `i−1`, or a 1D array is filled from high capacity downward | Check the item index on the take branch |
| Unbounded uses `i−1` only | Copies are accidentally forbidden | Rods and coins call the same item set at `x − w` | Match the problem’s “at most one” wording |
| LCS mismatch | Diagonal taken when characters differ | Diagonal only on a match; otherwise max of up and left | Write the two cases before filling |
| Substring vs subsequence | LCS rule used for a contiguous segment | Substring length resets to 0 on a mismatch | Read “subsequence” or “substring” |
| Edit match cost | A match adds 1 | A match costs 0; substitute, insert, and delete cost whatever the question states | Underline the cost table in the stem |
| LIS tails printed | Tail array output as the subsequence | It stores minimum tails, not a reconstruction | Keep parent indexes if the sequence is required |
| Strictness | `≤` and `<` mixed | Strict LIS uses `<`; non-decreasing uses `≤` | One word in the question changes the test |
| Matrix index | Cost `p[i]·p[k]·p[j]` | The left piece starts at dimension `p[i−1]` | Label each matrix with its two dimensions before writing the product |
| Chain vs Strassen | Cubic chain DP replaced by `n^{log2 7}` | Strassen is one product of two matrices | Ask whether the input is a sequence of dimensions |
| Polynomial claim | `Θ(nW)` called polynomial with `W` in binary | Pseudo-polynomial unless `W` is bounded by a polynomial in the input length | Count bits of `W` |
| Greedy coins | DP skipped on a non-canonical set | General optimum is the coin DP | If no canonicity is given, do not take the largest coin as optimal |
| Longest path | Bellman recurrence maximised on a graph with cycles | Simple longest paths lack that substructure and are NP-hard | Use the recurrence only for shortest paths, or for DAGs |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

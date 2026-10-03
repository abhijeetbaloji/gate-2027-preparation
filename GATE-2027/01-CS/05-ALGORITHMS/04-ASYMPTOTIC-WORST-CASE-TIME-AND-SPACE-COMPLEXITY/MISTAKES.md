# Asymptotic Complexity — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| `O` read as “equal to” | A loose upper bound is treated as tight | Use `Θ` for a matching upper and lower bound | If the question says “tight”, reject a strictly larger class |
| Master case 2 | `2T(n/2) + n` answered `Θ(n)` | Equal to `n^{log_b a}` adds a log: `Θ(n log n)` | Check whether `f` and the critical term match |
| Exponent `+1` | `2^{n+1}` placed above `2^n` | `2^{n+1} = 2 · 2^n = Θ(2^n)` | A constant factor never changes Theta; a constant *in* the exponent can |
| `4^n` vs `2^n` | Treated as the same class | Ratio `2^n` grows, so not Theta | Compare bases after writing both as powers of 2 |
| `log(n!)` | Simplified to `log n` | Stirling: `Θ(n log n)` | Bound `n!` by `(n/2)^{n/2}` |
| Loop step | `i = i + 2` called `O(log n)` | Adding a constant is linear; multiplying is logarithmic | Ask whether the counter doubles |
| Amortised vs worst | Doubling insert called worst-case `O(1)` | Amortised `O(1)`, worst-case `O(n)` | One resize copies the whole array |
| Best case as “the” complexity | Insertion sort quoted as `Θ(n)` in a worst-case question | Worst case is `Θ(n²)` | Read best, average, or worst |
| Uneven split | Master applied to `T(n/3)+T(2n/3)+n` | Master needs one `a` and one `b`; use a tree | Depth is the long branch; levels still sum to `Θ(n log n)` |
| Numeric `n` vs bits | `O(√N)` called polynomial in the input length | Input length is `Θ(log N)` bits; `√N = 2^{(1/2) log N}` is exponential in the length | State what `n` counts |
| Stack space | Recursive `Θ(1)` extra memory | Depth `d` uses `Θ(d)` stack | Include frames |
| `(log n)²` | Rewritten as `2 log n` | That identity is for `log(n²)`, not `(log n)²` | Keep the exponent outside the log |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

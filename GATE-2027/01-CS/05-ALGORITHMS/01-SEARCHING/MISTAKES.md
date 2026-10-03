# Searching — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Unsorted binary search | A larger middle is treated as “go left” | Discard a side only when the array is sorted, or the predicate is monotone | State the invariant before choosing a side |
| Duplicate index | Any match is returned | First, last, and count need bound searches | Read “first”, “last”, or “how many” |
| Absent-key average | `(n + 1) / 2` is used for a miss | That expectation needs the key present and uniform; a miss costs `n` | Check the probability model in the stem |
| Interpolation bound | `O(log log n)` quoted as worst case | That is an average for uniform keys; worst case is `Θ(n)` | Attach the word “expected” or “uniform” |
| Interval shrink | `lo` and `hi` stay put | Every iteration must drop at least one index | Prefer `lo = mid + 1` / `hi = mid - 1` on a closed interval |
| Rotated duplicates | `O(log n)` claimed with repeated keys | Identical neighbours can block the sorted-half test | Use the distinct-key version unless duplicates are handled |
| One-query sort | Sorting before a single lookup | Sort is `Ω(n log n)`; one scan is `O(n)` | Count preprocessing only if it is reused |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

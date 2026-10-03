# Searching — Formulas

Learn the reasoning in `NOTES.md`. This page is the compact reference.

| Result | When it applies |
|--------|-----------------|
| Comparison lower bound `ceil(log2(n + 1))` | Worst-case comparisons to identify one of `n` positions or “absent”, two-way tests |
| Linear search, key present and uniform: `(n + 1) / 2` comparisons expected | Scan from the start; key is equally likely in any index; key is present |
| Linear search worst case: `n` comparisons | Key last or absent |
| `T(n) = T(floor(n/2)) + Θ(1) = Θ(log n)` | Binary search, exponential search’s second phase, first/last occurrence |
| Worst-case probes, binary search: `floor(log2 n) + 1` | Standard closed interval that halves each step |
| Occurrence count = upper bound − lower bound | Sorted array, after two bound searches |
| Jump cost `n/m + m`, minimised at `m = √n`, cost `Θ(√n)` | Fixed jump on a sorted array, then a linear scan of one block |
| Interpolation average `O(log log n)`, worst `Θ(n)` | Uniform numeric keys for the average; skewed keys for the worst case |
| `T(n) = T(2n/3) + Θ(1) = Θ(log n)` | Ternary search on a unimodal function |
| Answer-space search: `O(C log R)` | Monotone predicate costing `C`, range size `R` |
| Sort once, then search: `Θ(n log n + q log n)` | `q` binary searches on a static array you may sort |

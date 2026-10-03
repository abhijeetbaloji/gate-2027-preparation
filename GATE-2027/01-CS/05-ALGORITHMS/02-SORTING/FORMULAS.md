# Sorting — Formulas

Learn the arguments in `NOTES.md`.

| Result | When it applies |
|--------|-----------------|
| `log2(n!) = n log2 n − n log2 e + O(log n)` | Height of a comparison-sort decision tree; Stirling |
| Worst-case comparison sort `Ω(n log n)` | Any algorithm that orders by pairwise key comparisons; at least `n!` leaves |
| Inversions `I ≤ n(n − 1)/2` | Maximum when the array is reversed |
| Insertion shifts = `I` | Shift test is strict `>`; each shift removes one inversion |
| Adjacent-swap sorts (bubble) also perform `I` swaps | Each swap removes exactly one inversion |
| Insertion best `n − 1` comparisons | Already sorted; inner loop never shifts |
| Selection comparisons `n(n − 1)/2` always | Every suffix is scanned fully |
| Selection swaps `≤ n − 1` | One placement per prefix index |
| `T(n) = 2T(n/2) + Θ(n) = Θ(n log n)` | Merge sort; Master case 2, `a = b = 2` |
| `T(n) = T(n − 1) + Θ(n) = Θ(n²)` | Quicksort when the pivot rank is always 1 or `n` |
| Average quicksort `Θ(n log n)` | Pivot rank uniform in the subarray |
| `Σ_h h / 2^h = 2` | Used to show bottom-up build-heap is `Θ(n)` |
| Heap height `floor(log2 n)` | Complete binary tree |
| Counting sort `Θ(n + k)` | Integer keys in `0..k` |
| LSD radix `Θ(d(n + b))` | `d` digits, alphabet size `b`, stable digit sort |
| Bucket worst `Θ(n²)`, expected `Θ(n)` if uniform | Inner sort quadratic; uniformity for the expectation |
| Median-of-medians `T(n) ≤ T(n/5) + T(7n/10) + O(n) = Θ(n)` | Groups of 5; worst-case selection |
| External passes `ceil(log_k (N/M))` | `N` records, memory `M`, `k`-way merge |
| Parent / children, 0-based | Parent `(i−1)/2`; children `2i+1`, `2i+2` |
| Parent / children, 1-based | Parent `i/2`; children `2i`, `2i+1` |

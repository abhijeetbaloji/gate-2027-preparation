# Sorting — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Quicksort always `n log n` | Worst case ignored | Worst case is `Θ(n²)` when every pivot is extreme | Name best, average, and worst separately |
| Sorted input helps quicksort | Endpoint pivot on sorted data | That pivot is the minimum or maximum; one side is empty | Check which element is the pivot |
| Merge sort best case `O(n)` | Standard top-down merge still splits | Best = worst = `Θ(n log n)` | Only natural merge sort stops early on runs |
| Merge sort in-place | Buffer forgotten | Auxiliary buffer is `Θ(n)` | Count the merge array |
| Build-heap `O(n log n)` | One-by-one insert mixed with bottom-up | Bottom-up build is `Θ(n)`; `n` later extracts are `Θ(n log n)` | Ask which build the question means |
| Selection sort `O(n)` | Swap count used as time | Comparisons are always `n(n−1)/2` | Time follows comparisons, not swaps |
| Bubble best case `O(n)` with no flag | Code always runs `n−1` passes | Linear best case needs the “no swap” stop | Read the loop |
| Lower bound vs counting sort | `Ω(n log n)` applied to all sorts | The bound is for comparison sorts only | Check the key domain |
| Unstable radix digit pass | LSD proof uses stability | Each digit sort must be stable | Counting sort right-to-left is the usual pass |
| Insertion stability | Shift on `≥` swaps equal keys | Shift only while `A[j] > key` | Test the equal-key case |
| Heap indexes | 0-based and 1-based formulas mixed | 0-based children `2i+1`, `2i+2`; 1-based `2i`, `2i+1` | Fix the base before computing a parent |
| Quicksort stack | Extra space called `O(1)` | Recursion depth is `Θ(log n)` average and `Θ(n)` worst | Space includes the call stack |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

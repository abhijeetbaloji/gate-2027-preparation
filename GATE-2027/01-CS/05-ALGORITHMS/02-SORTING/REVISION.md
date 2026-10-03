# Sorting — Revision

## Complexity

| Algorithm | Best | Average | Worst | Extra space | Stable |
|-----------|------|---------|-------|-------------|--------|
| Insertion | Θ(n) | Θ(n²) | Θ(n²) | Θ(1) | Yes (`>` shift) |
| Selection | Θ(n²) | Θ(n²) | Θ(n²) | Θ(1) | No |
| Bubble + flag | Θ(n) | Θ(n²) | Θ(n²) | Θ(1) | Yes (`>` swap) |
| Merge | Θ(n log n) | Θ(n log n) | Θ(n log n) | Θ(n) | Yes (tie → left) |
| Quick | Θ(n log n) | Θ(n log n) | Θ(n²) | Θ(log n) avg stack | No |
| Heap | Θ(n log n) | Θ(n log n) | Θ(n log n) | Θ(1) | No |
| Counting | Θ(n+k) | Θ(n+k) | Θ(n+k) | Θ(n+k) | Yes (right to left) |
| Radix LSD | Θ(d(n+b)) | Θ(d(n+b)) | Θ(d(n+b)) | Θ(n+b) | Yes if digits are |
| Bucket | Θ(n) | Θ(n) uniform | Θ(n²) | Θ(n) | Can be |

## Why

- Comparison lower bound: `log2(n!)` = Θ(n log n).
- Merge: `log n` levels × Θ(n) work. `T(n) = 2T(n/2) + Θ(n)`.
- Quick worst: `T(n) = T(n−1) + Θ(n)` when the pivot is always extreme.
- Quick average: uniform pivot rank → Θ(n log n).
- Build-heap: Σ h/2^h converges → Θ(n). Then n extracts → Θ(n log n).
- Insertion / bubble swaps = inversion count. Max inversions `n(n−1)/2`.
- Selection comparisons always `n(n−1)/2`.

## Conditions

- Counting: keys in `0..k`.
- Radix LSD: stable digit sort, fixed digit count.
- Bucket average: uniform keys.
- Quick `n²`: only if pivots can be forced to the end. Random pivot → expected n log n.

## Choose

- Stable + worst-case n log n: merge.
- In-place + worst-case n log n: heap.
- Fast average: quick.
- Nearly sorted: insertion.
- Small integers: counting. Fixed digits: radix.

## Traps

- Sorted input is quicksort’s *worst* case for an endpoint pivot.
- Merge sort is not in-place and not linear on sorted input (standard version).
- Build-heap is not Θ(n log n) bottom-up.
- Selection’s swaps are O(n); its time is not.
- Beating n log n requires leaving the comparison model.

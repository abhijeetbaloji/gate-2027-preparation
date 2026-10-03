# Searching — Revision

Use after `NOTES.md`.

## Which algorithm

| Situation | Use | Worst time | Extra space |
|-----------|-----|------------|-------------|
| Unsorted | Linear | Θ(n) | Θ(1) |
| Sorted array | Binary search | Θ(log n) | Θ(1) iterative |
| First / last / count | Lower and upper bound | Θ(log n) | Θ(1) |
| Rotated, distinct | Modified binary search | Θ(log n) | Θ(1) |
| Monotone feasibility | Binary search on the answer | Θ(C log R) | Θ(1) plus the test |
| Unimodal optimum | Ternary search | Θ(log n) | Θ(1) |
| Uniform keys, expected | Interpolation | average O(log log n), worst Θ(n) | Θ(1) |
| Block jumps | Jump search, block √n | Θ(√n) | Θ(1) |

## Why the bounds hold

- Linear: every cell is a candidate.
- Binary: `T(n) = T(n/2) + Θ(1)`.
- Comparison lower bound: `ceil(log2(n + 1))`.
- Jump: `n/m + m` is smallest at `m = √n`.

## Properties

- Binary search needs sorted order and random access.
- Plain binary search may return any duplicate.
- Iterative binary search is `Θ(1)` extra memory; recursion uses `Θ(log n)` stack.
- Sentinel linear search changes constants only.

## Conditions

- Discard half only when the predicate is monotone.
- Rotated search as taught here assumes distinct keys.
- Interpolation’s `log log n` needs a uniform model.

## Traps

- Binary search on unsorted data.
- `hi = mid` with floor division that never moves.
- `(n + 1) / 2` when the key might be absent.
- Calling interpolation worst-case `O(log log n)`.

## Comparisons

- One unsorted query: linear beats sort-then-search.
- Many queries: sort + binary search, or hashing (see Hashing).
- Ternary search is for one turning point, not for a sorted array.

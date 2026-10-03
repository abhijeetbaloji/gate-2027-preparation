# Asymptotic Complexity — Revision

## Definitions

- `O`: eventual upper bound, some `c`.
- `Ω`: eventual lower bound, some `c`.
- `Θ`: both.
- `o`: ratio → 0. `ω`: ratio → ∞.
- Theta is symmetric. Big-O is not. `n = O(n²)` is true; `n² = O(n)` is false.

## Growth

`1 < log n < n^ε < n log n < n² < … < c^n < n! < n^n` for `ε > 0`, `c > 1`.

- `log_b n = Θ(log n)`.
- `2^{n+1} = Θ(2^n)`. `4^n` is not `Θ(2^n)`.
- `log(n!) = Θ(n log n)`.
- `(log n)²` is not `log(n²)`.

## Loops and recurrences

| Shape | Bound |
|-------|-------|
| Nested `i, j` to `n` | `Θ(n²)` |
| `j` from 1 to `i` | `Θ(n²)` |
| Counter doubles or halves | `Θ(log n)` per loop |
| `T(n) = T(n−1) + n` | `Θ(n²)` |
| `T(n) = T(n/2) + 1` | `Θ(log n)` |
| `T(n) = 2T(n/2) + n` | `Θ(n log n)` |
| `T(n) = 2T(n/2) + n²` | `Θ(n²)` |
| `T(n) = 2T(n/2) + 1` | `Θ(n)` |

Master: compare `f` with `n^{log_b a}`. Case 2 (equal) adds one log. Needs a polynomial gap for cases 1 and 3, plus regularity for case 3.

## Cases of an algorithm

- Worst / best / average are different functions.
- Quicksort: best and average `Θ(n log n)`, worst `Θ(n²)`.
- Insertion: best `Θ(n)`, worst `Θ(n²)`.
- Merge and heap: `Θ(n log n)` all three.

## Space and amortised

- Auxiliary space excludes the input.
- Recursion stack = `Θ(depth)`.
- Doubling inserts: amortised `Θ(1)`, worst-case one insert `Θ(n)`.
- Amortised ≠ average-case. No probability is required.

## Traps

- Master case 2 written without `log n`.
- Loose `O(n²)` when the tight answer is `Θ(n log n)`.
- Bit length versus the numeric value.
- `i = i + 2` called logarithmic.

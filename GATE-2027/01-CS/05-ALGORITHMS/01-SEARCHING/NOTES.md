# Searching — Learning Notes

These notes are for learning the topic. After that, use `REVISION.md` for a short pass. Searching here means finding an element, or a boundary, in a collection. Binary search trees as a data structure sit under Programming and Data Structures; the search *idea* used on a sorted array is here.

---

## 1. What a search problem is

**What it is.** Given a collection and a target, report whether the target occurs and, if so, where. Variants ask for the first occurrence, the last occurrence, the insertion point, or any index that satisfies a yes/no condition.

**Intuition.** The cost depends on how much order the data already has. With no order, every element is a possible answer, so you may have to look at all of them. With sorted order, a comparison throws away a whole region.

**Formal definition.** A search algorithm returns an index `i` with `A[i] = key`, or a failure value if no such index exists. A *decision* version returns only yes or no.

**Why the lower bound exists.** In the comparison model, each comparison has two outcomes (three, if you count equal). To distinguish `n + 1` possibilities — the key equals one of `n` positions, or it is absent — you need a binary tree of height at least `ceil(log2(n + 1))` in the worst case. That is why comparison search cannot beat logarithmic time on sorted data, and why unsorted data needs linear time in the worst case.

**GATE observation.** “Minimum comparisons in the worst case” is this information bound, not the running time of one favourite implementation. State the model: comparisons of keys, or probes into a hash table, are different models.

---

## 2. Linear search

**What it is.** Scan from one end until the key is found or the collection ends.

**Intuition.** Nothing is known about order, so the next element is as likely as any other.

**How it works.**

```
for i from 0 to n - 1:
    if A[i] == key: return i
return NOT_FOUND
```

**Example.** `A = [4, 9, 1, 7]`, key `1`. Compare 4 (no), 9 (no), 1 (yes). Index 2. Three comparisons.

**Complexity.** One comparison per element examined. No extra array.

| Case | Time | Why |
|------|------|-----|
| Best | Θ(1) | Key is at the first position checked |
| Average | Θ(n) | If the key is equally likely in any position, or absent, about `n/2` or `n` comparisons |
| Worst | Θ(n) | Key is last, or absent |
| Auxiliary space | Θ(1) | Only the index |

If the key is present and equally likely in any slot, the expected number of comparisons is `(n + 1) / 2`. If it may be absent, say so before using that formula.

**Properties.** Works on unsorted data, linked lists, and streams. Stable in the weak sense that it returns the first match if you scan left to right. Online: you can stop early.

**Edge cases.** Empty collection. All elements equal. Key absent. Duplicates: the scan returns the first match only if you stop at the first hit.

**When to use.** Unsorted data, tiny `n`, one query, or a structure with no random access (a linked list).

**When not to use.** Many queries on a static array that you are allowed to sort or hash first. Sorting once then binary-searching is cheaper when the number of queries is large.

**Comparison.** Slower than binary search on sorted arrays. Faster to start than building a hash table for a single lookup. Hashing gives expected constant time after preprocessing; linear search needs none.

**GATE traps.**

- Average `(n + 1) / 2` assumes the key is present and uniform. Absent keys cost `n`.
- A sentinel (copy the key into `A[n]`) removes the bound check inside the loop. It changes constant factors, not the Θ(n) bound, and it needs a spare slot.

---

## 3. Binary search

**What it is.** On a sorted array, compare the key with the middle element and discard half of the remaining range.

**Intuition.** Sorted order means everything left of a larger middle is too small, and everything right of a smaller middle is too large. One comparison deletes half the candidates.

**Formal definition.** Array `A[0..n-1]` is non-decreasing. The invariant: if the key is present, it lies in the closed interval `[lo, hi]`.

**Why it works.** The invariant holds at the start (`lo = 0`, `hi = n - 1`). If `A[mid] < key`, no index `≤ mid` can hold the key, so `lo = mid + 1` preserves the invariant. If `A[mid] > key`, set `hi = mid - 1`. If equal, you may return `mid`. When `lo > hi` the interval is empty, so the key is absent. Each step strictly shrinks the integer interval, so the loop ends.

**How it works.**

```
lo = 0, hi = n - 1
while lo <= hi:
    mid = lo + (hi - lo) // 2
    if A[mid] == key: return mid
    if A[mid] < key: lo = mid + 1
    else: hi = mid - 1
return NOT_FOUND
```

`mid = lo + (hi - lo) // 2` avoids overflow of `lo + hi` in fixed-width integers. In mathematics the two forms match when there is no overflow.

**Example.** `A = [2, 5, 8, 12, 16, 23, 38]`, key `23`.

| lo | hi | mid | A[mid] | action |
|----|----|-----|--------|--------|
| 0 | 6 | 3 | 12 | 12 < 23, lo = 4 |
| 4 | 6 | 5 | 23 | found |

**Complexity.**

The range length roughly halves. The number of times you can halve `n` until one element remains is `floor(log2 n) + 1` probes in the worst case for this loop.

Recurrence for the time: `T(n) = T(n/2) + Θ(1)`, `T(1) = Θ(1)`. Unrolling: `T(n) = Θ(1) + Θ(1) + …` with `Θ(log n)` terms, so `T(n) = Θ(log n)`.

| Case | Time | Why |
|------|------|-----|
| Best | Θ(1) | Middle element is the key on the first probe |
| Average | Θ(log n) | A constant fraction of the tree is still logarithmic |
| Worst | Θ(log n) | Key absent, or at a deepest leaf of the decision tree |
| Auxiliary space | Θ(1) iterative; Θ(log n) if recursive (call stack) | The recursion depth is the number of halvings |

**Properties.** Requires random access and sorted order. Returns *some* matching index if duplicates exist, not necessarily the first. The algorithm is comparison-based and matches the logarithmic lower bound up to constants.

**Edge cases.**

- Empty array: `lo > hi` immediately.
- One element: one comparison.
- Duplicates: any match may be returned.
- Not sorted: the discard step is false, so the answer can be wrong. Binary search does not detect unsorted input.

**When to use.** Many lookups on a static sorted array. Also when you can sort once in `O(n log n)` and then answer `q` queries in `O(q log n)`.

**When not to use.** Unsorted data and only one query (linear search is simpler and the same worst-case order as sorting). Linked lists (no `O(1)` midpoint). Data that changes often in the middle (maintaining sorted order costs more; a balanced tree or hash table may fit better).

**Comparison with linear search.** Binary search needs sorted order and random access. It does fewer comparisons for large `n`. Linear search is the right tool when those assumptions fail.

**GATE traps.**

- Off-by-one: `lo < hi` versus `lo <= hi` changes whether the last element is checked. Pick one convention and keep the invariant.
- Infinite loop if `hi = mid` while `lo < hi` and `mid` is computed by floor toward `lo`. The update must move at least one endpoint.
- Counting comparisons: worst-case successful search is about `floor(log2 n) + 1`, not `n/2`.
- Applying binary search to a nearly sorted or rotated array without adjusting the predicate.

**GATE-style observation.** Write the predicate in words before the code: “the key, if present, is inside `[lo, hi]`.” Most wrong programs break that sentence.

---

## 4. First and last occurrence

**What it is.** Among duplicates, the leftmost or rightmost index equal to the key.

**Why the plain algorithm is not enough.** Equality returns immediately, so the index depends on where the middle falls.

**How it works (first occurrence).** Keep the same halving, but on equality search left and remember the index:

```
answer = NOT_FOUND
while lo <= hi:
    mid = lo + (hi - lo) // 2
    if A[mid] >= key:          # key is at mid or further left
        if A[mid] == key: answer = mid
        hi = mid - 1
    else:
        lo = mid + 1
```

Last occurrence flips the test: on `A[mid] <= key`, record a match and set `lo = mid + 1`.

**Example.** `A = [1, 2, 2, 2, 3]`, key `2`. First occurrence is index 1. Last is index 3.

**Complexity.** Still `Θ(log n)` worst case. Extra space `Θ(1)`. You do not stop at the first hit, so the best case is also `Θ(log n)` if you always run to an empty interval.

**Edge cases.** Key absent: `answer` stays `NOT_FOUND`. Key fills the whole array: first is 0, last is `n - 1`.

**Lower and upper bound.** The insertion point of `key` (first index with `A[i] >= key`) is the same loop without storing equality. The count of `key` is `upper_bound - lower_bound`.

**GATE trap.** “Number of occurrences” is not found by one equality test. It is the gap between the two bounds, still `O(log n)`, not `O(n)`.

---

## 5. Search on a rotated sorted array

**What it is.** A sorted array was cut and the two pieces swapped, for example `[4, 5, 6, 7, 0, 1, 2]`. Distinct elements are the usual GATE setting.

**Intuition.** One of the two halves is still fully sorted. The key lies in a sorted half exactly when it sits between that half’s endpoints.

**Why it works.** With distinct elements, `A[lo] <= A[mid]` means the left half has not crossed the rotation (it is sorted). Otherwise the right half is sorted. Restrict the range to the half that can contain the key. The interval shrinks, and the “which half is sorted” test stays valid.

**Example.** Key `0` in `[4, 5, 6, 7, 0, 1, 2]`.

- `lo = 0`, `hi = 6`, `mid = 3`, `A[mid] = 7`. Left `[4, 5, 6, 7]` is sorted and `0` is not in `[4, 7]`, so `lo = 4`.
- `mid = 5`, `A[5] = 1`. Right side from mid is sorted and `0 < 1`, so `hi = 4`.
- `A[4] = 0`. Found.

**Complexity.** `Θ(log n)` time, `Θ(1)` extra space, same recurrence as binary search. Worst, average, and best (if you count a full run) stay logarithmic; a lucky middle hit is `Θ(1)`.

**When not to use.** Duplicates such as `[1, 1, 1, 0, 1]` make both halves look unsorted or identical, and a single comparison may not discard half. Worst case falls back toward linear unless you add extra skips. Prefer the distinct-element statement unless the question allows duplicates.

**GATE trap.** Treating the array as fully sorted. The minimum element is the only place where `A[i] < A[i - 1]` (circularly); finding that pivot is itself a binary search.

---

## 6. Binary search on a monotonic predicate

**What it is.** The array is not a list of keys. You binary-search the *answer space*. A predicate `P(x)` is false up to some point and true after (or the reverse).

**Intuition.** “Smallest capacity that ships all packages in `D` days”, “largest minimum gap”, and similar problems have the shape: if `x` works, every larger `x` works. The transition point is unique.

**Why it works.** Monotonicity is the sorted order. Discard the half that cannot contain the transition, exactly as in section 3.

**Example.** Smallest integer `x` in `[1, 10]` with `x * x >= 30`.

- Mid 5: 25 < 30, too small, `lo = 6`.
- Mid 8: 64 ≥ 30, feasible, `hi = 8` and remember 8.
- Continue until the boundary is 6, because `5² = 25 < 30` and `6² = 36 ≥ 30`.

**Complexity.** `O(log R · C)` where `R` is the size of the numeric range and `C` is the cost of testing `P`. If the test scans an array of length `n`, time is `O(n log R)`.

**When to use.** The feasibility test is easier than constructing the optimum directly, and feasibility is monotonic.

**When not to use.** Two feasible answers do not imply that everything between them is feasible. Then halving can jump over the optimum.

**GATE trap.** Searching the array indexes when the unknown is a numeric parameter (a distance, a time, a capacity). Also forgetting to prove monotonicity before coding the discard rule.

---

## 7. Exponential search and unbounded arrays

**What it is.** If the sorted array is unbounded or the key is expected near the front, grow a window `1, 2, 4, …` until `A[bound] >= key`, then binary-search inside `(bound/2, bound]`.

**Why it works.** The window that first passes the key has size proportional to the true index `i`. Finding it takes `O(log i)` probes. Binary search inside a window of length `O(i)` takes another `O(log i)`.

**Complexity.** `O(log i)` where `i` is the index of the key, which is `O(log n)` if `i < n`. Worst case over all positions is still `O(log n)`. Auxiliary space `Θ(1)`.

**When to use.** Unknown or huge length, or keys biased toward the start.

**GATE observation.** This is binary search plus a range-finding phase, not a new comparison bound.

---

## 8. Jump search

**What it is.** On a sorted array, jump by fixed blocks of length `m`, then linear-scan one block.

**Why `m = √n`.** Jumps cost about `n/m`. The final block costs at most `m`. Total `n/m + m`. By AM–GM, or by setting the derivative to zero, the minimum is at `m = √n`, and the cost is `Θ(√n)`.

| Case | Time | Why |
|------|------|-----|
| Best | Θ(1) | Key in the first block, found immediately |
| Average / worst | Θ(√n) | With block `√n` |
| Space | Θ(1) | Index arithmetic only |

**Comparison.** Worse than binary search’s `Θ(log n)`, better than linear’s `Θ(n)`. Useful only if jumping is much cheaper than random access (rare in RAM; sometimes used as a teaching comparison). Binary search dominates jump search for arrays in memory.

**GATE trap.** Leaving the block size as `n/2` and still claiming `√n`. The bound holds for the optimal block size.

---

## 9. Interpolation search

**What it is.** Instead of the middle index, probe where the key would sit if values were linear between `A[lo]` and `A[hi]`:

```
mid = lo + (key - A[lo]) * (hi - lo) / (A[hi] - A[lo])
```

**Why it can be faster.** On data drawn uniformly, the probe lands near the key, and the expected number of probes is `O(log log n)`.

**Why the worst case is linear.** On highly skewed data the probe can advance by only one index each time, giving `Θ(n)`.

| Case | Time | Why |
|------|------|-----|
| Average (uniform) | `O(log log n)` | Expected probes under a uniform model |
| Worst | `Θ(n)` | Probe shrinks the interval by one |
| Space | Θ(1) | Iterative |

**When not to use.** Unless the question states uniformity, do not replace binary search. Division by `A[hi] - A[lo]` fails when the range is flat.

**GATE trap.** Quoting `O(log log n)` as a worst-case bound. It is an average-case bound under an assumption.

---

## 10. Ternary search on a unimodal function

**What it is.** The domain is numeric, and the function decreases then increases (a single valley), or increases then decreases. Split into thirds. Compare the two interior points and discard the third that cannot hold the optimum.

**Why one third dies.** Suppose you are minimising and `f(m1) < f(m2)`. The valley cannot lie to the right of `m2`: moving right of `m2` only climbs further if the function is unimodal and `m1` is already lower. So set `hi = m2`. The symmetric case sets `lo = m1`.

**Complexity.** `T(n) = T(2n/3) + Θ(1) = Θ(log n)`. The base is `3/2`, which changes the constant, not the class: `log_{3/2} n = Θ(log n)`.

**When not to use.** More than one turning point. Binary search on the derivative (or on the slope sign) is the discrete analogue: if the slope goes from negative to positive, the minimum is where the slope crosses.

**Comparison with binary search.** Binary search needs a monotone predicate. Ternary search needs a unimodal function and two evaluations per step. On a monotone array, ternary search is an unnecessary slowdown.

---

## 11. Selecting which search to run

| Situation | Algorithm | Worst time |
|-----------|-----------|------------|
| Unsorted, one query | Linear | Θ(n) |
| Sorted array, random access | Binary, or bounds | Θ(log n) |
| Sorted, key likely near the front, or unbounded | Exponential, then binary | Θ(log i) |
| Monotone feasibility on a numeric range | Binary search on the answer | Θ(C log R) |
| Unimodal real or integer function | Ternary, or binary on slope | Θ(log n) |
| Many queries, unsorted static data, equality only | Sort once, or hash (see Hashing) | preprocessing + fast query |
| Expected near-constant equality tests | Hashing | expected Θ(1), worst Θ(n) |

**Preprocessing tradeoff.** Sort in `Θ(n log n)`, then each binary search is `Θ(log n)`. Hash build is expected `Θ(n)`, then expected `Θ(1)` per query, with a worst-case linear chain or probe sequence. If the question demands a worst-case guarantee, binary search on a sorted array is the safe equality structure.

---

## 12. Common GATE traps (collected)

1. Binary search on unsorted data.
2. Using `(lo + hi) / 2` and ignoring overflow, or using a `mid` update that does not shrink the range.
3. Returning any duplicate index when the question asks for the first or the count.
4. Treating `O(log log n)` interpolation as worst-case.
5. Forgetting that the comparison lower bound is `ceil(log2(n + 1))` only in the comparison model.
6. Rotated-array search with duplicates, still claimed as `O(log n)` worst case.
7. Predicate search without a monotonicity argument.

---

## 13. Worked complexity comparisons

**One search, unsorted.** Linear search is `Θ(n)` worst case. Sorting first is `Θ(n log n)`, which is worse for a single query.

**`q` searches, static unsorted keys.** Sort then binary search: `Θ(n log n + q log n)`. Build a hash table: expected `Θ(n + q)`, worst case `Θ(n q)` if every query hits one long chain. The question’s wording (expected, worst, comparisons only) picks the answer.

**Successful binary search, `n = 1,000,000`.** `floor(log2 n) + 1 = 20` probes in the worst case for the standard halving argument. Linear search may look at all one million cells.

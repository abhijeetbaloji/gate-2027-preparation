# Searching — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Why can linear search run on an unsorted array while binary search cannot?

**2.** Write the recurrence for binary search and its solution.

**3.** What does the comparison lower bound `ceil(log2(n + 1))` count?

**4.** A sorted array has duplicate keys. What does ordinary binary search return?

**5.** When is jump search’s block size `√n`?

### Level 2 — Standard

**6.** Binary-search key `12` in `[1, 4, 7, 12, 18, 21]`. List the mid values until it is found. Take `mid = lo + (hi - lo) // 2` and indexes from 0.

**7.** How many comparisons does linear search use to find a key in position `k` (1-based), and what is the average if the key is present and uniform over `n` positions?

**8.** Array `[2, 2, 2, 3, 3]`. First and last index of `2`?

**9.** You will answer one membership question on an unsorted array of `n` keys, then discard the array. Is sorting first an improvement in the worst case?

**10.** Give best, average, and worst time of interpolation search, and the assumption on the average.

### Level 3 — Multi-step

**11.** Search key `1` in the rotated array `[6, 7, 1, 2, 3, 4, 5]`. Show which half you keep at the first mid.

**12.** Smallest integer `x ≥ 1` such that `x(x + 1)/2 ≥ 20`. Find it by binary search on the answer and show the final boundary test.

**13.** `n = 1024`. Upper-bound the worst-case probes of binary search. Compare with linear search’s worst case.

**14.** A predicate `P(x)` is false for all `x < 50` and true for all `x ≥ 50`, with `x` in `0..1000`. Each test scans an array of length `n`. Time to find the smallest true `x`?

**15.** Exponential search finds a key at index `i = 20` in a sorted array. Why is the cost `O(log i)` rather than `O(log n)` in the argument that uses the window size?

### Level 4 — Trap-based

**16.** A student claims interpolation search is `O(log log n)` in the worst case. What is wrong?

**17.** Binary search is run on `[1, 3, 2, 4]` for key `2`, mids chosen by halving. Show one execution that misses `2`.

**18.** Someone uses average linear-search cost `(n + 1)/2` for a key that is absent. What is the actual number of comparisons?

**19.** Rotated array `[1, 1, 1, 1, 0, 1]` and key `0`. Why can “the sorted half” fail to discard half the array?

**20.** Recursive binary search is described as `O(1)` extra memory. What is missing?

### Level 5 — Challenge

**21.** Prove that if `P` is monotone (false, then true), discarding the left half when `P(mid)` is true does not hide the first true index.

**22.** Show `n/m + m` is minimised at `m = √n` for positive real `m`, and state the minimum value.

**23.** You may preprocess a static sorted array. Give an `O(log n)` way to count occurrences of a key. Argue correctness from bounds.

**24.** Distinct rotated sorted array. Argue that at least one side of `mid` is sorted.

**25.** `q` queries on a static unsorted set of `n` integers, worst-case time, comparison model. Why is “hash every query in `O(1)`” not a worst-case answer? Give a correct worst-case bound that uses sorting.

---

## Answers and explanations

**1.** Linear search never discards an element without looking at it. Binary search discards a side only because sorted order makes every element on that side a non-match.

**2.** `T(n) = T(n/2) + Θ(1)`, `T(1) = Θ(1)`. There are `Θ(log n)` halvings, so `T(n) = Θ(log n)`.

**3.** The minimum number of two-outcome comparisons in the worst case needed to distinguish `n + 1` possibilities (hit one of `n` cells, or miss).

**4.** Some index whose value equals the key, not necessarily the first or the last.

**5.** When jumps of length `m` are followed by a linear scan of one block. The sum `n/m + m` is minimised at `m = √n`.

**6.** `lo = 0`, `hi = 5`. Mid index 2, value 7, too small, `lo = 3`. Mid index 4, value 18, too big, `hi = 3`. Mid index 3, value 12. Found. Mids: 2, 4, 3 (indexes).

**7.** `k` comparisons. Average `(n + 1) / 2`.

**8.** First index 0, last index 2.

**9.** No. Sorting is `Ω(n log n)` in the comparison model; one scan is `O(n)`.

**10.** Best `Θ(1)` if the first probe hits. Average `O(log log n)` for uniform independent keys. Worst `Θ(n)`.

**11.** Indexes 0..6, mid 3, value 2. Left side `[6, 7, 1, 2]` is not fully sorted; right side `[2, 3, 4, 5]` is sorted. Key `1` is not in `[2, 5]`, so keep the left (`hi = mid - 1` after the usual rotated test: key is not in the sorted right half). Next range contains index 2.

**12.** Search `1..20`. The transition is 6, because `6·7/2 = 21 ≥ 20` and `5·6/2 = 15 < 20`. A halving search that keeps the smallest feasible value ends at 6.

**13.** `floor(log2 1024) + 1 = 11` probes. Linear worst case is 1024 comparisons.

**14.** `Θ(n log 1001) = Θ(n)` times a constant about 10, more precisely `O(n log R)` with `R = 1001`.

**15.** The doubling phase stops at a window of length `O(i)`, after `O(log i)` steps. Binary search on that window is `O(log i)`. If `i` is much smaller than `n`, you never look at the far end.

**16.** `O(log log n)` is an average-case bound under a uniform model. Skewed keys can force a linear number of probes.

**17.** `lo = 0`, `hi = 3`, mid 1, value 3. Because the algorithm assumes sorted order, `3 > 2` sets `hi = 0`. Mid 0, value 1, `1 < 2` sets `lo = 1`. `lo > hi`, miss. The key was at index 2, which was discarded.

**18.** `n` comparisons. The average `(n + 1)/2` needs the key to be present.

**19.** Many equal values make `A[lo]`, `A[mid]`, and `A[hi]` identical, so neither half is certified as a clean sorted range that excludes the key. You may be unable to drop half the cells.

**20.** The call stack stores `Θ(log n)` frames. The iterative version is `Θ(1)` extra memory.

**21.** Let `t` be the first index with `P` true. If `P(mid)` is true, then `t ≤ mid`, because everything before `t` is false. Discarding indexes `> mid` keeps `t`. If `P(mid)` is false, then `t > mid`, so discarding indexes `≤ mid` keeps `t`.

**22.** For `m > 0`, `(√n − something)`: by AM–GM, `n/m + m ≥ 2√(n/m · m) = 2√n`, equality at `n/m = m`, so `m = √n`. Derivative: `−n/m² + 1 = 0` gives the same point. Minimum value `2√n`.

**23.** Lower bound = first index with `A[i] ≥ key`. Upper bound = first index with `A[i] > key`. Both are binary searches on monotone predicates. Every occurrence lies in `[lower, upper)` and nothing else does, so the count is `upper − lower`. Each bound is `O(log n)`.

**24.** Let the unknown rotation put the minimum at index `r`. For a mid, the segment that does not contain `r` in its interior is still in sorted order, because rotation only breaks order at the wrap. If `r` is strictly to the right of `mid`, the left side from `lo` through `mid` is sorted. If `r` is at most `mid`, the right side from `mid` through `hi` is sorted. So at least one of the two sides is sorted. (If `r` is exactly an endpoint the same conclusion holds.)

**25.** A hash table’s worst-case chain is `Θ(n)` per query, so `Θ(nq)` is possible. Sorting once (`O(n log n)` comparisons) and binary-searching each query (`O(log n)` each) gives worst-case `O(n log n + q log n)`.

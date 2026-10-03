# Sorting — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Why is every comparison sort `Ω(n log n)` in the worst case?

**2.** Why does merge sort stay `Θ(n log n)` on a sorted array?

**3.** Why can quicksort become `Θ(n²)`?

**4.** Which of insertion, selection, merge, heap, and quicksort are stable in the standard versions described in the notes?

**5.** Why is bottom-up build-heap `Θ(n)` even though one sift is `O(log n)`?

### Level 2 — Standard

**6.** How many comparisons does selection sort perform on 5 distinct keys?

**7.** Count inversions in `[2, 4, 1, 3]`. How many shifts does insertion sort perform?

**8.** Array `[3, 1, 4, 2]`, Lomuto partition, pivot = last element. What is the array just after the first partition?

**9.** Keys in `0..99`, `n = 10,000`. Time of counting sort?

**10.** Give best, average, and worst time, and extra space, for in-place quicksort with a fixed endpoint pivot (stack included).

### Level 3 — Multi-step

**11.** Merge `[1, 4, 7]` and `[2, 4, 8]`, and on equal keys take the left list. Write the output and say why the two 4s stayed in the original cross-list order.

**12.** Show the recursion cost of quicksort on `[1, 2, 3, 4]` if the pivot is always the first element. How many partition steps touch a subarray, in the `T(n) = T(n−1) + Θ(n)` sense?

**13.** LSD radix, decimal, on `[32, 11, 43, 21]`. Show the array after the ones pass and after the tens pass. Use a stable sort.

**14.** A file has `N = 10^6` records. Memory holds `M = 10^4`. You merge 10 runs at a time. How many merge passes after the initial run creation?

**15.** Median-of-medians uses `T(n) ≤ T(n/5) + T(7n/10) + O(n)`. Why does this not solve to `Θ(n log n)`?

### Level 4 — Trap-based

**16.** “Heap sort’s build phase is `Θ(n log n)`, so the sort is `Θ(n log n)`.” Which half is wrong, and does the final bound survive?

**17.** “Bubble sort is always `Θ(n²)`.” Give a version and an input where it is `Θ(n)`.

**18.** Insertion sort is coded with `while A[j] ≥ key`. Is it stable? Give a two-element counterexample if not.

**19.** Someone sorts integer keys in `0..n²` with counting sort and claims `Θ(n)` time. What fails?

**20.** Quicksort extra space is listed as `Θ(1)` because the partition is in-place. What is omitted for a sorted array and a last-element pivot?

### Level 5 — Challenge

**21.** Argue that `log2(n!) ≥ c n log2 n` for some `c > 0` and large `n`, using only `n! ≥ (n/2)^{n/2}`.

**22.** During mergesort, the next output comes from the right half while `r` keys remain in the left half. How many inversions does that emission reveal, and why is the total inversion-count still `Θ(n log n)` time?

**23.** Explain why a random pivot makes quicksort’s *expected* time `Θ(n log n)` on a sorted array, while a fixed last-element pivot does not.

**24.** Selection sort on `[2a, 3, 2b, 1]`, where `2a` appears before `2b`. Show the swaps and the final order of the two 2s.

**25.** You must sort records by `(year, month, day)` using three stable passes on one field each. Which field do you sort last, and why does an unstable middle pass break the method?

---

## Answers and explanations

**1.** The decision tree needs at least `n!` leaves, one per permutation. Height is at least `log2(n!) = Θ(n log n)`.

**2.** The algorithm always halves the array and always merges. The recurrence `T(n) = 2T(n/2) + Θ(n)` does not look at the data. There are `Θ(log n)` levels and `Θ(n)` work on each.

**3.** If every pivot is the smallest or largest remaining key, one side has size `n − 1`. Then `T(n) = T(n − 1) + Θ(n) = Θ(n²)`.

**4.** Stable: insertion (shift on `>`), merge (ties from the left). Unstable: selection, heap, quicksort.

**5.** A node of height `h` costs `O(h)`, and there are `O(n / 2^h)` such nodes. `Σ h/2^h` is a constant, so the sum is `Θ(n)`. Leaves, which are half the nodes, cost nothing.

**6.** `5·4/2 = 10`.

**7.** Inversions: `(2,1), (4,1), (4,3)`. Three. Insertion sort shifts three times.

**8.** Pivot 2. Scan: 3 stays, 1 swaps toward the boundary → `[1, 3, 4, 2]`, 4 stays, then pivot swaps with 3 → `[1, 2, 4, 3]`.

**9.** `Θ(n + k) = Θ(10000 + 99) = Θ(n)`.

**10.** Best `Θ(n log n)`, average `Θ(n log n)`, worst `Θ(n²)`. Stack `Θ(log n)` average and `Θ(n)` worst.

**11.** Output `[1, 2, 4_left, 4_right, 7, 8]`. On the tie the left 4 is emitted first, so the earlier list’s 4 stays before the other 4.

**12.** Pivot 1 leaves a right side of length 3. Then pivot 2 leaves length 2, then pivot 3 leaves length 1. Partition costs proportional to 4 + 3 + 2. That is the `Θ(n²)` pattern for `n = 4`.

**13.** Ones digits are 2, 1, 3, 1. Stable order: `11`, `21` (both ones-digit 1, input order kept), then `32`, then `43`. After the ones pass: `[11, 21, 32, 43]`. Tens digits are already increasing, so the tens pass leaves `[11, 21, 32, 43]`.

**14.** Number of initial runs = `10^6 / 10^4 = 100`. Each pass divides the run count by 10. Passes: 100 → 10 → 1, so 2 passes.

**15.** The two subproblem fractions sum to `0.9 < 1`. The non-recursive work per level of the inequality forms a geometric series `n + 0.9n + 0.9²n + … = O(n)`. A logarithm appears when the fractions sum to 1, as in `2 · (n/2)`.

**16.** Bottom-up build is `Θ(n)`, so that half is wrong if “build” means heapify. The sort is still `Θ(n log n)` because of the `n` extracts. The final bound survives; the reason given for the build does not.

**17.** Bubble sort that stops when a pass performs no swap, on an already sorted array: one pass, `Θ(n)`.

**18.** Not stable. `[2a, 2b]`: `2a ≥ 2b` is true if the keys are equal, so `2a` shifts right and the result is `[2b, 2a]`.

**19.** The count array has length `k + 1 = n² + 1`. Time and space are `Θ(n + n²) = Θ(n²)`, not `Θ(n)`.

**20.** The recursion depth is `n`. The call stack is `Θ(n)` extra memory on that input.

**21.** `log2(n!) ≥ log2((n/2)^{n/2}) = (n/2) log2(n/2) = (n/2) log2 n − n/2`. For large `n` this is at least `(1/4) n log2 n`. So `c = 1/4` works eventually.

**22.** Those `r` remaining left keys are each greater than the emitted right key and stand before it in the original array (left half is entirely before the right half). That is `r` inversions. They are charged in `O(1)` time during a merge that already costs linear work, so the whole mergesort remains `Θ(n log n)`.

**23.** A random pivot’s rank is uniform even if the array is sorted, because the pivot index is random, not because the values are. The average-case recurrence applies to every input. A fixed last element of a sorted array is always the maximum, so every split is `0` and `n − 1`.

**24.** Minimum is `1`, swapped with `2a`: `[1, 3, 2b, 2a]`. Next minimum among the suffix is `2b`, swapped with `3`: `[1, 2b, 3, 2a]`. Next, `2a` swaps with `3`: `[1, 2b, 2a, 3]`. `2b` is now before `2a`. Unstable.

**25.** Sort by day, then month, then year. The last pass is the primary key, year. Stability keeps the earlier month order inside one year. An unstable month pass can reorder days that share a month, and the later year pass will not repair that.

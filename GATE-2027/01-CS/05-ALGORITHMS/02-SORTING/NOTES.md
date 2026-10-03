# Sorting — Learning Notes

These notes are for learning sorting as it is examined in GATE. After you can derive the bounds, use `REVISION.md` for a short pass. Binary heaps as a data structure are also under Programming and Data Structures; heap-sort’s running time is derived here.

A **comparison sort** decides order only by tests of the form `A[i] ? A[j]`. Its worst case is `Ω(n log n)`. Counting sort, radix sort, and bucket sort use the structure of the keys and can be faster when that structure is promised.

---

## 1. What sorting asks for

**What it is.** Rearrange `n` keys so that `A[0] ≤ A[1] ≤ … ≤ A[n-1]` (non-decreasing). A stable sort also keeps the original relative order of equal keys.

**Intuition.** Equal keys are not identical records. If you sort students by marks and two students share a mark, stability decides whether their earlier order survives.

**Why stability matters.** Multi-key sorting (day, then month, then year) is correct if you sort by the least significant key first and every pass is stable. An unstable pass can undo the previous key.

**In-place.** Extra memory is `O(1)` or `O(log n)` beyond the input, ignoring the output. Merge sort’s auxiliary buffer is `Θ(n)`, so the usual implementation is not in-place. Recursion stacks are easy to forget: quicksort’s stack is `O(log n)` on average and `O(n)` in the worst case.

---

## 2. Decision-tree lower bound

**What it is.** Any comparison sort corresponds to a binary tree. Each internal node is a comparison. Each leaf is one permutation of the input.

**Why there are at least `n!` leaves.** Every permutation of distinct keys must reach a different leaf. Otherwise two different orders would be treated as already sorted by the same sequence of answers, and one of them would be wrong.

**Why the height is `Ω(n log n)`.** A binary tree of height `h` has at most `2^h` leaves. So `2^h ≥ n!`, hence `h ≥ log2(n!)`.

Stirling: `log2(n!) = n log2 n − n log2 e + O(log n)`. The dominant term is `n log n`. Therefore every comparison sort uses `Ω(n log n)` comparisons in the worst case.

**Average case.** The same tree argument, using the average depth of a binary tree with `n!` leaves, also gives `Ω(n log n)` average comparisons.

**What the bound does not say.** It says nothing about counting sort. Counting sort does not ask “is this key smaller than that key?”. It uses key values as array indexes. If the question says “comparison-based”, the bound applies. If the keys are integers in a small range, it may not.

**GATE trap.** “The best sorting algorithm is `O(n)`.” That is false for comparison sorts. It can be true for integers in a restricted range.

---

## 3. Insertion sort

**What it is.** Grow a sorted prefix. Insert the next key into its place by shifting larger prefix keys one step right.

**Intuition.** How you sort a hand of cards: the left part stays sorted, and you slide the new card in.

**Why it works.** After `i` insertions the prefix `A[0..i]` is sorted. The next key moves left only across keys that are strictly larger, so the new prefix is sorted. Equal keys stay to the left if the shift condition is `>`, so the sort is stable.

```
for i = 1 to n - 1:
    key = A[i]
    j = i - 1
    while j >= 0 and A[j] > key:
        A[j + 1] = A[j]
        j = j - 1
    A[j + 1] = key
```

**Example.** `[5, 2, 4, 2]`.

- Insert 2: `[2, 5, 4, 2]`
- Insert 4: `[2, 4, 5, 2]`
- Insert 2: the last 2 slides past 5 and 4 and stops before the first 2, because the test is strict `>`. Result `[2, 2, 4, 5]`. The two 2s kept their order.

**Complexity.**

| Case | Time | Why |
|------|------|-----|
| Best | `Θ(n)` | Already sorted: the inner while never shifts; `n − 1` comparisons |
| Average | `Θ(n²)` | About half of the pairs are inversions on random distinct keys |
| Worst | `Θ(n²)` | Reverse sorted: `1 + 2 + … + (n − 1) = n(n − 1)/2` shifts |
| Auxiliary space | `Θ(1)` | The key and the index |

An **inversion** is a pair `i < j` with `A[i] > A[j]`. Each shift undoes one inversion. Insertion sort’s shift count equals the inversion count. The maximum is `n(n − 1)/2`.

**When to use.** Nearly sorted data, tiny `n`, or as the base case of a fast sort (a short run is cheaper to insert than to recurse). Online: you can insert keys as they arrive.

**When not to use.** Large random inputs. Use mergesort or heapsort for a worst-case `n log n` guarantee, or quicksort for a fast average.

**Comparison.** Selection sort always does `Θ(n²)` comparisons. Insertion sort adapts: sorted input is linear. Bubble sort with a swap flag has the same best case, but insertion sort does better on “almost sorted” inputs because each key moves directly to its place.

**GATE traps.**

- Best case is linear only if the inner loop stops on order. A version that always scans the whole prefix is `Θ(n²)` even when sorted.
- Stability needs `>` rather than `≥` in the shift test.
- “Number of swaps” may mean shifts. Read the question. The inversion count is the shift count.

---

## 4. Selection sort

**What it is.** For position `i`, scan the unsorted suffix, find the minimum, and swap it into `i`.

**Intuition.** Pick the next champion by looking at everyone still waiting.

**Why it works.** The minimum of the suffix belongs at the next index. Swapping it there extends a sorted prefix of the `i` smallest keys. The suffix is whatever remains.

```
for i = 0 to n - 2:
    m = i
    for j = i + 1 to n - 1:
        if A[j] < A[m]: m = j
    swap A[i], A[m]
```

**Example.** `[3, 1, 2]`. Swap 3 and 1 → `[1, 3, 2]`. Swap 3 and 2 → `[1, 2, 3]`. Comparisons: 2, then 1. Total 3 = `3·2/2`.

**Complexity.** The inner scan length is `n − 1, n − 2, …, 1` no matter what the values are.

| Case | Time | Why |
|------|------|-----|
| Best, average, worst | `Θ(n²)` | Comparisons always `n(n − 1)/2` |
| Swaps | at most `n − 1` | One swap per position |
| Auxiliary space | `Θ(1)` | In-place |

**Properties.** Not stable. `[2a, 3, 2b, 1]` swaps `1` with `2a` and produces `[1, 3, 2b, 2a]`. The two equal keys changed order. The algorithm does the minimum possible number of swaps among algorithms that place one element per pass, but comparisons dominate.

**When to use.** You must minimise writes (expensive memory) and `n` is small. Rarely the right general sort.

**When not to use.** Large `n`, or when stability is required.

**GATE trap.** “Selection sort is `O(n)` because it swaps only `n` times.” Writes are `O(n)`; comparisons are still quadratic. Time follows the comparisons.

---

## 5. Bubble sort

**What it is.** Repeatedly walk the array and swap adjacent keys that are out of order. Each pass places the next maximum at the end.

**Intuition.** Large keys bubble to the end through adjacent swaps. Each pass shortens the unsorted prefix by one.

**Why it works.** After one pass the maximum sits at the end, because it wins every adjacent comparison. Induction on the suffix gives a full sort. Adjacent swaps generate the symmetric group, so every permutation can be sorted this way.

```
repeat
    swapped = false
    for i = 0 to n - 2:
        if A[i] > A[i + 1]:
            swap A[i], A[i + 1]
            swapped = true
until not swapped
```

**Example.** `[3, 2, 1]`. Pass 1: `[2, 3, 1]` then `[2, 1, 3]`. Pass 2: `[1, 2, 3]`. Pass 3 sees no swap and stops if the flag is used. Without the flag you still run `n − 1` passes.

**Complexity.**

| Case | Time | Why |
|------|------|-----|
| Best, with swap flag | `Θ(n)` | Sorted input: one pass, `n − 1` comparisons, no swap |
| Best, without flag | `Θ(n²)` | Always `n − 1` passes |
| Average and worst | `Θ(n²)` | Reverse order needs `Θ(n²)` adjacent swaps |
| Auxiliary space | `Θ(1)` | In-place |

The number of adjacent swaps equals the number of inversions, same as insertion sort’s shift count. Worst case `n(n − 1)/2`.

**Properties.** Stable if you swap only on strict `>`. Easy to code. Poor locality compared with insertion sort in practice, and the same asymptotic worst case.

**When not to use.** Any large input. It is a teaching algorithm and a source of inversion-count questions.

**GATE trap.** Quoting best-case `Θ(n)` for a version that always runs `n − 1` passes. The flag is part of the claim.

---

## 6. Merge sort

**What it is.** Split the array in half, sort each half, merge the two sorted halves.

**Intuition.** Two sorted piles can be merged by always taking the smaller front element. The split produces those piles.

**Why it works.** A single element is sorted. If both halves are sorted, the merge output is sorted: the element you emit is the smallest among those not yet emitted, because both fronts are the smallest remaining in their halves. Stability: on a tie, emit from the left half first.

```
mergesort(A, lo, hi):
    if lo >= hi: return
    mid = lo + (hi - lo) // 2
    mergesort(A, lo, mid)
    mergesort(A, mid + 1, hi)
    merge the two halves into a buffer, then copy back
```

Merge: walk two pointers. Each step copies one element into the buffer. Ties prefer the left half.

**Example.** `[4, 1, 3, 2]`.

- Halves `[4, 1]` and `[3, 2]`.
- Those become `[1, 4]` and `[2, 3]`.
- Merge: 1 then 2 then 3 then 4.

**Why the time is always `Θ(n log n)`.** Draw the recursion tree. The top level merges `n` elements and does `Θ(n)` work. The next level merges two blocks of `n/2`, still `Θ(n)` altogether. There are `1 + log2 n` levels until the pieces have size 1 (exactly `log2 n` split levels when `n` is a power of two). Total `Θ(n log n)`.

The recurrence is `T(n) = 2T(n/2) + Θ(n)`, `T(1) = Θ(1)`. Master theorem: `a = 2`, `b = 2`, `log_b a = 1`, and `f(n) = Θ(n) = Θ(n^{log_b a})`, so case 2 gives `T(n) = Θ(n log n)`. The input values never appear in the recurrence, so best, average, and worst time match.

| Case | Time | Auxiliary space |
|------|------|-----------------|
| Best, average, worst | `Θ(n log n)` | `Θ(n)` for the merge buffer |
| Recursion stack | — | `Θ(log n)` extra |

**Comparisons.** Merging two lists of length `n/2` uses at most `n − 1` comparisons and at least about `n/2`. Over the whole tree the total stays `Θ(n log n)`.

**Properties.** Stable if ties prefer the left half. Not in-place in this form. Excellent for linked lists (merge needs no random access and can relink nodes with `O(1)` extra memory) and for external sorting.

**When to use.** You need a worst-case guarantee, stability, or you are sorting data on disk (runs, then a multi-way merge).

**When not to use.** Tight extra memory and no need for stability: heapsort is in-place and also `Θ(n log n)` worst case. Random RAM data where average speed matters: quicksort’s inner loop is often faster, without a worst-case promise unless you change the pivot rule.

**External sort sketch.** If only `M` records fit in memory, sort runs of length `M`, then merge `k` runs at a time. The number of passes is about `ceil(log_k (N/M))`. GATE uses this counting argument more often than it asks for code.

**GATE traps.**

- “Merge sort is in-place.” The buffer is linear.
- “Best case is linear because the array might be sorted.” The standard top-down algorithm still splits and merges everything. (Natural merge sort, which finds existing runs, is a different algorithm.)
- Forgetting that the `Θ(n)` per level is the sum of all merges on that level, not `Θ(n)` per subproblem on top of another `n`.

---

## 7. Quicksort

**What it is.** Pick a pivot, partition so that keys less than the pivot lie to its left and keys greater lie to its right, then recurse on the two sides. The pivot is then in its final place.

**Intuition.** One partition does not fully sort, but it permanently places one key and reduces two smaller independent problems. Unlike mergesort, the expensive combine step is empty; the cost is in the partition.

**Why a good pivot gives `n log n`.** If the pivot always falls in the middle fraction of the ranks, both sides shrink by a constant factor. The recursion tree has `O(log n)` levels and each level partitions `O(n)` keys in total, so the cost is `O(n log n)`.

**Why a bad pivot gives `n²`.** If the pivot is always the smallest or largest remaining key, one side has `n − 1` elements. Then

```
T(n) = T(n − 1) + Θ(n) = Θ(n) + Θ(n − 1) + … + Θ(1) = Θ(n²)
```

Sorted input with “pivot = first element” does exactly this: the first element is the smallest, the left side is empty, and the right side is `n − 1` long.

**Average case.** Assume distinct keys and a pivot whose rank is uniform in the current subarray (true for a random pivot, or for a random permutation with a fixed pivot position). Then

```
T(n) = Θ(n) + (1/n) · Σ_{q=0}^{n−1} (T(q) + T(n − 1 − q))
```

This solves to `Θ(n log n)`. The constant is larger than mergesort’s: about `2 ln 2 ≈ 1.39` times `n log2 n` comparisons in the usual analysis. Average and best are both `Θ(n log n)`. The best case is a perfectly balanced pivot every time, which is the same class, with a smaller constant than the average.

| Case | Time | Why | Auxiliary space |
|------|------|-----|-----------------|
| Best | `Θ(n log n)` | Pivot rank near the middle every time | `Θ(log n)` stack |
| Average | `Θ(n log n)` | Uniform pivot rank; recurrence above | `Θ(log n)` expected stack |
| Worst | `Θ(n²)` | Pivot always extreme; `T(n) = T(n − 1) + Θ(n)` | `Θ(n)` stack |

**Lomuto partition (pivot = last element).** Scan `i` from the left. Maintain a boundary `s` of keys known to be `< pivot`. Swap when you see a smaller key. Finally swap the pivot into `s`.

**Example.** `[3, 1, 4, 2]`, pivot `2`.

- 3 is not smaller. 1 is smaller: swap with the boundary → `[1, 3, 4, 2]`.
- 4 is not smaller. Place pivot: `[1, 2, 4, 3]`.
- Recurse on `[1]` and `[4, 3]`.

**Hoare partition** uses two pointers moving inward and does fewer swaps on average. Either partition is correct if every key on the left is `≤` pivot and every key on the right is `≥` pivot (the treatment of equals must be consistent).

**Properties.** In-place aside from the stack. Not stable: partition swaps can leapfrog equal keys. Cache-friendly on arrays. The worst case is a real input pattern, not a theoretical curiosity.

**Making the worst case unlikely.**

- Random pivot: expected time `Θ(n log n)` on every input. Worst case still `Θ(n²)`, but only on unlucky random choices.
- Median-of-three: better in practice, still `Θ(n²)` on some inputs.
- True linear-time median (median of medians) as pivot: worst case `Θ(n log n)`, with a large constant. Rarely used in the inner loop; important as an existence result.

**When to use.** General in-memory sorting of primitive keys when an expected `n log n` bound is acceptable.

**When not to use.** You need stability (use mergesort) or a hard worst-case bound without a heavy pivot algorithm (use heapsort or mergesort). Linked lists: partition is awkward; mergesort fits lists better.

**Comparison with mergesort.** Mergesort pays `Θ(n)` extra memory and always runs in `Θ(n log n)`. Quicksort pays almost no extra memory, is usually faster by constants, and can run in `Θ(n²)`.

**GATE traps.**

- “Quicksort is always `O(n log n)`.” That is the average, or the best, not the worst.
- “Sorted input is the best case.” For a naive first-element pivot it is the worst case.
- Space `O(1)` forgets the recursion stack. Tail-recursion elimination on the larger side brings the worst-case stack down to `O(log n)` even when the time is still quadratic — time and stack are different.
- Duplicates: a partition that puts all equals on one side can still degenerate. A three-way partition (less, equal, greater) fixes many-duplicate inputs.

---

## 8. Heap sort

**What it is.** Build a max-heap, then repeatedly swap the root (the maximum) with the last unsorted position and restore the heap on the prefix.

**Intuition.** A heap lets you read the maximum in `O(1)` and delete it in `O(log n)`. Doing that `n` times emits keys from largest to smallest.

**Array heap (0-based).** Parent of `i` is `floor((i − 1) / 2)`. Children are `2i + 1` and `2i + 2`. A max-heap satisfies `A[parent] ≥ A[child]`. It is a complete binary tree, so the height is `floor(log2 n)`.

**Why build-heap is linear.** Sift-down from the last non-leaf `floor(n/2) − 1` toward the root. A node at height `h` costs `O(h)`. At most about `n / 2^{h+1}` nodes have height `h`.

```
Σ_h h · n / 2^{h+1} = O(n) · Σ_h h / 2^h
```

The series `Σ h / 2^h` converges (its sum is 2). Most nodes are leaves and do not sift at all. So build-heap is `Θ(n)`, not `Θ(n log n)`.

**Why the whole sort is `Θ(n log n)`.** After the build, you extract `n − 1` times. Each extract sifts from the root, height `Θ(log n)`. Total `Θ(n log n)`. The linear build is absorbed.

| Case | Time | Why | Auxiliary space |
|------|------|-----|-----------------|
| Best, average, worst | `Θ(n log n)` | `n` extracts, each `O(log n)`; build is `O(n)` | `Θ(1)` extra (the heap is the array) |

The heap shape does not depend on key order, and a sift from the root is `Θ(log n)` whenever the root must travel to a leaf. Best and worst stay in the same class. (The exact number of swaps varies, but not enough to leave `Θ(n log n)`.)

**Properties.** In-place. Not stable: the last leaf can jump to the root and pass equal keys. Worse locality than quicksort. Worst-case guarantee as strong as mergesort, without the buffer.

**When to use.** You need in-place and `O(n log n)` worst case together.

**When not to use.** Stability required. Or average speed is the only goal and a quadratic worst case is acceptable (quicksort).

**GATE traps.**

- Build-heap quoted as `O(n log n)`. Bottom-up build is `O(n)`. Inserting `n` keys one by one into an empty heap is `O(n log n)`. The phrase “build heap” in heap-sort means the bottom-up method unless the question says otherwise.
- 0-based versus 1-based child indexes. 1-based: children `2i` and `2i + 1`, parent `floor(i/2)`.
- Heap-sort is not a stable sort.

---

## 9. Counting sort

**What it is.** Keys are integers in `0 … k`. Count how many times each value occurs, turn the counts into end positions, and write each input key into a slot reserved for its value.

**Intuition.** If you know the only possible names are a small set, you can make a pigeonhole for each name instead of comparing names.

**Why it is stable.** Process the input from right to left. The cumulative count `C[v]` is the last free slot for value `v`. The rightmost input key of value `v` is placed first, into the rightmost slot, then `C[v]` decreases. Earlier equal keys land further left. Original order is preserved.

```
count[0..k] = 0
for each key x: count[x] += 1
for v = 1 to k: count[v] += count[v - 1]    # count[v] = number of keys ≤ v
output = array of size n
for i = n - 1 down to 0:
    v = A[i]
    output[count[v] - 1] = A[i]
    count[v] -= 1
```

**Example.** `A = [2, 0, 2, 1]`, `k = 2`.

- Counts: 0 once, 1 once, 2 twice. Prefix: `[1, 2, 4]`.
- Place from the right: last 2 goes to index 3, the 1 goes to index 1, the first 2 goes to index 2, the 0 goes to index 0.
- Output `[0, 1, 2, 2]`.

**Complexity.**

| Case | Time | Space |
|------|------|-------|
| Best, average, worst | `Θ(n + k)` | `Θ(n + k)` for the count array and the output |

There is no “bad order”. The loops do not compare keys. If `k = O(n)`, time is `Θ(n)`, which beats the comparison lower bound because the model is different.

**When to use.** Integers, or keys that map to integers, with `k` not much larger than `n`. As the stable digit sort inside radix sort.

**When not to use.** `k` is huge (counting to `10^12` is impossible). Arbitrary comparable objects with no small integer code. Memory is tighter than `Θ(n + k)`.

**GATE traps.**

- Calling it a comparison sort.
- Forgetting the output buffer: a naive in-place rewrite is easy to make unstable or wrong.
- `k` is the largest key, not the number of distinct keys, in the implementation above. (You can compress ranks, but that needs a sort or a map.)

---

## 10. Radix sort

**What it is.** Sort integers by one digit at a time, least significant digit first, using a stable sort (counting sort) for each digit.

**Why LSD works.** After the ones digit is stable-sorted, equal ones-digits keep the order they already had. Sorting by the tens digit then groups by tens, and within one ten the ones order survives because the digit sort is stable. After the last digit, the keys are fully ordered. This is the same reason multi-key stable sorting works.

**Example.** `[170, 45, 75, 90]`, padded to three digits: `170, 045, 075, 090`.

- Ones digits `0, 5, 5, 0`. Stable order: `170, 090, 045, 075`.
- Tens digits `7, 9, 4, 7`. Stable order: `045, 170, 075, 090`. The two tens-digit 7s keep the order `170` then `075`.
- Hundreds digits `0, 1, 0, 0`. Stable order: `045, 075, 090, 170`.

Result: `[45, 75, 90, 170]`.

**Complexity.** `d` digits, each counting sort `Θ(n + b)` where `b` is the digit alphabet (10, or 256, or `2^r`).

| Case | Time | Space |
|------|------|-------|
| All cases | `Θ(d(n + b))` | `Θ(n + b)` |

For word-sized integers, `d` and `b` are often treated as constants, giving `Θ(n)`. If you set the digit width so that `b = n` and the word has `O(log n)` bits, then `d = O(log n / log n) = O(1)` only when the word length is `O(log n)` bits — machine words. For integers in `0 … n^c − 1`, a careful radix is linear. Do not claim `O(n)` for arbitrary-precision integers with `Θ(n)` digits.

**MSD radix sort** buckets by the first digit and recurses. It does not need stability in the same way, and it can stop early on buckets of size 1. Worst-case class is the same order.

**When not to use.** Variable-length strings unless you define the digit passes carefully. Comparison sorts are simpler when `d` is large.

**GATE trap.** Using an unstable sort for the digit pass and still claiming LSD radix is correct. Stability is the reason LSD works.

---

## 11. Bucket sort

**What it is.** Throw keys into `n` buckets that cover equal slices of the key range, sort each bucket, concatenate.

**Why the average can be linear.** If keys are uniform on an interval, each bucket receives `O(1)` expected keys. Sorting a bucket of constant size is constant work. `n` buckets give expected `Θ(n)` plus the distribution pass.

**Why the worst case is quadratic.** Every key can fall into one bucket. Sorting that bucket with insertion sort is `Θ(n²)`.

| Case | Time | Space |
|------|------|-------|
| Best | `Θ(n)` | `Θ(n)` buckets |
| Average, uniform | `Θ(n)` | `Θ(n)` |
| Worst | `Θ(n²)` | `Θ(n)`, if the inner sort is quadratic |

**When to use.** Numeric keys known to be uniform, and an expected linear bound is what the question asks.

**When not to use.** No distribution promise. Adversarial or skewed data.

**GATE trap.** Stating `O(n)` with no uniformity assumption.

---

## 12. Quickselect and worst-case linear selection

**What it is.** Find the `k`-th smallest without fully sorting. Partition as in quicksort. Recurse only into the side that contains rank `k`.

**Average.** With a random pivot the expected cost satisfies `T(n) ≤ O(n) + (1/n) Σ T` on the larger side in the bad splits, and the solution is `T(n) = Θ(n)`. You discard a constant fraction of the array on average, so the series is `n + n/2 + n/4 + …` only in a rough balanced picture; the real proof charges the unlucky splits and still gets a linear expectation (at most `4n` or a similar constant in CLRS).

**Worst case of plain quickselect.** `Θ(n²)`, same degenerate pivots as quicksort.

**Median of medians (groups of 5).** Split into groups of 5, sort each group (`O(n)`), take the `n/5` medians, and recursively find the median of those medians. That pivot is guaranteed to be greater than at least about `3n/10` keys and smaller than at least about `3n/10`. The recursive call is on at most `7n/10` elements, plus `T(n/5)` to find the pivot:

```
T(n) ≤ T(n/5) + T(7n/10) + O(n)
```

`1/5 + 7/10 = 0.9 < 1`, so the work shrinks geometrically and `T(n) = Θ(n)` in the worst case.

**When to use.** Order statistics: median, `k`-th smallest. As a theoretical pivot for worst-case quicksort.

**GATE observation.** “Selection is `O(n)`” is true for the worst-case algorithm and for the *expected* time of randomised quickselect. It is false as a worst-case claim about naive quickselect.

---

## 13. Special linear patterns

**Sorting 0, 1, 2 (Dutch national flag).** Three pointers: `lo` for the next 0, `mid` for the scan, `hi` for the next 2. Swap 0s left and 2s right. One pass, `Θ(n)` time, `Θ(1)` space. This is partition, not a general sort.

**Counting inversions.** During mergesort, when the right-half front is emitted before `r` keys remain on the left, those `r` left keys form inversions with it. Total time stays `Θ(n log n)`. Insertion sort counts the same quantity in `Θ(n + I)` time, which is quadratic when `I` is quadratic.

---

## 14. Comparison table

| Algorithm | Best | Average | Worst | Extra space | Stable | Comparison sort |
|-----------|------|---------|-------|-------------|--------|-----------------|
| Insertion | `Θ(n)` | `Θ(n²)` | `Θ(n²)` | `Θ(1)` | Yes, if shift on `>` | Yes |
| Selection | `Θ(n²)` | `Θ(n²)` | `Θ(n²)` | `Θ(1)` | No | Yes |
| Bubble, with flag | `Θ(n)` | `Θ(n²)` | `Θ(n²)` | `Θ(1)` | Yes, if swap on `>` | Yes |
| Merge | `Θ(n log n)` | `Θ(n log n)` | `Θ(n log n)` | `Θ(n)` | Yes, if ties take the left | Yes |
| Quick | `Θ(n log n)` | `Θ(n log n)` | `Θ(n²)` | `Θ(log n)` avg stack, `Θ(n)` worst | No | Yes |
| Heap | `Θ(n log n)` | `Θ(n log n)` | `Θ(n log n)` | `Θ(1)` | No | Yes |
| Counting | `Θ(n + k)` | `Θ(n + k)` | `Θ(n + k)` | `Θ(n + k)` | Yes, if filled right to left | No |
| Radix (LSD) | `Θ(d(n + b))` | `Θ(d(n + b))` | `Θ(d(n + b))` | `Θ(n + b)` | Yes, if digits are stable | No |
| Bucket | `Θ(n)` | `Θ(n)` uniform | `Θ(n²)` | `Θ(n)` | Possible | No |

Shell sort depends on the gap sequence (Hibbard gaps are `O(n^{3/2})`). It is a comparison sort and in-place. Do not memorise a single “shell sort complexity” unless the gaps are given.

---

## 15. How to choose

| Requirement | Choice |
|-------------|--------|
| Worst-case `n log n`, stable, memory available | Merge sort |
| Worst-case `n log n`, in-place | Heap sort |
| Fast average, in-place, stability irrelevant | Quick sort |
| Nearly sorted | Insertion sort |
| Integers in `0..k` with small `k` | Counting sort |
| Fixed-length integers or digit strings | Radix sort |
| Uniform floats, expected linear | Bucket sort |
| Linked list | Merge sort |
| Disk, runs of size `M` | External multi-way merge |
| Only the `k`-th smallest | Quickselect or median of medians |

---

## 16. Common GATE traps

1. Quicksort’s worst case called `n log n`, or its average called `n²`.
2. Sorted input treated as quicksort’s best case under a fixed endpoint pivot.
3. Build-heap called `O(n log n)` when the bottom-up algorithm is used.
4. Merge sort called in-place, or given a linear best case.
5. Selection sort’s time taken from its swap count.
6. Bubble sort’s best case quoted as linear when the code has no early exit.
7. Counting or radix sort used to “beat” the comparison lower bound inside the comparison model.
8. LSD radix with an unstable digit sort.
9. Stability destroyed by `≥` in insertion sort.
10. Heap child indexes mixed between 0-based and 1-based layouts.

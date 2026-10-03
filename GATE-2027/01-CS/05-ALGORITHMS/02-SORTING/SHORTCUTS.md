# Sorting — Shortcuts

### Endpoint pivot + sorted input → quadratic quicksort

**Shortcut.** If the pivot is always the first or last cell, a sorted or reverse-sorted array makes one side empty every time.

**Why it works.** The pivot is then the extreme key. The recurrence collapses to `T(n) = T(n − 1) + Θ(n)`.

**When to use.** The question names the pivot rule and the input order.

**Example.** Pivot = last, array already increasing: each partition peels off one key.

**Limitation.** A random pivot has expected `Θ(n log n)` even on sorted input. Do not quote `n²` unless the pivot rule can be forced.

---

### Values do not appear in the recurrence → same best and worst

**Shortcut.** Merge sort and the heap-extract loop stay `Θ(n log n)` on every input, because the cost is the shape of the recursion or the heap, not the number of inversions.

**Why it works.** Merge always splits in half. A sift from the root walks `Θ(log n)` edges whenever the heap height is logarithmic, which it always is.

**When to use.** “Best-case time of merge sort / heap sort.”

**Example.** A sorted array still produces `log n` full merge levels.

**Limitation.** Natural merge sort, which detects existing runs, is a different algorithm and can be linear on sorted input. Heap-sort’s exact swap count does vary; the class does not.

---

### Inversions tell you the adjacent-swap cost

**Shortcut.** Insertion-sort shifts and bubble-sort adjacent swaps both equal the inversion count.

**Why it works.** Each such move removes exactly one inversion and never creates one.

**When to use.** “How many swaps does bubble sort perform on this array?”

**Example.** `[3, 1, 2]` has inversions `(3,1), (3,2)`. Two swaps.

**Limitation.** Selection sort’s swaps are not the inversion count. It can repair many inversions with one long swap.

---

### Small integer range → you may leave the comparison model

**Shortcut.** If every key is an integer in `0..k`, counting sort is `Θ(n + k)`. If that `k` is `O(n)`, the bound is linear.

**Why it works.** Keys are used as indexes. The decision-tree bound counts only comparison algorithms.

**When to use.** The stem gives a range, or asks for a stable linear sort of small integers.

**Example.** `n` keys in `0..n`: counting sort is `Θ(n)`.

**Limitation.** A huge range makes `k` the dominant term. Arbitrary real keys do not have a `k`.

---

### LSD radix needs a stable digit sort

**Shortcut.** Sort digits from right to left, and keep the digit sort stable. Otherwise a later digit pass scrambles the earlier one.

**Why it works.** Stability is what preserves the order of the less significant digits inside one bucket of the current digit.

**When to use.** A question asks why radix sort is correct, or whether an unstable pass is allowed.

**Example.** Sorting by tens with an unstable sort can reorder two numbers that share a tens digit and were already ordered by ones.

**Limitation.** MSD radix sort recurses inside buckets and does not rely on the same left-to-right stability argument.

---

### Build-heap bottom-up is linear

**Shortcut.** `Θ(n)` to heapify an array from the bottom; `Θ(n log n)` if you insert `n` keys one by one.

**Why it works.** Almost all nodes have tiny height. `Σ h/2^h` is constant, so the sift costs sum to linear.

**When to use.** Heap-sort’s build phase, or “time to build a heap from an unsorted array.”

**Example.** A million keys: bottom-up build is proportional to a million siftdown steps of small height, not a million times 20.

**Limitation.** One `extract-max` is still `O(log n)`. The sort’s later phase is `Θ(n log n)`.

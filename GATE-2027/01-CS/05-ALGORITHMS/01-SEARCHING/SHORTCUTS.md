# Searching — Shortcuts

### Sorted random-access array → binary search

**Shortcut.** If the array is sorted and you can read any index in constant time, search in `Θ(log n)`.

**Why it works.** One comparison discards half the remaining interval, and the invariant “the key is inside `[lo, hi]` if it exists” is preserved.

**When to use.** Equality, first or last occurrence, or a count of duplicates on a sorted array.

**Example.** One million sorted keys: worst case about 20 probes, not a million.

**Limitation.** Unsorted input makes the discard step false. Duplicates: a plain equality return is not the first index.

---

### Monotone yes/no → binary search the number, not the array

**Shortcut.** If “`x` is feasible” implies “every larger `x` is feasible” (or the opposite), binary-search `x`.

**Why it works.** The feasible set is a suffix or a prefix of the integer line, so it has one boundary.

**When to use.** Minimum capacity, minimum maximum load, maximum minimum gap.

**Example.** Smallest `x` with `x² ≥ 30` is 6. Test the middle and discard one side.

**Limitation.** If feasibility is not monotone, the discarded side can hide the only feasible point.

---

### One query, unsorted → do not sort first

**Shortcut.** A single lookup on unsorted data is a linear scan. Sorting first costs more.

**Why it works.** `n log n` preprocessing dominates one `n` scan.

**When to use.** The structure is thrown away after one question.

**Example.** Find 7 in an unsorted list of 1000 numbers: scan. Sorting is extra work.

**Limitation.** If the same array answers many later queries, preprocessing pays off. Read the whole question.

---

### `log log n` is not the worst case of interpolation

**Shortcut.** Quote `O(log log n)` only as an average under uniformity. The worst case is linear.

**Why it works.** A linear probe formula can step by one index on skewed data. Uniform data is what makes the expected probe count double-logarithmic.

**When to use.** A question that states “uniformly distributed keys” and asks expected time.

**Example.** Keys `1, 2, 4, 8, …` can force a bad interpolation sequence.

**Limitation.** Do not “improve” a worst-case binary-search answer to `log log n`.

---

### Rotated sorted array, distinct keys → still logarithmic

**Shortcut.** At each mid, one half is fully sorted. Keep the half whose range can contain the key.

**Why it works.** A single rotation leaves one contiguous sorted run on at least one side of `mid`.

**When to use.** The problem says the array was sorted and then rotated, and keys are distinct.

**Example.** `[4, 5, 6, 7, 0, 1, 2]`, key `0`, goes to the right half first.

**Limitation.** Many duplicate keys can make both halves uninformative. Worst case can be linear.

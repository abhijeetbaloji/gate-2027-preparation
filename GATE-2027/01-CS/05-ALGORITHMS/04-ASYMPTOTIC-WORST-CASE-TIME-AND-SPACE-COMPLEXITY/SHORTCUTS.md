# Asymptotic Complexity — Shortcuts

### The heaviest positive term wins

**Shortcut.** `n³ + 100 n² + n log n = Θ(n³)`.

**Why it works.** For positive functions, `f + g = Θ(max(f, g))`. A polynomial’s degree is that max.

**When to use.** Closed forms and loop sums you have already solved.

**Example.** `n(n+1)/2 = Θ(n²)`, not `Θ(n² + n)`.

**Limitation.** This does not compare `2^n` with `n!`. Use the growth list. It also does not apply to alternating or negative terms; complexities in this course are non-negative.

---

### Same exponential base, constant factor in front

**Shortcut.** `2^{n+1}` and `5 · 2^n` are both `Θ(2^n)`. `4^n` is not.

**Why it works.** `2^{n+1} = 2 · 2^n`. `4^n = (2^n)² = 2^{2n}`, and `2^{2n} / 2^n = 2^n` grows, so no constant `c` works.

**When to use.** Options that differ only by a coefficient or by `+1` in the exponent.

**Example.** Recurrence solution `Θ(2^{n+1})` may be rewritten `Θ(2^n)`.

**Limitation.** `2^{n} · n` is `Θ(n 2^n)`, which is not `Θ(2^n)`. A polynomial factor in front of an exponential is a different class from the bare exponential.

---

### Case 2 of the Master theorem adds a log

**Shortcut.** If `f(n)` matches `n^{log_b a}` exactly, multiply by an extra `log n`.

**Why it works.** Every level of the tree costs the same, and there are `Θ(log n)` levels.

**When to use.** `T(n) = 2T(n/2) + n`, `T(n) = T(n/2) + 1`, and similar.

**Example.** Merge sort is `Θ(n log n)`, not `Θ(n)`.

**Limitation.** A polynomial gap (`n²` against critical exponent 1) is case 3 or case 1, with no extra log. If `f` is `n log n` and the critical term is `n`, the extended case 2 gives `Θ(n log² n)`.

---

### Doubling or halving inside a loop is logarithmic

**Shortcut.** `i = i * 2` or `i = i // 2` running until `n` contributes `Θ(log n)` iterations, not `Θ(n)`.

**Why it works.** After `k` steps the counter is `2^k`. Set `2^k = n`.

**When to use.** Inner while-loops whose counter multiplies or divides by a constant.

**Example.** For each of `n` outer indexes, a doubling inner loop gives `Θ(n log n)`.

**Limitation.** `i = i + 2` is still linear. Adding a constant does not halve the remaining work.

---

### Amortised `O(1)` still allows a linear spike

**Shortcut.** A doubling array’s insert is amortised `O(1)` and worst-case `O(n)`.

**Why it works.** Resizes are rare. Their total copy cost sums to linear, so the average over the sequence is constant. The resize step itself copies the whole array.

**When to use.** Dynamic tables, binary counters, stacks with multipop.

**Example.** The insert that grows 1024 to 2048 copies 1024 cells.

**Limitation.** Do not use this shortcut for a single operation that is always expensive. Amortised bounds need the whole sequence.

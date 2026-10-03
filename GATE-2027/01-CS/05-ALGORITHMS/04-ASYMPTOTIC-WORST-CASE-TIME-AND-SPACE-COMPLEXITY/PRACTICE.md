# Asymptotic Complexity — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** State the definition of `f(n) = O(g(n))`.

**2.** Why is `n = O(n²)` true, while `n = Θ(n²)` is false?

**3.** Solve `T(n) = 2T(n/2) + n`.

**4.** What is the difference between worst-case time and amortised time?

**5.** Order these by increasing growth: `n log n`, `n²`, `2^n`, `log n`, `n!`.

### Level 2 — Standard

**6.** Is `3n² + 9n + 1 = Θ(n²)`? Give constants `c1`, `c2` that work for all `n ≥ 1`.

**7.** How many times does the body run?

```
for i = 1 to n:
    for j = 1 to i:
        body
```

**8.** Solve `T(n) = T(n/2) + n`, `T(1) = Θ(1)`.

**9.** A doubling array performs `n` inserts starting from capacity 1. Total copying work, and amortised cost per insert?

**10.** Auxiliary space of mergesort, and of a recursion that only halves and stores `Θ(1)` locals, in terms of `n`.

### Level 3 — Multi-step

**11.** Use the Master theorem on `T(n) = 8T(n/2) + n²`. Name the case.

**12.** `T(n) = T(n/3) + T(2n/3) + Θ(n)`. Why is the Master theorem not directly applicable, and what is the solution?

**13.** Show `log2(n!) = Θ(n log n)` using ` (n/2)^{n/2} ≤ n! ≤ n^n `.

**14.** Nested loop: outer `i` from 1 to `n`, inner `j` starts at 1 and doubles while `j ≤ n`. Total cost?

**15.** Binary counter increments from 0 to `n − 1`. Why is the total number of bit flips `O(n)` even though some increments flip many bits?

### Level 4 — Trap-based

**16.** A student says merge sort is `O(n²)`, so its complexity matches quicksort’s worst case. What is misleading?

**17.** Is `2^{2n} = Θ(2^n)`? Prove or disprove from the definition.

**18.** Someone applies case 2 and answers `Θ(n²)` for `T(n) = 2T(n/2) + n²`. Which case is it really?

**19.** “Insert into a doubling vector is `O(1)`.” Add the missing adjective, and state the worst case of one insert.

**20.** Trial division tests divisibility of `N` by every integer up to `√N`. The input is the binary encoding of `N`. Is this polynomial in the input length?

### Level 5 — Challenge

**21.** Prove that `f + g = Θ(max(f, g))` for positive `f, g`.

**22.** The extended Master case has `f(n) = Θ(n^{log_b a} log^k n)`. State `T(n)`. Apply it to `T(n) = 2T(n/2) + n log n`.

**23.** For `T(n) = 2T(n/2) + n`, expand the inductive claim `T(n) ≤ n log2 n` one step, assuming it holds for `n/2`. Does the algebra close? What base-case condition do you still need?

**24.** Recursion tree for `T(n) = 2T(n/2) + n²`. Show the level costs form a geometric series and sum to `Θ(n²)`.

**25.** Potential `Φ` = number of 1-bits in a binary counter. Increment flips a suffix of 1-bits to 0 and one 0 to 1. Argue the amortised cost is `O(1)`.

---

## Answers and explanations

**1.** There exist `c > 0` and `n0` such that for every `n ≥ n0`, `f(n) ≤ c g(n)`.

**2.** `n ≤ 1 · n²` for `n ≥ 1`, so `O` holds. For Theta you also need `n ≥ c n²` for some `c > 0` and all large `n`, i.e. `c ≤ 1/n`, which cannot stay true for a fixed `c`.

**3.** `a = 2`, `b = 2`, `log_b a = 1`, `f(n) = n = Θ(n^{log_b a})`. Case 2. `T(n) = Θ(n log n)`.

**4.** Worst-case time is the maximum cost of one operation (or one input of size `n`). Amortised time is the total cost of a sequence divided by the length of the sequence. A rare expensive step can be worst-case linear and amortised constant.

**5.** `log n`, `n log n`, `n²`, `2^n`, `n!`.

**6.** Yes. Lower: `3n² + 9n + 1 ≥ 3n²`, so `c1 = 3`. Upper: `9n ≤ 9n²` and `1 ≤ n²` for `n ≥ 1`, so `3n² + 9n + 1 ≤ 13 n²`, `c2 = 13`.

**7.** `n(n+1)/2 = Θ(n²)`.

**8.** Unroll: `n + n/2 + n/4 + … + Θ(1) = Θ(n)`. Master: `a = 1`, `b = 2`, `log_b a = 0`, `f(n) = n = Ω(n^{0+ε})`, regularity `1 · (n/2) ≤ c n` with `c = 1/2`. Case 3. `Θ(n)`.

**9.** Copies at capacities 1, 2, 4, …, up to the largest power below `n`, sum to less than `2n`. Amortised `Θ(1)` per insert. (A single resizing insert is `Θ(n)`.)

**10.** Mergesort buffer `Θ(n)`, plus `Θ(log n)` stack if recursive. A single halving recursion has depth `Θ(log n)` and `Θ(log n)` stack.

**11.** `log2 8 = 3`. `f(n) = n² = O(n^{3−ε})` with `ε = 1`. Case 1. `T(n) = Θ(n³)`.

**12.** The two subproblems have different size ratios, so there is not a single `b` with `a` equal subproblems. The longer branch shrinks by `2/3` each time, so depth is `Θ(log n)`. Every level partitions the `n` work across disjoint subproblems and costs `Θ(n)`. Total `Θ(n log n)`.

**13.** `log2(n!) ≤ log2(n^n) = n log2 n`. `log2(n!) ≥ log2((n/2)^{n/2}) = (n/2)(log2 n − 1) = Ω(n log n)`. Together, `Θ(n log n)`.

**14.** Inner loop runs `Θ(log n)` times for each of `n` values of `i`. Total `Θ(n log n)`.

**15.** Bit 0 flips every step, bit 1 every two steps, bit `i` every `2^i` steps. Total flips are `Σ_{i≥0} floor(n / 2^i) < n · Σ 1/2^i < 2n`.

**16.** `O(n²)` is a true but loose upper bound for merge sort, whose tight bound is `Θ(n log n)`. Quicksort’s worst case is tightly `Θ(n²)`. The `O` statement hides the gap the question usually wants.

**17.** No. `2^{2n} / 2^n = 2^n`, which is larger than every constant `c` for large `n`. The upper bound in the definition of `O(2^n)` fails. (It is `Θ(4^n)`.)

**18.** Critical exponent is `log2 2 = 1`. `n²` is larger by a polynomial gap. Case 3, solution `Θ(n²)`. The *answer* `Θ(n²)` happens to be right; the case name is wrong. Regularity: `2 · (n/2)² = n²/2 ≤ (1/2) n²`.

**19.** Amortised `O(1)`. Worst case of the insert that resizes is `Θ(n)`.

**20.** No. Input length is `m = Θ(log N)` bits. The algorithm does `Θ(√N) = Θ(2^{m/2})` divisions, which is exponential in `m`.

**21.** Let `M = max(f, g)`. Then `M ≤ f + g ≤ 2M`. So `1 · M ≤ f + g ≤ 2 · M`. That is the definition of `Θ(M)`.

**22.** `T(n) = Θ(n^{log_b a} log^{k+1} n)`. Here `log_b a = 1` and `f(n) = Θ(n log n)`, so `k = 1`. `T(n) = Θ(n log² n)`.

**23.** Assume `T(n/2) ≤ (n/2) log2(n/2)`. Then `T(n) ≤ 2 · (n/2) log2(n/2) + n = n(log2 n − 1) + n = n log2 n`. The step closes with equality in the bound. You still need the claim to hold at the base (check the smallest `n` you recurse from, often `n = 2`, and define `T(1)` separately so you never take `log 1` inside a failing base). The `−n` from `log(n/2)` cancels the `+n` from the recurrence, which is why this particular guess does not need an extra slack term.

**24.** Level 0 costs `n²`. Level 1 has two subproblems costing `(n/2)²` each, total `n²/2`. Level `i` costs `n² / 2^i`. Sum from `i = 0` to `log2 n` is `n² (1 + 1/2 + 1/4 + …) < 2 n²`. Also `≥ n²`. So `Θ(n²)`.

**25.** Suppose an increment flips `t` ones to zero and one zero to one. Actual bit writes: `t + 1`. Potential change: `−t + 1`. Amortised cost: `(t + 1) + (−t + 1) = 2`. So every increment has amortised cost 2, which is `O(1)`. `Φ` never goes negative.

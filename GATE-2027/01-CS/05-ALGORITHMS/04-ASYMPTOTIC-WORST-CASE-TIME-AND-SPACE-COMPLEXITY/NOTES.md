# Asymptotic Worst-Case Time and Space Complexity — Learning Notes

Asymptotics is the language of every other topic in this section. A bound is a claim about a function for large input size, with constant factors and lower-order terms suppressed. GATE asks you to place a function in a class, solve a recurrence, read a loop nest, and separate best, average, and worst case.

---

## 1. Input size and cost

**What it is.** Fix a size measure `n`: array length, number of vertices plus edges, number of bits, or the numeric value, depending on the problem. Time `T(n)` counts primitive steps. Space counts memory cells, usually the **auxiliary** cells beyond the input itself.

**Intuition.** Two algorithms with costs `100 n` and `2 n log2 n` cross. For small `n` the linear one can be slower. Asymptotics describes the large-`n` side, which is what “efficient for big inputs” means.

**Why constants are hidden.** A step’s real time depends on the machine. Multiplying `T` by a positive constant, or adding a slower term, should not change the class. The definitions below are exactly that agreement.

**GATE trap.** Using the numeric value as `n` when the input length is the number of bits. Trial division up to `√N` is polynomial in the *value* `N` and exponential in the *bit length* `log N`. Say which `n` you mean.

---

## 2. Big-O, big-Omega, Theta

Let `f` and `g` be non-negative functions on the positive integers.

**Big-O (upper bound).** `f(n) = O(g(n))` if there exist constants `c > 0` and `n0` such that for all `n ≥ n0`,

```
f(n) ≤ c · g(n)
```

`g` is an asymptotic upper bound. The constant `c` must not depend on `n`.

**Big-Omega (lower bound).** `f(n) = Ω(g(n))` if there exist `c > 0` and `n0` such that for all `n ≥ n0`,

```
f(n) ≥ c · g(n)
```

**Theta (tight bound).** `f(n) = Θ(g(n))` if `f = O(g)` and `f = Ω(g)`. Equivalently, there exist positive `c1, c2, n0` with `c1 g(n) ≤ f(n) ≤ c2 g(n)` for all `n ≥ n0`.

**Why these quantifiers.** “There exists `c`” lets you ignore a fixed overhead. “For all sufficiently large `n`” lets a finite number of exceptions go. If you cannot find such a `c`, the claim is false.

**Example.** `3n² + 5n + 7 = Θ(n²)`.

- Upper: `3n² + 5n + 7 ≤ 3n² + 5n² + 7n² = 15 n²` for `n ≥ 1`. So `c2 = 15`.
- Lower: `3n² + 5n + 7 ≥ 3n²`. So `c1 = 3`.

**Example that is O but not Theta.** `n = O(n²)` because `n ≤ 1 · n²` for `n ≥ 1`. It is not `Ω(n²)`: `n ≥ c n²` would mean `1 ≥ c n` for all large `n`, which fails for every fixed `c > 0`.

**Little-o.** `f(n) = o(g(n))` if `f(n) / g(n) → 0`. For every `c > 0`, eventually `f(n) < c g(n)`. Little-o is a *strict* upper bound. `n = o(n²)`, but `3n²` is not `o(n²)`.

**Little-omega.** `f(n) = ω(g(n))` if `f / g → ∞`. `n² = ω(n)`.

**Limit test (when the limit exists).**

| Limit of `f/g` | Conclusion |
|----------------|------------|
| `0` | `f = o(g)` and `f = O(g)`, not `Θ` unless `g` is eventually 0 |
| positive constant | `f = Θ(g)` |
| `∞` | `f = ω(g)` and `f = Ω(g)` |

If the limit does not exist, the definitions with `c` and `n0` still apply. Oscillating functions need those, not the limit shortcut.

---

## 3. Properties you can use without reproving

For positive functions:

- `f = Θ(g)` if and only if `g = Θ(f)`. Theta is symmetric. Big-O is not.
- If `f = O(g)` and `g = O(h)`, then `f = O(h)`. Same for `Ω` and `Θ`.
- `f + g = Θ(max(f, g))` when `f, g` are positive. The faster-growing term swallows the other. So `n² + n = Θ(n²)`, and `n² + n³ = Θ(n³)`.
- `O(f) + O(g) = O(f + g) = O(max(f, g))`.
- `c · f = Θ(f)` for any constant `c > 0`. In particular `2^{n+1} = Θ(2^n)`, because `2^{n+1} = 2 · 2^n`.
- `2^{2n} = 4^n` is **not** `Θ(2^n)`. The ratio is `2^n`, which grows. Bases of exponentials matter; constant factors in the exponent do not stay inside Theta of the same exponential.
- `log_b n = Θ(log n)` for any fixed bases `> 1`, because `log_b n = log_k n / log_k b` and the denominator is constant. You may drop the base inside Theta. You may not drop a base inside an exponent.
- Polynomials: `a_d n^d + … + a0 = Θ(n^d)` if `a_d > 0`.
- `log n = o(n^ε)` for every `ε > 0`. Any positive power of `n` beats every logarithm.
- `n^k = o(c^n)` for every fixed `k` and every `c > 1`. Every polynomial loses to every growing exponential.
- `n! = ω(c^n)` for every fixed `c`. Factorial beats exponential.
- Stirling: `log(n!) = Θ(n log n)`.

**Standard order, slowest to fastest growth:**

```
1,  log n,  √n,  n,  n log n,  n²,  n³,  2^n,  n!,  n^n
```

**GATE traps.**

- `2^{n+1}` called “exponentially larger” than `2^n`. It is twice as large, hence Theta of `2^n`.
- `log(n²)` treated as a different class from `log n`. It equals `2 log n`, so it is Theta of `log n`.
- `(log n)²` confused with `log(n²)`. They are not the same. `(log n)²` grows faster than `log n` and slower than every `n^ε`.
- Writing `O(n²)` when the tight bound is `Θ(n)` . Big-O is not wrong (`n = O(n²)` is true) but a question that says “tightest” wants Theta.

---

## 4. Best, average, worst, and the word “asymptotic”

**Worst-case time** is `max` over inputs of size `n` of the cost of that input. **Best-case** is the minimum. **Average-case** is the expectation under a stated distribution, often uniform random permutations.

These are three functions of `n`. Each can wear an `O`, `Ω`, or `Θ`.

| Phrase | Means |
|--------|--------|
| Worst-case `O(n²)` | The worst input costs at most order `n²`. Other inputs may be cheaper |
| Worst-case `Θ(n²)` | The worst input costs on the order of `n²`, not less |
| Best-case `Θ(n)` | The cheapest input still costs linear time, and some input achieves it |
| Average-case `Θ(n log n)` | Under the stated distribution, the mean cost is that class |

**Why quicksort illustrates all three.** Best and average are `Θ(n log n)`. Worst is `Θ(n²)`. Saying “quicksort is `O(n²)`” is true and weak, because merge sort is also `O(n²)` (it is `O(n log n)`, which implies `O(n²)`). The tight worst-case statement is what distinguishes them.

**Space.** Auxiliary space is extra memory. Merge sort’s buffer is `Θ(n)` auxiliary. The input array is not counted again. Recursion depth counts: it occupies stack frames. In-place usually means `O(1)` or `O(log n)` auxiliary, and the question should be read for which convention it uses.

**Amortised cost** is a separate notion (section 8). It is an average over a sequence of operations on one structure, not an average over random inputs.

---

## 5. Reading loops

**Straight code.** A constant number of primitive statements is `Θ(1)`.

**One loop from 1 to `n`.** `Θ(n)`, if the body is `Θ(1)`.

**Nested loops, independent bounds.** `for i in 1..n` for `for j in 1..n` is `Θ(n²)`. Three deep is `Θ(n³)`.

**Dependent loops.**

```
for i = 1 to n:
    for j = 1 to i:
        Θ(1)
```

The body runs `1 + 2 + … + n = n(n+1)/2 = Θ(n²)`.

```
for i = 1 to n:
    j = 1
    while j < n:
        j = j * 2
```

The inner while runs `Θ(log n)` times for each `i`, so the total is `Θ(n log n)`.

**Halving a counter.**

```
i = n
while i > 1:
    i = i // 2
```

`Θ(log n)` iterations.

**Loop that adds a shrinking piece.**

```
i = 1
while i < n:
    i = i + i    # or i = i * 2
```

Also `Θ(log n)`.

**Multiple sequences.** If you do `Θ(n)` work and then `Θ(n²)` work, the sum is `Θ(n²)`.

**GATE trap.** A loop `for i = 1; i < n; i = i * 2` is logarithmic, not linear. Count iterations, not the final value of `i` alone — here they match only because `i` doubles. A loop `j = 1; while j < n: j = j + 2` is `Θ(n)`, not logarithmic.

---

## 6. Sums that appear inside analyses

| Sum | Closed form | Class |
|-----|-------------|-------|
| `Σ_{i=1}^{n} 1` | `n` | `Θ(n)` |
| `Σ_{i=1}^{n} i` | `n(n+1)/2` | `Θ(n²)` |
| `Σ_{i=1}^{n} i²` | `n(n+1)(2n+1)/6` | `Θ(n³)` |
| `Σ_{i=0}^{k} r^i`, `r ≠ 1` | `(r^{k+1} − 1)/(r − 1)` | `Θ(r^k)` if `r > 1`; `Θ(1)` if `0 < r < 1` and `k → ∞` |
| `Σ_{i=1}^{n} 1/i` | harmonic number `H_n` | `Θ(log n)` |
| `Σ_{i=1}^{log n} n` | `n log n` | `Θ(n log n)` |

**Geometric series are why recurrence trees often sum to the cost of the largest level.** If each level costs a constant fraction less than the level above, the first level dominates and the total is `Θ` of that level. If levels are equal, multiply by the number of levels.

---

## 7. Recurrences

A recurrence defines `T(n)` from smaller values, plus the non-recursive cost.

**Unrolling `T(n) = T(n − 1) + 1`, `T(1) = Θ(1)`.**  
`T(n) = Θ(1) + Θ(1) + …` with `n` terms → `Θ(n)`. One subtraction per call, `n` calls. This is linear search and a skewed recursion.

**`T(n) = T(n − 1) + n`.**  
`n + (n−1) + … + 1 = Θ(n²)`. This is the bad quicksort split and the cost of insertion sort’s worst case.

**`T(n) = T(n/2) + 1`.**  
`Θ(log n)` additions of 1. Binary search.

**`T(n) = T(n/2) + n`.**  
`n + n/2 + n/4 + … + 1 = Θ(n)`. The top call dominates. A one-sided scan that also recurses on half.

**`T(n) = 2T(n/2) + 1`.**  
The tree has `Θ(n)` constant-time leaves and `Θ(n)` internal cost if you sum a geometric series of nodes. Total `Θ(n)`.

**`T(n) = 2T(n/2) + n`.**  
Every level costs `n`, and there are `Θ(log n)` levels. Total `Θ(n log n)`. Merge sort.

**`T(n) = 2T(n/2) + n²`.**  
Level `i` (root is level 0) costs `n² / 2^i`. The series is geometric with ratio `1/2`, dominated by the root. Total `Θ(n²)`.

You can substitute `n = 2^k` to turn these into ordinary recurrences in `k`, solve, then substitute back. Floor and ceiling change only constant factors for these divide-by-two shapes; the Theta class is unchanged.

---

## 8. Master theorem

Use it on `T(n) = a T(n/b) + f(n)` with constants `a ≥ 1`, `b > 1`, and `f` positive. Compare `f(n)` with `n^{log_b a}`. That critical exponent is the leaf contribution: `a` subproblems, size ratio `b`, so `a^{log_b n} = n^{log_b a}` leaves of constant size.

Let `c_crit = log_b a`.

**Case 1.** `f(n) = O(n^{c_crit − ε})` for some `ε > 0`. The leaves dominate. `T(n) = Θ(n^{c_crit})`.

**Case 2.** `f(n) = Θ(n^{c_crit} log^k n)` for some `k ≥ 0`. Root work and leaves are in the same class up to a log factor. `T(n) = Θ(n^{c_crit} log^{k+1} n)`. The textbook case `k = 0` is `f(n) = Θ(n^{c_crit})` and `T(n) = Θ(n^{c_crit} log n)`.

**Case 3.** `f(n) = Ω(n^{c_crit + ε})` for some `ε > 0`, and the regularity condition `a f(n/b) ≤ c f(n)` for some `c < 1` and all large `n`. The root dominates. `T(n) = Θ(f(n))`.

**Why the cases differ.** In the recursion tree the level costs form a geometric series. Ratio `< 1` (leaves win, case 1), ratio `= 1` (all levels equal, case 2, an extra log), ratio `> 1` toward the root (case 3).

**Worked cases.**

| Recurrence | `c_crit` | `f` | Case | Solution |
|------------|----------|-----|------|----------|
| `T(n) = 2T(n/2) + n` | 1 | `Θ(n)` | 2, `k = 0` | `Θ(n log n)` |
| `T(n) = 2T(n/2) + 1` | 1 | `O(n^{1−ε})` | 1 | `Θ(n)` |
| `T(n) = 2T(n/2) + n²` | 1 | `Ω(n^{1+ε})` | 3 | `Θ(n²)` |
| `T(n) = T(n/2) + 1` | 0 | `Θ(1) = Θ(n^0)` | 2 | `Θ(log n)` |
| `T(n) = 8T(n/2) + n²` | 3 | `n² = O(n^{3−ε})` | 1 | `Θ(n³)` |
| `T(n) = 7T(n/2) + n²` | `log2 7 ≈ 2.807` | `n² = O(n^{2.807 − ε})` | 1 | `Θ(n^{log2 7})` |

Strassen’s matrix recurrence is the last row. The regularity check for case 3 on `f(n) = n²`, `a = 2`, `b = 2`: `a f(n/b) = 2 · (n/2)² = n²/2 ≤ c n²` with `c = 1/2 < 1`. Good.

**When you cannot apply it.**

- Uneven splits: `T(n) = T(n/3) + T(2n/3) + n`. Use a recursion tree. That one is still `Θ(n log n)`, because the depth is `Θ(log n)` along the longer branch and every level costs `Θ(n)`.
- `f` falls between cases, for example `f(n) = n / log n` against `n^{c_crit} = n`. The polynomial gap `ε` is missing, so case 1 does not apply, and case 2 does not apply either.
- Subtracting recurrences `T(n) = T(n − 1) + f(n)`. Unroll them.
- Non-constant `a` or `b`.

**GATE trap.** Case 2 quoted as `Θ(f(n))` instead of `Θ(f(n) log n)`. Merge sort is the standard casualty: people write `Θ(n)` because `f(n) = n`.

---

## 9. Substitution and the recursion tree

**Substitution.** Guess `T(n) ≤ c n log n`, prove it by induction. You may need a stronger guess (`c n log n − b n`) because the inductive step can fail on a loose guess even when the theorem is true. Base cases absorb small `n`.

**Recursion tree.** Draw one level of subproblem sizes, add the non-recursive costs, count the depth, sum. This is the right tool for uneven branches and the right explanation of the Master theorem.

**Change of variables.** `T(n) = 2 T(√n) + log n`. Set `n = 2^m`, `S(m) = T(2^m)`. Then `S(m) = 2 S(m/2) + Θ(m)`, so `S(m) = Θ(m log m)`, hence `T(n) = Θ(log n · log log n)`.

---

## 10. Amortised analysis

**What it is.** A sequence of `m` operations costs `T` in total. The amortised cost per operation is `T/m`. Some operations are expensive, but only rarely enough that the average over the sequence is small. This is not probability. The bound holds on every sequence, once you have proved the total.

**Aggregate method.** Bound the total directly.

*Dynamic array, doubling.* Inserting `n` elements copies 1, then 2, then 4, … elements at the resize points. Total copies `< 2n`. Amortised `O(1)` per insert. One insert can still take `Θ(n)` time in the worst case. Both statements are true.

*Binary counter.* Incrementing a `k`-bit counter from 0 through `n − 1`. Bit `i` flips every `2^i` increments. Total flips `< 2n`. Amortised `O(1)` per increment, even though one increment can flip all `k` bits.

**Accounting method.** Charge each operation a bit more than its typical cost. Store the surplus as credit on the object. An expensive operation spends saved credit. If credit never goes negative, the sum of charges pays for every real step.

**Potential method.** Define a potential `Φ ≥ 0` on the structure, usually `Φ(start) = 0`. Amortised cost of a step is `actual cost + Φ(after) − Φ(before)`. Telescoping: the sum of amortised costs equals the sum of actual costs plus `Φ(final) − Φ(start)`. If `Φ` stays non-negative and starts at 0, the sum of amortised costs upper-bounds the real total.

*Stack with multipop.* `Φ` = number of items. Push: actual 1, potential +1, amortised 2. Multipop of `k` items: actual `k`, potential −`k`, amortised 0. Both are `O(1)` amortised.

**GATE traps.**

- Replacing “amortised `O(1)`” by “worst-case `O(1)`”.
- Averaging over random inputs and calling it amortised. Average-case needs a distribution. Amortised needs a total over a sequence.
- Forgetting that the potential must stay non-negative for the upper bound, or handling a nonzero start potential.

---

## 11. Space complexity

Count the largest simultaneous auxiliary memory.

| Pattern | Auxiliary space | Why |
|---------|-----------------|-----|
| A few indices | `Θ(1)` | No array allocated |
| Merge buffer | `Θ(n)` | A second copy of the data |
| Recursion of depth `d` with `Θ(1)` locals | `Θ(d)` | Frames live until the call returns |
| Balanced quicksort stack | `Θ(log n)` | Depth of balanced recursion |
| Skewed quicksort stack | `Θ(n)` | Depth `n` |
| Hash table | `Θ(n + m)` | Slots plus keys |
| Adjacency matrix | `Θ(V²)` | This is input representation, not a temporary, if the graph is given that way |
| BFS queue | `O(V)` | The queue can hold a whole level |

**In-place** in GATE almost always means `Θ(1)` extra memory besides the input and the output, with recursion discussed separately when it matters.

**Time–space exchange.** You can recompute instead of storing a DP row, or store the row and save time. A question that gives both bounds is asking which resource is which. Do not quote time as space.

---

## 12. How to answer a complexity question

1. Name `n` (and `V`, `E`, `k`, `W` if they exist).
2. Decide best, average, or worst. If the question is silent, GATE usually wants worst-case Theta.
3. Write a recurrence or a sum. Do not jump to a class from the algorithm’s name if the input shape is given — a sorted array changes quicksort and insertion sort.
4. Solve it (Master, unroll, or tree).
5. Match the tight class. If two options are `O(n)` and `O(n log n)` and the truth is `Θ(n log n)`, both upper bounds can be formally true for a looser reading; pick the tight one when the question says “complexity of” and the options are the standard menu. If the question explicitly says “which upper bound is correct”, every valid upper bound is correct.
6. For space, say auxiliary, and include the stack if the algorithm is recursive.

---

## 13. Common GATE traps

1. `O` used as if it were `Θ`, or a loose `O` chosen when the question wants the tight bound.
2. Master case 2 missing the extra `log n`.
3. `2^{n+1}` placed in a different class from `2^n`.
4. `log(n!)` simplified to `log n` instead of `Θ(n log n)`.
5. Dependent loops counted as `n · n` when the inner bound is `i`, or counted as `n` when the inner loop doubles.
6. Amortised and worst-case swapped on dynamic arrays.
7. Best-case time of an algorithm quoted as its complexity with no adjective. Insertion sort’s “complexity” in a worst-case question is `Θ(n²)`.
8. Applying the Master theorem to `T(n/3) + T(2n/3)` blindly.
9. Bit-length versus numeric value.
10. Space of a recursive algorithm ignoring the stack.

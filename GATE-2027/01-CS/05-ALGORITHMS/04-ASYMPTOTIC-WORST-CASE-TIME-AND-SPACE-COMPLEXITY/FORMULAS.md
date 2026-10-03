# Asymptotic Complexity — Formulas

| Result | When it applies |
|--------|-----------------|
| `f = O(g)` | Exists `c > 0`, `n0` with `f(n) ≤ c g(n)` for all `n ≥ n0` |
| `f = Ω(g)` | Exists `c > 0`, `n0` with `f(n) ≥ c g(n)` for all `n ≥ n0` |
| `f = Θ(g)` | Both of the above; equivalently `c1 g ≤ f ≤ c2 g` eventually |
| `f = o(g)` | `f/g → 0` |
| `f = ω(g)` | `f/g → ∞` |
| Limit of `f/g` is a positive constant | `f = Θ(g)`, when the limit exists |
| `f + g = Θ(max(f, g))` | `f` and `g` eventually positive |
| `log_b n = Θ(log n)` | Fixed bases `b > 1`; not true for changing bases inside exponents |
| `2^{n+1} = Θ(2^n)` | Constant factor `2` |
| `4^n ≠ Θ(2^n)` | Ratio `2^n` unbounded |
| `Σ i = n(n+1)/2 = Θ(n²)` | Independent or triangular loop nests |
| `Σ i² = Θ(n³)` | Inner work proportional to `i²` |
| `H_n = Σ_{i=1}^{n} 1/i = Θ(log n)` | Harmonic sums |
| `Σ_{i=0}^{k} r^i = Θ(r^k)` for fixed `r > 1` | Geometric, growing |
| `log(n!) = Θ(n log n)` | Comparison-sort lower bound, Stirling |
| `T(n) = T(n−1) + 1 = Θ(n)` | One unit of work per size |
| `T(n) = T(n−1) + n = Θ(n²)` | Bad quicksort split, worst-case insertion |
| `T(n) = T(n/2) + 1 = Θ(log n)` | Binary search |
| `T(n) = T(n/2) + n = Θ(n)` | Root dominates a halving chain |
| `T(n) = 2T(n/2) + n = Θ(n log n)` | Master case 2 |
| `T(n) = 2T(n/2) + n² = Θ(n²)` | Master case 3 |
| `T(n) = 2T(n/2) + 1 = Θ(n)` | Master case 1 |
| Master case 1 | `f = O(n^{log_b a − ε})` → `Θ(n^{log_b a})` |
| Master case 2 | `f = Θ(n^{log_b a} log^k n)` → `Θ(n^{log_b a} log^{k+1} n)` |
| Master case 3 | `f = Ω(n^{log_b a + ε})` and `a f(n/b) ≤ c f(n)`, `c < 1` → `Θ(f)` |
| Doubling array, `n` inserts | Total copy cost `< 2n`; amortised `Θ(1)`; one insert can be `Θ(n)` |
| Binary counter, `n` increments | Total bit flips `< 2n`; amortised `Θ(1)` |
| Recursion space | `Θ(depth)` frames if each frame is `Θ(1)` extra |

# Hashing — Formulas

| Result | When it applies |
|--------|-----------------|
| Load factor `α = n / m` | `n` stored keys, `m` slots |
| Chaining, unsuccessful search `Θ(1 + α)` | Simple uniform hashing; scan a full list |
| Chaining, successful search `Θ(1 + α/2)` element exams | Insert-at-head analysis under simple uniform hashing |
| Chaining worst case `Θ(n)` | All keys in one slot |
| Open addressing, unsuccessful probes `1 / (1 − α)` | Uniform probing (double hashing idealisation), `α < 1` |
| Open addressing, successful probes `(1/α) ln(1/(1 − α))` | Same model; natural log |
| Linear probing | Same first hash plus `i`; primary clustering; do not quote the two probe formulas unless the question assumes uniform probing |
| Quadratic probe `(h(k) + c1 i + c2 i²) mod m` | Secondary clustering; sequence may miss slots |
| Double hash `(h1(k) + i h2(k)) mod m` | `h2(k)` coprime to `m` so the sequence is a full permutation |
| Universal pair collision `P ≤ 1/m` | `h` drawn from a universal family; `x ≠ y` fixed |
| Expected colliding pairs `n(n − 1) / (2m)` | Independent uniform slot choices |
| Birthday scale `n ≈ √(2 m ln 2)` | `n` where some collision becomes likely |
| Direct address space `Θ(|U|)` | Keys are table indexes; no collisions |
| Rehash, doubling, expected amortised insert `O(1)` | Geometric table growth, constant load between rebuilds |

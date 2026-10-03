# Hashing — Mistakes

### Common GATE Traps

| Trap | What goes wrong | Correct rule | Prevention |
|------|-----------------|--------------|------------|
| Worst case `O(1)` | Pigeonhole ignored | With a fixed `h` and `|U| > m`, all keys can share one slot; search is `Θ(n)` | Say “expected” only under a stated hashing model |
| Wrong collision formula | `1/(1−α)` used for chaining | Chaining is `Θ(1+α)` unsuccessful; `1/(1−α)` is uniform open addressing | Name the scheme before the formula |
| Inverted load | `α = m/n` | `α = n/m` | `α` grows when you insert |
| Load 1 means no collisions | `n = m` read as a perfect placement | Empty slots and long chains can coexist | Remember the birthday scale `√m` |
| Blank-slot delete | Search stops early | Open addressing needs a tombstone | Ask what a probe does at a deleted cell |
| Quadratic covers the table | Insert fails with empty slots left | Some `c1, c2, m` repeat slots | Prefer double hashing when a full permutation is required |
| Rehash by copying indexes | New `m` changes `h` | Reinsert every key | If `m` changes, recompute `h` |
| Linear probing = uniform probing | Ideal probe count too optimistic | Linear probing has primary clustering | Use `1/(1−α)` for double hashing or an explicit uniform model |
| Hash for ranges | Successor or range done with `h` | Hash tables do not keep key order | Switch to a tree or a sorted array |
| Successful vs unsuccessful | Half-chain formula used on a miss | A miss scans the whole chain: `Θ(1+α)` | Check whether the key is present |

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|-----------|--------------|------------|
| | | | | | | |

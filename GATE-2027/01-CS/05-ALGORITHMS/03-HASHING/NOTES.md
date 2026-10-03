# Hashing — Learning Notes

Hashing answers equality queries: “does this key occur, and what record is attached to it?” It does not answer range queries or predecessor queries. Those need sorted order or a search tree. The syllabus line is hashing as an algorithm, so this file treats hash functions, collisions, load, and the cost of search, insert, and delete.

---

## 1. The idea

**What it is.** A hash function `h` maps a key to a slot in a table of `m` slots. The hope is that the key you want sits in that slot, so a search ignores the rest of the table.

**Intuition.** A dictionary’s thumb index sends you to one page. If two words share a page, you scan only that page, not the whole book.

**Formal definition.** Universe `U`, table size `m`, function `h: U → {0, 1, …, m − 1}`. Store `n` keys. The **load factor** is `α = n / m`.

**Why it is not worst-case constant time.** There are more possible keys than slots whenever `|U| > m`. By the pigeonhole principle some two keys share a slot. An adversary who knows `h` can send every key to one slot. Worst-case search is then `Θ(n)`, the same as a list. The useful bounds are *expected* bounds under a randomness assumption on `h` or on the keys.

**When to use.** Equality tests, symbol tables, counting frequencies, deduplication, and joins on a key — when average or expected time matters and you control the hash function or can assume simple uniform hashing.

**When not to use.** Ordered traversal, successor, range reporting, or a hard worst-case bound with a hash function the adversary knows. A balanced search tree gives `O(log n)` worst case for order-based queries. Sorting gives order as well.

---

## 2. What a good hash function does

**Deterministic.** The same key always lands in the same slot during one execution. Otherwise you cannot find what you inserted.

**Fast.** Computing `h(k)` should be `O(1)` for machine-word keys, or linear in the key length for strings.

**Uniform.** For a key taken from the usage distribution, `P(h(k) = i) ≈ 1/m` for every slot `i`. **Simple uniform hashing** strengthens this: each key is equally likely to land in any slot, independent of the other keys. Expected-time theorems in this file assume that, unless a line says otherwise.

**Division method.** `h(k) = k mod m`. Choose `m` prime, and avoid sizes that share a hidden factor with the keys (powers of 10 if keys are decimal-patterned, powers of 2 if the low bits of `k` are biased).

**Multiplication method.** `h(k) = floor(m · {k A})` where `{·}` is the fractional part and `A` is a constant in `(0, 1)`, often an irrational related to the golden ratio. The table size `m` may be a power of two, which makes the implementation cheap. You still need `A` to spread the keys.

**Folding and mid-square.** Split a long key into chunks, add them, then reduce mod `m`. Or square the key and take middle digits. These are heuristics. Use them only if the question names them; the complexity results below do not depend on which uniform function you picked.

**Strings.** A polynomial hash `s[0] a^{L−1} + s[1] a^{L−2} + … + s[L−1]`, reduced mod `m`, with a small prime base `a`. A bad base or a tiny `m` produces many collisions on similar strings.

**GATE trap.** A hash function that is “random looking” on the board can still map an entire given set to one slot. Always separate the worst case from the expected case.

---

## 3. Collision handling: chaining

**What it is.** Each slot holds a list of all keys that hash there. Insert at the head (or tail) of that list. Search scans the list. Delete unlinks one node.

**Why it works.** Every key with `h(k) = i` is on list `i` and nowhere else. A search that walks list `h(k)` cannot miss the key, and it never needs to look at other lists.

**Example.** `m = 5`, `h(k) = k mod 5`, insert `12, 7, 2, 17`.

- `12 → 2`, `7 → 2`, `2 → 2`, `17 → 2`.
- Slot 2’s list is `17, 2, 7, 12` if you insert at the head in that order. The other slots are empty.
- Search `7`: go to slot 2 and scan three nodes if `17` and `2` sit in front.

**Why the expected cost is `Θ(1 + α)`.** Under simple uniform hashing the `n` keys fall into `m` lists like random bins. The average list length is exactly `α = n/m`, because the lengths sum to `n`.

- **Unsuccessful search.** You hash once and scan a whole list. The expected list length is `α`, so expected time is `Θ(1 + α)`.
- **Successful search.** You stop at the key. If insertion was at the head, a key looks at the keys that arrived later in the same slot, plus itself. The standard analysis gives expected time `Θ(1 + α/2)`, about half a list, plus the hash computation.

Both stay `Θ(1)` when `α` is held constant, for example `α ≤ 1` by growing the table. If you never grow the table and `n ≫ m`, the bound degrades toward linear: `α = n/m` becomes `Θ(n)` when `m` is fixed.

| Operation | Expected time | Worst time | Why worst |
|-----------|---------------|------------|-----------|
| Search, unsuccessful | `Θ(1 + α)` | `Θ(n)` | Every key on one list |
| Search, successful | `Θ(1 + α)` (more tightly `Θ(1 + α/2)` element inspections) | `Θ(n)` | Key at the end of a long list |
| Insert at head | `Θ(1)` expected and worst, after computing `h` | `Θ(1)` | No scan if duplicates are allowed or checked elsewhere |
| Delete | same as successful search | `Θ(n)` | Must find the node |

**Space.** `Θ(n + m)` for the slots plus the nodes. Load `α` small means more empty slots.

**Properties.** Chaining tolerates `α > 1`. Deletion is ordinary list deletion. The chains can be sorted to speed unsuccessful search to the key’s place, at extra insert cost. Cache behaviour is weaker than open addressing because list nodes may be scattered.

**When to use.** Load may exceed 1, deletions are common, or keys are large records you would rather not shuffle inside an array.

**Comparison with open addressing.** Chaining uses extra pointers and allows `α > 1`. Open addressing stores keys in the table itself, needs `α < 1`, and suffers clustering. Expected probe counts have different formulas (next section).

**GATE traps.**

- Using the successful-search formula for a miss.
- Forgetting that `α = n/m` must stay bounded to keep the expectation constant.
- Calling the worst case `O(1)`.

---

## 4. Collision handling: open addressing

**What it is.** Every key lives in the table array. If slot `h(k)` is taken, a **probe sequence**

```
h(k, 0), h(k, 1), …, h(k, m − 1)
```

lists the slots to try. The sequence should be a permutation of all slots, so a key can always be inserted when `n < m`.

**Linear probing.** `h(k, i) = (h(k) + i) mod m`. You try the next slot, then the next.

**Why clusters form.** A occupied block of length `L` absorbs any key whose first hash lands inside it, and the block grows. Two neighbouring blocks merge. This is **primary clustering**. Long runs are more likely to get longer. Linear probing’s expected cost is higher than the ideal open-addressing formulas once `α` is not tiny. The ideal formulas in the next subsection assume **uniform probing**: each probe sequence is equally likely among all permutations. Double hashing approximates that. Linear probing does not.

**Quadratic probing.** `h(k, i) = (h(k) + c1 i + c2 i²) mod m`. Primary clustering goes away. **Secondary clustering** remains: two keys with the same first hash follow the same entire probe sequence. For some `c1, c2, m` the sequence does not visit every slot, so an insert can fail even though empty slots exist. A common safe case is `m` prime and carefully chosen constants, or `m` a power of two with a known good polynomial. Do not assume full coverage unless the question states it.

**Double hashing.** `h(k, i) = (h1(k) + i · h2(k)) mod m`. Choose `h2(k)` coprime to `m` (if `m` is prime, any `h2` in `1..m−1` works). Different keys with the same `h1` still split because `h2` differs. Probe sequences are closer to uniform. This is the usual open-addressing scheme when a question wants the ideal formulas.

**Example (linear probing).** `m = 7`, `h(k) = k mod 7`, insert `8, 15, 2`.

- `8 mod 7 = 1`. Slot 1 stores 8.
- `15 mod 7 = 1`, taken. Probe `2`. Slot 2 stores 15.
- `2 mod 7 = 2`, taken. Probe `3`. Slot 3 stores 2.

Search `2`: inspect slots 2 and 3. Two probes.

**Ideal expected probes** (uniform probing, `α < 1`):

| Search | Expected probes |
|--------|-----------------|
| Unsuccessful | `1 / (1 − α)` |
| Successful | `(1 / α) ln(1 / (1 − α))` |

The successful-search expression is the average, over the loads at insertion time, of a geometric number of probes. As `α → 1`, both quantities grow without bound: the last few empty slots are hard to find. At `α = 0.5`, unsuccessful search expects `1 / 0.5 = 2` probes. Successful search expects `(1/0.5) ln 2 ≈ 1.386` probes.

**Worst case.** `Θ(n)` probes if the sequence walks through `n` occupied slots, and `Θ(m)` if you scan a nearly full table.

**Space.** `Θ(m)` for the table. Keys sit in the slots, so `α` cannot exceed 1. Practical tables resize at `α` around `0.5` to `0.7`.

| Scheme | Extra problem | Full permutation of slots? |
|--------|---------------|----------------------------|
| Linear | Primary clustering | Yes |
| Quadratic | Secondary clustering | Not always |
| Double hashing | Needs a good `h2` | Yes if `h2` is coprime to `m` |

**When to use.** You want one array, keys are small, and deletions are rare.

**When not to use.** `n` may exceed `m` with no resize. Frequent deletion (next subsection). Worst-case guarantees.

**GATE traps.**

- Applying `1/(1−α)` to chaining. That formula is for open addressing under uniform probing.
- Applying it to linear probing as if clustering did not exist. Quote it for double hashing or when the question says “uniform probing”.
- Quadratic probing assumed to try every slot.
- Load factor `≥ 1` in an open-addressed table that has not been resized: insertion is impossible once `n = m`.

---

## 5. Deletion

**Chaining.** Unlink the node. Later searches are correct. Expected times still follow `α` computed with the new `n`.

**Open addressing.** Clearing a slot to “empty” breaks probe sequences. A later key that probed past that slot becomes invisible, because search stops at the first empty slot.

The fix is a third state, **deleted** (a tombstone). Search skips tombstones. Insert may reuse a tombstone. If tombstones are never removed, a search can walk a long deleted run, and the `1/(1−α)` analysis no longer describes the table. Rehashing rebuilds a clean table.

**GATE trap.** “Delete by writing NULL” in a linear-probing table, with no tombstone. A question that then searches a key inserted after the deleted one should be answered “not found” under that wrong procedure, or “found” if tombstones are used. Read which rule the question adopted.

---

## 6. Growing the table

**What it is.** When `α` crosses a threshold, allocate a larger table (often `2m`) and insert every key again. This is **rehashing**. You cannot copy slots blindly: the hash function depends on `m`, so `k mod m` and `k mod 2m` differ.

**Why the expected cost amortises.** A geometric growth means the expensive rebuilds happen at sizes `m, 2m, 4m, …`. The total expected rebuild cost up to size `n` is `n + n/2 + n/4 + … = O(n)`, the same charging argument as a doubling array. Each insert pays expected `O(1)` amortised, provided each rebuild inserts into a table with constant load.

**Worst case of one insert.** `Θ(n)` when it triggers a rehash, or when it walks a long probe sequence.

**GATE observation.** Amortised `O(1)` is not worst-case `O(1)`. Say which one you mean.

---

## 7. Collisions as a counting problem

**Birthday paradox.** With `m` slots and random hashes, the probability of some collision becomes constant near `n ≈ √(2 m ln 2)`, about `1.177 √m`. For `m = 365`, that is near 23 keys. This is why a “large” table can still collide early.

**Expected number of colliding pairs.** Under uniform independent hashes, each pair collides with probability `1/m`. There are `n(n−1)/2` pairs, so the expected number of colliding pairs is `n(n−1)/(2m)`.

**Longest chain.** Even with a good hash, the longest chain in chaining is `Θ(log n / log log n)` with high probability when `α = Θ(1)`, not `O(1)`. Expected *average* chain length is constant; the maximum is larger. Worst-case time of one search is the longest chain, not `α`.

**GATE trap.** “`α = 1` means no collisions.” Load 1 means `n = m`, not that every slot has exactly one key. Some slots can be empty while others hold several keys.

---

## 8. Universal hashing

**What it is.** A family `H` of functions is universal if for every two distinct keys `x, y`,

```
P_{h ∈ H}(h(x) = h(y)) ≤ 1/m
```

when `h` is drawn from `H`. A standard construction for integer keys and prime `m` is `h_{a,b}(k) = ((a k + b) mod p) mod m` with `p` prime, `p > m`, `a ≠ 0`.

**Why it helps.** The adversary can pick the keys, but not the random choice of `h` from `H`. No fixed pair is likely to collide. Chaining then has expected list length `O(1 + α)` for any set of `n` keys. This removes the assumption that the keys themselves are random.

**What it does not do.** A single unlucky draw of `h` can still collide. The guarantee is expectation or high probability over the choice of `h`, not a deterministic worst-case `O(1)`.

**Perfect hashing.** When the key set is static, a two-level scheme hashes to buckets and then picks, for each bucket, a collision-free secondary table. Expected construction time is linear in `n`, and searches are `O(1)` worst case after construction. This needs a static set: inserts would force a rebuild of a level.

**GATE observation.** If the question says “universal”, the probability `≤ 1/m` is the fact to use. If it says nothing, simple uniform hashing is the usual model behind `Θ(1 + α)`.

---

## 9. Choosing among structures

| Need | Structure | Expected search | Worst search |
|------|-----------|-----------------|--------------|
| Equality, dynamic, chaining, `α = Θ(1)` | Hash table | `Θ(1)` | `Θ(n)` |
| Equality, static set, perfect hashing | Two-level hash | `Θ(1)` | `Θ(1)` after build |
| Equality plus order, successor, range | Balanced BST | `Θ(log n)` | `Θ(log n)` |
| Sorted array, rare updates | Binary search | `Θ(log n)` | `Θ(log n)` |
| Integer keys in a small range | Direct address table | `Θ(1)` | `Θ(1)` |

**Direct addressing.** If keys are exactly the integers `0..m−1` and `m` is acceptable memory, the table *is* the hash, with `h(k) = k` and no collisions. Space `Θ(m)`, which is wasteful when the used set is much smaller than the universe. Hashing compresses a large universe into `m` slots and accepts collisions.

---

## 10. Worked load calculations

**Chaining, `n = 100`, `m = 50`.** `α = 2`. Unsuccessful search expects on the order of `1 + 2` list steps. Successful search expects on the order of `1 + 1`. Worst case is still 100 if one list holds everything.

**Open addressing, uniform probing, `α = 0.75`.** Unsuccessful: `1 / 0.25 = 4` expected probes. Successful: `(1/0.75) ln(1/0.25) = (4/3) ln 4 ≈ (4/3)(1.386) ≈ 1.85` probes.

**Open addressing at `α = 0.9`.** Unsuccessful expects `10` probes. Tables are resized before this region when constant factors matter.

---

## 11. Common GATE traps

1. Worst-case hash search stated as `O(1)`.
2. Chaining formula `1/(1−α)` (that is open addressing).
3. Load factor `n/m` replaced by `m/n`.
4. `α = 1` read as “zero collisions”.
5. Deleting from open addressing by emptying the slot.
6. Division method with `m` a power of two when the question points out biased low bits.
7. Quadratic probing claimed to probe all slots for every `m`.
8. Rehash copy that keeps old indexes after `m` changes.
9. Birthday paradox replaced by “collisions start at `m` keys”.
10. Using hashing for a range-count question that needs order.

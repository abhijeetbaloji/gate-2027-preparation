# Hashing — Practice

These are practice questions, not GATE questions.

### Level 1 — Concept

**1.** Define the load factor. Why do expected hash-table bounds mention it?

**2.** Why is the worst-case search time of a fixed hash function `Θ(n)` in the worst key set?

**3.** What does simple uniform hashing assume?

**4.** Why does an unsuccessful chained search take longer, in expectation, than a successful one?

**5.** Name primary clustering and the probe scheme that causes it.

### Level 2 — Standard

**6.** Chaining, `n = 200`, `m = 100`. Expected unsuccessful-search cost in `Θ` notation, and the tighter successful-search element count `Θ(1 + α/2)`.

**7.** Uniform open addressing, `α = 0.8`. Expected probes for an unsuccessful search?

**8.** `m = 11`, `h(k) = k mod 11`, linear probing. Insert `22, 12, 13`. Where does `13` land?

**9.** Why must `h2(k)` be coprime to `m` in double hashing?

**10.** A direct-address table stores keys that are integers in `0..999`. Search time and space?

### Level 3 — Multi-step

**11.** `m = 5`, `h(k) = k mod 5`, linear probing. Insert `6`, then `11`. Delete `6` by storing empty. Does a search for `11` succeed? What changes if that slot is a tombstone instead?

**12.** `α = 0.5`, uniform probing. Compute unsuccessful and successful expected probes. Use `ln 2 ≈ 0.693`.

**13.** Universal family, `m = 100`. Upper-bound the probability that two particular keys collide. If you insert `n = 100` keys with chaining, what expected chain-length order does universality give for any fixed set?

**14.** You double the table whenever `α` exceeds 1, and each rebuild reinserts every live key. Why is the expected amortised cost per insert `O(1)` if each insertion into a half-full table is expected `O(1)`?

**15.** Birthday scale: `m = 10^4`. Around how many random keys make some collision likely?

### Level 4 — Trap-based

**16.** A solution says chaining with `α = 0.9` has unsuccessful expected probes `1/0.1 = 10`. What is the right expression?

**17.** “`n = m`, so chaining has no collisions.” Give a two-key counterexample with `m = 2`.

**18.** Quadratic probing is said to examine every slot before it reports the table full. Why is that not always true?

**19.** After rehashing from `m = 5` to `m = 11`, a student copies a key from old slot `k mod 5` into the same index. Why can search fail?

**20.** The question asks for the number of keys lying between 100 and 200 inclusive. Why is a hash table the wrong structure?

### Level 5 — Challenge

**21.** Under independent uniform slots, derive the expected number of colliding pairs: pairs `i < j` with `h(i) = h(j)`.

**22.** Explain why search in open addressing must stop at an empty slot, and why a tombstone cannot be treated as empty.

**23.** Show that for `α < 1` the unsuccessful uniform-probe expectation `1/(1−α)` is at least the chaining unsuccessful cost `1 + α`, or compare them numerically at `α = 0.5` and say which model scans more.

**24.** Perfect hashing is worst-case `O(1)` search. Why does that not contradict the pigeonhole argument in section 1 of the notes?

**25.** Insert-at-head chaining. In one sentence, why a successful search looks at about half a chain rather than a full chain.

---

## Answers and explanations

**1.** `α = n/m`. Expected chain length and expected probe counts are functions of how full the table is. Constant `α` is what makes those expectations constant.

**2.** If `|U| > m`, some slot is the image of many keys. An adversary puts all `n` stored keys on one slot. Finding one of them, or confirming a miss on that slot, scans `Θ(n)` records.

**3.** Each key is equally likely to hash to any of the `m` slots, independently of the other keys.

**4.** A miss walks the entire chain, expected length `α`. A hit stops at its own key. With insert-at-head, that is about half the keys that share the slot, expected `Θ(1 + α/2)` inspections.

**5.** Primary clustering: a occupied run grows because any first hash that lands inside it extends it. Linear probing does this.

**6.** `α = 2`. Unsuccessful `Θ(1 + 2) = Θ(1)`. More precisely `Θ(1 + α) = Θ(1)` since 2 is constant; you may also write `Θ(α) = Θ(1)`. Element inspections on success: `Θ(1 + 2/2) = Θ(1)`, i.e. `Θ(1 + α/2)`.

**7.** `1 / (1 − 0.8) = 5`.

**8.** `22 mod 11 = 0`, slot 0. `12 mod 11 = 1`, slot 1. `13 mod 11 = 2`, slot 2 is free, so `13` lands in slot 2. No collision in this particular insert.

**9.** Otherwise the step `h2` shares a factor with `m` and the probe cycle is shorter than `m`. Some empty slots are never visited.

**10.** Worst-case `Θ(1)` search. Space `Θ(1000)`.

**11.** `h(6) = 1`, `h(11) = 1`. Insert 6 in slot 1. Insert 11: slot 1 is full, so slot 2. Delete 6 by emptying slot 1. Search 11 starts at slot 1, sees empty, and stops. Miss. A tombstone in slot 1 is skipped, and slot 2 still holds 11. Hit.

**12.** Unsuccessful: `1 / 0.5 = 2`. Successful: `(1/0.5) ln 2 = 2 · 0.693 = 1.386`.

**13.** At most `1/100`. Universality gives expected chain length `O(1 + α) = O(1)` for any fixed set of 100 keys when `m = 100`, because each other key collides with a given key with probability `≤ 1/m`.

**14.** Rebuild costs occur at sizes proportional to `1, 2, 4, …, n`. If each costs expected linear in the current size, the sum is expected `O(n)`. Divided by `n` inserts, expected amortised `O(1)` each.

**15.** `√(2 · 10^4 · ln 2) ≈ √(1.386 · 10^4) ≈ √13860 ≈ 118`. Order `√m = 100`.

**16.** Chaining unsuccessful search is `Θ(1 + α) = Θ(1.9)`, not `1/(1−α)`. The factor 10 is the open-addressing miss cost.

**17.** `m = 2`, keys `2` and `4`, `h(k) = k mod 2`. Both map to 0. `n = m = 2` and slot 0 has a collision while slot 1 is empty.

**18.** The map `i ↦ (h + c1 i + c2 i²) mod m` can repeat before `i` runs through `0..m−1`. Coverage depends on `c1`, `c2`, and `m`.

**19.** The new function is `k mod 11`, which need not equal `k mod 5`. Search will look in the new slot and miss a key left at the old index.

**20.** Slot order is not key order. Answering a range requires looking at keys by value. Use a sorted array or a balanced search tree.

**21.** Indicator `X_{ij} = 1` if pair `(i, j)` collides. `E[X_{ij}] = 1/m`. Linearity: expected number is `C(n, 2) / m = n(n−1)/(2m)`.

**22.** The insert probe stops at the first hole and stores the key there, so every earlier slot on that sequence is occupied. Search must follow the same prefix. If it treated a tombstone as a hole, it would stop before keys that were inserted further along while the deleted key still occupied that slot.

**23.** At `α = 0.5`, open addressing expects 2 probes on a miss; chaining expects `1 + 0.5 = 1.5` list steps. Open addressing does more work at this load under the ideal model. (They are different operations — probes versus chain nodes — but the usual comparison is that chaining’s miss cost stays linear in `α` while uniform probing’s miss cost blows up as `α → 1`.)

**24.** The pigeonhole argument says a single fixed `h: U → {0..m−1}` cannot be injective on all of `U`. Perfect hashing uses a first hash into buckets and a second hash *per bucket*, chosen after seeing the static key set, with secondary tables large enough that the keys actually stored in that bucket do not collide. It does not inject the whole universe into one small table.

**25.** Keys that sit in front of you are those inserted later into the same slot, about half the chain in the uniform insert-at-head analysis, not the keys inserted earlier, which sit behind you.

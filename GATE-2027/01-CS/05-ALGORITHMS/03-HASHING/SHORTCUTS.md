# Hashing — Shortcuts

### Constant expected time needs a bounded load

**Shortcut.** Keep `α = n/m` at most a constant. Then chaining search is expected `Θ(1)`.

**Why it works.** Expected chain length equals `α`. A constant `α` is a constant scan.

**When to use.** “Expected time of search in a hash table with chaining.”

**Example.** `n = 2m` gives `α = 2`, still constant. `m` fixed and `n → ∞` does not.

**Limitation.** The worst case is `Θ(n)` even at `α = 1`. Expectation is not a guarantee against a bad set.

---

### `1/(1−α)` belongs to open addressing

**Shortcut.** Unsuccessful search under uniform probing expects `1/(1−α)` probes. Chaining expects `Θ(1+α)`.

**Why it works.** Open addressing stops at the first empty slot; the probability a probe is occupied behaves like `α, α, …` in the uniform model, and the expectation sums to `1/(1−α)`. Chaining jumps to one list whose mean length is `α`.

**When to use.** The question says open addressing, double hashing, or uniform probing, and `α < 1`.

**Example.** `α = 1/2` → 2 expected probes on a miss.

**Limitation.** Linear probing clusters, so the ideal formula understates its cost. The formula explodes as `α → 1` and is undefined for `α ≥ 1`.

---

### Tombstones, not blank cells

**Shortcut.** In open addressing, mark a deleted slot as deleted. Do not make it empty.

**Why it works.** Search treats empty as “stop”. A key placed further along the probe sequence would be cut off.

**When to use.** Any delete followed by a search in linear probing, quadratic probing, or double hashing.

**Example.** Insert `a`, then `b` which probed past `a`, then delete `a`. Search `b` must skip `a`’s tombstone.

**Limitation.** A table full of tombstones makes search slow. Rehash to clear them.

---

### Collisions start near `√m`, not near `m`

**Shortcut.** A random hashing of about `√(2 m ln 2)` keys already has a good chance that some two keys share a slot.

**Why it works.** There are `Θ(n²)` pairs and each collides with probability `1/m`. The expected number of colliding pairs hits a constant when `n²/m` does, so `n` is on the order of `√m`.

**When to use.** “How can a table of size 365 collide with 23 keys?”

**Example.** `m = 365`, `n = 23`.

**Limitation.** This is a probability of *some* collision, not a claim that search is already linear. Average chain length at `n = √m` is still `1/√m`, which is small.

---

### Order queries are the wrong job

**Shortcut.** If the question asks for successor, predecessor, or a range, do not reach for a hash table.

**Why it works.** A hash destroys order. Slots are not sorted by key.

**When to use.** Choosing a structure from a one-line requirement.

**Example.** “All keys between 20 and 40” → sorted array or a balanced tree, not a hash.

**Limitation.** If you hash *and* keep a separate sorted index, you have built the other structure anyway. Equality-only frequency counts are a hashing job.

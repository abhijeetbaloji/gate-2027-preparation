# Hashing — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A table of \(m\) slots stores \(n\) keys. The load factor is

A. \(\alpha = m/n\)

B. \(\alpha = n/m\)

C. \(\alpha = n + m\)

D. \(\alpha = 1\) whenever a collision has occurred

---

## Q2 — MSQ

Select all that apply. Collisions are handled by chaining. The hash is simple and uniform, and a search that misses scans the whole chain of the home slot.

A. An unsuccessful search takes expected time \(\Theta(1 + \alpha)\).

B. The worst-case search time is \(\Theta(1)\) for a fixed hash function.

C. If \(\alpha\) is held at a constant, the expected search time is \(\Theta(1)\).

D. Chaining is legal when \(n > m\).

---

## Q3 — NAT

Keys are stored by chaining in a table of \(m = 7\) slots. The hash is \(h(k) = k \bmod 7\). Each insertion is at the head of the chain. The keys arrive in the order \(10, 17, 3, 24, 8\). A successful search of 10 walks the chain from the head and stops at 10. How many keys does it inspect?

---

## Q4 — NAT

Under simple uniform hashing, \(n\) keys are placed independently into \(m\) slots. The expected number of unordered pairs that land in the same slot is \(n(n-1)/(2m)\). For \(n = 8\) and \(m = 4\), that expectation equals

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Open addressing uses linear probing. The table has \(m = 11\) slots, the hash is \(h(k) = k \bmod 11\), and the probe sequence is

\[
(h(k) + i) \bmod 11, \qquad i = 0, 1, 2, \ldots
\]

The table starts empty. Insert \(18, 29, 7, 40, 51\) in that order. A later successful search of 40 follows the same probe sequence and stops when 40 is found. How many slots does that search inspect?

---

## Q6 — MSQ

Select all that apply. The collision policy is named in each statement.

A. Linear probing, with sequence \((h(k) + i) \bmod m\), suffers from primary clustering: a filled block absorbs new keys whose home slot lies inside the block.

B. The ideal unsuccessful-search formula \(1/(1-\alpha)\) assumes uniform probing, which double hashing approximates and linear probing does not.

C. Quadratic probing, with sequence \((h(k) + c_1 i + c_2 i^2) \bmod m\), always visits every slot for every choice of \(c_1\), \(c_2\), and \(m\).

D. Double hashing uses \((h_1(k) + i \cdot h_2(k)) \bmod m\). If \(m\) is prime and \(h_2(k) \in \{1, \ldots, m-1\}\), the probe sequence is a permutation of all slots.

---

## Q7 — NAT

Double hashing uses a table of \(m = 13\) slots and the probe sequence

\[
h(k, i) = \bigl(h_1(k) + i \cdot h_2(k)\bigr) \bmod 13,
\]

where \(h_1(k) = k \bmod 13\) and \(h_2(k) = 1 + (k \bmod 12)\). The table starts empty. Insert \(15, 28, 41, 19, 6\) in that order. In which slot does 6 land?

---

## Q8 — MCQ

Open addressing is analysed under uniform probing, with load \(\alpha < 1\). The expected number of probes in an unsuccessful search is

A. \(\Theta(1 + \alpha)\), the chaining bound

B. \(1/(1-\alpha)\)

C. \((1/\alpha) \ln(1/(1-\alpha))\), which is the successful-search formula, used here for a miss

D. \(\Theta(1)\) even when \(\alpha\) tends to 1

---

## Q9 — NAT

The same uniform-probing model is used at load \(\alpha = 1/2\). The expected number of probes in an unsuccessful search is the integer

---

## Level 3 — Multi-Step

## Q10 — MCQ

Linear probing stores keys in the table itself. A key is removed by writing the empty marker into its slot, and search stops at the first empty slot. No tombstone is used. Which statement is correct?

A. Later keys that originally probed past that slot remain findable, because the hash still computes the same home slot.

B. A later key that probed past the deleted slot can be reported missing, because search stops at the new empty cell.

C. Deletion is impossible in every hash table, including chaining.

D. The empty marker is safe precisely when the deleted key was the last key inserted into the table.

---

## Q11 — MSQ

Select all that apply.

A. A family \(H\) is universal when, for every two distinct keys, a function drawn from \(H\) collides on them with probability at most \(1/m\).

B. Universal hashing makes every search \(\Theta(1)\) in the worst case for the unlucky draw of \(h\) as well as in expectation.

C. With chaining and a universal family, the expected chain length is \(O(1+\alpha)\) for every fixed set of \(n\) keys.

D. Hash tables answer successor and range queries in expected \(\Theta(1)\) time, because equality and order use the same structure.

---

## Q12 — NAT

After the chaining insertions of Q3, what is the length of the longest chain?

---

## Q13 — MCQ

A hash table is doubled from \(m\) slots to \(2m\) slots when the load crosses a threshold. The hash is \(h(k) = k \bmod m\). The correct rebuild is

A. copy slot \(i\) of the old table into slot \(i\) of the new table

B. reinsert every key, recomputing \(k \bmod 2m\)

C. copy each chain in order but keep the old slot indexes

D. leave the keys where they are, because doubling does not change a modular hash

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Which use of a collision formula is correct?

A. Chaining, unsuccessful search, simple uniform hashing: expected cost \(\Theta(1+\alpha)\).

B. Chaining, unsuccessful search: expected cost \(1/(1-\alpha)\), including when \(\alpha > 1\).

C. Linear probing: quote \(1/(1-\alpha)\) as if primary clustering were absent, without a uniform-probing hypothesis.

D. Open addressing with \(\alpha = 1\): unsuccessful search expects 1 probe.

---

## Q15 — MSQ

Select all that apply.

A. Load \(\alpha = 1\) means the \(n = m\) keys occupy \(m\) distinct slots, so there is no collision.

B. Some quadratic-probe sequences repeat a slot while other slots are still empty, so an insertion can fail early.

C. Under simple uniform hashing, collisions become likely near \(n \approx \sqrt{2 m \ln 2}\), which is much smaller than \(m\).

D. Open addressing without resizing can store a key when \(n = m\) and every slot is already full.

---

## Q16 — MCQ

A linear-probing table uses three slot states: empty, occupied, and deleted (a tombstone). Search skips tombstones and stops at an empty slot. Insert may reuse the first tombstone it sees. Which statement is correct?

A. Replacing a deleted key by the empty marker is equivalent, because both states mean “not this key”.

B. A tombstone keeps a probe sequence intact, so a key that was inserted further along the sequence can still be found.

C. Tombstones may be ignored when computing load, and a long run of tombstones cannot make a search scan more than \(\alpha\) slots.

D. Chaining also needs tombstones, because unlinking a node breaks the home-slot rule.

---

## Level 5 — Challenge

## Q17 — MCQ

Keys are rehashed into a table of double size whenever an insertion would push the load above a fixed constant. Over a sequence of \(n\) insertions, the total expected copying work is \(O(n)\). Which description matches that analysis?

A. Every individual insertion is \(O(1)\) in the worst case.

B. The amortised expected cost of one insertion is \(O(1)\), while the insertion that triggers a rebuild can take \(\Theta(n)\) time.

C. The bound is an average over random keys only, and it can fail on some insertion sequences of length \(n\).

D. After the last rebuild the worst-case search, for a hash the adversary knows, is \(O(1)\).

---

## Q18 — MSQ

Select all that apply. The key set is static.

A. A two-level perfect hash can be built so that, after construction, every search is \(O(1)\) in the worst case.

B. Perfect hashing stays \(O(1)\) in the worst case after arbitrary insertions, with no further rebuild.

C. The construction relies on choosing secondary hashes that are collision-free on each bucket of a static set.

D. The same static set, stored in a balanced search tree, answers a successor query in \(O(\log n)\) worst-case time, which a hash of the key alone does not.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C, D |
| 3 | NAT | 4 |
| 4 | NAT | 7 |
| 5 | NAT | 4 |
| 6 | MSQ | A, B, D |
| 7 | NAT | 0 |
| 8 | MCQ | B |
| 9 | NAT | 2 |
| 10 | MCQ | B |
| 11 | MSQ | A, C |
| 12 | NAT | 4 |
| 13 | MCQ | B |
| 14 | MCQ | A |
| 15 | MSQ | B, C |
| 16 | MCQ | B |
| 17 | MCQ | B |
| 18 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: B

The load is the average number of keys per slot, \(\alpha = n/m\). It grows when a key is inserted and the table size stays fixed. Option (D) confuses the average with a guarantee about individual slots. Load 1 means \(n = m\), not that every slot holds exactly one key.

### Q2

Answer: A, C, D

Under simple uniform hashing the \(n\) keys are spread over \(m\) chains, so the average chain length is exactly \(\alpha\). An unsuccessful search hashes once and reads a whole chain, which is expected \(\Theta(1+\alpha)\) time. Holding \(\alpha\) constant, for example by growing the table, makes that expectation \(\Theta(1)\). The worst case is different: every key can share one slot, and the search is \(\Theta(n)\). Chaining stores lists, so it does not need an empty slot inside the array and it allows \(n > m\).

### Q3

Answer: 4

Home slots: \(10 \bmod 7 = 3\), \(17 \bmod 7 = 3\), \(3 \bmod 7 = 3\), \(24 \bmod 7 = 3\), \(8 \bmod 7 = 1\). Inserting at the head of slot 3 produces the chain

\[
24 \to 3 \to 17 \to 10.
\]

The search inspects 24, 3, 17, and 10, then stops. That is 4 keys. Slot 1 holds only 8. The policy matters: insertion at the tail would have put 10 at the head, and the same search would have inspected one key.

### Q4

Answer: 7

Each of the \(n(n-1)/2\) unordered pairs collides with probability \(1/m\) when hashes are independent and uniform. The expectation is

\[
\frac{8 \cdot 7}{2 \cdot 4} = 7.
\]

This counts pairs, not the length of the longest chain. Several colliding pairs can sit in different slots, and one slot can hold more than one pair.

### Q5

Answer: 4

The home slot of every inserted key is \(k \bmod 11 = 7\): \(18 = 1\cdot 11 + 7\), \(29 = 2\cdot 11 + 7\), \(7 = 7\), \(40 = 3\cdot 11 + 7\), \(51 = 4\cdot 11 + 7\).

| Key | Slots inspected | Placed in |
|----:|-----------------|----------:|
| 18 | 7 | 7 |
| 29 | 7, 8 | 8 |
| 7 | 7, 8, 9 | 9 |
| 40 | 7, 8, 9, 10 | 10 |
| 51 | 7, 8, 9, 10, 0 | 0 |

The search for 40 repeats the probe sequence and finds the key in slot 10, so it inspects 4 slots. Linear probing placed the whole run in consecutive slots because every home hash agreed. That run is primary clustering.

### Q6

Answer: A, B, D

(A) describes primary clustering: the next key whose home slot falls inside a block of length \(L\) extends that block. (B) is the modelling distinction. The closed forms \(1/(1-\alpha)\) for a miss and \((1/\alpha)\ln(1/(1-\alpha))\) for a hit assume that probe sequences are random permutations. Double hashing is the usual approximation. Linear probing’s sequences are shifts, so the ideal formula is optimistic once clusters form. (C) is false. For some coefficients and some \(m\), the quadratic sequence repeats before it has seen every slot, and insertion can fail with empty slots left. (D) is true: if \(m\) is prime and the step \(h_2(k)\) is not 0 modulo \(m\), then as \(i\) runs from 0 to \(m-1\) the probes hit every residue exactly once.

### Q7

Answer: 0

| Key | \(h_1\) | \(h_2\) | Probe that finds an empty slot | Slot |
|----:|--------:|--------:|--------------------------------|-----:|
| 15 | 2 | 4 | \(i = 0\) | 2 |
| 28 | 2 | 5 | \(i = 1\): \((2+5) \bmod 13\) | 7 |
| 41 | 2 | 6 | \(i = 1\): \((2+6) \bmod 13\) | 8 |
| 19 | 6 | 8 | \(i = 0\) | 6 |
| 6 | 6 | 7 | \(i = 1\): \((6+7) \bmod 13\) | 0 |

Key 6 does not share the whole probe sequence of 19, because \(h_2(6) \ne h_2(19)\). That is why double hashing avoids the secondary clustering of quadratic probing, where one home slot fixes the entire sequence. The occupied slots are 0, 2, 6, 7, and 8.

### Q8

Answer: B

Uniform probing looks for an empty slot by trying essentially random free positions. The probability the first probe hits an occupied slot is \(\alpha\), the next independent chance is again governed by the remaining load, and the resulting expectation for a miss is \(1/(1-\alpha)\). The chaining expression \(\Theta(1+\alpha)\) is a different policy. The logarithmic expression is the average over the loads at which the successful keys were inserted; it is the successful-search formula. As \(\alpha \to 1\) the miss cost grows without a constant bound, because empty slots become rare.

### Q9

Answer: 2

Substitute \(\alpha = 1/2\):

\[
\frac{1}{1 - 1/2} = 2.
\]

A successful search at the same load expects \((1/(1/2)) \ln 2 = 2 \ln 2 \approx 1.386\) probes, which is smaller because a hit can stop inside the probe sequence. The question asks for the unsuccessful figure.

### Q10

Answer: B

Search stops at the first empty slot so that it does not walk the whole table after the end of a cluster. If a deleted key is turned into that empty marker, the walk stops before any key that had probed past the deleted one. Those keys are still in the table and are reported missing. A tombstone is a third state that search skips and insertion may reuse. The failure does not depend on the deleted key being the last insertion. Chaining does not have this problem: unlinking a node leaves the other nodes of that chain reachable.

### Q11

Answer: A, C

Universality is a statement about a random choice of \(h\), not about one fixed function. For any two distinct keys the collision probability is at most \(1/m\). Chaining then has expected list length \(O(1+\alpha)\) even if an adversary picked the keys, because the adversary did not pick \(h\). One unlucky draw of \(h\) can still put many keys in one chain, so the worst case of that draw is not \(O(1)\). A hash value does not preserve order. Successor and range queries need a search tree or a sorted array.

### Q12

Answer: 4

From the chains in Q3, slot 3 holds four keys and every other slot holds at most one. The longest chain has length 4. The load is only \(5/7 < 1\), so a load below 1 does not forbid a chain this long. The worst-case search looks at the longest chain, not at the average \(\alpha\).

### Q13

Answer: B

The slot of a key is \(k \bmod m\). After the size becomes \(2m\), the new slot is \(k \bmod 2m\), which need not equal the old slot. Copying indexes would look up a key in the wrong place. Every key has to be inserted again under the new hash. The same is true of any hash whose definition mentions \(m\).

### Q14

Answer: A

Chaining’s unsuccessful search reads one chain of expected length \(\alpha\), plus the hash computation, which is \(\Theta(1+\alpha)\). The formula \(1/(1-\alpha)\) belongs to uniform open addressing and is undefined or meaningless for a miss once \(\alpha \ge 1\), whereas chaining still works above load 1. Quoting it for linear probing also drops primary clustering. At \(\alpha = 1\) an open-addressed table has no empty slot, so a miss cannot finish in one probe.

### Q15

Answer: B, C

(A) is false. Load 1 fixes only the average. Empty slots and chains of length greater than 1 can occur together; the birthday scale is the quantitative version of that fact. (B) is true: quadratic sequences are not automatically permutations of the slots. (C) is true: a collision appears with constant probability near \(n \approx \sqrt{2 m \ln 2}\), about \(1.177\sqrt{m}\), long before the table is full. (D) is false. Open addressing stores one key per slot, so \(n = m\) leaves no place for another key until the table grows.

### Q16

Answer: B

A tombstone says “a key used to live here; keep probing.” An empty slot says “no later key in this sequence was placed beyond here.” Replacing the tombstone by empty changes that message and recreates the bug in Q10. Search must skip tombstones, so a long deleted run costs real probes; the ideal formula \(1/(1-\alpha)\) no longer describes the table until it is rehashed. Chaining deletes by unlinking. There is no probe hole to preserve.

### Q17

Answer: B

Geometric growth charges the rebuilds at sizes proportional to \(1, 2, 4, \ldots\) up to \(n\). Those copying costs sum to less than \(2n\), so the total expected work of \(n\) insertions is \(O(n)\) and the amortised expected cost is \(O(1)\). Amortised cost is a total divided by the length of the sequence. It does not say that the single insertion which allocates the new table and reinserts every key is \(O(1)\). That insertion is \(\Theta(n)\). The charging holds for every sequence of \(n\) insertions once each rebuild is into a table of constant load; it is not a probability over the key order. A fixed hash can still pile every key into one chain, so a search after the rebuild is not worst-case \(O(1)\).

### Q18

Answer: A, C, D

For a static set, the first hash splits the keys into buckets and each bucket receives a secondary table whose hash is chosen to be one-to-one on that bucket. After those choices are fixed, a search evaluates two hashes and reads one slot, which is \(O(1)\) in the worst case. An insertion can collide inside a secondary table and force that level to be rebuilt, so the worst-case bound is a property of the finished static table. Successor order is not stored in the hash. A balanced search tree keeps that order and answers a successor query in \(O(\log n)\) worst-case time.

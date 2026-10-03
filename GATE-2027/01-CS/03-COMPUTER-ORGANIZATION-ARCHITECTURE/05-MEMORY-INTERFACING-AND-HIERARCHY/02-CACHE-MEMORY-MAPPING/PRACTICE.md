# Cache Memory Mapping — Practice (original questions)

All 36 questions below are **original**; none is a previous-year question, and none repeats the questions of the separate 14-PRACTICE-QUESTIONS file. Answers are directly under each question. Try the question before opening the answer.

**Global conventions** (unless a question overrides them): 1 K = 2^10, 1 M = 2^20; memory is byte-addressable; the cache starts empty; sets use LRU; the miss penalty is the *extra* time beyond the hit time; AMAT uses the hierarchical model unless stated; every study aid is in [`NOTES.md`](NOTES.md).

Level map: L1 Q1–Q6 · L2 Q7–Q14 · L3 Q15–Q22 · L4 Q23–Q29 · L5 Q30–Q36.

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1

Which statement about a **fully associative** cache is correct?

A. The tag is the whole block number, i.e. the address bits left after removing the block-offset bits.
B. It has the fewest tag bits of the three organisations.
C. A lookup needs only one tag comparator.
D. Conflict misses are impossible in a direct-mapped cache but possible in a fully associative one.

**Answer:** A

**Solution:** With one set there is no index field, so the address is just tag + offset and the tag is the block number (A). That makes the tag the *widest* of the three organisations (B false). Every line may hold the block, so all tags are compared at once — one comparator per line (C false). Conflict misses arise from several blocks competing for one set; direct-mapped has the most, fully associative none (D reversed).

**Concept tested:** organisations and field widths (NOTES §3, §4).
**Difficulty:** Easy.
**Common trap:** remembering "associative = more flexible" and concluding "fewer tag bits".

---

### Q2 — MSQ — Level 1

(One or more options correct.) Which statements about locality and caching are correct?

A. Instruction fetches inside a loop exhibit temporal locality.
B. Reading the elements of an array one after another exhibits spatial locality.
C. Doubling the block size always lowers the miss ratio.
D. Loading a whole block on a miss is how a cache exploits spatial locality.

**Answer:** A, B, D

**Solution:** A: the same instruction addresses recur → temporal. B: neighbouring addresses in order → spatial. D: the extra bytes of the block are the neighbours expected to be used next. C is false: beyond some size, fewer lines fit, conflicts and pollution rise and the miss ratio goes up again (NOTES §12.2).

**Concept tested:** locality, block size.
**Difficulty:** Easy.
**Common trap:** "always" statements.

---

### Q3 — NAT — Level 1

A fully associative cache has 4 KB of data with 16-byte blocks. How many tag comparators does the hardware need to search all lines in parallel in one lookup? (Integer.)

**Answer:** 256

**Solution:** lines = 4 KB / 16 B = 4096 / 16 = 256. A fully associative lookup compares the incoming tag with the tag of every line, so one comparator per line: **256**.

**Concept tested:** hardware cost of full associativity (NOTES §3.3–3.4, §6.4).
**Difficulty:** Easy.
**Common trap:** answering with the number of sets (1) or the associativity of a set-associative design.

---

### Q4 — MCQ — Level 1

In which situation can a **read miss** cause a block to be written from the cache to main memory?

A. Only in a write-through cache.
B. In a write-back cache, when the replaced block is dirty.
C. In a write-through cache, when the replaced block is valid.
D. Never; main memory is written only by store instructions.

**Answer:** B

**Solution:** A read miss may need to evict a victim. In a write-back cache a dirty victim holds data newer than memory and must be written back first (B). A write-through cache never holds data newer than memory, so evicting a block needs no transfer (A and C false). D ignores write-backs.

**Concept tested:** write-back vs write-through (NOTES §14.1, §14.3).
**Difficulty:** Easy.
**Common trap:** thinking only write instructions cause memory writes.

---

### Q5 — MCQ — Level 1

For a given trace, a miss occurs on a block that was referenced earlier and has since been evicted. A fully associative cache of the same total capacity (same trace) would **also** miss on this reference. This miss is a

A. compulsory miss
B. capacity miss
C. conflict miss
D. coherence miss

**Answer:** B

**Solution:** Not the first reference to the block → not compulsory. If a fully associative cache of the same size also misses, associativity would not have helped, so the working set simply exceeded the capacity → capacity miss. A conflict miss would be a miss in the real cache that *hits* in the fully associative reference. Coherence misses belong to multiprocessors and are out of scope.

**Concept tested:** 3C classification (NOTES §12.1).
**Difficulty:** Easy.
**Common trap:** calling every non-first miss a "conflict" miss.

---

### Q6 — MSQ — Level 1

(One or more options correct.) A direct-mapped cache keeps its total data capacity and address width fixed while the block size is doubled. Which statements are correct?

A. The number of lines halves.
B. The miss penalty typically increases.
C. The number of tag bits per line increases.
D. The total number of tag bits stored in the cache halves.

**Answer:** A, B, D

**Solution:** lines = C/B → halves (A). A bigger block takes longer to transfer (B). The DM tag is `A − log₂C`, independent of B, so the tag width per line is unchanged (C false). Same width × half as many lines = half the total tag bits (D). Example: 16 KB DM, 32-bit address: B = 32 → 512 lines × 18 bits = 9216; B = 64 → 256 × 18 = 4608.

**Concept tested:** block-size trade-offs (NOTES §5.4, §6.1, §12.2).
**Difficulty:** Easy–Medium.
**Common trap:** assuming the tag grows with the offset.

---

## Level 2 — Standard GATE style

### Q7 — NAT — Level 2

A byte-addressable machine has 36-bit physical addresses. Its cache is 8-way set-associative, 64 KB, with 128-byte blocks. How many tag bits does each line store?

**Answer:** 23

**Solution:**

```
 offset = log2 128 = 7
 lines  = 64 KB / 128 B = 65536 / 128 = 512
 sets   = 512 / 8 = 64   → index = 6
 tag    = 36 − 6 − 7 = 23
 check: DM tag = 36 − log2(64K) = 36 − 16 = 20;  +log2 8 = 3 → 23 ✓
```

**Concept tested:** tag bits for set-associative (NOTES §4.2, §5.1).
**Difficulty:** Easy.
**Common trap:** dividing lines by 8 twice, or using the 64 KB/8 way size as the index.

---

### Q8 — NAT — Level 2

A byte-addressable system has 28-bit physical addresses and a 32 KB direct-mapped cache with 16-byte blocks. How many **kilobits** (1 Kbit = 1024 bits) are needed to store all the tag values (tags only; ignore valid bits)? (Integer.)

**Answer:** 26

**Solution:**

```
 offset = 4;  lines = 32 KB / 16 B = 2048 → index = 11;  tag = 28 − 11 − 4 = 13 bits
 total tag bits = 2048 × 13 = 26 624 bits = 26 624 / 1024 = 26 Kbit
```

**Concept tested:** tag directory size (NOTES §6.1).
**Difficulty:** Easy–Medium.
**Common trap:** multiplying by the number of sets in a DM cache is fine (equal to lines), but in a k-way cache it must be lines, not sets.

---

### Q9 — MCQ — Level 2

A byte-addressable system has a direct-mapped cache whose address is divided into a 6-bit tag, a 9-bit index and an offset field. Each block is 8 bytes. What are the sizes of the main memory and of the cache's data store (tag bits excluded)?

A. 128 KB and 2 KB
B. 256 KB and 4 KB
C. 256 KB and 512 B
D. 128 KB and 4 KB

**Answer:** B

**Solution:** offset = log₂8 = 3 bits. Address = 6 + 9 + 3 = 18 bits → memory = 2^18 B = 256 KB. Cache = 2^9 lines × 8 B = 2^12 B = 4 KB.

**Concept tested:** memory and cache size from field widths (NOTES §6.2).
**Difficulty:** Easy–Medium.
**Common trap:** forgetting the offset in the address width or using the index alone for the cache size.

---

### Q10 — NAT — Level 2

A byte-addressable machine has 40-bit addresses. A set-associative cache of 256 KB uses 64-byte blocks and a 24-bit tag. What is its associativity (number of ways)?

**Answer:** 4

**Solution:** offset = 6; index = 40 − 6 − 24 = 10 → 1024 sets; lines = 256 KB / 64 B = 4096; ways = 4096 / 1024 = **4**.

**Concept tested:** associativity from tag width (NOTES §7.1).
**Difficulty:** Medium.
**Common trap:** stopping at the index bits and reporting 1024.

---

### Q11 — NAT — Level 2

A byte-addressable machine has 24-bit addresses and a 2-way set-associative cache of 16 KB with 32-byte blocks. To which set (numbered from 0) does the address 0x7C3A5E map?

**Answer:** 210

**Solution:**

```
 lines = 16 KB / 32 = 512;  sets = 256 → index 8 bits;  offset 5 bits;  tag 11 bits
 0x7C3A5E = 0111 1100 0011 1010 0101 1110
 drop 5 offset bits:  0x7C3A5E >> 5 = 0x3E1D2 (254 418)... as bits: 0111 1100 0011 1010 0101 1110 → [0111 1100 0011 1][010 0101 1][110 ...]
 simpler: block = ⌊0x7C3A5E / 32⌋ = 0x3E1D2;  set = block mod 256 = 0xD2 = 210
```

(The low 13 bits of the address are `0x1A5E`; `0x1A5E >> 5 = 210`.)

**Concept tested:** hex address → set (NOTES §8).
**Difficulty:** Medium.
**Common trap:** using the low 8 bits of the address as the index (ignoring the 5 offset bits).

---

### Q12 — MCQ — Level 2

A k-way set-associative cache has v = 16 sets and k = 2. The lines of set s are numbered 2s and 2s + 1, in increasing order of s. Main-memory block 37 may be placed in which cache lines?

A. lines 10 to 11
B. lines 5 to 6
C. lines 1 to 16
D. lines 16 to 31

**Answer:** A

**Solution:** set = 37 mod 16 = 5; lines of set 5 = 5·2 … 5·2 + 1 = 10 … 11. B forgets the factor k; C uses `j mod k` = 1 and a range of v lines; D uses `(j mod k)·v` … `+v−1`.

**Concept tested:** block → set → line numbers (NOTES §9).
**Difficulty:** Medium.
**Common trap:** swapping the roles of k and v.

---

### Q13 — NAT — Level 2

A cache has a hit time of 1.5 ns and a hit ratio of 0.96. A block is 8 words. On a miss main memory supplies the first word in 30 ns and each of the other words in 6 ns. The miss penalty is the extra time of this block transfer. Find the AMAT in ns (two decimals).

**Answer:** 4.38

**Solution:**

```
 miss penalty P = 30 + 7 × 6 = 72 ns
 AMAT = t_hit + m × P = 1.5 + 0.04 × 72 = 1.5 + 2.88 = 4.38 ns
```

**Concept tested:** AMAT with block-transfer penalty (NOTES §15.1).
**Difficulty:** Medium.
**Common trap:** using 8 × 30 or 8 × 6 for the penalty.

---

### Q14 — NAT — Level 2

L1: 2 ns, hit ratio 0.85. L2: 10 ns, **local** hit ratio 0.70. Main memory: 80 ns. Lookup is **simultaneous** (L1, L2 and memory are started together and the first correct source is used). Find the AMAT in ns (two decimals).

**Answer:** 6.35

**Solution:**

```
 T = H1·t1 + (1−H1)·H2·t2 + (1−H1)(1−H2)·t_m
   = 0.85·2 + 0.15·0.70·10 + 0.15·0.30·80
   = 1.70 + 1.05 + 3.60 = 6.35 ns
 (hierarchical would give 2 + 0.15·(10 + 0.3·80) = 7.10 ns)
```

**Concept tested:** simultaneous-access AMAT (NOTES §15.2).
**Difficulty:** Medium.
**Common trap:** adding the L1 time to every term (that is the hierarchical model).

---

## Level 3 — Multi-step

### Q15 — NAT — Level 3

A byte-addressable machine has 16-bit addresses and a direct-mapped data cache of 1 KB with 16-byte blocks, initially empty. Four one-byte variables W, X, Y, Z are accessed in the order W, X, Y, Z, repeated 8 times (32 references). Their addresses are W = 0x3A14, X = 0x7E1C, Y = 0x1D48, Z = 0x1D4F. How many of the 32 references are hits?

**Answer:** 15

**Solution:** offset = 4, lines = 64 → index = 6, tag = 6 bits. Fields (index = bits 4..9):

| Var | Address | Block | Line | Tag |
|---|---|---|---|---|
| W | 0x3A14 | 929 | 33 | 0x0E |
| X | 0x7E1C | 2017 | 33 | 0x1F |
| Y | 0x1D48 | 468 | 20 | 0x07 |
| Z | 0x1D4F | 468 | 20 | 0x07 |

W and X share line 33 with different tags → each evicts the other every iteration: 0 hits for W and X (16 misses). Y and Z are the same block (offsets 8 and 15): Y misses once, then hits; Z hits every time (its block is loaded by Y before Z runs). Y: 7 hits; Z: 8 hits. Total = 7 + 8 = **15** hits (17 misses).

**Concept tested:** PQRS-style conflict loop (NOTES §10.2).
**Difficulty:** Medium.
**Common trap:** treating Y and Z as different blocks (they share a block) or missing the W/X conflict.

---

### Q16 — MCQ — Level 3

A cache has 4 sets and is 2-way set-associative with LRU replacement, one memory block per line, initially empty. Memory blocks are referenced in this order: 1, 10, 9, 5, 14, 15, 9, 15, 10, 7, 2, 6, 1, 11 (set = block mod 4). Which of the following blocks is **not** in the cache at the end?

A. 9
B. 5
C. 6
D. 11

**Answer:** B

**Solution:** (set contents LRU → MRU)

| Ref | Set | Result | Set after |
|---|---|---|---|
| 1 | 1 | M | [1] |
| 10 | 2 | M | [10] |
| 9 | 1 | M | [1, 9] |
| 5 | 1 | M | [9, 5] (full) |
| 14 | 2 | M | [10, 14] |
| 15 | 3 | M | [15] |
| 9 | 1 | H | [5, 9] |
| 15 | 3 | H | [15] |
| 10 | 2 | H | [14, 10] |
| 7 | 3 | M | [15, 7] |
| 2 | 2 | M | evict 14 → [10, 2] |
| 6 | 2 | M | evict 10 → [2, 6] |
| 1 | 1 | M | set 1 is [5, 9]; evict LRU = 5 → [9, 1] |
| 11 | 3 | M | set 3 is [15, 7]; evict 15 → [7, 11] |

Final: set 1 {9, 1}, set 2 {2, 6}, set 3 {7, 11}. Block 5 is absent. (A FIFO cache would have evicted 9 instead of 5 — the hit on 9 refreshes it only under LRU.)

**Concept tested:** per-set LRU trace (NOTES §10.4, §13.4).
**Difficulty:** Medium.
**Common trap:** forgetting that the hit on 9 made 5 the LRU block (picking A).

---

### Q17 — NAT — Level 3

A byte-addressable machine has a direct-mapped data cache of 8 lines of 32 bytes. An 18 × 18 array of bytes is stored in row-major order starting at address 0x1C28. The whole array is read twice in row-major order; the cache is initially empty and only the array is accessed. How many cache misses occur in total?

**Answer:** 17

**Solution:**

```
 array = 324 bytes; first byte at offset 0x28 mod 32 = 8 in its block.
 blocks touched = ⌈(8 + 324) / 32⌉ = ⌈10.375⌉ = 11 consecutive blocks → 11 cold misses (pass 1).
 Cache = 8 lines, so blocks b0..b10 wrap: b8, b9, b10 evict b0, b1, b2 (same lines).
 Pass 2: b0, b1, b2 miss (they evict b8, b9, b10); b3..b7 hit; b8, b9, b10 miss again.
   → 3 + 3 = 6 misses.
 Total = 11 + 6 = 17.
```

**Concept tested:** two-pass array access with wrap-around conflicts (NOTES §11.3).
**Difficulty:** Medium–Hard.
**Common trap:** ignoring the unaligned start (10 blocks) or assuming the second pass is all hits.

---

### Q18 — NAT — Level 3

An `int A[32][32]` (4-byte ints, row-major) is read once entirely, first in row-major order and then (in a separate run with an empty cache) in column-major order. The data cache is direct-mapped, 2 KB, with 32-byte blocks; the array starts at a block-aligned address and no other data is accessed. How many more misses does the column-major run have than the row-major run?

**Answer:** 896

**Solution:** Row = 128 B = 4 blocks; lines = 2048 / 32 = 64.

- Row-major: each of the 32·4 = 128 blocks is fetched once → 128 misses.
- Column-major: element (i, j) is in block 4i + ⌊j/8⌋, line (4i + ⌊j/8⌋) mod 64. For a fixed column the rows i and i+16 map to the same line, so a sweep of 32 rows reuses 16 lines twice and nothing survives to the next column: every one of the 1024 accesses misses.

Difference = 1024 − 128 = **896**.

**Concept tested:** row- vs column-major locality, conflict stride (NOTES §11.4).
**Difficulty:** Medium–Hard.
**Common trap:** assuming the next column finds the block still cached (8 consecutive columns share a block, but the sweep evicts it).

---

### Q19 — NAT — Level 3

A byte-addressable machine has 32-bit addresses. Its cache is 8-way set-associative, 64 KB, 64-byte blocks, write-back. Each line stores a tag, one valid bit and one dirty bit. Each set stores the state for **true LRU** of its ways. How many metadata bits does the cache store in total (data bits excluded)?

**Answer:** 23552

**Solution:**

```
 offset 6;  lines 64K/64 = 1024;  sets 1024/8 = 128 → index 7;  tag = 32 − 7 − 6 = 19
 per line  = 19 + 1 + 1 = 21 bits;  per set lines = 8 × 21 = 168
 true LRU for 8 ways = ⌈log2 8!⌉ = ⌈log2 40320⌉ = 16 bits per set
 per set = 168 + 16 = 184;  total = 128 × 184 = 23 552 bits
```

**Concept tested:** total storage with valid, dirty, LRU bits (NOTES §6.3).
**Difficulty:** Medium–Hard.
**Common trap:** using 3 bits per way (8 × 3 = 24) or 7 (tree) instead of true LRU's ⌈log₂8!⌉.

---

### Q20 — NAT — Level 3

A two-level cache uses the hierarchical model. L1 hit time 1 ns; L2 hit time 5 ns; L2-to-memory miss penalty 50 ns. The **local** miss ratio of L1 is **twice** the local miss ratio of L2. The AMAT is 1.75 ns. Find the L1 local miss ratio (two decimals).

**Answer:** 0.10

**Solution:** Let L2's local miss ratio be m; L1's is 2m.

```
 1 + 2m·(5 + 50m) = 1.75   →   100m² + 10m − 0.75 = 0
 m = (−10 + √(100 + 300)) / 200 = (−10 + 20)/200 = 0.05
 L1 miss ratio = 2m = 0.10      check: 1 + 0.10·(5 + 0.05·50) = 1 + 0.10·7.5 = 1.75 ✓
```

**Concept tested:** solving for miss ratios from AMAT (NOTES §15.3).
**Difficulty:** Hard.
**Common trap:** reporting m (0.05) instead of 2m, or taking the negative root.

---

### Q21 — NAT — Level 3

A processor has a base CPI of 1.2 with a perfect memory system. Every instruction is fetched from the I-cache (miss ratio 2 %). 25 % of instructions are loads and 10 % are stores, all of which access the D-cache (miss ratio 5 % per data access). Every miss costs 40 cycles; ignore write-buffer effects. Find the effective CPI (two decimals).

**Answer:** 2.70

**Solution:**

```
 I-cache stall/instr = 1 × 0.02 × 40 = 0.80
 D-cache stall/instr = (0.25 + 0.10) × 0.05 × 40 = 0.70
 CPI = 1.2 + 0.80 + 0.70 = 2.70   (speedup with a perfect cache = 2.70/1.2 = 2.25)
```

**Concept tested:** effective CPI with cache stalls (NOTES §15.6).
**Difficulty:** Medium.
**Common trap:** omitting the I-cache term or counting only loads for the D-cache.

---

### Q22 — NAT — Level 3

A write-back, write-allocate, direct-mapped cache has 2 lines (line = block mod 2), one-word blocks, initially empty. The operations are: W0, R2, W2, W1, R3, W0, R2 (W = write, R = read, the number is the block). How many times is a block written back to main memory during these 7 operations (do not flush at the end)?

**Answer:** 4

**Solution:**

| Op | Line | Result | Action | Line after |
|---|---|---|---|---|
| W0 | 0 | miss | fetch 0, write | 0 (dirty) |
| R2 | 0 | miss | write back 0; fetch 2 | 2 (clean) |
| W2 | 0 | hit | set dirty | 2 (dirty) |
| W1 | 1 | miss | fetch 1, write | 1 (dirty) |
| R3 | 1 | miss | write back 1; fetch 3 | 3 (clean) |
| W0 | 0 | miss | write back 2; fetch 0, write | 0 (dirty) |
| R2 | 0 | miss | write back 0; fetch 2 | 2 (clean) |

Write-backs: 4; fetches: 6; hits: 1. (For comparison, a write-through/no-write-allocate cache would do 4 word writes and only 2 block fetches here — fewer transactions in this short, write-scattered stream.)

**Concept tested:** write-back traffic count (NOTES §14.4).
**Difficulty:** Medium.
**Common trap:** counting the final dirty line (not flushed) or forgetting that a write miss with write-allocate may evict a dirty victim.

---

## Level 4 — Tricky / trap-based

### Q23 — MCQ — Level 4

A byte-addressable processor has a 2³²-byte physical address space and a 2²³-byte cache. The block size is 128 bytes. The cache may be direct-mapped or K-way set-associative with K = 2^L and L ∈ {1, 2, 3}. Let the direct-mapped tag width be M bits and the set-associative tag width be N bits. Which relation holds?

A. N = M + L  
B. N = M − L  
C. N = M + K  
D. N = M − K  

**Answer:** A

**Solution:** DM: lines = 2²³/128 = 2¹⁶, index 16, offset 7, **M = 32 − 16 − 7 = 9**. For K = 2^L: index = 16 − L, tag **N = 9 + L**. So **N = M + L** (not +K). L = 1, 2, 3 gives N = 10, 11, 12.

**Concept tested:** tag grows by log₂K (NOTES §5.1, §5.3).
**Difficulty:** Medium–Hard.
**Common trap:** using K instead of L = log₂K in the relation.

---

### Q24 — NAT — Level 4

A byte-addressable system has 512 KB of physical memory (19-bit addresses). Its direct-mapped cache is initially empty. The byte address 0x52CE8 maps to cache line 75₁₀. What is the **maximum** possible cache data capacity in kilobytes? (Integer.)

**Answer:** 256

**Solution:** Write a = 0x52CE8 = 1010010110011101000₁₉. L = 75 = 1001011₂ (7 bits). The 7-bit pattern occurs at bits 16..10 → o = 10. Bit 17 = 0 extends L to 8 bits; bit 18 = 1 stops further extension. Best o + i = 10 + 8 = 18 → capacity = 2¹⁸ B = **256 KB** (tag = 1 bit). Smaller alignments give smaller caches.

**Concept tested:** max-cache reverse problem (NOTES §7.2, example 7.3).
**Difficulty:** Hard.
**Common trap:** taking the smallest o or forgetting zero-extension above L.

---

### Q25 — MCQ — Level 4

For the **inclusion** property to hold between an L1 and an L2 cache in a hierarchy, which of the following is **necessary**?

A. L1 must be write-through  
B. L2 must be write-through  
C. The associativity of L2 must exceed that of L1  
D. The L2 cache must be at least as large as the L1 cache  

**Answer:** D

**Solution:** Inclusion requires every L1 block to have a copy in L2, so L2 capacity (in blocks, with compatible block size) must be ≥ L1. Write-through and higher L2 associativity are common **design** choices to help maintain inclusion but are not logically necessary (NOTES §16).

**Concept tested:** inclusion policy (NOTES §16; 2008 Q.35 pattern).
**Difficulty:** Medium.
**Common trap:** picking write-through options (I or II) as "necessary."

---

### Q26 — MSQ — Level 4

(One or more options correct.) WB and WT are two set-associative caches with LRU replacement; WB is write-back and WT is write-through. Which statements are **FALSE**?

A. Every cache block in WB and WT has a dirty bit.  
B. Every write hit in WB causes a data transfer from cache to main memory.  
C. Evicting a block from WT never causes a write to main memory.  
D. A read miss in WB never evicts a dirty block.

**Answer:** A, B, D

**Solution:** A false: WT has no dirty bit. B false: WB write hits update the cache only. C true: WT keeps memory current, so eviction needs no write-back. D false: a read miss may replace a dirty victim in WB.

**Concept tested:** write policies (NOTES §14; 2022 Q.24 pattern).
**Difficulty:** Medium–Hard.
**Common trap:** reading "FALSE" as "TRUE" or assuming WT has dirty bits.

---

### Q27 — MCQ — Level 4

Use the same cache and reference string as Q16 (4 sets, 2-way, FIFO replacement, blocks 1, 10, 9, 5, 14, 15, 9, 15, 10, 7, 2, 6, 1, 11). Which block is **not** in the cache at the end?

A. 9  
B. 5  
C. 6  
D. 11  

**Answer:** A

**Solution:** Under FIFO the hit on 9 does **not** change eviction order. When 1 arrives at set 1, the queue is [1, 9] from insertion order; FIFO evicts **9** (not 5). Final set 1: {5, 1}. Sets 2 and 3 match Q16. Block **9** is absent.

**Concept tested:** LRU vs FIFO on the same trace (NOTES §13.4).
**Difficulty:** Medium–Hard.
**Common trap:** applying LRU reasoning from Q16 (answer B there).

---

### Q28 — NAT — Level 4

A 4-way set-associative cache has 16 KB of data. Each block holds 8 words and each word is 32 bits. Physical memory is 4 GB and byte-addressable. How many tag bits does each line store?

**Answer:** 20

**Solution:** Block = 8 × 4 B = 32 B → offset 5. Lines = 16 KB/32 B = 512 → sets = 512/4 = 128 → index 7. A = 32 → tag = 32 − 7 − 5 = **20**.

**Concept tested:** block size in words (NOTES §4.4; 2014 Q.9 pattern).
**Difficulty:** Medium.
**Common trap:** using 8 words as 8 bytes for the block size.

---

### Q29 — MCQ — Level 4

Which statement about cache **block size** is correct when other parameters are held fixed?

A. A smaller block implies better spatial locality.  
B. A smaller block implies a smaller tag field per line and therefore lower tag overhead.  
C. A smaller block implies a larger tag field and therefore lower hit time.  
D. A smaller block implies a lower cache miss penalty.  

**Answer:** D

**Solution:** Smaller blocks transfer fewer bytes on a miss → lower penalty (D). They capture less spatial locality (A false). Per-line tag width is unchanged when only B changes at fixed C and A (B false). Smaller tags do not imply lower hit time (C false).

**Concept tested:** block-size trade-offs (NOTES §12.2; 2014 Q.43 pattern).
**Difficulty:** Medium.
**Common trap:** choosing A because "spatial locality" sounds positive.

---

## Level 5 — Challenge

### Q30 — NAT — Level 5

A byte-addressable machine uses a virtually indexed, physically tagged 32 KB cache, 4-way set-associative, 64-byte blocks, and 4 KB pages. What is the minimum number of **page colours** required so that no two synonym virtual pages map to different sets? (Integer.)

**Answer:** 2

**Solution:** Sets = 32 KB/(4×64 B) = 128 → index 7; offset log₂64 = 6; index+offset = 13 bits alias in a page. Page offset bits = log₂4096 = 12. Extra bits x = 13 − 12 = 1 → colours = 2¹ = **2** (NOTES §17.2).

**Concept tested:** page colours / VIPT bridge (NOTES §17; 2013 pattern).
**Difficulty:** Hard.
**Common trap:** using cache size in bytes without dividing by associativity for #sets.

---

### Q31 — NAT — Level 5

A fully associative cache has 3 lines. References to memory blocks (in order): 0, 1, 2, 0, 1, 3, 0, 3, 1, 2, 1. Using the **OPT** (Belady) replacement policy, how many misses occur?

**Answer:** 5

**Solution:** OPT evicts the block used farthest in the future (or never). Trace yields misses on 0, 1, 2, 3, and the last 2 → **5** misses (7 hits). Verified by simulator.

**Concept tested:** OPT vs LRU/FIFO (NOTES §13.2).
**Difficulty:** Hard.
**Common trap:** simulating LRU instead of OPT.

---

### Q32 — NAT — Level 5

A byte-addressable machine has 32-bit addresses, a 64 KB cache, 64-byte blocks, and a 19-bit tag per line. What is the associativity (number of ways)?

**Answer:** 8

**Solution:** offset = 6; lines = 64 KB/64 B = 1024; index bits = 32 − 6 − 19 = 7 → sets = 128; ways = 1024/128 = **8**.

**Concept tested:** reverse associativity from tag width (NOTES §7.1).
**Difficulty:** Medium–Hard.
**Common trap:** reporting 128 (sets) or 1024 (lines).

---

### Q33 — MSQ — Level 5

(One or more options correct.) A byte-addressable fully associative data cache holds 8 KB with 32-byte blocks. Physical addresses are 24 bits. Which statements are correct?

A. The tag field is 16 bits wide.  
B. The cache has 256 lines.  
C. A lookup compares the incoming tag against 256 tags in parallel.  
D. Conflict misses are impossible for this cache organisation.

**Answer:** B, C, D

**Solution:** Lines = 8 KB/32 B = **256** (B). Fully associative: **256 comparators** (C). No index → conflicts from set contention do not arise; only compulsory and capacity misses (D). Tag = 24 − log₂32 = 24 − 5 = **19** bits (A false).

**Concept tested:** fully associative organisation (NOTES §3.2–3.4).
**Difficulty:** Medium–Hard.
**Common trap:** choosing A by subtracting only the offset from the address without noting FA tag = A − o.

---

### Q34 — NAT — Level 5

A byte-addressable system has 1 MB of physical memory (20-bit addresses). A direct-mapped cache maps the address 0xA2C28 to cache line 176₁₀. What is the maximum possible cache data capacity in kilobytes? (Integer.)

**Answer:** 128

**Solution:** a = 0xA2C28. Pattern for 176 = 10110000₂ fits at o = 6 with i up to 11 (bits 17..6 of a are zero above the 8-bit field). o + i = 6 + 11 = 17 → capacity = 2¹⁷ B = **128 KB**. (2026-pattern with original numbers.)

**Concept tested:** max-cache size (NOTES §7.2).
**Difficulty:** Hard.
**Common trap:** stopping at the 8-bit alignment (64 KB) without extending i while high field bits are zero.

---

### Q35 — NAT — Level 5

A fully associative cache with **3 lines** is filled using FIFO in one experiment and LRU in another (same empty start). The reference string is 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 (one block per reference). How many **more hits** does FIFO achieve than LRU?

**Answer:** 1

**Solution:** LRU: 2 hits, 10 misses. FIFO: 3 hits, 9 misses (Belady anomaly). FIFO − LRU = **1** extra hit.

**Concept tested:** Belady anomaly (NOTES §13.3; SHORTCUTS "Do NOT use").
**Difficulty:** Hard.
**Common trap:** assuming LRU always has ≥ hits.

---

### Q36 — NAT — Level 5

A byte-addressable cache has 32-bit addresses, 16 KB of data, 4-way set-associativity, 64-byte blocks, write-back. Each line stores tag + valid + dirty; each set stores true-LRU bits. What percentage of the **total** cache storage (data + metadata) is metadata? Give one decimal place.

**Answer:** 4.3

**Solution:** N = 256 lines, S = 64 sets, t = 20, per-line meta = 22, LRU/set = ⌈log₂24⌉ = 5. Metadata = 64×(4×22+5) = 5952 bits. Data = 131 072 bits. Total = 137 024 bits. Metadata share of total = 100×5952/137024 = **4.34%** → **4.3** at one decimal. (Metadata as a fraction of data alone would be 4.54% — not what is asked.)

**Concept tested:** metadata overhead (NOTES §6.3, example 6.3).
**Difficulty:** Hard.
**Common trap:** using 3 LRU bits (tree) instead of 5 (true LRU); counting only tag bits.

---

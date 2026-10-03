# Cache Memory Mapping — Notes (GATE CS 2027)

Topic path: `Computer Organization & Architecture → Memory Interfacing and Hierarchy → Cache Memory Mapping`

Sibling topic (memory-side theory: AMAT, interleaving, interfacing): [`../01-PERFORMANCE`](../01-PERFORMANCE/NOTES.md).

---

## 0. Where this fits

**Syllabus line (COA):** "… Memory interfacing and hierarchy: performance, **cache memory mapping**. …"

**Prerequisites (read first if shaky):**

- Binary/hex conversion and powers of two (log₂ of sizes) — [`../../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC`](../../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC).
- What a word, a byte, byte-addressable and word-addressable memory mean.
- Weighted averages (for AMAT) and solving a linear/quadratic equation.

**What depends on this topic:**

- Pipeline stalls caused by cache misses (CPI with memory stalls) → `../../07-INSTRUCTION-PIPELINING`, `../../08-PIPELINE-HAZARDS`.
- Memory performance / AMAT theory → [`../01-PERFORMANCE`](../01-PERFORMANCE/NOTES.md).
- Virtual memory, TLB and paging (the physically-indexed vs virtually-indexed cache question) → OS folder [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY).
- DMA/IO and cache consistency (only conceptually) → `../../06-IO-INTERFACE`.

**Conventions used in every file of this folder (and the whole COA set):**

```
1 K = 2^10, 1 M = 2^20, 1 G = 2^30        (binary prefixes unless the question says otherwise)
Address split:   block offset = log2(block size)
                 index        = log2(#sets)
                 tag          = address bits − index − offset
Sizes of tag / storage are counted in BITS; cache "size" (capacity) means DATA BYTES only,
unless the question explicitly says "including tag / valid / dirty bits".
AMAT, hierarchical access :  T = H1·T1 + (1−H1)(T1 + H2·T2 + (1−H2)(T2 + …))
AMAT, simultaneous access :  T = H1·T1 + (1−H1)·H2·T2 + (1−H1)(1−H2)·T3 + …
```

Every time an AMAT is computed here the access model is **named**. Addressability (byte vs word) is always stated.

---

## 1. Evidence snapshot (what drives the depth of each section)

Counted by me from the mapping file [`questions.md`](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/questions.md): **66 mapped entries (2007–2026), of which 43 are genuine cache-mapping/organisation entries, 2 are performance-type, 4 are page-colour (bridge) entries and 17 are misfiled.** The 43 cache entries collapse to 40 distinct questions (one question was printed in four booklets in 2013). Details: [`PYQ.md`](PYQ.md).

| Section | Skill | Value | Evidence (counted among the 43 on-topic entries) |
|---|---|---|---|
| §4–§6 | Address split, tag/index/offset, storage bits, hardware | **HIGH** | 15 entries ask for tag bits, tag-directory size, or main-memory/cache size from field widths (2007–2026), plus the 2026 "tag grows by log₂K" relation |
| §7–§9 | Address → line/set, reverse problems, hex extraction | **HIGH** | 8 entries: hex address → set/line/tag, "which block maps where", max cache size from a given line (2026), same-index array elements (2008) |
| §10–§11 | Hit/miss tracing, conflict loops, array loops | **HIGH** | 7 entries: P,Q,R,S loops (2022, 2026), LRU block stream (2009), array traversals (2007, 2008), LRU miss-ratio reasoning (2014) |
| §12–§13 | 3C, block size/associativity trade-offs, replacement | MEDIUM | 2014 block-size trade-off, 2014 LRU theory, 2009 LRU trace; no mapped FIFO/OPT item, but the practice file needs LRU |
| §14 | Write policies | MEDIUM | 2 entries (2022, 2024) — both are "true/false statements about write-back vs write-through" |
| §15–§16 | AMAT with cache, multi-level, CPI, inclusion | **HIGH** | 9 AMAT-style entries (2010, 2014, 2015, 2017×2, 2020, 2022, 2025) + 1 inclusion entry (2008) |
| §17 | Sector/word-addressable/VIPT bridge | LOW–MEDIUM | 4 page-colour entries (2013, one question), word-addressed practice Q11, block-size-in-words PYQs |

Existing practice file (22 questions) skills: field widths for DM/SA/FA, k-way vs DM tag change, word addressable tag, 3 hit/miss traces (DM and 2-way LRU), tag + valid bit storage, dirty/LRU storage, line number from hex address, a cycle-count formula. §21 maps each to a section.

---

## 2. Why a cache works, and the vocabulary

### 2.1 Intuition

A processor can execute an instruction in about a nanosecond, but DRAM needs tens of nanoseconds. A cache is a small, fast memory placed between the CPU and main memory that **keeps copies of recently used pieces of main memory**. It works only because programs are not random:

- **Temporal locality** — a location used now will probably be used again soon (loop counters, loop code, a sum variable).
- **Spatial locality** — locations near one just used will probably be used soon (the next array element, the next instruction).

Temporal locality is exploited by *keeping* a block after use; spatial locality is exploited by *fetching a whole block* (several neighbouring bytes) on a miss.

Library picture: the main memory is a huge library; the cache is the desk. You carry a *whole shelf segment* (a block) to the desk whenever you need one book (spatial), and you leave the books on the desk until you need the space (temporal).

### 2.2 Vocabulary

| Term | Meaning |
|---|---|
| Block (line) | The unit of transfer between cache and memory; size is a power of 2 bytes (or words). "Block" = memory-side unit, "line" = cache-side slot; many books use them interchangeably. |
| Hit / miss | The requested block is / is not present in the cache. |
| Hit time (t_c) | Time to access the cache and detect a hit. |
| Miss penalty | Extra time, beyond the hit time, to bring the block from the next level (assume this meaning unless a question defines "miss time" as total). |
| Hit ratio H, miss ratio m = 1−H | Fraction of accesses that hit / miss. |
| Set | A group of lines that one memory block may occupy. |
| Associativity k | Number of lines per set ("ways"). |
| Tag | The high-order address bits stored with a line to identify *which* memory block it holds. |
| Valid bit | 1 if the line holds real data (all valid bits are 0 at start-up). |
| Dirty (modified) bit | 1 if the line was written and memory is stale (write-back caches). |
| Block number | `⌊byte address / block size⌋`, i.e. address with the offset bits removed. |

### 2.3 The memory hierarchy picture

```
 CPU registers ──► L1 cache ──► L2 cache ──► (L3) ──► main memory (DRAM) ──► disk
   fastest, smallest, costliest per byte  ─────────────────►  slowest, largest, cheapest
 Each level holds a subset of the next level. Data moves between neighbouring levels in blocks.
```

---

## 3. Cache organisations: what a line stores and where a block may go

### 3.1 What one cache line contains

```
 ┌───────┬───────┬──────────┬──────────────────────────────┐
 │ valid │ dirty │   tag    │   data (one block: B bytes)  │   + per-set replacement state (LRU bits)
 └───────┴───────┴──────────┴──────────────────────────────┘
   1 bit   1 bit*  t bits           8·B bits                       (* only in write-back caches)
```

On a lookup the hardware (1) uses part of the address to select a line or set, (2) compares the stored tag(s) with the address tag **and** checks valid, (3) on a hit uses the offset to pick the byte/word inside the block.

### 3.2 The three placement rules

| Organisation | A memory block can go to … | Lines per set | Sets |
|---|---|---|---|
| **Direct-mapped** (k = 1) | exactly 1 line | 1 | = #lines |
| **k-way set-associative** | any of the k lines of 1 specific set | k | #lines / k |
| **Fully associative** (k = #lines) | any line | #lines | 1 |

All three are one family: **direct-mapped is the special case k = 1, fully associative is k = #lines**. Every formula below is written for general k and specialised by substituting k = 1 or k = #lines.

```
 Direct-mapped (8 lines)           2-way set-associative (4 sets)       Fully associative (8 lines)
 block j → line j mod 8            block j → set j mod 4, either way    block j → any line
 ┌──┐                              set0 [way0][way1]                   [  ][  ][  ][  ]
 │L0│ ← blocks 0, 8, 16, …         set1 [way0][way1]                   [  ][  ][  ][  ]
 │L1│ ← blocks 1, 9, 17, …         set2 [way0][way1]
 │… │                              set3 [way0][way1]
```

### 3.3 Trade-offs in one table

| | Direct-mapped | k-way | Fully associative |
|---|---|---|---|
| Conflict misses | most | fewer as k grows | none (only capacity/compulsory) |
| Tag comparators | 1 | k | #lines |
| Way-select multiplexer | none | k-to-1 | #lines-to-1 (or priority encoder) |
| Replacement policy needed | no (only one choice) | yes, among k | yes, among all lines |
| Tag bits per line | smallest | tag_DM + log₂k | largest (no index) |
| Hit time / cost | lowest | middle | highest |

### 3.4 Hardware picture of a k-way lookup

```
          address:  | TAG | INDEX | OFFSET |
                         │     │
                         │     └──► decoder selects ONE set (k lines read out in parallel)
                         │
      k comparators:  tag_0 == TAG ?   tag_1 == TAG ?  …  tag_{k-1} == TAG ?   (each ANDed with valid)
                          │                 │                    │
                          └─────── OR → HIT          one-hot select → k-to-1 MUX → data block → offset MUX → word
```

Counting facts used in GATE-style questions (per lookup): **k comparators** (each `tag`-bits wide), **one k-to-1 multiplexer per data bit** that is sent onward, and a set decoder of `index` inputs. Direct-mapped has 1 comparator and no way multiplexer; fully associative has one comparator per line.

---

## 4. Address anatomy: offset, index, tag

### 4.1 Derivation

Take a **byte-addressable** memory with A-bit addresses (so 2^A bytes) and a cache of C bytes with B-byte blocks.

1. *Block offset.* Inside a block we must name one of B bytes → `o = log₂B` low bits.
2. *Block number.* The remaining A − o bits identify the memory block: `block = ⌊addr / B⌋`.
3. *Lines and sets.* #lines `N = C / B`. With k ways: #sets `S = N / k`.
4. *Index.* A block can sit only in the set `block mod S` — taking `mod S` of a binary number with S = 2^i keeps its low i bits, so **index = low i = log₂S bits of the block number** (the bits just above the offset).
5. *Tag.* Different blocks with the same index differ in the remaining high bits; storing these identifies the occupant → `t = A − i − o`.

```
 |<─────────────── A bits ───────────────>|
 +--------------------+-----------+--------+
 |        TAG         |   INDEX   | OFFSET |
 |     t = A−i−o      | i=log2(S) | o=log2B|
 +--------------------+-----------+--------+
        high bits       middle        low
```

Why the index is in the *middle* and not at the top: consecutive blocks should go to *different* sets (a sequential scan then uses the whole cache). If the index were the top bits, an entire array would pile onto one set.

### 4.2 Direct, k-way and fully-associative field widths

```
 N = C / B                     (#lines)
 S = N / k                     (#sets)
 o = log2 B
 i = log2 S = log2 N − log2 k
 t = A − i − o = A − log2 N + log2 k − o = A − log2 C + log2 k       ← note B cancels (see §5)

 Direct-mapped : k = 1          → i = log2 N,         t = A − log2 C
 Fully assoc.  : k = N, S = 1   → i = 0,              t = A − o
```

### 4.3 Worked example 4.1 — one cache, four organisations

*Byte-addressable, A = 30 bits (1 GB). Cache C = 16 KB, block B = 32 B.* N = 16 KB / 32 B = 512 lines; o = log₂32 = 5.

| Organisation | k | Sets S | Index i | Offset o | Tag t = 30 − i − 5 | Comparators |
|---|---|---|---|---|---|---|
| Direct-mapped | 1 | 512 | 9 | 5 | **16** | 1 |
| 2-way | 2 | 256 | 8 | 5 | **17** | 2 |
| 4-way | 4 | 128 | 7 | 5 | **18** | 4 |
| 8-way | 8 | 64 | 6 | 5 | **19** | 8 |
| Fully associative | 512 | 1 | 0 | 5 | **25** | 512 |

Each doubling of associativity removes one index bit and adds it to the tag.

### 4.4 Worked example 4.2 — word-addressable machine and "block size in words"

Memory is **word-addressable** when the address names a word, not a byte. Then the offset counts *words inside the block*, and the address has fewer bits than a byte address would.

*A machine has 2^24 words of 4 bytes each, word-addressable. The cache has 64 KB of data, direct-mapped, block = 8 words.*

1. Capacity in words: 64 KB / 4 B = 16 384 words = 2^14.
2. Lines: 2^14 / 8 = 2048 = 2^11 → index 11.
3. Offset: log₂8 = 3 (a word index inside the block).
4. Tag: 24 − 11 − 3 = **10**.

Cross-check on the byte-addressed view of the same machine: byte address = 24 + 2 = 26 bits; block = 32 B → offset 5; index 11; tag = 26 − 11 − 5 = 10. **The tag, index and number of lines do not change with the addressing unit; only the offset width (and total address width) do.** This is the safest consistency check for word-addressed problems.

Procedure:

```
 1. Convert capacity and block size to the SAME unit as the address (words if word-addressable).
 2. offset = log2(block size in that unit)
 3. index  = log2(#sets)       4. tag = address bits − index − offset
```

Trap: if a question gives the block size "in words" and the cache size "in bytes", convert one of them before dividing.

---

## 5. Tag-bit relationships

### 5.1 Tag grows by log₂k when associativity grows (fixed C, B, A)

From §4.2: `t_k = A − log₂C + log₂k`, hence

```
 t_k − t_DM = log2 k           and, for k and k' ways:   t_{k'} − t_k = log2(k'/k)
 t_FA = A − log2 B             (k = N)   → t_FA − t_DM = log2 N
```

It depends only on *k* (through its logarithm), not on the block size or on the cache size. The wrong forms `+k`, `−k`, `−log₂k` appear as distractors.

### 5.2 Worked example 5.1 — symbolic form

*Physical address space 2^P bytes, word = 2^W bytes, cache capacity 2^N bytes, block = 2^M words, K-way set-associative.*

```
 offset (bytes in block)  = M + W
 #lines                    = 2^N / 2^(M+W)  = 2^(N−M−W)
 #sets                     = 2^(N−M−W) / K → index = N − M − W − log2K
 tag = P − index − offset  = P − (N − M − W − log2K) − (M + W) = P − N + log2K
```

M and W cancel completely. **Check (numbers):** P = 32, W = 2, N = 16, M = 3, K = 4 → direct computation: block = 8 words × 4 B = 32 B; 64 KB / 32 B = 2048 lines; 512 sets; index 9; offset 5; tag = 32 − 9 − 5 = 18; formula 32 − 16 + 2 = 18. ✓ (verified over a parameter grid by script.)

### 5.3 Worked example 5.2 — "direct-mapped tag M vs K-way tag N" pattern

*Physical address space 2^28 bytes, cache 2^20 bytes, block 64 B. DM tag = M bits; K-way tag (K = 2^L, L ∈ {1,2,3}) = N bits. Relation?*

DM: lines 2^20/2^6 = 2^14, index 14, offset 6, tag M = 28 − 14 − 6 = 8. For K = 2^L: index 14 − L, tag N = 28 − (14 − L) − 6 = 8 + L. So **N = M + L** (L = 1, 2, 3 gives 9, 10, 11 — verified). The relation is in terms of L = log₂K, not K.

### 5.4 Quick table to remember

| Change (C, B, A fixed) | Index | Tag |
|---|---|---|
| DM → 2-way | −1 | +1 |
| DM → 4-way | −2 | +2 |
| k-way → fully associative | → 0 | + (index lost) |
| Block size ×2 (C, A, k fixed) | −1 | 0 (offset +1, index −1) |
| Cache size ×2 (B, A, k fixed) | +1 | −1 |
| Address width +1 | 0 | +1 |

Check of the "block size ×2" row: A = 30, C = 16 KB, DM: B = 32 → i = 9, o = 5, t = 16; B = 64 → i = 8, o = 6, t = 16. So the DM **tag per line is unchanged** when block size changes, but the **number of lines halves, so total tag storage halves** (§6).

---

## 6. Counting storage, hardware and sizes

### 6.1 Tag directory ("bits needed to store all tags")

```
 total tag bits = (#lines) × (tag bits per line)            (valid/dirty/LRU NOT included unless asked)
 tag directory entry = tag + valid + dirty (+ other status)  → directory size = #lines × entry width
```

**Worked example 6.1.** *Byte-addressable memory 16 MB (A = 24), cache 8 KB DM, B = 32 B.* N = 8 KB/32 B = 256 lines; o = 5; i = 8; t = 24 − 8 − 5 = 11. Tag bits to store = 256 × 11 = **2816 bits** (= 2.75 Kbit). Each line also needs a valid bit if asked: 256 × 12 = 3072 bits.

Why it matters: tag storage scales with the *number of lines*. Halving the block size doubles the lines and doubles tag storage — the source of the "smaller blocks → larger tag overhead" trade-off (§12.2). Illustration (16 KB DM, A = 32): B = 16 / 32 / 64 / 128 → lines 1024 / 512 / 256 / 128, tag 18 bits each → total tag bits 18432 / 9216 / 4608 / 2304.

### 6.2 Main-memory size and cache size from the field widths

*The direct-mapped cache of a byte-addressable system uses 5 tag bits, 10 index bits and 2 offset bits.*

```
 address bits = 5 + 10 + 2 = 17     → main memory = 2^17 B = 128 KB
 cache data   = 2^(10+2) = 2^12 B   = 4 KB      (lines × block size; tag not counted unless told so)
```

General rule: **main memory = 2^(tag+index+offset) bytes; cache capacity = 2^(index+offset) × k bytes** (k = 1 for direct-mapped). A trap: if a question says "no other information stored per line" it is hinting that the cache size is the data capacity only; if it says "including tag and valid bits", add them.

### 6.3 Total storage including valid, dirty and replacement bits

**Worked example 6.3.** *32-bit byte address, 16 KB, 4-way, B = 64 B, write-back, one valid and one dirty bit per line, true-LRU state per set.*

```
 N = 16K/64 = 256 lines;  S = 256/4 = 64 sets;  o = 6;  i = 6;  t = 32 − 6 − 6 = 20
 per line metadata  = 20 + 1 + 1 = 22 bits
 LRU per set (true LRU of 4 ways): ⌈log2 4!⌉ = ⌈log2 24⌉ = 5 bits
 per set metadata   = 4×22 + 5 = 93 bits
 total metadata     = 64 × 93 = 5952 bits
 data               = 16 KB × 8 = 131 072 bits
 total storage      = 137 024 bits   (metadata overhead = 5952 / 131 072 = 4.54 % of the data)
```

**Bits needed for LRU state in one set of k ways**

| k | True LRU: ⌈log₂ k!⌉ | Per-way age counters: k·⌈log₂k⌉ | Tree pseudo-LRU: k−1 |
|---|---|---|---|
| 2 | 1 | 2 | 1 |
| 3 | 3 | 6 | — |
| 4 | 5 | 8 | 3 |
| 8 | 16 | 24 | 7 |

(True LRU needs to remember one of the k! orderings of the ways; pseudo-LRU only approximates this — concept only.) If a question says "one replacement bit per tag-directory entry" it fixes the number itself; use what it states.

**Worked example 6.4 (tag entry with extra status bits).** *128 KB, 8-way, B = 64 B, A = 32; each directory entry holds the tag plus 2 valid bits, 1 modified bit and 1 replacement bit.* N = 2048, S = 256, i = 8, o = 6, t = 18; entry = 18 + 4 = 22 bits; directory = 2048 × 22 = 45 056 bits = **44 Kbit**. Note the unit (Kbit = 1024 bits), the entry count (lines, not sets) and that the status bits come per entry.

### 6.4 Hardware bill of materials (comparators, multiplexers)

For a lookup in a k-way cache with tag width t, data word width w:

```
 comparators          : k, each t bits wide      (comparator bits = k·t)
 way-select mux       : k-to-1, one per output data bit
 set decoder          : i inputs → S outputs
 fully associative    : N comparators of (A − o) bits each, no decoder
```

Example (16 KB, B = 64 B, A = 32): DM → 1 comparator × 18 bits; 4-way → 4 × 20 = 80 comparator bits; fully associative → 256 × 26 = 6656 comparator bits. This is why large caches are never fully associative.

**What changes when associativity doubles at fixed C and B:** tag comparator width +1, number of comparators ×2, set-index decoder width −1, way-select multiplexer width ×2 (more inputs), offset field and the processor–memory data path width: unchanged.

---

## 7. Reverse problems (given the fields or a mapping fact, find the cache)

### 7.1 Associativity or size from a tag width

Everything in §4 is an equation in a handful of unknowns; solve for the one that is missing.

```
 tag = A − log2(#sets) − log2(B)   →   log2(#sets) = A − log2(B) − tag
 #lines = C / B,   k = #lines / #sets
```

**Worked example 7.1 (find k).** *A = 32 bits, C = 8 KB, B = 64 B, tag width given as 21 bits.* o = 6, so index = 32 − 6 − 21 = 5, #sets = 32; #lines = 8192/64 = 128; k = 128 / 32 = **4** (a 4-way cache). Verified.

**Worked example 7.2 (find the address width / capacity).** *A DM cache has tag 9, index 7, offset 4.* Address = 9 + 7 + 4 = 20 bits; cache data = 2^(7+4) = 2048 bytes; memory = 2^20 = 1 MB.

### 7.2 "Address X maps to cache line L — how large can the cache be?" (2026 pattern)

Here neither the block size nor the number of lines is given. You know only: byte-addressable, direct-mapped, an A-bit physical address, one concrete address `a`, and the line number `L` that `a` falls in. Unknown: o (offset bits) and i (index bits). The cache capacity is `2^(o+i)` bytes. We want the largest o + i that is consistent.

**Facts.** The line number of `a` is the i-bit field of `a` starting at bit o:

```
 line(a) = ( a >> o ) mod 2^i  = bits [o, o+i) of a        (bit 0 = LSB)
```

**Constraints.**

1. Bits `[o, o+i)` of `a` must equal `L` read as an i-bit number. So `i ≥ bit-length of L` (2^i > L), and if i is larger than the bit-length of L, the *extra high bits of that field in a must be 0*.
2. `o ≥ 0` (a block of at least 1 byte; word = 1 byte here) and `o + i ≤ A` (the tag has ≥ 0 bits; check whether the question allows a 0-bit tag — a cache as large as the whole memory — before accepting o + i = A).
3. Maximise `o + i`.

**Procedure.**

```
 1. Write a in A-bit binary and L in binary (length m).
 2. Find every position o where the m-bit pattern of L occurs in a with its LSB at bit o
    (field bits [o, o+m) equal L).
 3. For each such o, extend the field upward by z bits, where z = the number of consecutive 0 bits of a
    immediately above bit o+m−1  (these become the leading zeros of L as an (m+z)-bit number).
    Then i_max(o) = m + z and o + i = o + m + z.
 4. Answer = 2^(max over o of (o + i)) bytes.   Also sanity-check the other direction: a smaller o
    never beats a larger one unless it admits more zeros above.
```

**Worked example 7.3 (original numbers).** *Physical memory 512 KB (A = 19), byte-addressable, direct-mapped. Address 0x52CE8 maps to line 75. Largest possible cache?*

```
 a = 0x52CE8 = 1010010110011101000   (19 bits, bit 18 on the left)
 L = 75      = 1001011               (m = 7)
 search:  the pattern 1001011 occurs once in a, occupying bits 16..10  → o = 10
          bits above it: bit 17 = 0, bit 18 = 1
          z = 1 (bit 17 is 0; bit 18 is 1 and stops the extension)
 i_max = 7 + 1 = 8,   o + i = 18  → cache = 2^18 B = 256 KB   (tag = 19 − 18 = 1 bit)
 (feasible pairs found by brute force: (o,i) = (10,7) and (10,8) only.)
```

Why not i = 9? That would require bit 18 of `a` to be 0 for the index to read 75; it is 1, so the line number would be 75 + 256 = 331 instead. Why not a smaller o? No other position of `a` holds the pattern. Verified by script (exhaustive search over all (o, i)).

Common errors: forgetting the zero-extension (answer too small); allowing an i that does not cover L (line numbers ≥ 2^i do not exist); ignoring `o + i ≤ A`; mixing KB with bytes.

### 7.3 Set-associative variant

For a k-way cache the field is the *set index*, and the question gives a "set number". The same search works with `i = log₂(#sets)`; the cache capacity is `k · 2^(i+o)`. If associativity is also unknown, the problem is under-determined and the question will fix it.

---

## 8. Reading a hex address: extracting tag, index, offset

### 8.1 Method (bits)

1. Write the address in binary; pad on the left to exactly A bits (each hex digit = 4 bits).
2. Cut from the right: the last `o` bits = offset, the next `i` bits = index, the rest = tag.
3. Read the fields back as numbers (or hex after re-grouping).

### 8.2 Method (arithmetic — safer when fields do not align to hex digits)

```
 block number = ⌊addr / B⌋ = addr >> o
 index        = block mod S          (= (addr >> o) & (S−1))
 tag          = ⌊block / S⌋          (= addr >> (o + i))
 offset       = addr mod B
 Same-set test in one line:  ((addr & (2^(o+i) − 1)) >> o)     i.e. mask the low (o+i) bits, then shift right by o.
```

Two addresses can occupy the same line/set **iff** their index fields are equal; they are the *same block* iff block numbers are equal (tag and index both equal).

### 8.3 Worked example 8.1 — which addresses share a set?

*A = 24 bits, byte-addressable, C = 32 KB, 4-way, B = 128 B.* N = 256, S = 64, o = 7, i = 6, t = 11. The set is bits 7..12, so mask with `0x1FFF` (13 bits) then shift by 7.

| Address | Binary (24 bits) | Low 13 bits (hex) | Set = low13 >> 7 | Tag (11 bits) | Offset |
|---|---|---|---|---|---|
| 0x31A4C8 | 0011 0001 1010 0100 1100 1000 | 0x04C8 | **9** | 0x18D | 72 |
| 0x5B24C0 | 0101 1011 0010 0100 1100 0000 | 0x04C0 | **9** | 0x2D9 | 64 |
| 0x07A4F8 | 0000 0111 1010 0100 1111 1000 | 0x04F8 | **9** | 0x03D | 120 |
| 0x2D2448 | 0010 1101 0010 0100 0100 1000 | 0x0448 | **8** | 0x169 | 72 |

The first three addresses compete for the same 4-way set (different tags, so they are different blocks); the last one is in a different set. At a glance: the low 13 bits of the first three, `0x04C8`, `0x04C0`, `0x04F8`, all lie in the same 128-byte window `0x0480–0x04FF`, which is set 9.

General rule: `S × B = 2^(i+o) = 2^13 = 0x2000` bytes is the **way size** (cache size / k). Two addresses are in the same set iff their low 13 bits lie in the same B-byte window. Addresses that differ by an exact multiple of the way size have identical low-13 bits, so they are certainly in the same set (and the same offset) — but that is only a sufficient test; other pairs, like the three above, also share a set.

### 8.4 Worked example 8.2 — tag and line in hex (DM)

*A = 24 bits, DM with 2^9 lines, B = 32 B; address 0x3A7F1C.* o = 5, i = 9, t = 10.

```
 0x3A7F1C = 0011 1010 0111 1111 0001 1100
 offset = low 5 bits  = 11100 = 28
 block  = addr >> 5   = 0x1D3F8  (119 800)
 line   = block mod 512 = 0x1F8 = 504          → index bits 1 1111 1000
 tag    = block >> 9  = 0xE9   (233)           → tag bits 00 1110 1001
 next byte 0x3A7F20:  offset 0, block 0x1D3F9, line 0x1F9 = 505, same tag 0xE9
```

The adjacent bytes `...1C` and `...20` are in different blocks (offset 28 is the 29th byte of a 32-byte block; the next byte begins a new block), so they have **different line numbers but the same tag**. Whenever a question gives "two consecutive bytes", check whether a block boundary lies between them.

### 8.5 When "tag in hex" is asked

Give the tag as the numeric value of the tag field, not the leftmost hex digits of the address. If the tag is 10 bits, the hex value ranges 0..0x3FF; re-group bits from the right in fours (`00 1110 1001` → `0E9`).

---

## 9. From a block number to its allowed lines

Memory blocks are numbered 0, 1, 2, … (`block = ⌊addr/B⌋`). With N lines, k ways, S = N/k sets:

```
 direct-mapped : line = j mod N
 k-way         : set  = j mod S          and the block may use any of the k lines of that set
 fully assoc.  : any of N lines
 If the k lines of set s are stored consecutively in the numbering  s·k, s·k+1, …, s·k+k−1  then
   block j may occupy lines   (j mod S)·k   …   (j mod S)·k + (k − 1)
```

**Worked example 9.1.** *v = 8 sets, k = 4 lines per set, lines of a set consecutive, set 0 first. Block 45.* set = 45 mod 8 = 5; lines 5·4 = 20 … 23. ✓ Typical distractors: using `j mod k`, or forgetting to multiply by k, or placing the range at `j mod v` directly (that would be a layout where the lines of a set are *not* consecutive).

Equivalent statement for two blocks: **blocks j₁ and j₂ conflict iff j₁ ≡ j₂ (mod S)** (same set), whatever k is. They are in the same *line* of a direct-mapped cache iff j₁ ≡ j₂ (mod N).

---

## 10. Tracing hits and misses

### 10.1 Procedure

```
 For each reference:
   1. block = ⌊addr / B⌋ (or word index / words-per-block);  set = block mod S;  tag = block div S.
   2. Look in the set: if some valid line has the same tag → HIT (update LRU order if LRU).
   3. Otherwise MISS: fetch the whole block. If a free line exists in the set use it,
      else evict according to the replacement policy (DM: the only line).
   4. Record the new content of that set. Count hits and misses.
 Cache starts empty (all valid bits 0): the first access to any block is a miss ("cold" miss).
```

Always trace by **blocks**, not by byte addresses — two different addresses in the same block hit each other (spatial locality).

### 10.2 Worked example 10.1 — a P,Q,R,S loop in a direct-mapped cache

*A = 20 bits (byte-addressable; each variable is one byte), DM cache of 2 KB with B = 32 B → N = 64 lines, o = 5, i = 6, t = 9.* The loop accesses P, Q, R, S in this order, 10 times (40 references), starting from an empty cache.

| Var | Address | Binary (20 bits) | Tag | Line | Offset |
|---|---|---|---|---|---|
| P | 0x4C2A4 | 0100 1100 0010 1010 0100 | 0x98 | 21 | 4 |
| Q | 0x4C6A8 | 0100 1100 0110 1010 1000 | 0x98 | 53 | 8 |
| R | 0x2A2A8 | 0010 1010 0010 1010 1000 | 0x54 | 21 | 8 |
| S | 0x4C6B6 | 0100 1100 0110 1011 0110 | 0x98 | 53 | 22 |

Observations: P and R have the **same line (21) but different tags** → they conflict. Q and S have the same line **and the same tag** (same block 9781, offsets 8 and 22) → S is a hit once Q has loaded the block.

Per-iteration behaviour: P (miss; loads P's block into line 21) → Q (first iteration: miss, then hit) → R (miss; evicts P) → S (hit, Q's block still in line 53) → P again: line 21 holds R → miss, evicts R → … So every P and every R access misses; Q misses once, S never misses.

```
 Var   outcomes over 10 iterations    hits
 P     M M M M M M M M M M            0
 Q     M H H H H H H H H H            9
 R     M M M M M M M M M M            0
 S     H H H H H H H H H H           10
 Total: 19 hits, 21 misses out of 40 (hit ratio 19/40 = 47.5 %)
```

Same loop on a fully associative 64-line cache: only 3 distinct blocks → 3 misses, 37 hits. (Verified by simulation.)

**Method summary for any "P,Q,R,S" question:** (1) compute the (tag, line) of each address; (2) group variables by line; (3) same line & same tag = same block (co-hits); same line & different tag = conflict, and in a cyclic loop the conflicting blocks evict each other every time (in a DM cache); (4) count per variable, then answer each option. Options such as "every access to X is a hit" or "once X is loaded it is never evicted" are tested by exactly this table. Be careful with "initially empty": the very first access of each distinct block always misses.

### 10.3 Worked example 10.2 — cyclic access to more blocks than ways

*8 sets in every configuration; blocks 0, 8, 16 all map to set 0. Reference string: 0, 8, 16 repeated 5 times (15 references), LRU.*

| Ways | Capacity (lines) | Misses | Hits | Why |
|---|---|---|---|---|
| 1 (DM) | 8 | 15 | 0 | each block evicts the previous one |
| 2 | 16 | 15 | 0 | LRU always evicts exactly the block that is needed next (3 blocks cycling through 2 ways) |
| 3 | 24 | 3 | 12 | all three fit; only cold misses |

Lesson: with LRU, a cyclic reference pattern over **k + 1 blocks in a k-way set** misses every time. Associativity helps only when it reaches the number of blocks competing for one set.

### 10.4 Worked example 10.3 — tracing a 2-way LRU cache with byte addresses

*Byte-addressable, 4 sets, 2-way, B = 16 B → o = 4, i = 2 (A = 8 bits used here).* set = (addr >> 4) mod 4.

| # | Addr | Block | Set | Tag | Result | Set contents after (LRU → MRU) |
|---|---|---|---|---|---|---|
| 1 | 0x00 | 0 | 0 | 0 | miss | [0] |
| 2 | 0x20 | 2 | 2 | 0 | miss | set2: [2] |
| 3 | 0x40 | 4 | 0 | 1 | miss | [0, 4] |
| 4 | 0x04 | 0 | 0 | 0 | **hit** (same block as #1) | [4, 0] |
| 5 | 0x24 | 2 | 2 | 0 | **hit** (same block as #2) | set2: [2] |
| 6 | 0x80 | 8 | 0 | 2 | miss, evicts 4 (LRU) | [0, 8] |
| 7 | 0x44 | 4 | 0 | 1 | miss, evicts 0 | [8, 4] |
| 8 | 0x00 | 0 | 0 | 0 | miss, evicts 8 | [4, 0] |
| 9 | 0x30 | 3 | 3 | 0 | miss | set3: [3] |
| 10 | 0x70 | 7 | 3 | 1 | miss | set3: [3, 7] |
| 11 | 0x34 | 3 | 3 | 0 | **hit** | set3: [7, 3] |

3 hits, 8 misses. Note #4: byte 0x04 is in block 0 (not "a new address, so a miss").

### 10.5 Streams with word addresses and multi-word blocks

If the question lists **word addresses** and the block is w words, `block = ⌊word / w⌋`. Example: DM, 4 lines, 2 words per block; word stream 0, 1, 2, 3, 8, 9, 16, 17, 0, 1 → blocks 0,0,1,1,4,4,8,8,0,0 → lines 0,0,1,1,0,0,0,0,0,0 → M H M H M H M H M H → 5 hits (the 1-miss-1-hit pattern per block pair; blocks 4, 8 and 0 all evict each other in line 0, so the last 0 is a miss even though word 0 was used earlier). The first access to each 2-word block misses; the second word of that block hits as long as no other block has taken the line in between (spatial locality).

---

## 11. Spatial locality, arrays and loops

### 11.1 Sequential scans

A cold sequential scan of elements of size `e` bytes with `e ≤ B` misses once per block:

```
 hit ratio = 1 − e / B          (every block: 1 miss, then B/e − 1 hits)   — if e divides B and base is aligned
 misses    = number of distinct blocks touched = ⌈(offset of first byte in its block + total bytes) / B⌉
```

Example: 4-byte ints, B = 32 B → hit ratio = 1 − 4/32 = 7/8 = 87.5 %. A scan of 4096 ints (16 KB) = 512 blocks → 512 misses (verified).

**Unaligned start.** 100 ints (400 B) starting at byte 0x1014: first byte is at offset 0x14 = 20 within its 32-byte block → blocks touched = ⌈(20 + 400)/32⌉ = ⌈13.125⌉ = **14** (an aligned array would need ⌈400/32⌉ = 13). Verified by simulation.

### 11.2 Repeated sweeps and capacity

Array of S bytes swept repeatedly (contiguous, DM or LRU cache, capacity C, aligned):

| Case | First sweep | Later sweeps |
|---|---|---|
| S ≤ C (and no wrap-around conflicts) | S/B misses | 0 misses |
| S > C (cyclic sweep) | S/B misses | S/B misses again (every block is evicted before reuse) |

Example (8 KB DM, 32 B blocks, 4-byte ints, two sweeps): array 4 KB → 128 misses total (second sweep all hits); array 8 KB → 256 misses (fits exactly); array 16 KB → 1024 misses (the second sweep misses everything). All verified.

### 11.3 A 2-D byte array accessed twice (conflict at the wrap-around)

*DM cache with 16 lines of 32 B (512 B), byte-addressable. A 24 × 24 byte array stored row-major from byte address 0x2A10 (offset 16 within its block) is read completely twice, row by row.* Array size 576 B > 512 B cache.

```
 First pass : blocks touched = ⌈(16 + 576)/32⌉ = ⌈18.5⌉ = 19  → 19 cold misses.
 The 19 consecutive blocks use lines 0..15 and then wrap: blocks 16, 17, 18 evict blocks 0, 1, 2
   (lines 0, 1, 2 of the cache, counted relative to the array's first block).
 Second pass: blocks 0, 1, 2 miss (each evicts 16, 17, 18's lines);
              blocks 3..15 hit;  blocks 16, 17, 18 miss again (their lines were just taken by 0, 1, 2).
   → 3 + 3 = 6 misses.            Total = 19 + 6 = 25
```

If the array were 20 × 20 (400 B < 512 B) from the same address: 13 blocks, no wrap → 13 misses on pass 1, 0 on pass 2. Verified by simulation. If the start address were block-aligned, 24×24 would need ⌈576/32⌉ = 18 blocks (18 + 4 = 22 misses). Lesson: for arrays larger than the cache, find which blocks wrap onto the same lines and count the evictions on the second pass; for arrays smaller than the cache and contiguous, pass 2 is all hits.

### 11.4 Row-major versus column-major traversal

Layout: row-major means `A[i][j]` is at `base + (i·COLS + j)·e`; consecutive j are adjacent in memory.

*int A[64][64], e = 4 B → row = 256 B = 8 blocks of 32 B. DM cache 4 KB (128 lines).*

| Traversal | Misses | Hits | Why |
|---|---|---|---|
| Row-major (i outer, j inner) | 512 | 3584 | each block loaded once, 7 further hits per block |
| Column-major (j outer, i inner) | **4096** | 0 | stride 256 B = 8 blocks; rows i and i+16 map to the same line; a column sweep of 64 blocks cannot be retained (only 16 distinct lines are used), so the next column re-fetches everything |
| Column-major, DM cache 16 KB (512 lines) | 512 | 3584 | the 64 blocks of a column no longer conflict and survive until the next 7 columns |
| Column-major, rows padded to 72 ints | 512 | 3584 | stride 288 B = 9 blocks; 9 is odd, so 64 consecutive rows hit 64 different lines |

Rule: in column-major traversal of a row-major array the successive accesses are `stride = row length` apart. Compute `stride mod (S·B)`; if it hits only a few distinct sets the accesses collide. Padding the row length so that `stride / B` is coprime to the number of sets spreads them. (Row-major vs column-major miss ratios depend on whether the working set of one column fits in the cache.)

### 11.5 Which array elements share a cache index?

*double A[R][512], 8 B each; cache 32 KB, 2-way, B = 32 B → S = 512 sets, "way size" S·B = 16 KB.* Row length = 512 × 8 = 4096 B.

```
 set(addr) = ⌊addr/32⌋ mod 512.   Two addresses share a set if their block numbers differ by a multiple of 512,
 i.e. their addresses differ by (a multiple of 16384) plus anything inside a block.
 A[0][0] at 0 → set 0.     A[0][1], A[0][3] → same block (bytes 8, 24) → set 0 (same block, not a conflict).
 A[0][4] at 32 → set 1.    A[1][0] at 4096 → set 128.    A[2][0] at 8192 → set 256.
 A[4][0] at 16384 → set 0 (different block, SAME set as A[0][0]).    A[8][0] at 32768 → set 0 as well.
```

So with 2 ways, A[0][0], A[4][0], A[8][0] all compete for set 0, and a column walk with stride 4 rows can thrash a 2-way set when ≥ 3 such blocks are live. The rule "stride in bytes divisible by S·B → same set" is the quick test.

### 11.6 Initialisation loops that only write

*double A[256][256] initialised in row-major order with stores only; B = 32 B (4 doubles per block).*

| Write policy | Hit ratio of the loop | Why |
|---|---|---|
| Write-allocate (WB or WT) | 3/4 = 75 % | first store to a block misses and loads the block; the next 3 stores hit |
| No-write-allocate (typical with WT) | 0 % | a store miss writes memory directly and never allocates the block, so no later store ever hits |

This is why "what is the hit ratio of the loop" cannot be answered without the write-miss policy when the loop only stores. (Verified by simulation.)

---

## 12. Types of misses and the effect of block size and associativity

### 12.1 The 3C classification

| Class | Definition | How to identify in a trace | Remedy |
|---|---|---|---|
| **Compulsory (cold)** | First reference ever to a block | block never seen before | bigger blocks, prefetch |
| **Capacity** | Misses even in a *fully associative* cache of the same total size | would also miss in the FA reference | bigger cache |
| **Conflict** | Misses in the real cache but would hit in a fully associative cache of the same size | hit in FA reference, miss in real cache | more associativity, better mapping |

**Worked example 12.1.** *DM cache with 4 lines; reference blocks: 0, 4, 0, 4, 1, 2, 3, 5, 0, 4, 1, 2; the FA reference is a 4-line LRU cache.*

| # | Block | DM line | DM | FA-LRU | Class of the DM miss |
|---|---|---|---|---|---|
| 1 | 0 | 0 | M | M | compulsory |
| 2 | 4 | 0 | M | M | compulsory |
| 3 | 0 | 0 | M | H | conflict |
| 4 | 4 | 0 | M | H | conflict |
| 5 | 1 | 1 | M | M | compulsory |
| 6 | 2 | 2 | M | M | compulsory |
| 7 | 3 | 3 | M | M | compulsory |
| 8 | 5 | 1 | M | M | compulsory |
| 9 | 0 | 0 | M | M | capacity |
| 10 | 4 | 0 | M | M | capacity |
| 11 | 1 | 1 | M | M | capacity |
| 12 | 2 | 2 | H | M | — (DM hit) |

DM misses 11 = 6 compulsory + 3 capacity + 2 conflict. (Verified by script.)

**Trap — fully associative LRU is not always better.** Blocks 0,1,2,3,4 repeated twice on a 4-line cache: DM misses 7 (the blocks 1, 2, 3 stay put and only 0/4 fight over line 0) while a 4-line FA-LRU cache misses all 10 (cyclic pattern over 5 blocks, LRU evicts exactly the block needed next). So "more associativity ⇒ fewer misses" is true for LRU only on average, not for every sequence.

### 12.2 Block size trade-off (fixed cache capacity)

| If block size grows … | Effect |
|---|---|
| Spatial locality | more neighbours fetched per miss → fewer compulsory misses (up to a point) |
| Number of lines (C/B) | falls → total tag storage falls, but fewer distinct blocks can be kept → more conflict/pollution when locality is poor |
| Miss penalty | rises (more bytes to transfer) |
| Tag bits per line (DM) | unchanged (the offset gains the bit the index loses) |
| Miss rate | usually U-shaped in B: falls, then rises when the cache holds too few blocks |

So *smaller* blocks mean more lines, more total tag overhead, less spatial prefetching and a *lower* miss penalty; larger blocks the reverse. A statement like "smaller block ⇒ better spatial locality" or "smaller block ⇒ smaller tag overhead" is false; "smaller block ⇒ lower miss penalty" is true.

### 12.3 Associativity trade-off (fixed capacity and block size)

| If k grows … | Effect |
|---|---|
| Conflict misses | decrease (zero in the fully associative limit) |
| Tag width | +log₂ factor each doubling (§5) |
| Comparators / mux inputs | ×2 per doubling; hit time and energy rise |
| Index width / set decoder | −1 bit per doubling |
| Replacement logic | needed for k ≥ 2 and grows with k |
| Offset, block size, processor–memory bus width | unchanged |

---

## 13. Replacement policies

When a set is full and a new block arrives, the policy chooses the victim (not needed in direct-mapped caches).

| Policy | Rule | Hardware state | Notes |
|---|---|---|---|
| **LRU** | evict the block unused for the longest time | order of the k ways: ⌈log₂ k!⌉ bits per set (true LRU) | best on temporal locality; exact LRU too costly for k ≥ 8 → pseudo-LRU (k−1 tree bits, concept only) |
| **FIFO** | evict the block that has been in the set longest | a pointer/queue per set | ignores use; can show Belady's anomaly |
| **Random** | evict a random way | none (or a small PRNG) | simple, near-LRU on large caches |
| **Optimal (OPT/MIN)** | evict the block whose next use is farthest in the future | needs the future | offline lower bound for comparison |

### 13.1 Worked example 13.1 — one fully associative cache of 3 lines (or one 3-way set)

Reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1.

| Ref | LRU result | LRU contents (LRU→MRU) | FIFO result | FIFO contents (oldest→newest) | OPT result | OPT contents |
|---|---|---|---|---|---|---|
| 7 | M | 7 | M | 7 | M | 7 |
| 0 | M | 7 0 | M | 7 0 | M | 7 0 |
| 1 | M | 7 0 1 | M | 7 0 1 | M | 7 0 1 |
| 2 | M | 0 1 2 | M | 0 1 2 | M | 2 0 1 |
| 0 | H | 1 2 0 | H | 0 1 2 | H | 2 0 1 |
| 3 | M | 2 0 3 | M | 1 2 3 | M | 2 0 3 |
| 0 | H | 2 3 0 | M | 2 3 0 | H | 2 0 3 |
| 4 | M | 3 0 4 | M | 3 0 4 | M | 2 4 3 |
| 2 | M | 0 4 2 | M | 0 4 2 | H | 2 4 3 |
| 3 | M | 4 2 3 | M | 4 2 3 | H | 2 4 3 |
| 0 | M | 2 3 0 | M | 2 3 0 | M | 2 0 3 |
| 3 | H | 2 0 3 | H | 2 3 0 | H | 2 0 3 |
| 2 | H | 0 3 2 | H | 2 3 0 | H | 2 0 3 |
| 1 | M | 3 2 1 | M | 3 0 1 | M | 1 0 3 |

Totals: **LRU 10 misses (4 hits); FIFO 11 misses (3 hits); OPT 8 misses (6 hits).** (OPT's physical slot positions are shown as they were replaced in place.) LRU and FIFO first diverge at the third access to block 0 (row 7): LRU refreshed block 0 when it hit earlier, FIFO did not, so FIFO had already evicted 0.

### 13.2 Worked example 13.2 — FIFO can get worse with more ways (Belady's anomaly)

Reference string 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 on one set:

| Ways | FIFO misses | LRU misses | OPT misses | FIFO pattern |
|---|---|---|---|---|
| 3 | **9** | 10 | 7 | M M M M M M M H H M M H |
| 4 | **10** | 8 | 6 | M M M M H H M M M M M M |

FIFO has 10 misses with 4 ways but 9 with 3 ways: more capacity, more misses. LRU and OPT never show this (they are *stack algorithms*: the contents with k ways are always a subset of the contents with k+1 ways). Caches with LRU therefore never get worse by adding ways **to the same set** with the same set count.

### 13.3 LRU hit criterion (stack distance)

```
 In a k-way LRU set, a reference to block X hits  ⇔  the number of DISTINCT other blocks of the SAME SET
 referenced since the previous reference to X is at most k − 1.   (first reference: always a miss)
```

Verified by script on thousands of random reference streams. Consequences:

- If every re-use has at most d distinct same-set blocks in between and k ≥ d + 1, **all misses are compulsory** (miss ratio = distinct blocks / total references). With k = d the boundary case fails (the block has just been pushed out): e.g. sequence 1,2,3,1,2,3,1,2,3,4,1,2,3 has max distance 3; fully associative LRU with 2 / 3 / 4 lines gives 13 / 7 / 4 misses and only 4 lines (= d + 1) reaches the 4 compulsory misses.
- In a set-associative cache the distance is counted *within the set*, which is never larger than the global count. So a bound on distinct blocks globally also bounds the per-set distance.
- When a question bounds the distinct blocks "between accesses" by k and gives associativity A, check whether the question's bound counts the block itself and whether it is `≤ A−1` or `≤ A`; the guarantee needs the former.

### 13.4 LRU update rule during a trace (practice Q13, Q14, Q22)

Keep each set as an ordered list. Hit → move that block to the MRU end. Miss with free way → append at MRU end. Miss on a full set → remove the LRU end, append the new block at MRU end. A hit *changes the order*, which changes the next victim (Q14 type).

---

## 14. Write policies

### 14.1 Write hit policies

| | **Write-through (WT)** | **Write-back (WB)** |
|---|---|---|
| Write hit | update cache **and** main memory (often via a write buffer) | update cache only; set the **dirty bit** |
| Dirty bit needed? | not needed (cache never holds data newer than memory) | **yes**, one per block |
| Eviction of a block | never needs a write back | write the block back **iff dirty** |
| Memory traffic | one word per store | one block per dirty eviction, none for repeated stores to a block |
| Memory consistency | memory always current | memory stale until write-back |
| Typical pairing for write miss | no-write-allocate | write-allocate |

### 14.2 Write miss policies

- **Write-allocate (fetch-on-write):** on a write miss, bring the block into the cache first, then perform the write as a hit.
- **No-write-allocate (write-around):** on a write miss, write straight to memory (via the write buffer); the block is not brought in.

Four combinations exist; WB + WA and WT + NWA are the natural pairs. In WT + WA a write miss still loads the block, but no victim write-back is ever needed.

### 14.3 Which statements are always / never / possibly true (concept checks)

| Event | WT | WB |
|---|---|---|
| Write hit transfers data to main memory | **always** | never (at that moment) |
| Write hit changes the dirty bit | n/a | **can** (0→1; stays 1 if already dirty) |
| Eviction on a *read* miss writes a block to memory | **never** | **possible** (if the victim is dirty) |
| Eviction on a *write* miss writes a block to memory | never | possible (write-allocate and dirty victim) |
| Every cache block has a dirty bit | not required | required |

A true/false question on "read miss in a WB cache never evicts a dirty block" is false because replacement on a read miss can pick a dirty victim. "Eviction from a WT cache will not lead to data transfer to memory" is true for the usual definition (no dirty data). Read the option's quantifier (always / never / can).

### 14.4 Worked example 14.1 — memory traffic for two policy pairs

*Direct-mapped, 4 lines; references (blocks): R0, W0, W4, R4, W1, R0, W0, R4. Blocks 0 and 4 share line 0. Count block fetches and writes to memory.*

**Write-back + write-allocate**

| Op | Line | Result | Action | Line after |
|---|---|---|---|---|
| R0 | 0 | miss | fetch 0 | 0 (clean) |
| W0 | 0 | hit | set dirty | 0 (dirty) |
| W4 | 0 | miss | write back 0 (dirty), fetch 4, write | 4 (dirty) |
| R4 | 0 | hit | — | 4 (dirty) |
| W1 | 1 | miss | fetch 1, write | 1 (dirty) |
| R0 | 0 | miss | write back 4 (dirty), fetch 0 | 0 (clean) |
| W0 | 0 | hit | set dirty | 0 (dirty) |
| R4 | 0 | miss | write back 0 (dirty), fetch 4 | 4 (clean) |

3 hits, 5 misses, **5 block fetches, 3 block write-backs.**

**Write-through + no-write-allocate**

| Op | Line | Result | Action | Line after |
|---|---|---|---|---|
| R0 | 0 | miss | fetch 0 | 0 |
| W0 | 0 | hit | word → memory | 0 |
| W4 | 0 | miss | word → memory, no allocation | 0 |
| R4 | 0 | miss | fetch 4 (evict 0, nothing to write) | 4 |
| W1 | 1 | miss | word → memory | — |
| R0 | 0 | miss | fetch 0 | 0 |
| W0 | 0 | hit | word → memory | 0 |
| R4 | 0 | miss | fetch 4 | 4 |

2 hits, 6 misses, **4 block fetches, 4 single-word writes.** With 32-byte blocks and 4-byte words, WB+WA moved 8 × 32 = 256 B, WT+NWA moved 4 × 32 + 4 × 4 = 144 B in this short stream. Write-back wins when a block receives *many* stores before being evicted; with sparse writes to many different blocks it can lose. (Both traces verified by the simulator.)

### 14.5 Write buffer

A small queue between the cache and memory: the CPU deposits a store and continues; the buffer drains to memory in the background. It hides write latency for WT caches (and for write-backs of dirty victims). Costs: reads that miss must check the buffer for a pending write to the same block; if the buffer is full the CPU stalls. It does not change hit/miss counts.

### 14.6 Average time with writes

If reads and writes have different hit/miss times, weight by their frequencies (§15.5). For write-back caches add the write-back cost to the miss penalty: `AMAT = t_hit + m·(P + d·P_wb)` where d = fraction of replaced blocks that are dirty. Example: t = 2 ns, m = 0.05, P = 50 ns, d = 0.3, P_wb = 50 ns → AMAT = 2 + 0.05·(50 + 15) = **5.25 ns**. If a question says "the dirty bit is always 0", d = 0 and write-backs vanish.

---

## 15. Cache performance and AMAT

### 15.1 Single-level AMAT

```
 AMAT = t_hit + m · P            (P = miss penalty = EXTRA time beyond the cache lookup)
      = H·t_hit + (1 − H)·(t_hit + P)                 ← identical
 If the question gives the TOTAL time taken on a miss, T_miss (already containing the lookup):
 AMAT = H·t_hit + (1 − H)·T_miss
```

State which reading you use; compare the wording "miss penalty" (extra) vs "time on a miss" (total). The two readings differ by exactly `m·t_hit`.

**Miss penalty from a block transfer.** A block of B bytes moved over a path of w bytes per beat needs `n = B / w` beats. If the first beat costs `t_first` and each further beat `t_next`:

```
 P = t_first + (n − 1)·t_next
```

**Worked example 15.1.** *t_hit = 2 ns, H = 0.95; block = 4 words; main memory delivers the first word in 40 ns and each further word in 10 ns.* P = 40 + 3·10 = 70 ns. AMAT (miss penalty is extra) = 2 + 0.05·70 = **5.5 ns**. If instead the question defined 70 ns as the *total* miss time, AMAT = 0.95·2 + 0.05·70 = **5.4 ns**. The 0.1 ns gap is `m·t_hit` — read the sentence for which one is intended.

**Early restart / critical-word-first.** If the CPU resumes as soon as the *requested* word arrives, the penalty seen by the processor is the latency of that word (e.g. `t_first`), not the whole block transfer; the rest of the block fills in the background. Questions saying "referred word first" use the first-word latency as the penalty.

### 15.2 Two levels — two access models

Let L1: hit time t₁, hit ratio H₁; L2: hit time t₂, **local** hit ratio H₂ (hits among accesses that reach L2); memory time t_m.

```
 Hierarchical (sequential) access:   T = t1 + (1−H1)·( t2 + (1−H2)·t_m )
 Simultaneous (parallel) access:     T = H1·t1 + (1−H1)·H2·t2 + (1−H1)(1−H2)·t_m
```

**Worked example 15.2.** *t₁ = 1 ns, H₁ = 0.9, t₂ = 8 ns, H₂ = 0.8 (local), t_m = 60 ns.*

- Hierarchical: 1 + 0.1·(8 + 0.2·60) = 1 + 0.1·20 = **3.00 ns**.
- Simultaneous: 0.9·1 + 0.1·0.8·8 + 0.1·0.2·60 = 0.9 + 0.64 + 1.2 = **2.74 ns**.
- Global L2 miss ratio = 0.1 × 0.2 = **0.02**; local L2 miss ratio = 0.2.

If the question gives "miss penalty" figures (e.g. L2→L1 penalty and memory→L2 penalty) use the penalty form: `T = t1 + m1·(P_L2 + m2·P_mem)` where each P is the *extra* time for that level — the same as the hierarchical formula with t₂ = P_L2 and t_m = P_mem.

**Worked example 15.3 (three levels, hierarchical).** t₁ = 1, t₂ = 6, t₃ = 20, t_m = 100 ns; local miss ratios m₁ = 0.1, m₂ = 0.4, m₃ = 0.5: T = 1 + 0.1·(6 + 0.4·(20 + 0.5·100)) = 1 + 0.1·(6 + 0.4·70) = 1 + 0.1·34 = **4.4 ns**; global miss ratio to memory = 0.1·0.4·0.5 = 0.02.

### 15.3 Solving for unknown miss ratios

**Worked example 15.4.** *Two-level cache, t₁ = 2 cycles, L2 hit time 10 cycles, L2→memory penalty 40 cycles, hierarchical model. Local miss ratio of L1 is twice that of L2. Target AMAT = 3.2 cycles. Find both ratios.*

Let m = L2 local miss ratio, L1 = 2m:

```
 2 + 2m·(10 + 40m) = 3.2   →   80m² + 20m − 1.2 = 0   →   m = (−20 + √(400 + 384)) / 160 = (−20 + 28)/160 = 0.05
 so L2 miss ratio 0.05, L1 miss ratio 0.10.    Check: 2 + 0.1·(10 + 0.05·40) = 2 + 0.1·12 = 3.2 ✓
```

Take the positive root; ratios must lie in [0, 1]. A "twice/half" relation can be swapped between the levels — read which is which. Check the answer back in the formula.

### 15.4 Split caches and instruction/data mix

**Worked example 15.5.** *70 % of reads are instruction fetches (I-cache: t = 1 ns, H = 0.9), 30 % are data reads (D-cache: t = 1 ns, H = 0.85). Both miss into a shared L2 (t = 6 ns, local H = 0.8) and then memory (70 ns); hierarchical.*

```
 T_I = 1 + 0.1·(6 + 0.2·70) = 1 + 0.1·20 = 3.0 ns
 T_D = 1 + 0.15·20           = 4.0 ns
 T   = 0.7·3.0 + 0.3·4.0     = 3.3 ns
```

### 15.5 Different times for reads and writes (weighted by operation)

**Worked example 15.6.** *In a program segment: 120 instruction fetches, 50 operand reads, 30 operand writes (200 references), hit ratio 0.8 for all. Times: read hit 2 ns, read miss 12 ns, write hit 3 ns, write miss 20 ns.*

```
 reads  (170): 0.8·2 + 0.2·12 = 4.0 ns
 writes ( 30): 0.8·3 + 0.2·20 = 6.4 ns
 average = (170·4.0 + 30·6.4) / 200 = (680 + 192) / 200 = 4.36 ns
```

Instruction fetches are reads. Weight by counts, not by an equal split of the three categories.

### 15.6 Cache stalls in CPI; speedup with a perfect cache

```
 CPI_effective = CPI_base + (instruction-fetch miss ratio × penalty)
                          + (memory refs per instruction × data miss ratio × penalty)
 speedup (perfect cache) = CPI_effective / CPI_base          (same clock, same instruction count)
```

**Worked example 15.7.** *CPI_base = 1.5; 30 % of instructions are loads/stores; I-cache miss ratio 3 %, D-cache miss ratio 6 %, penalty 50 cycles.* Stalls per instruction = 0.03·50 + 0.3·0.06·50 = 1.5 + 0.9 = 2.4; CPI = 3.9; speedup with a perfect cache = 3.9 / 1.5 = **2.6**. Every instruction fetches one instruction (hence factor 1 for the I-cache) — a classic omission.

### 15.7 Break-even hit ratio when hit time changes

**Worked example 15.8.** *Cache: hit time 4 ns, hit ratio 0.9, miss penalty 60 ns (extra). A redesign makes hit time 5 ns with the same penalty. Minimum hit ratio so that AMAT does not increase?*

AMAT₀ = 4 + 0.1·60 = 10 ns. Need 5 + (1 − H′)·60 ≤ 10 → (1 − H′) ≤ 1/12 → **H′ ≥ 0.9167**. (If the "60 ns" were a total miss time, the condition changes slightly: 0.9·4 + 0.1·60 = 9.6 and H′·5 + (1 − H′)·60 ≤ 9.6 → H′ ≥ 50.4/55 = 0.9164.) Choose the reading from the wording and round only at the end.

### 15.8 Block transfer between levels (multi-level timing questions)

When a block moves L2 → L1, the time depends on bus width and on how the question accounts for the access of each level. A common model: each bus beat needs one access of the *source* memory and one write into the *destination* level, with no overlap.

**Worked example 15.9.** *L1 block 8 words, L2 block 32 words, bus 4 words wide; access times: L1 1 ns, L2 12 ns, main memory 120 ns.* L2→L1: 8/4 = 2 beats × (12 + 1) = 26 ns. Memory→L2: 32/4 = 8 beats × (120 + 12) = 1056 ns. A miss in both levels followed by the refill chain: 1056 + 26 = **1082 ns**. **Other accounting models exist** (e.g. pipelined beats); when a figure or statement fixes the model use it. Missing figures in a mapped entry cannot be filled by guessing.

### 15.9 Performance-type items (service time and bandwidth)

*Block-fill bandwidth.* A single-level cache, 100 MHz memory clock, miss service: 2 cycles (address accept) + 5 cycles (access) + 4 cycles (4 words, one per cycle) = 11 cycles = 110 ns for a 16-byte block → 16 B / 110 ns = 145.45 × 10⁶ B/s (decimal M here because the unit is "10⁶ bytes/s"; always check the unit in the answer line). More of this theory in [`../01-PERFORMANCE`](../01-PERFORMANCE/NOTES.md).

*Disk-block (file system) cache with a miss-rate curve.* AMAT = H·t_cache + m·t_disk when the cache check is free. Original numbers: hit 1 ms, disk 10 ms; miss ratio vs cache size: 10 MB 0.60, 20 MB 0.45, 30 MB 0.30, 40 MB 0.20, 50 MB 0.12 → AMAT = 1 + 9m = 6.40, 5.05, 3.70, 2.80, 2.08 ms. The smallest size giving AMAT below 5 ms is 30 MB. Read the figure at each allowed size (steps of 10 MB), compute AMAT, pick the smallest that satisfies the strict inequality. If the figure is not available (as in the mapping), the number cannot be recovered from the text alone.

---

## 16. Multi-level caches: local versus global, inclusion

- **Local miss ratio** of a level = misses at that level / accesses *reaching* that level. **Global miss ratio** = misses at that level / all processor accesses = product of the local miss ratios down to that level. AMAT uses local ratios (as in §15.2) or global ratios consistently — never mix.
- The L2 sees only L1 misses, so its *local* miss ratio looks high even when it is very useful.

**Inclusion policies**

| Policy | Meaning | Consequence |
|---|---|---|
| **Inclusive** | every block in L1 is also in L2 | an L2 eviction must invalidate the L1 copy (back-invalidation); L2 capacity ≥ L1 capacity is necessary |
| **Exclusive** | a block is in L1 or L2, not both | total capacity = L1 + L2 |
| **Non-inclusive (NINE)** | no guarantee either way | simplest |

For inclusion to be *possible*, L2 must hold at least as many bytes as L1 (it must contain L1's contents). Whether L1/L2 use write-through or write-back, and their associativities, are design choices; inclusion can be maintained with back-invalidation whatever the write policy, so those are mechanisms rather than necessary conditions. (L2's block size is normally ≥ L1's block size so one L1 block lies inside one L2 block.)

---

## 17. Special organisations and bridge material

### 17.1 Sector (sub-block) caches

A *sector* is a large block with **one tag** but divided into sub-blocks, each with its own valid bit. On a miss only the requested sub-block is fetched.

**Worked example 17.1.** *A = 32, 16 KB DM, sector = 128 B with 4 sub-blocks of 32 B.* lines (sectors) = 16 KB / 128 = 128; o = 7; i = 7; t = 32 − 14 = 18. Metadata per sector = 18 tag + 4 valid = 22 bits → 128 × 22 = **2816 bits**. A conventional cache with 32-byte blocks has 512 lines, t = 18, and 512 × (18 + 1) = **9728 bits**. The sector design needs 3.45× fewer metadata bits for the same capacity but a sector miss evicts all 4 sub-blocks even if only one is needed, and unused sub-blocks waste capacity.

Rules: tag matches & sub-block valid → hit; tag matches & sub-block invalid → fetch that sub-block only (no eviction); tag mismatch → evict the sector (clear all valid bits, write back dirty sub-blocks), fetch only the requested sub-block.

### 17.2 Bridge: virtually indexed physically tagged (VIPT) caches and page colours

*(Prerequisite for the OS folder: [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY) covers paging and the TLB.)*

A cache may be indexed with the **virtual** address (fast: lookup starts while the TLB translates) while the **tag** is physical (VIPT). Problem: two virtual pages that map to the same physical page (**synonyms**) must reach the same cache set, otherwise the physical block can live twice.

- Page offset bits (low `p = log₂ page size` bits) are identical in virtual and physical addresses.
- If **index + block offset ≤ p**, the whole index comes from the page offset → synonyms always agree → no problem. This holds iff `cache size / k ≤ page size`.
- Otherwise `x = (index + offset) − p` index bits come from the virtual page number (VPN) and the OS must give synonyms the same value in those x bits. The number of distinct values is the number of **page colours**:

```
 page colours = 2^x = 2^(index + offset − p) = (cache size / k) / page size   (use 1 if the ratio is ≤ 1)
 largest cache that is colour-free (no constraint):   k × page size
```

**Worked example 17.2.** *32 KB, 4-way, B = 64 B, page = 4 KB.* sets = 32768/(4·64) = 128 → index 7, offset 6, index+offset = 13; p = 12 → x = 1 → **2 colours**. Colour-free maximum for 4-way with 4 KB pages: 4 × 4 KB = 16 KB. Verified. The 2013 mapped question (four booklets) asks the number of colours for a given VIPT cache; the linked previous question (not in this mapping) supplies the page size from a page-table layout — compute that first.

**Event-consistency reasoning (physically addressed cache + TLB).** If the system invalidates the cache blocks of a page when the page leaves main memory, then *a cache hit implies the page is resident*, and *a TLB hit implies the page is resident*; "page not in memory (page-table miss)" therefore cannot coexist with a cache hit or a TLB hit. Use this to eliminate impossible event sequences.

### 17.3 Out of scope here

Cache coherence protocols (MESI etc.) and the detailed design of TLBs are not part of this topic's syllabus line.

---

## 18. PYQ patterns: recognise, recipe, trap (no answers are given — mapping answers are all "VERIFICATION REQUIRED")

| # | Pattern | How to recognise | Recipe | Trap |
|---|---|---|---|---|
| P1 | Tag bits for a DM/SA/FA cache | "number of bits in the TAG", gives address bits, cache size, block size, k (years 2007, 2012, 2014, 2016, 2017, 2018, 2019, 2021, 2023, 2025, 2026) | §4: offset → lines → sets → index → tag | block size in *words* with word size; "kB" vs "KB"; fully associative has no index; mixing bits and bytes |
| P2 | Tag relation DM vs k-way | symbolic (2018) or "N vs M" (2026) | `tag_k = tag_DM + log₂k` (§5) | answering with k instead of log₂k |
| P3 | Tag directory / storage / "all tags" | "size of the tag directory", "bits to store all tag values" (2008, 2012, 2025) | #lines × entry width (§6) | using #sets; forgetting status bits when they are stated; Kbit = 1024 bits |
| P4 | Memory/cache size from field widths | gives tag+index bits, byte-sized blocks (2025) | memory = 2^(t+i+o); cache = 2^(i+o) per way (§6.2) | adding the tag to the cache size; forgetting offset |
| P5 | Associativity from tag width | gives tag bits, asks k (2021) | §7.1 | integer log slips |
| P6 | Max cache size from "address → line number" | 2026 | §7.2 | ignoring leading-zero extension; ignoring `o+i ≤ A` |
| P7 | Hex addresses → same set? / tag & line | 2015, 2020, 2008 | §8: mask low (o+i) bits, shift by o | block boundary between consecutive bytes; wrong width when fields cross hex digits |
| P8 | Block number → allowed lines | 2013 (four booklets) | `(j mod S)·k … +k−1` (§9) | `mod k`; forgetting `·k` |
| P9 | P,Q,R,S loop in DM cache | 2022, 2026 | §10.2: group by line, compare tags | same block via offsets (hit); first access always a miss |
| P10 | Block stream with LRU, which block is NOT in cache | 2009 | §10.4 / §13.4 with per-set lists | tracing by global LRU instead of per-set |
| P11 | Array loops: hit ratio / misses / replaced lines / same index | 2007 (two linked parts), 2008 (3 linked parts) | §11 | unaligned base; stores with no-write-allocate; element size vs block |
| P12 | LRU miss ratio from reuse-distance bound | 2014 | §13.3 | `≤ A` vs `≤ A−1` |
| P13 | AMAT with hit ratios/latencies | 2010, 2014, 2015, 2017, 2020, 2022, 2025 | §15 (state model) | hierarchical vs simultaneous; local vs global; penalty vs total miss time; block-transfer arithmetic |
| P14 | Unknown miss rates from AMAT | 2017 | §15.3 | wrong sign root |
| P15 | Write policy statements | 2022, 2024 | §14.3 table | always/never/can |
| P16 | Design trade-off statements | 2014 (block size), 2008 (inclusion) | §12.2, §16 | reversing tag overhead |
| P17 | Page colours | 2013 | §17.2 | forgetting that the page size comes from the linked question |

---

## 19. Traps and misconceptions

1. **Tag = address − index − offset, nothing else.** Memory and cache sizes go in through log₂C and log₂B only.
2. **Fully associative has index = 0**, but the *most* tag bits and the *most* comparators.
3. **k enters the tag as log₂k.**
4. **Index depends on #sets, not #lines**, for k-way caches.
5. **A "word" is not a byte.** Check the addressability and the width of a word before dividing.
6. **Trace by blocks.** Two addresses in the same block share a cache line; the second is a hit.
7. **First reference to a block is always a miss** ("initially empty").
8. **Conflict in a DM cache needs same index, different tag.** Same index and same tag = same block = hit.
9. **A hit under LRU updates the order**; a hit under FIFO does not.
10. **Write-through has no dirty bit; write-back needs one.** A read miss in WB can still evict a dirty block.
11. **AMAT averages times, not hit ratios**; local vs global ratios must not be mixed.
12. **"Miss penalty" is extra time** unless the question defines a total miss time.
13. **Cache capacity = data bytes** unless told otherwise; tags/valid/dirty are overhead.
14. **LRU state ≠ one bit per line**: true LRU of k ways needs ⌈log₂k!⌉ bits per set.
15. **DM can beat FA+LRU on cyclic patterns** (§12.1).
16. **Store-only loops with no-write-allocate have 0 % hits.**
17. **1 K = 2^10** in this repository's convention; “10⁶ B/s” units use decimal M — read the answer unit.

## 20. Edge cases and assumptions to state in an answer

- Byte- vs word-addressable memory; word size; block size units.
- Cache initially empty (valid bits 0) — and whether the question counts the first access as a miss.
- Replacement policy (LRU unless stated), write policy, write-miss policy.
- Hit-time model: hierarchical or simultaneous; local or global miss ratios; whether miss penalty includes the cache lookup.
- Whether a 0-bit tag (cache = memory) is acceptable in "maximum cache size" problems.
- Block-boundary check when two "consecutive" bytes are given.
- For arrays: the base address alignment and row-major layout.
- Pipeline/CPI problems: instruction fetch misses on *every* instruction.

---

## 21. Connections to other COA topics

- **Memory performance** (AMAT, interleaving, bus width, burst transfer): [`../01-PERFORMANCE`](../01-PERFORMANCE/NOTES.md). The miss penalty in §15.1 is usually computed there.
- **Instruction pipelining / hazards:** an instruction-fetch or data-memory miss adds stall cycles to the IF/MEM stage → CPI_effective in §15.6 → `../../07-INSTRUCTION-PIPELINING`, `../../08-PIPELINE-HAZARDS`.
- **Addressing modes / instruction set:** the effective address that reaches the cache is produced by the addressing mode (`../../02-ADDRESSING-MODES`); array indexing `A[i][j]` in a loop is just base + scaled index.
- **I/O and DMA:** DMA writes memory behind the cache's back; a write-through/write-back or flush policy decides coherence (`../../06-IO-INTERFACE/02-DMA`).
- **OS memory management:** paging and TLB hit/miss, page size and the VIPT constraint (§17.2) → [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY).
- **Digital logic:** the comparator and multiplexer counts of §3.4 are ordinary combinational circuits (`../../../02-DIGITAL-LOGIC`).

---

## 22. Existing practice coverage map (22 questions in the 14-PRACTICE-QUESTIONS file)

| Q# | Section(s) | Skill |
|---|---|---|
| 1 | §3.2 | direct-mapped placement |
| 2 | §4.1 | block offset bits |
| 3 | §3.2, §4.2 | FA has no index |
| 4 | §4.2 | #lines = C/B |
| 5 | §2.2, §3.1 | role of the tag |
| 6 | §4.2–4.3 | DM tag bits |
| 7 | §5.1 | same cache as 4-way |
| 8 | §5.1, §5.4 | tag change = log₂k |
| 9 | §4.2–4.3 | FA tag |
| 10 | §4.2, §10 | field widths; same-index conflict |
| 11 | §4.4 | word-addressable tag |
| 12 | §10.1–10.2 | DM trace |
| 13 | §10.4, §13.4 | 2-way LRU trace |
| 14 | §13.4 | which block LRU evicts after a hit |
| 15 | §6.1, §6.3 | tag + valid storage |
| 16 | §3.3, §12.3, §13, §14.1 | mixed true/false: dirty bit, DM replacement, ways, index change |
| 17 | §10.5, §11.1 | multi-word blocks, spatial locality |
| 18 | §4.2, §5 | 8-way tag |
| 19 | §8.2, §9 | line number of a hex address |
| 20 | §10.2, §11.2 | repeated string, conflict + stable block |
| 21 | §6.3 | total metadata with dirty, valid, LRU |
| 22 | §10.4, §13.4, §15.1 | 2-way LRU trace + cycle formula |

---

## 23. Self-check (answer without looking)

1. Write the three address fields and the formula for each in terms of C, B, k, A.
2. How does the tag change from direct-mapped to 8-way at fixed C, B, A, and why?
3. Why is the index taken from the middle bits, not the top bits?
4. How many comparators and multiplexer inputs does a k-way lookup need?
5. For a tag-directory entry with a tag, 2 valid bits, 1 dirty bit and 1 replacement bit, how do you get the directory size?
6. Given a hex address, how do you find its set in under a minute?
7. What is the hit criterion for LRU in terms of distinct blocks between accesses?
8. When do a DM cache and an LRU FA cache differ on cyclic patterns?
9. Which of write-through / write-back needs a dirty bit, and can a read miss write to memory?
10. Hierarchical vs simultaneous AMAT — write both formulas.
11. How do local and global miss ratios relate for L2?
12. How do you obtain the number of page colours of a VIPT cache?

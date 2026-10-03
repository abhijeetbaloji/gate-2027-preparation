# Memory Hierarchy Performance and Memory Interfacing — NOTES

Syllabus line (COA): "Memory interfacing and hierarchy: performance, cache memory mapping."
This folder owns the **performance** half: how long memory references take on average, what that does to CPU time,
how main memory is organised for speed, and how big memories are wired from small chips.
The **mapping half** (address split, direct/set/fully associative, replacement, tag-store sizes, cache traces) is the sibling
folder [`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/). Both folders must agree; where a formula is shared the
cache folder uses the same conventions listed in §0.2.

---

## 0. Where this fits

### 0.1 Position in the syllabus

| Item | Detail |
|---|---|
| Prerequisites | Binary prefixes and number systems ([`../../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC`](../../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/)); decoders and multiplexers (Digital Logic, combinational circuits); the iron law CPU time = IC × CPI × clock period. |
| Directly depends on this | Cache folder [`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/) (hit/miss ratios come from mapping; AMAT comes from here); [`../../07-INSTRUCTION-PIPELINING`](../../07-INSTRUCTION-PIPELINING/) and [`../../08-PIPELINE-HAZARDS`](../../08-PIPELINE-HAZARDS/) (memory stalls add to CPI); [`../../06-IO-INTERFACE/02-DMA`](../../06-IO-INTERFACE/02-DMA/) (DMA steals memory cycles — the cycle-time idea of §2). |
| Bridge to Operating Systems | Effective access time with TLB / page faults: owned by [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/). §8 gives only the formulas GATE asks as "memory hierarchy" numerics. |
| Official syllabus | [`syllabus.md`](../../../../00-GATE-2027/official-syllabus/CS/syllabus.md) |
| PYQ mapping for this folder | [`questions.md`](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/questions.md) — contains **no entries**. The performance-type PYQs were mapped into the cache folder; see [`PYQ.md`](PYQ.md). |

### 0.2 Conventions used in every file here

```
1 K = 2^10, 1 M = 2^20, 1 G = 2^30      for SIZES (capacity, address space)
1 MHz = 10^6 Hz, 1 MB/s = 10^6 B/s       for RATES (clock, bandwidth) unless the question says MiB/s
Word / byte addressability is always stated.  "Memory of 64 K words" and "64 KB byte-addressable" are different.
hit ratio h, miss ratio m = 1 − h   (decimals; "92 %" means 0.92)
Hit ratios of lower levels are LOCAL (fraction of references that REACH that level) unless the text says "overall / global".
Iron law:  CPU time = IC × CPI × T_clk = IC × CPI / f
```

Access models (must always be stated in any answer):

```
Hierarchical (sequential)  : lower level is touched only after the upper level has missed.
                             T = T1 + m1·(T2 + m2·(T3 + …))            (last level always hits)
Simultaneous (look-aside)  : all levels are probed in parallel; the first one that has the data supplies it.
                             T = h1·T1 + m1·h2·T2 + m1·m2·h3·T3 + …
```

### 0.3 Evidence snapshot (what drives the depth of each section)

Counts below are my own counts of the mapping files (see [`PYQ.md`](PYQ.md) for the row-by-row list).

| Skill cluster | Evidence | Value |
|---|---|---|
| Single-level and multi-level AMAT (hit ratios, access times, penalties; sometimes solving for an unknown) | 7 mapped entries in the cache file are numerical AMAT-type (2025, 2022, 2020, 2017 ×2, 2015, 2014); 1 more unmapped 2-level AMAT question (2025 CS-2) found by text search; existing practice Q4, Q5, Q7, Q8, Q11, Q13, Q14 | **HIGH-VALUE** |
| Block-transfer miss penalty: first word + subsequent words, bus width, referred-word-first | 2020, 2019, 2010 ×2 mapped entries (2017 mentions the referred-word-first policy); existing practice Q8 uses an "extra latency" form | **HIGH-VALUE** |
| Read / write / instruction-fetch weighted average | 2017 (I-cache, D-cache, L2), 2014 (reads, writes, ifetches) | **HIGH-VALUE** |
| Write-through vs write-back behaviour (statement truth) | 2024, 2022 mapped entries; existing practice Q12 | **HIGH-VALUE** (conceptual, easy marks) |
| Memory bandwidth of a burst-transfer memory | 2019 (one mapped entry) | MEDIUM |
| Solve backwards for hit ratio / miss rate / cache size | 2022, 2017, 2016 (figure missing) | MEDIUM |
| CPI with memory stalls, speedup of perfect cache | 1 entry (2024 CS1) mapped in `08-PIPELINE-HAZARDS`; existing practice Q9 | MEDIUM-HIGH (formula is short; appears in pipelining too) |
| Locality, block size / miss penalty trade-off, inclusion | 2014 (block size), 2008 (inclusion); existing practice Q1, Q6 | MEDIUM (conceptual) |
| Memory chip interfacing and decoder sizing | 2023, 2020 mapped in Digital Logic (decoder for a RAM block); user brief asks for it | MEDIUM |
| DRAM refresh as % of time | 1 PDF-text hit (2018) not mapped anywhere | MEDIUM-LOW (but a cheap, fully formulaic question) |
| Interleaving, wide memory | No mapped entry; belongs to the "performance" syllabus word and underlies the burst/bus-width PYQs | LOW-MEDIUM (needed for block-transfer time) |
| VM effective access time (bridge) | 4 entries mapped in OS folder (2020, 2018, 2014, 2011) | bridge only (§8) |

---

## 1. The memory hierarchy

### 1.1 Intuition: a desk, a bookshelf, a library

You are writing an essay. The two books you are using now lie open on the desk (fast, tiny). The ten books you
may need soon are on the shelf (a few seconds to fetch, bigger). The rest of the world's books are in the library
(minutes away, huge). You do not walk to the library for every sentence because **what you will read next is very
likely a book you read a moment ago, or the next page of the same book**. A computer memory system is built on the same bet.

```
          faster, smaller, costlier per bit
              ▲
   registers  │  ~ 1 clock cycle, hundreds of bytes
   L1 cache   │  ~ 1–4 cycles,    tens of KB          (SRAM)
   L2/L3      │  ~ 10–40 cycles,  hundreds of KB–MB   (SRAM)
   main memory│  ~ 100+ cycles,   GB                  (DRAM)
   disk/SSD   │  ~ 10^5–10^7 cycles, hundreds of GB+  (not random-access at word level)
              ▼
          slower, bigger, cheaper per bit
```

The cycle counts are only orders of magnitude to build a feel; every GATE question gives its own numbers.

### 1.2 Locality — why the bet pays off

| Kind | Meaning | Typical source | What exploits it |
|---|---|---|---|
| Temporal locality | a location used now is likely to be used again soon | loop counters, accumulators, a loop body's instructions | keeping recently used blocks in the cache (replacement policy) |
| Spatial locality | locations near a used location are likely to be used soon | sequential instruction fetch, array scans, structures | fetching a whole **block** (several words) on a miss |

Both are needed for a cache to pay off (existing practice Q1). A program with neither (a random walk over a huge table)
gets a hit ratio close to (cache size ÷ working-set size), whatever the policy.

### 1.3 Terminology

```
hit            : requested word found in this level
miss           : not found; must go to the next level
hit ratio h    : hits / references           miss ratio m = 1 − h
hit time       : time to deliver a word on a hit (includes the tag check)
miss penalty   : EXTRA time, beyond the hit time, spent to bring the data from the next level
               (some questions instead give the TOTAL miss time; read the wording)
block (line)   : unit of transfer between adjacent levels (several words)
block transfer : the movement of one whole block on a miss
```

The three causes of misses (use when a statement-type question asks "why"):

| Miss kind | Cause | Reduced by |
|---|---|---|
| Compulsory (cold) | first-ever reference to a block | larger blocks (fewer blocks), prefetching |
| Capacity | working set larger than the cache (even a fully associative cache misses) | larger cache |
| Conflict | too many live blocks map to the same set | higher associativity, better mapping |

(Existing practice Q6, option D, is the classic mistake: associativity does not cure capacity misses.)

### 1.4 Block size trade-off

```
block size ↑ :  + more spatial locality captured  → miss ratio falls at first
                − fewer blocks fit in the cache   → conflict/capacity misses rise past an optimum
                − miss penalty rises (more bytes per block transfer)
                + fewer tag bits in total (fewer blocks)           − but each block holds more unused bytes when locality is poor
block size ↓ :  larger tag store (more blocks), lower per-miss transfer time, less spatial locality
```

Net effect: the miss-ratio curve is U-shaped in block size, while miss penalty increases roughly linearly in transfer time.
A statement such as "a smaller block always means a lower miss rate" is false; "a smaller block has a smaller block-transfer
miss penalty" is true.

### 1.5 Inclusion (concept only)

A multi-level hierarchy is **inclusive** if every block present in L1 is also present in L2. Why designers want it: to check
whether some other processor/DMA has a copy, only L2 needs to be searched.

What inclusion *needs* versus what is merely a *way of maintaining* it:

- Necessary: L2 must be able to hold everything L1 holds, so L2 capacity must be at least L1 capacity (and its block size at
  least that of L1, otherwise one L1 block would need pieces from several L2 blocks).
- The bad event: L1 keeps hitting on block X, so L2 never sees X referenced and LRU in L2 may evict X. Now X is in L1 but not L2 —
  inclusion is broken. It is repaired by **back-invalidation** (when L2 evicts a block, remove it from L1).
- Write policy (write-through vs write-back) and relative associativity are *design choices* that make maintenance easier,
  not logical requirements; with back-invalidation inclusion can be forced regardless.
- The opposite design, **exclusive** (a block is in exactly one of L1/L2), gives more total capacity.

### 1.6 Why average access time is dominated by misses

If h = 0.99, T_hit = 1 ns, penalty = 100 ns: AMAT = 1 + 0.01 × 100 = 2 ns. The 1 % of references that miss cost as much as the
other 99 %. Halving the miss ratio or halving the penalty gives the same gain (existing practice Q14); improving hit
time by 1 ns beats both only when misses are rare. This "everything is misses" view makes the sections below easy.

---

## 2. Basic timing quantities

### 2.1 Definitions

```
Access time (latency)  t_A : time from presenting the address to getting the data.
Cycle time             t_C : minimum time between the START of two successive accesses.  t_C ≥ t_A
                             (DRAM needs precharge/restore after a read, so t_C > t_A).
Bandwidth (throughput) BW  : bytes transferred per second  = (bytes per access) / (time per access).
Transfer rate of a burst   : (bytes in burst) / (total burst time, including the first-word latency).
```

Latency and bandwidth are different: a truck full of tapes has huge bandwidth and terrible latency.

**Example 2.1 — access vs cycle.** A memory has t_A = 60 ns and t_C = 80 ns. Back-to-back random reads can start every 80 ns,
not every 60 ns. Rate = 1 / 80 ns = 12.5 × 10^6 accesses/s. With 4-byte words: 50 MB/s (10^6 B/s). The 20 ns difference is the restore time.

### 2.2 Burst (block) transfer: first word + subsequent words

Memories (DRAM page mode / burst mode) deliver the first word after a long latency and the following words quickly:

```
T_block = t_first + (W − 1) × t_next            W = words per block = block bytes / word bytes

timeline for W = 8, t_first = 40 ns, t_next = 10 ns
 0        40  50  60  70  80  90  100 110 (ns)
 |-first--|w2 |w3 |w4 |w5 |w6 |w7 |w8 |
 T_block = 40 + 7×10 = 110 ns
```

**Example 2.2.** 32-byte block (8 words of 4 B): 110 ns, so the block bandwidth = 32 B / 110 ns = 290.9 × 10^6 B/s. The raw "one word per 10 ns"
bandwidth would be 400 MB/s; the first-word latency costs 27 %.

Questions in this family give: clock (MHz → period = 1/f), cycles for the controller to accept an address, cycles to fetch,
cycles to transfer words. Recipe: (1) total **cycles per block** = sum of the stages that are NOT overlapped; (2) time = cycles × period;
(3) bandwidth = block bytes / time, converting to the unit asked (×10^6 B/s). Check whether stages overlap — if the statement says
the transfer of the words is "at the rate of one word per cycle" after a fixed fetch, they are sequential stages.

### 2.3 Bus width and number of transfers

If the block has `Wb` words and the bus carries `Bw` words per transfer, the block needs `⌈Wb / Bw⌉` bus transfers.
If each transfer takes the time `t` of the source level (a common textbook simplification stated in the question), then

```
T_block_transfer = ⌈Wb / Bw⌉ × t
```

**Example 2.3 (two-level, bus widths differ).** L1 block = 4 words, L2 block = 8 words. L2↔L1 bus is 2 words wide with t = 15 ns per
transfer; memory↔L2 bus is 4 words wide with t = 120 ns per transfer.
- Block L2 → L1: ⌈4/2⌉ × 15 = 30 ns.
- Block memory → L2: ⌈8/4⌉ × 120 = 240 ns.
- L1 miss and L2 miss: first memory → L2, then L2 → L1: 240 + 30 = 270 ns (the two moves happen one after the other).

(Check the question for: "is the access time of the level added once or per transfer?", "is a bigger block fetched into L2 and only a
smaller block forwarded to L1?" — the block sizes differ at different levels.)

---

## 3. Main memory organisation for performance

A DRAM chip is slow relative to the processor and it delivers few bits at a time. The hierarchy designer therefore widens or interleaves memory
so a **miss** (a block transfer) takes less time.

### 3.1 Notation

```
t_a : time to send the address               t_m : memory access (cycle) time of one bank/chip
t_b : time to move one bus-width of data     B   : words in a block
m   : number of banks (low-order interleaved)   W_mem: memory width in words (wide memory)
```

### 3.2 Three organisations (non-overlapped rounds)

```
(a) Simple      : 1-word memory, 1-word bus.      each word: send address, access, transfer
                  T = B × (t_a + t_m + t_b)

(b) Wide        : memory & bus W words wide.      ⌈B / W⌉ rounds
                  T = ⌈B / W⌉ × (t_a + t_m + t_b)
    (cost: wide bus & multiplexer; a bus narrower than the memory adds W transfers: T = ⌈B/W⌉ × (t_a + t_m + W × t_b))

(c) Interleaved : m independent banks, 1-word bus.   each round fetches m words in parallel, then ships them one by one
                  T = ⌈B / m⌉ × (t_a + t_m + m × t_b)         (if B < m: the last round ships B words)
```

**Example 3.1.** t_a = 1, t_m = 6, t_b = 1 (clock cycles). Block of 4 words:
- Simple: 4 × (1 + 6 + 1) = 32 cycles.
- Wide, 4-word bus: 1 × (1 + 6 + 1) = 8 cycles.
- Wide memory, 1-word bus (multiplexer): 1 + 6 + 4 = 11 cycles.
- 4-way interleaved: 1 + 6 + 4 × 1 = 11 cycles.
Block of 8 words with 4 banks: ⌈8/4⌉ × (1 + 6 + 4) = 22 cycles (simple: 64; two banks: 4 × (1 + 6 + 2) = 36).

Interleaving gives the benefit of a wide memory without a wide bus, only more banks and a bank-select decoder.

### 3.3 Overlapped (staggered) interleaving — how many banks are enough?

If bank i+1 may start t_b after bank i and a bank can start a new access every t_m, then bank utilisation keeps the bus busy when

```
m × t_b ≥ t_m          ⇒    m_min = ⌈ t_m / t_b ⌉           (bank count for one word per t_b)
block time (ignoring address) ≈ t_m + B × t_b        (first word at t_m + t_b, then one every t_b)
```

**Example 3.2.** t_m = 40 ns, t_b = 10 ns, B = 8: m_min = 4. Time = 40 + 8 × 10 = 120 ns; the simple memory needs 8 × (40 + 10) = 400 ns.
With only m = 2 banks the sustained rate is one word per t_m / m = 20 ns — the banks, not the bus, are the bottleneck.

### 3.4 Low-order vs high-order interleaving

```
address = [ bank number | word within bank ]   high-order  : consecutive addresses stay in ONE bank;
                                                              banks = contiguous regions (also how chips expand a memory, §6)
address = [ word within bank | bank number ]   low-order    : consecutive addresses go to DIFFERENT banks (word i → bank i mod m)
```

Low-order interleaving is what speeds up sequential block reads. High-order is natural for size expansion and for letting independent masters work in different regions.

**Bank conflict.** With low-order interleaving over m banks and a constant stride s (words), the accesses touch only `m / gcd(s, m)` distinct banks, so sustained bandwidth is reduced by that
fraction. m = 8: stride 1 → 8 banks; stride 2 → 4; stride 3 → 8; stride 4 → 2; stride 6 → 4; stride 8 → 1 (every access hits the same bank). Using a **prime** number of banks
(e.g. 7) keeps all banks busy for any stride that is not a multiple of 7, at the price of a modulo-7 address decode.

### 3.5 Bandwidth formulas

```
Peak bandwidth of a simple memory     = (word size) / t_C
Peak, m banks, enough bus capacity    = m × (word size) / t_C                    (limited by bus: (word size)/t_b)
Sustained burst bandwidth             = (block bytes) / T_block
```

---

## 4. Average memory access time (AMAT)

This is the centre of the topic. **Every AMAT question is a weighted average over the events "hit at level 1", "hit at level 2", …,
weighted by the probability of each event and by the total time of that event.** The models differ only in what "total time of the event" means.

### 4.1 Single level, the two models

Cache time T_c, next-level (memory) time T_m, hit ratio h, miss ratio m = 1 − h.

| Model | What a miss costs | Formula |
|---|---|---|
| **Hierarchical / sequential** (cache is checked first; only then memory) | T_c + T_m (the failed lookup is wasted time) | T = h·T_c + m·(T_c + T_m) = **T_c + m·T_m** |
| **Simultaneous / look-aside** (cache and memory probed in parallel; memory request cancelled on a hit) | T_m only | T = h·T_c + m·T_m |
| **Additive penalty form** ("hit time + miss rate × miss penalty") | hit time + P | T = T_c + m·P |

Relationships (verified, Example 4.1):
- The additive form with P = T_m equals the hierarchical model.
- The additive form with P = T_m − T_c equals the simultaneous model.
- So hierarchical − simultaneous = m·T_c for a single level. For two levels the gap is m1·T1 + m1·m2·T2 (each level's access time times the probability of
  missing it); in general: each level except the last contributes T_i × (probability of missing level i).

**Example 4.1.** T_c = 5 ns, T_m = 50 ns, h = 0.8.
- Hierarchical: 5 + 0.2 × 50 = 15.0 ns.
- Simultaneous: 0.8 × 5 + 0.2 × 50 = 14.0 ns.
- Additive with P = T_m − T_c = 45: 5 + 0.2 × 45 = 14.0 ns.

### 4.2 Which model does the question mean? (do not pick silently)

GATE questions normally say which model — or give the sentence that determines it. Use this decision table:

| Wording in the question | Meaning |
|---|---|
| "a read takes X ns on a hit and Y ns on a miss" | X and Y are the **total event times**: T = h·X + (1−h)·Y. No ambiguity. |
| "hit time T_c and miss penalty P" | additive form: T = T_c + m·P |
| "first looks in L1, if not found goes to L2, if not found goes to memory" | hierarchical |
| "caches and memory are accessed simultaneously / in parallel" | simultaneous |
| access times T_c and T_m given, **nothing else** | **ambiguous**: hierarchical gives T_c + m·T_m, simultaneous gives h·T_c + m·T_m. |

What to do for the ambiguous row: compute both, look at the options. If only one value appears, that is the model the setter used. If both appear, the textbook
(Hennessy–Patterson) convention "hit time + miss rate × miss penalty" corresponds to the **hierarchical** model, and it matches how a typical cache behaves
(tag check first, then the next level). The risk is real: the two answers differ by m·T_c. Write the model you assume at the top of your working. I am not giving frequency statistics of which
model setters used; this repo has no verified data for that, so the safe habit is: read for the keywords in the table.

### 4.3 Two and three levels

Local hit ratios h_i (fraction of references reaching level i that hit there); T_i = time to access level i alone; the last level always hits.

```
Hierarchical:  T = T1 + m1·( T2 + m2·( T3 + m3·T4 ) )
               equivalently  = h1·T1 + m1·h2·(T1+T2) + m1·m2·h3·(T1+T2+T3) + m1·m2·m3·(T1+T2+T3+T4)

Simultaneous:  T = h1·T1 + m1·h2·T2 + m1·m2·h3·T3 + m1·m2·m3·T4
```

Evaluate **from the inside out**: compute the innermost bracket first (existing practice Q13).

**Example 4.2 (two levels).** T1 = 2, T2 = 20, T_mem = 100 ns; h1 = 0.9, h2 = 0.8 (local).
- Hierarchical: 2 + 0.1 × (20 + 0.2 × 100) = 2 + 0.1 × 40 = 6.0 ns.
- Simultaneous: 0.9 × 2 + 0.1 × 0.8 × 20 + 0.1 × 0.2 × 100 = 1.8 + 1.6 + 2.0 = 5.4 ns.
- Difference 0.6 = m1·T1 + m1·m2·T2 = 0.2 + 0.4. ✓.

**Example 4.3 (three levels).** T1 = 1, T2 = 5, T3 = 30, T_mem = 200 ns; h1 = 0.95, h2 = 0.8, h3 = 0.9.
- Hierarchical: 1 + 0.05 × (5 + 0.2 × (30 + 0.1 × 200)) = 1 + 0.05 × (5 + 0.2 × 50) = 1 + 0.05 × 15 = 1.75 ns.
- Simultaneous: 0.95 + 0.05·0.8·5 + 0.05·0.2·0.9·30 + 0.05·0.2·0.1·200 = 0.95 + 0.20 + 0.27 + 0.20 = 1.62 ns.

**Penalty-style data (additive extra latencies).** If the question gives "miss penalty L1→L2 = P12 and miss penalty memory→L2 = P2m", then
T = T1 + m1·(P12 + m2·P2m), with m2 the local L2 miss ratio. Example: T1 = 2, m1 = 0.08, P12 = 12, m2 = 0.25, P2m = 150: 2 + 0.08 × (12 + 37.5) = 5.96 ns.
Pitfall: the L2 hit ratio quoted in the question is usually local; multiply by m1 before using it as an overall fraction.

### 4.4 Local vs global miss ratios

```
local  miss ratio of L2 : m2 = (misses in L2) / (references reaching L2)
global miss ratio of L2 : g2 = (misses in L2) / (all processor references) = m1 × m2
```

Hierarchical AMAT in global terms: T = T1 + m1·T2 + g2·T3 (T_i the access time of level i; every reference pays T1, every L1 miss pays T2, every L2 miss pays T3).

**Example 4.4.** m1 = 0.08, local m2 = 0.25 → g2 = 0.02. With T1 = 2, T2 = 10, T_mem = 100: 2 + 0.08 × 10 + 0.02 × 100 = 4.8 ns = 2 + 0.08 × (10 + 0.25 × 100). If the question
gives g2 = 0.02 and m1 = 0.1, the local ratio is 0.02 / 0.1 = 0.2.

### 4.5 The block-transfer miss penalty

On a miss, the whole block is fetched. The miss penalty is the block-transfer time of §2.2–2.3 (or §3):

```
P = t_first + (W − 1) × t_next                     (burst memory)
```

Add that to the model in force. **Example 4.5.** Block 64 B, word 8 B ⇒ W = 8. t_first = 30 ns, t_next = 6 ns ⇒ P = 30 + 7 × 6 = 72 ns. Cache hit time 2 ns, h = 0.95.
- Hierarchical (the cache lookup of 2 ns happens, then the 72 ns block fetch): 2 + 0.05 × 72 = 5.6 ns.
- Simultaneous (memory started in parallel with the lookup): 0.95 × 2 + 0.05 × 72 = 5.5 ns.
- If the cache **restarts the CPU when the requested word arrives** (referred-word-first / critical-word-first), the CPU sees only t_first = 30 ns: 2 + 0.05 × 30 = 3.5 ns.
  (The rest of the block still streams in; a later access to the same block may be delayed — this is why simple questions state "assume…")

Traps: (i) word size in bits vs bytes — 64-bit word = 8 bytes, so a 256-byte block has 32 words; (ii) subsequent words are W − 1, not W; (iii) the hit time is paid in addition in the hierarchical model.

### 4.6 Reads, writes and instruction fetches

When the question separates reference types, compute a **per-type average** first, then weight by the reference mix (counts or percentages).

```
T = Σ_types  f_type × T_type        f_type = fraction of references of that type, Σ f = 1
T_type = h_type × (hit time of type) + m_type × (miss time of type)        (miss time as a total time) or via the model in force
```

**Example 4.6 (I-cache, D-cache, L2, hierarchical, reads only).** 70 % of reads are instruction fetches, 30 % data reads. I-cache: T = 1 ns, h = 0.9. D-cache: T = 1 ns, h = 0.85.
L2: T = 6 ns, local h = 0.8. Memory 60 ns. For an instruction fetch: 1 + 0.1 × (6 + 0.2 × 60) = 2.8 ns; for data: 1 + 0.15 × 18 = 3.7 ns. Average = 0.7 × 2.8 + 0.3 × 3.7 = 3.07 ns.
(Both L1 caches share the L2, so the same bracket (6 + 0.2 × 60) = 18 appears.)

**Example 4.7 (events with different times).** A trace has 120 instruction fetches, 50 data reads, 30 data writes. Times: read hit 2 ns, read miss 12 ns, write hit 3 ns, write miss 20 ns.
Hit ratio 0.95 for everything. Reads (instruction + data) = 170: 0.95 × 2 + 0.05 × 12 = 2.5 ns; writes: 0.95 × 3 + 0.05 × 20 = 3.85 ns. Average = (170 × 2.5 + 30 × 3.85) / 200 = 2.7025 ns.
Trap: the **weights are counts of each type over the total** (here 170/200 and 30/200), not 1/3 each, and not the hit ratio.

### 4.7 Write policies and their effect on time

| | Write-through | Write-back |
|---|---|---|
| On a write hit | update cache **and** memory | update cache only; set the **dirty** bit |
| Dirty bit | not needed (memory always up to date) | needed |
| Evicting a block | never needs a write to memory | write the block to memory **only if dirty** |
| Read miss | may replace a block, but the victim is never written back | **may evict a dirty block**, so a read miss can cost a write-back plus the fetch |
| Memory traffic | every store | only dirty replacements (repeated stores to a block cost one write-back) |
| Write miss | usually **no-write-allocate** (store goes to memory/buffer) — but write-allocate is possible | usually **write-allocate** (fetch block, then write) |
| Hides latency with | **write buffer** (CPU continues while the buffer drains) | fewer writes; a write-back buffer for the dirty victim |

Facts that statement-questions test (all follow from the table): a write buffer hides latency, it does not remove the memory writes; write-back needs a dirty bit; write-through
does not; the dirty bit of a write-back block can change on a write hit (0→1); a read miss in a write-back cache can write a dirty block to memory; a read miss in a write-through
cache cannot cause a write-back; whether a write miss evicts anything depends on allocate policy, not on write-through vs write-back alone.

**Timing models.**

```
Write-back, write-allocate :  miss penalty = P_fetch + d × P_writeback          d = probability that the victim is dirty
Write-through, no buffer   :  every store pays the memory write time t_w  (hit or miss)
Write-through, ideal buffer:  stores cost the cache write time (no stall), unless the buffer is full
Write buffer stalls        :  if stores arrive faster than memory drains them, the CPU waits; a buffer only helps when the average store rate < 1 per t_w
```

**Example 4.8 (write-back).** T_c = 2 ns, m = 0.04, block fetch 50 ns, block write-back 50 ns, 40 % of victims dirty: AMAT = 2 + 0.04 × (50 + 0.4 × 50) = 2 + 0.04 × 70 = 4.8 ns
(4.0 if you forget the write-backs; 6.0 if you assume every victim is dirty).

**Example 4.9 (write-through vs buffer).** 25 % stores. Reads: T_c = 1 ns, m = 0.05, P = 60 → 1 + 3 = 4.0 ns. Store goes straight to memory in 50 ns.
- No buffer: 0.75 × 4.0 + 0.25 × 50 = 15.5 ns.
- Ideal buffer (store takes the 1 ns cache write): 0.75 × 4.0 + 0.25 × 1 = 3.25 ns.
These are *models with stated assumptions* — in a real comparison against write-back, write-miss behaviour also matters.

### 4.8 Solving backwards

Most "find the unknown" questions are one linear/quadratic equation in the AMAT formula:

1. **Minimum hit ratio so the new design is not slower.** Old: T_old = T_c + m·P. New hit time T_c' (slower), same P: need T_c' + m'·P ≤ T_old ⇒ m' ≤ (T_old − T_c')/P ⇒ h' ≥ 1 − m'.
   Example: T_c = 4, h = 0.9, P = 60 ⇒ T_old = 10; new T_c' = 5 ⇒ m' ≤ 5/60 = 0.0833 ⇒ h' ≥ 0.9167 (0.92 to two decimals).
2. **Unknown miss ratios with a ratio constraint.** Write AMAT with m1 = k·m2, get a quadratic in m2, take the root in [0, 1]. Check by substituting back.
   Example: hierarchical, T1 = 1, T2 = 6, T_mem = 20 (cycles), AMAT = 1.8, m1 = 3·m2: 1 + 3m2(6 + 20m2) = 1.8 ⇒ 60m2² + 18m2 − 0.8 = 0 ⇒ m2 = 0.0393, m1 = 0.1179
   (under the simultaneous model the same data gives m2 = 0.0471, m1 = 0.1414 — model matters!).
3. **Smallest cache size from a miss-ratio curve.** Tabulate AMAT for each size and take the first that satisfies the target — mind **strict** "<" vs "≤".
   Example (buffer cache; T_c = 2 ms, disk 20 ms, target AMAT < 7 ms):

```
 size (MB)   miss ratio   hierarchical 2+20m   simultaneous 2(1−m)+20m
    10         0.60          14.0                 12.8
    20         0.40          10.0                  9.2
    30         0.25           7.0 (not < 7)        6.5
    40         0.15           5.0                  4.7
```
   Hierarchical ⇒ 40 MB (30 MB gives exactly 7.0, not less than 7); simultaneous ⇒ 30 MB. Another case where the model changes the answer.
   (A figure-based PYQ of this type exists; its figure is not in the mapping text — see [`PYQ.md`](PYQ.md).)

### 4.9 Speedup due to the memory system

```
Speedup of cache = (average time without cache) / (average time with cache)      (same reference stream)
```
Example: no cache, every reference 100 ns; AMAT with cache 5.6 ns ⇒ 100 / 5.6 = 17.86 (existing practice Q11 is this form).
Amdahl-style: if memory stalls are a fraction f of execution time and an improvement reduces them by a factor s, speedup = 1 / ((1 − f) + f / s) (see §5.3).

---

## 5. Effect on the CPU: CPI with memory stalls

**This folder is the home of the CPU-time-with-memory-stalls formulas.**

### 5.1 Formulas

```
CPU time        = IC × CPI_eff × T_clk
CPI_eff         = CPI_base + (memory stall cycles per instruction)
stall cycles/instr = (memory refs / instr) × (miss ratio) × (miss penalty in cycles)
                   = [ 1 × m_I × P_I ]  +  [ (data refs / instr) × m_D × P_D ]        (separate I- and D-cache)
miss penalty in cycles = miss penalty in ns / T_clk   (round UP if the memory is synchronous and the question asks for whole cycles)
two-level:  stalls/instr = refs/instr × ( m1 × P12_cycles + g2 × P2mem_cycles )         g2 = global L2 miss ratio
```

Assumptions that must be stated: **CPI_base already includes the cache-hit time** (so hits cost nothing extra); one instruction fetch per instruction (so I-cache references
per instruction = 1); data references per instruction = fraction of loads/stores (one data reference each); the CPU stalls for the whole miss penalty (no miss overlap); writes
count as D-cache references (a write-through buffer may remove their stall).

**Example 5.1.** CPI_base = 1.2; 2 GHz; I-miss 1 %, D-miss 4 %; 35 % loads/stores; memory miss penalty 80 ns.
Penalty = 80 ns × 2 GHz = 160 cycles. Stalls = 1 × 0.01 × 160 + 0.35 × 0.04 × 160 = 1.60 + 2.24 = 3.84. CPI_eff = 5.04. For 10^9 instructions: 10^9 × 5.04 × 0.5 ns = 2.52 s.

### 5.2 Comparing two cache designs

Compare **time per instruction**, not CPI: a design with a lower miss ratio may have a slower clock.

**Example 5.2.** Refs/instr = 1.4 (1 fetch + 0.4 data), CPI_base = 1.1, miss penalty fixed at 60 ns.
- Design A: direct mapped, T_clk = 0.50 ns, miss ratio 3 % ⇒ penalty 120 cycles ⇒ CPI = 1.1 + 1.4 × 0.03 × 120 = 6.14 ⇒ 3.07 ns/instr.
- Design B: 2-way, T_clk = 0.55 ns, miss ratio 2 % ⇒ penalty 60/0.55 = 109.09 → 110 cycles (rounded up) ⇒ CPI = 1.1 + 1.4 × 0.02 × 110 = 4.18 ⇒ 2.299 ns/instr (2.285 ns if the penalty is left fractional).
B is faster by 3.07 / 2.299 = 1.335 ×. Fixed-in-ns penalties give fewer cycles at a slower clock — a frequent source of mistakes.

### 5.3 Speedup with a perfect cache; Amdahl view

Perfect cache removes all stalls: speedup = CPI_eff / CPI_base.
Example: CPI_base = 2; I-miss 3 %, D-miss 6 %, 30 % loads/stores, penalty 50 cycles. Stalls = 1.5 + 0.9 = 2.4. CPI_eff = 4.4. Perfect-cache speedup = 4.4 / 2 = 2.2.
Amdahl: stall fraction f = 2.4 / 4.4 = 0.545; halving the penalty (s = 2) gives 1 / (0.4545 + 0.2727) = 1.375 = 4.4 / (2 + 1.2) ✓.
A limit view: even a perfect memory cannot give more than CPI_eff / CPI_base.

### 5.4 If the hit time is not in CPI_base

If a hit takes H cycles (e.g. 2) and CPI_base counted 1 cycle per access, add (H − 1) cycles per reference to the stalls, or work with AMAT in cycles:
`CPU time per instruction = (CPI_core_without_memory + refs/instr × (AMAT_cycles − 1)) × T_clk`. State your assumption.

---

## 6. Memory interfacing: building a big memory from small chips

### 6.1 Terms

```
A chip "K × N" has K locations (words) of N bits  → capacity K·N bits, log₂K address pins, N data pins, chip-select (CS), read/write.
System memory "M × W" : M locations, W-bit data bus.
Addressability: byte-addressable → each address names one byte; the data bus may still be 16/32 bits (then 2/4 byte lanes share an address).
```

### 6.2 Rules

```
chips in a ROW (to widen the data bus)   = ⌈W / N⌉      all chips in a row share address pins and chip-select
rows of chips (to add locations)         = ⌈M / K⌉
total chips                              = rows × columns = ⌈M/K⌉ × ⌈W/N⌉          (= total bits / chip bits if all divide evenly)
address lines of the system              = log₂ M
lines to every chip (internal address)   = log₂ K  (the LOW-order bits)
lines to the decoder (row select)        = log₂ M − log₂ K = log₂ (M/K)           (the HIGH-order bits)
decoder size                             = (log₂ rows)-to-(rows)   : e.g. 3-to-8, 2-to-4; outputs drive chip-select of each row
```

The picture (rows = high-order interleaving of §3.4):

```
 address A(a−1)…A(k) ──► decoder ──► CS_0 … CS_(r−1)             k = log₂ K
 address A(k−1)…A0   ──► all chips in parallel
 row 0: [chip][chip] … ← CS_0     (columns give data bits  D(N−1..0), D(2N−1..N), …)
 row 1: [chip][chip] … ← CS_1
```

**Example 6.1 — 64 KB byte-addressable from 16 K × 4 chips.** M = 64 K × 1 byte = 65 536 locations × 8 bits. Rows = 64 K / 16 K = 4, columns = 8 / 4 = 2 ⇒ 8 chips.
Address = 16 bits; chip address = A13…A0 (14 lines); A15…A14 → 2-to-4 decoder.
Address map (hex): row 0: 0000–3FFF; row 1: 4000–7FFF; row 2: 8000–BFFF; row 3: C000–FFFF.

**Example 6.2 — word-addressable 256 K words × 16 from 32 K × 4 chips.** Rows = 256 K / 32 K = 8; columns = 16 / 4 = 4 ⇒ 32 chips. Address = 18 bits; chip address = 15 bits (A14…A0);
A17…A15 → 3-to-8 decoder. Row r starts at r × 32 K: row 4 starts at 0x20000 and ends at 0x27FFF.

**Decoders from smaller decoders.** A 4-to-16 decoder = 1 + 4 decoders of 2-to-4 (the first selects which of the four second-stage ones is enabled by using their enable input).
Using bigger chips (larger K) reduces the number of rows, so the row-select decoder stays small.

### 6.3 Decoding variants

**Partial (incomplete) decoding / aliasing.** If some high address bits are not used in the chip-select, the memory appears **several times** (images, fold-back) in the address space.
Example: 16-bit address, 8 K RAM (13 internal lines), CS = A15 only. Then A14 and A13 are "don't care", so the RAM appears 2² = 4 times in 8000–FFFF.
Full decoding uses every upper bit and gives a unique address range.

**Non-contiguous chip selects.** The select bits need not be the top ones. Example: 8 KB byte-addressable memory (13-bit address) built from 4 blocks of 2 KB (11 internal lines),
decoder inputs A6, A5; block internal address lines = A12…A7 and A4…A0. Block i is selected when (A6A5) = i, so its lowest address (all other bits 0) is i × 32 = 0, 32, 64, 96 —
the blocks interleave in 32-byte stripes. Address 0x1A5 has A6A5 = 01, so it sits in block 1. Naive "address ÷ block size" is wrong here.
General rule: **the block is determined by the select bits, wherever they are; the chip's internal address is the remaining bits.**

**Memory map with ROM and RAM.** Example: 16-bit address bus. ROM 4 KB at 0000–0FFF: CS_ROM = ¬A15·¬A14·¬A13·¬A12. RAM 8 KB at 2000–3FFF (13 internal lines A12…A0): CS_RAM = ¬A15·¬A14·A13.
Unused: 1000–1FFF and 4000–FFFF (if nothing else is mapped). Overlaps are errors (two chips drive the bus).

**Unused address space.** A 32-bit address space with 256 MB installed leaves 2³² − 2²⁸ locations unmapped; accesses to them need a bus-error/default response.

**Byte lanes.** A 32-bit data bus with byte-addressable memory is built of four 8-bit-wide chip columns (or banks); the low 2 address bits are not sent to the chips (they select lanes /
byte-enables); the chips receive the word address A(k+1)…A2.

### 6.4 DRAM vs SRAM (only as it affects performance)

| | SRAM | DRAM |
|---|---|---|
| Cell | 6 transistors (flip-flop) | 1 transistor + 1 capacitor |
| Speed, cost per bit | faster, costlier | slower, cheap |
| Refresh | none | needed (charge leaks); read is destructive and restored |
| Use | caches, register files | main memory |
| Address pins | all at once | **multiplexed**: row address then column address (RAS/CAS); a 2²⁴-location 1-bit chip needs 12 address pins |

Why the access time ≠ cycle time for DRAM: precharge/restore after the read.

**Refresh overhead.**

```
overhead fraction = (number of rows × time per row refresh) / (refresh period)         (all chips refreshed in PARALLEL; one row per refresh operation)
time available for reads/writes = 1 − overhead
distributed refresh: one row every (refresh period / rows)
burst refresh      : all rows back to back, memory unavailable for rows × t_refresh, once per refresh period
```
**Example 6.3.** 8192 rows, 60 ns per row refresh, 64 ms period: 8192 × 60 ns = 491.52 µs per period ⇒ 0.768 % overhead; 99.232 % of time is available. Distributed: a refresh every
64 ms / 8192 = 7.8125 µs. If the question states that 4 chips are refreshed one after another (not in parallel), the busy time is 4 × 491.52 µs ⇒ 3.072 %.
(A chip with 2ⁿ cells arranged as a square array has 2^(n/2) rows. Use the number of rows the question gives, and do not confuse the number of chips with the number of rows.)

---

## 7. Putting it together: a GATE-solving procedure

1. **Classify**: AMAT (which model?), CPI/CPU time, bandwidth/block time, interfacing/decoder, refresh, VM bridge, or statement-truth.
2. **Write the units**: ns vs cycles; bytes vs words vs bits; K = 2^10 for sizes; MHz = 10^6 for rates.
3. **State the model**: hierarchical / simultaneous / additive; local vs global ratios; whether the hit time is included in CPI_base.
4. **Compute inside-out** for nested AMAT; compute per-type averages first for mixed reference streams.
5. **Check limits**: AMAT must be between T1 and the total worst-case path (T1 + T2 + … for hierarchical); a probability must lie in [0, 1]; CPI_eff ≥ CPI_base.
6. **Check the form of the answer**: NAT precision, MCQ distractors (they usually correspond to the common model/units mistakes — see §10).

---

## 8. Prerequisite / bridge: virtual memory effective access time

*Owned by [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/). Only the formulas GATE asks as memory-hierarchy numerics are given here.*

Symbols: t_tlb = TLB lookup time, t_m = main-memory access time, α = TLB hit ratio, k = number of page-table levels, p = page-fault probability per reference, S = page-fault service time.

```
TLB hit          : t_tlb + t_m                                  (translation from TLB, then the data access)
TLB miss         : t_tlb + k·t_m + t_m = t_tlb + (k+1)·t_m       (k page-table reads, then the data access; page table in memory)
EAT (no faults)  : α·(t_tlb + t_m) + (1−α)·(t_tlb + (k+1)·t_m)
if the TLB lookup is overlapped / "negligible": drop t_tlb
page faults      : EAT_total = (1 − p)·EAT_no_fault + p·S       (S is the TOTAL time of a faulting access; if the question gives an EXTRA service time, add it to EAT_no_fault instead)
rare faults      : EAT ≈ EAT_no_fault + p·S                     (the "disk penalty × rare event" is often as large as the base time — existing practice Q10)
```
Memory-as-cache view: if a faulting access costs D on average and a normal access M, the measured average X = (1−p)·M + p·D, so p = (X − M)/(D − M).

**Example 8.1.** t_tlb = 5 ns, t_m = 80 ns, 2-level page table, α = 0.9. Hit: 85 ns. Miss: 5 + 3 × 80 = 245 ns. EAT = 0.9 × 85 + 0.1 × 245 = 76.5 + 24.5 = 101.0 ns.
If the TLB lookup time is ignored: 0.9 × 80 + 0.1 × 240 = 96.0 ns.

**Example 8.2 (page faults).** Normal EAT 100 ns, a faulting access takes 8 ms = 8 × 10^6 ns, p = 2 × 10^-6: EAT = (1 − 2×10^-6)·100 + 2×10^-6·8×10^6 ≈ 116.0 ns. A fault every 500 000 accesses
adds 16 ns to a 100 ns access — 16 %.

**Example 8.3 (design target).** With the data of 8.1, what α gives EAT ≤ 110 ns? 85α + 245(1 − α) ≤ 110 ⇒ 245 − 160α ≤ 110 ⇒ α ≥ 135/160 = 0.84375.

(A cache between the CPU and memory changes t_m into an AMAT; combining both gives nested averages — compute the memory-side AMAT first, then use it as t_m.)

---

## 9. PYQ patterns (recipes, no answers)

The mapping file for this folder is empty. The patterns below come from the performance-type entries that sit in the cache folder's mapping and a few found elsewhere (listed in [`PYQ.md`](PYQ.md)). No official answers are given.

| # | Pattern (recognise by) | Recipe | Trap |
|---|---|---|---|
| P1 | Basic one-level AMAT with "read takes X on hit, Y on miss" | h·X + (1−h)·Y | adding hit time again (X, Y are totals) |
| P2 | Two-level AMAT from a figure of hit rates and times (figure not available in mapping) | model from wording; inside-out | local vs global hit rates; forgetting the hit time of L1 on every reference |
| P3 | Solve for miss rate(s) from a given AMAT with a ratio relation between levels | write the equation with the model; unknown m2; quadratic; check | root outside [0, 1]; swapped m1, m2; wrong model |
| P4 | "Minimum hit rate such that the optimised cache is no slower" | T' ≤ T_old ⇒ solve for m' ; h' = 1 − m' | rounding direction (round the hit rate up so the condition still holds, then quote what the question asks) |
| P5 | Block-transfer penalty: first word + subsequent words, word size in bits, block in bytes | W = block bytes / word bytes; P = t_first + (W − 1)t_next; plug into the model | W vs W − 1; word 64-bit = 8 B |
| P6 | Memory-system bandwidth with controller cycles, fetch cycles and 1 word/cycle transfer | cycles per block = sum of non-overlapped stages; time = cycles / f; BW = block bytes / time | MB/s vs MiB/s; counting fetch cycles per word |
| P7 | Weighted average over I-cache, D-cache, L2 with fractions | per-stream hierarchical time, then weights | weights not summing to 1; ignoring the shared L2 |
| P8 | Weighted average over reads / writes / fetches with different hit/miss times | totals per type then count-weighted average | using 1/3 each |
| P9 | Time to move a block between levels with different block sizes and bus widths (figure partly missing) | ⌈block words / bus words⌉ × access time per level; sum the sequential moves | using the wrong block size for the level |
| P10 | WB vs WT statements | table in §4.7 | confusing victim-dirty with write-hit |
| P11 | Block-size effect statements | §1.4 | "smaller block ⇒ better spatial locality" |
| P12 | Inclusion conditions | §1.5 | treating design choices as logical requirements |
| P13 | CPI with I/D miss rates, penalty, speedup with perfect cache | §5.1, §5.3 | applying the data-miss rate to all instructions; forgetting one fetch per instruction |
| P14 | DRAM refresh % (chip rows, ns per row, ms period) | §6.4 | counting chips instead of rows, ms vs ns |
| P15 | Decoder + memory blocks: start address of each block, decoder size | §6.2–6.3 | assuming contiguous blocks when select bits are not the top bits |
| P16 | EAT with TLB, page-table levels, page faults | §8 | forgetting the final data access; page-table walk uses memory not TLB |

---

## 10. Traps and misconceptions

1. **Using hit ratio where miss ratio belongs** (and the reverse) — e.g. T_c + h·P.
2. **Model mix-up**: applying the simultaneous formula to a "first checks L1, then L2" statement, or forgetting that the hierarchical model repeats T1 on a miss.
3. **Local vs global**: treating the quoted L2 hit ratio as overall.
4. **Penalty vs total time**: a "miss penalty" is *extra*; a "miss time" is *total*. Never add the hit time twice when the number is a total.
5. **Block penalty**: W − 1 subsequent words; words vs bytes vs bits.
6. **Rate units**: MHz and MB/s are decimal; sizes are binary. 1 cycle at 60 MHz = 16.67 ns.
7. **ns vs cycles** in CPI formulas; mixing a penalty in ns with a clock in GHz without converting.
8. **Average CPI vs time**: a faster clock can offset a worse CPI; compare times.
9. **Interleaving**: more banks help only when the access pattern spreads over them (stride); and only up to the bus rate.
10. **Write-back** reduces traffic but increases the penalty of a miss with a dirty victim.
11. **Refresh**: overhead uses rows per chip × per-row time, not chip count.
12. **Interfacing**: assuming blocks are contiguous; forgetting that the chip receives the low-order bits and the decoder the high-order bits; forgetting data-width columns.
13. Fully associative removes conflict misses only; capacity misses stay.

### Edge cases and assumptions to state

- hit time included or not in CPI_base; one fetch per instruction; no miss overlap; stalls for the whole penalty.
- hierarchical vs simultaneous; local vs global; write-through with/without buffer; write-allocate or not.
- block restart on the critical word or only after the whole block.
- unit conventions (K, M, MHz, MB/s); byte vs word addressing.
- the last level always hits (a miss in memory is a page fault in §8).
- AMAT is an **average**; it says nothing about the worst-case time of one access.

---

## 11. Connections to other COA topics

- **Cache mapping** ([`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/)): decides h; this folder turns h into time.
- **Pipelining and hazards**: a memory stall is another stall cycle in CPI_pipelined = 1 + average stall cycles per instruction; the I-cache miss stalls IF, the D-cache miss stalls MEM.
- **I/O and DMA**: DMA and the CPU compete for memory cycles; the cycle-time concept of §2 gives the available bandwidth.
- **Addressing modes / instruction set**: loads/stores per instruction (the data-reference rate used in §5).
- **Digital Logic**: decoders, multiplexers, flip-flop vs capacitor cells; number representation for hex address ranges.
- **Operating Systems**: virtual memory and TLB (§8), page replacement affects p.

---

## 12. Existing practice coverage map

The existing file [`practice.md`](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/practice.md) (14 questions). The map gives only the skill and where to learn it.

| Q# | Skill | NOTES section |
|---|---|---|
| 1 | spatial + temporal locality | §1.2 |
| 2 | miss ratio = 1 − hit ratio | §1.3 |
| 3 | percent conversion | §1.3 |
| 4 | AMAT with the additive formula | §4.1 |
| 5 | effect of changing the miss ratio on AMAT | §4.1, §1.6 |
| 6 | block size, miss types, associativity | §1.3, §1.4 |
| 7 | AMAT from hit ratio | §4.1 |
| 8 | two-level extra-latency AMAT | §4.3 (penalty-style data) |
| 9 | CPI with I- and D-cache stalls | §5.1 |
| 10 | page-fault average access time | §8 |
| 11 | speedup of cache over no cache | §4.9 |
| 12 | write-through vs write-back statements | §4.7 |
| 13 | three-level nested AMAT | §4.3 |
| 14 | comparing two design changes via AMAT | §1.6, §4.1 |

The existing file defines its own formula "AMAT = T_hit + miss rate × miss penalty (penalty is extra)" (the additive form). If you move to a PYQ, confirm that model with the question text (§4.2).

---

## 13. Self-check

1. State the formula for AMAT in the hierarchical and simultaneous models and give the difference for one level.
2. Why is the L2 hit ratio usually local, and how do you convert to a global miss ratio?
3. What is the miss penalty for a 128-byte block, 8-byte word, 40 ns first word, 5 ns subsequent words?
4. Write CPI_eff for separate I- and D-caches and convert a penalty from ns to cycles.
5. How does write-through differ from write-back in dirty bit, eviction, read-miss behaviour and traffic?
6. How many banks are needed for one word per t_b if a bank needs t_m between starts?
7. What does stride 4 do to an 8-bank low-order interleaved memory?
8. How many chips and what decoder to build 128 K × 16 from 32 K × 8 chips?
9. Why can a memory built with the decoder on middle address bits have non-contiguous blocks?
10. What fraction of time is lost to refresh for R rows, t per row, period T?
11. Write the EAT formula with a TLB and a k-level page table.
12. Which of the quantities "capacity, cost per bit, access time" increase as you go down the hierarchy?

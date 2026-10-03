# Memory Hierarchy Performance and Interfacing — PRACTICE

25 original questions (not from GATE papers; not copied from the existing practice file). Solve from [`NOTES.md`](NOTES.md). Answers are directly under each question; try first.
Conventions: K = 2^10, M = 2^20 for sizes; MHz = 10^6 and MB/s = 10^6 B/s for rates; hit ratios of lower levels are local unless stated. All answers were checked by script.

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1

A program makes **one pass** over a very large array `a[0 … 999999]` stored contiguously, adding each element once to a variable `total` that lives in memory. Which statement about locality is correct?

A. `total` shows spatial locality only; `a[i]` shows temporal locality only
B. `total` shows temporal locality; the sequential scan of `a[i]` shows spatial locality
C. both show temporal locality only
D. both show spatial locality only

**Answer:** B

**Solution:** `total` is read and written again and again — the same location is reused soon after it was used: temporal. Each `a[i]` is used only once in this pass (no temporal reuse) but its neighbours are used right after it: spatial. A is the reverse; C and D each deny one kind that is clearly present.

**Concept tested:** temporal vs spatial locality (NOTES §1.2).
**Difficulty:** Easy.
**Common trap:** calling every cache benefit "temporal"; ignoring that a single pass over an array has no reuse of the elements.

### Q2 — MSQ — Level 1 (one or more options correct; no partial marking)

Which statements about the memory hierarchy are correct?

A. Moving from registers down to secondary storage, the cost per bit generally decreases.
B. Moving down the hierarchy, the access time generally increases.
C. The hierarchy gives a low average access time because most references are satisfied by the upper, small levels, thanks to locality.
D. If the L1 hit ratio is 99 %, the average access time is essentially the access time of the next lower level.

**Answer:** A, B, C

**Solution:** A and B are the basic cost/speed gradient. C is the reason the hierarchy works. D is false: with a 99 % hit ratio, average time ≈ T1 + 0.01 × (penalty) — it stays close to T1 unless the penalty is huge (e.g. T1 = 1, penalty 100 ⇒ 2).

**Concept tested:** hierarchy properties, AMAT dominance of hits (NOTES §1.1, §1.6).
**Difficulty:** Easy.
**Common trap:** thinking a few misses make the lower level's speed dominate.

### Q3 — MCQ — Level 1

A memory has access time 50 ns and cycle time 70 ns; one word is read per access. What is the maximum number of back-to-back random read accesses per second?

A. 20.00 × 10^6
B. 14.29 × 10^6
C. 8.33 × 10^6
D. 50.00 × 10^6

**Answer:** B

**Solution:** A new access can start only every cycle time: 1 / 70 ns = 14.2857 × 10^6 per second. A uses the access time (50 ns); C uses 50 + 70 = 120 ns; D uses 20 ns (the difference).

**Concept tested:** access time vs cycle time (NOTES §2.1).
**Difficulty:** Easy.
**Common trap:** using the access time for the rate.

### Q4 — NAT — Level 1

A cache has a hit ratio of 0.985. On average, how many references out of every 1000 are misses?

**Answer:** 15

**Solution:** miss ratio = 1 − 0.985 = 0.015; 0.015 × 1000 = 15.

**Concept tested:** hit/miss ratio (NOTES §1.3).
**Difficulty:** Easy.
**Common trap:** reporting 985 or 1.5.

---

## Level 2 — Standard GATE

### Q5 — NAT — Level 2

A cache has access time 4 ns and hit ratio 0.95. Main memory has access time 80 ns. The memory is accessed **only after** the cache lookup has missed (the 4 ns lookup is wasted on a miss). Average memory access time in ns?

**Answer:** 8.0

**Solution:** hierarchical: T = T_c + m·T_m = 4 + 0.05 × 80 = 4 + 4 = 8.0 ns. (Check as events: 0.95 × 4 + 0.05 × (4 + 80) = 3.8 + 4.2 = 8.0.)

**Concept tested:** hierarchical single-level AMAT (NOTES §4.1).
**Difficulty:** Easy.
**Common trap:** using 0.95·4 + 0.05·80 = 7.8 (the other model).

### Q6 — MCQ — Level 2

Same hardware as Q5 (T_c = 4 ns, T_m = 80 ns, hit ratio 0.95). By how much is the AMAT of the **sequential** (memory after miss) design larger than that of the **simultaneous** (cache and memory probed in parallel) design?

A. 0.2 ns
B. 0.4 ns
C. 3.8 ns
D. 4.0 ns

**Answer:** A

**Solution:** sequential 8.0 ns, simultaneous 0.95 × 4 + 0.05 × 80 = 7.8 ns. Difference = m × T_c = 0.05 × 4 = 0.2 ns. B doubles it, C = 0.95 × 4 and D = T_c are not the gap.

**Concept tested:** gap between the two models (NOTES §4.1, SHORTCUTS S2).
**Difficulty:** Medium.
**Common trap:** thinking the gap equals the hit time.

### Q7 — NAT — Level 2

A cache has hit time 3 ns and hit ratio 0.97. A miss fetches a 128-byte block from a burst memory: the first 8-byte word takes 50 ns and each following word 8 ns. Use hit time + miss ratio × (block fetch time). Average memory access time in ns (1 decimal)?

**Answer:** 8.1

**Solution:** W = 128 / 8 = 16 words. P = 50 + (16 − 1) × 8 = 50 + 120 = 170 ns. AMAT = 3 + 0.03 × 170 = 3 + 5.1 = 8.1 ns.

**Concept tested:** block-transfer miss penalty (NOTES §4.5).
**Difficulty:** Medium.
**Common trap:** using 16 × 8 or 16 × 50 as the penalty; using W instead of W − 1.

### Q8 — NAT — Level 2

A cache miss is served as follows: the controller needs 1 clock cycle to accept the block address, 4 cycles to fetch the block, and then sends the 16 words (4 bytes each) of the 64-byte block at one word per cycle. The stages happen one after the other. The memory clock is 100 MHz. The bandwidth for back-to-back block reads, in MB/s (10^6 bytes/s), to 2 decimals?

**Answer:** 304.76

**Solution:** cycles per block = 1 + 4 + 16 = 21; period = 10 ns ⇒ 210 ns. Bandwidth = 64 B / 210 ns = 304.76 × 10^6 B/s.

**Concept tested:** burst bandwidth (NOTES §2.2).
**Difficulty:** Medium.
**Common trap:** forgetting the fetch cycles, or using 2^20 B/s; counting 16 × (1 + 4) cycles.

### Q9 — MCQ — Level 2

A low-order interleaved memory has banks that each need 60 ns between the start of two accesses. The bus transfers one word every 15 ns and bank starts are staggered by one bus slot. What is the minimum number of banks needed so that the bus delivers one word every 15 ns?

A. 2
B. 3
C. 4
D. 6

**Answer:** C

**Solution:** m ≥ t_m / t_b = 60 / 15 = 4. With 3 banks a bank would be needed again after 45 ns, before its 60 ns are over. 6 works but is not the minimum. For a 16-word block: 60 + 16 × 15 = 300 ns, versus a simple memory: 16 × (60 + 15) = 1200 ns.

**Concept tested:** number of banks (NOTES §3.3).
**Difficulty:** Medium.
**Common trap:** t_m / t_b − 1; or picking 2 because "both banks run in parallel".

---

## Level 3 — Multi-step

### Q10 — NAT — Level 3

Hierarchical access. L1: 1 ns, hit ratio 0.92. L2: 8 ns, local hit ratio 0.75. L3: 40 ns, local hit ratio 0.90. Main memory: 300 ns (always hits). Average memory access time in ns (2 decimals)?

**Answer:** 3.04

**Solution:** inside-out: 40 + 0.1 × 300 = 70; 8 + 0.25 × 70 = 25.5; 1 + 0.08 × 25.5 = 1 + 2.04 = 3.04 ns.

**Concept tested:** three-level hierarchical AMAT (NOTES §4.3).
**Difficulty:** Medium.
**Common trap:** using global instead of local ratios; evaluating outside-in.

### Q11 — NAT — Level 3

Hierarchical access, T1 = 2 ns, T2 = 12 ns, T_mem = 120 ns. The L1 miss ratio is 0.06; 1.5 % of **all** processor references miss in both L1 and L2. Average memory access time in ns (2 decimals)?

**Answer:** 4.52

**Solution:** global L2 miss ratio g2 = 0.015 (local m2 = 0.015 / 0.06 = 0.25). T = T1 + m1·T2 + g2·T_mem = 2 + 0.06 × 12 + 0.015 × 120 = 2 + 0.72 + 1.8 = 4.52 ns (equals 2 + 0.06 × (12 + 0.25 × 120)).

**Concept tested:** local vs global miss ratio (NOTES §4.4).
**Difficulty:** Medium.
**Common trap:** multiplying 0.015 by 0.06 again.

### Q12 — NAT — Level 3

A processor has base CPI 1.25 (all cache hits included) and a 2.5 GHz clock. Instruction cache miss ratio 2 %, data cache miss ratio 6 %, 30 % of instructions are loads/stores (one data reference each), and every miss costs 40 ns. The CPU stalls for the whole miss. The execution time of 2 × 10^9 instructions in seconds (2 decimals)?

**Answer:** 4.04

**Solution:** penalty = 40 ns × 2.5 GHz = 100 cycles. Stalls per instruction = 1 × 0.02 × 100 + 0.30 × 0.06 × 100 = 2 + 1.8 = 3.8. CPI = 1.25 + 3.8 = 5.05. Period = 0.4 ns. Time = 2 × 10^9 × 5.05 × 0.4 ns = 4.04 s.

**Concept tested:** CPI with memory stalls, CPU time (NOTES §5.1).
**Difficulty:** Medium.
**Common trap:** applying the data miss ratio to all instructions; skipping the fetch stalls; using 40 cycles for 40 ns.

### Q13 — MCQ — Level 3

A write-back cache with write-allocate has hit time 2 ns and miss ratio 0.04. Fetching a block takes 50 ns, writing a dirty block back takes 50 ns, and 40 % of the replaced blocks are dirty. The fetch and the write-back are done one after the other. What is the AMAT (hierarchical, penalty form)?

A. 4.0 ns
B. 4.8 ns
C. 6.0 ns
D. 2.8 ns

**Answer:** B

**Solution:** P = 50 + 0.4 × 50 = 70 ns; AMAT = 2 + 0.04 × 70 = 4.8 ns. A ignores the write-back; C assumes every victim is dirty (2 + 0.04 × 100); D includes only the write-back term (2 + 0.04 × 0.4 × 50).

**Concept tested:** write-back penalty with dirty probability (NOTES §4.7).
**Difficulty:** Medium.
**Common trap:** forgetting the probability d.

### Q14 — NAT — Level 3

Reads only, hierarchical. 65 % of reads are instruction fetches (I-cache: 1 ns, hit ratio 0.9); 35 % are data reads (D-cache: 2 ns, hit ratio 0.85). Both L1 caches miss to a shared L2 (10 ns, local hit ratio 0.8); main memory 100 ns. Average read time in ns (3 decimals)?

**Answer:** 4.875

**Solution:** L2+memory bracket = 10 + 0.2 × 100 = 30. Instruction: 1 + 0.1 × 30 = 4.0. Data: 2 + 0.15 × 30 = 6.5. Average = 0.65 × 4.0 + 0.35 × 6.5 = 2.6 + 2.275 = 4.875 ns.

**Concept tested:** weighted average over reference streams (NOTES §4.6).
**Difficulty:** Medium.
**Common trap:** averaging 4.0 and 6.5 equally (5.25).

### Q15 — NAT — Level 3

A byte-addressable memory of 1 MB (1 M locations of 8 bits) is built from 128 K × 4-bit chips. How many chips are needed?

**Answer:** 16

**Solution:** columns = 8 / 4 = 2 (to form 8 data bits); rows = 1 M / 128 K = 8 ⇒ 8 × 2 = 16 chips. (Address: 20 bits, 17 to each chip, 3 to a 3-to-8 decoder.) Total bits check: 8 Mbit / 512 Kbit = 16.

**Concept tested:** chip count (NOTES §6.2).
**Difficulty:** Easy–Medium.
**Common trap:** forgetting the width factor (answer 8).

### Q16 — NAT — Level 3 (bridge: virtual memory)

TLB lookup 10 ns, main-memory access 100 ns, a 3-level page table held in memory, TLB hit ratio 0.95. On a TLB hit, translation comes from the TLB; on a miss, the three page-table entries are read from memory one after another, then the data is read. No page faults. Effective access time in ns (1 decimal)?

**Answer:** 125.0

**Solution:** hit: 10 + 100 = 110 ns. Miss: 10 + 3 × 100 + 100 = 410 ns. EAT = 0.95 × 110 + 0.05 × 410 = 104.5 + 20.5 = 125.0 ns.

**Concept tested:** EAT with TLB (NOTES §8).
**Difficulty:** Medium.
**Common trap:** counting only the three table reads and forgetting the final data access.

---

## Level 4 — Tricky / trap-based

### Q17 — NAT — Level 4

A cache has hit time 3 ns, hit ratio 0.90, and miss penalty 50 ns. A redesign raises the hit time to 4 ns and leaves the penalty unchanged. What is the minimum hit ratio (2 decimals) so that the redesign is **not slower** than the original? Use hit time + miss ratio × penalty.

**Answer:** 0.92

**Solution:** original AMAT = 3 + 0.1 × 50 = 8.0 ns. Need 4 + m' × 50 ≤ 8 ⇒ m' ≤ 0.08 ⇒ h' ≥ 0.92.

**Concept tested:** break-even hit ratio (NOTES §4.8).
**Difficulty:** Medium.
**Common trap:** using the hit-time increase of 1 ns as a fraction of the hit ratio (0.91); mixing hit and miss ratios.

### Q18 — MSQ — Level 4 (one or more options correct; no partial marking)

Which statements about write policies are correct?

A. In a write-through cache with no write buffer and no overlap, a store stalls the CPU for the memory write time.
B. A read miss in a write-back cache can cause a write to main memory.
C. In a write-back cache, the average miss penalty depends on the fraction of replaced blocks that are dirty.
D. A write buffer removes all memory write traffic of a write-through cache.

**Answer:** A, B, C

**Solution:** A is the definition of the unbuffered model. B: the victim of the read miss may be dirty and must be written back. C: P = P_fetch + d × P_writeback. D is false: a buffer only hides the latency; every store is still written to memory.

**Concept tested:** write policies (NOTES §4.7).
**Difficulty:** Medium.
**Common trap:** thinking write buffering reduces the amount of write traffic.

### Q19 — NAT — Level 4

A DRAM memory has 4096 rows per chip; one refresh operation (one row, all chips in parallel) takes 50 ns, and every row must be refreshed once per 32 ms. What percentage of time is available for normal reads and writes (2 decimals)?

**Answer:** 99.36

**Solution:** refresh time per period = 4096 × 50 ns = 204.8 µs. Fraction = 204.8 µs / 32 ms = 0.0064 = 0.64 %. Available = 100 − 0.64 = 99.36 %.

**Concept tested:** refresh overhead (NOTES §6.4).
**Difficulty:** Medium.
**Common trap:** µs vs ms; multiplying by the number of chips even though the refresh is in parallel.

### Q20 — MCQ — Level 4

A 16 KB byte-addressable memory (14-bit address A13…A0) is built from four 4 KB blocks (12 address lines each). The inputs of the 2-to-4 decoder driving the block chip-selects are A7 and A6; the address lines to every block are A13…A8 and A5…A0. For address 0x2D9, which block holds the byte, and what is the lowest address (all non-select bits 0) in that block?

A. block 0, address 0x000
B. block 3, address 0x0C0
C. block 3, address 0x3000
D. block 2, address 0x080

**Answer:** B

**Solution:** 0x2D9 = 10 1101 1001₂ (bit 9 … bit 0). A7 = 1, A6 = 1 ⇒ block 3. The block's lowest address is when every other bit is 0: A7A6 = 11 ⇒ 192 = 0xC0. A assumes contiguous blocks (0x2D9 / 0x1000 = 0); C uses contiguous start 3 × 0x1000; D reads the wrong bits.

**Concept tested:** non-contiguous chip-select bits (NOTES §6.3).
**Difficulty:** Hard.
**Common trap:** block number = address ÷ block size.

### Q21 — NAT — Level 4

A processor has a 20-bit address bus. A 16 KB RAM (14 internal address lines) has its chip select asserted when A19 = 1 and A18 = 0; A17…A14 are not connected to the decoding logic. At how many different 20-bit addresses does the same RAM byte appear (images)?

**Answer:** 16

**Solution:** internal lines A13…A0; decoded A19, A18; the four unused bits A17…A14 are don't-care ⇒ 2^4 = 16 images. Check: the selected region is A19A18 = 10, i.e. 2^18 addresses = 16 × 16 KB ✓.

**Concept tested:** partial decoding / aliasing (NOTES §6.3).
**Difficulty:** Medium.
**Common trap:** counting only the decoded bits; answering 1 or 4.

### Q22 — MSQ — Level 4 (one or more options correct; no partial marking)

An 8-bank memory is low-order interleaved by word. A program accesses words at a constant stride s (in words), starting at address 0, many times. For which strides do the accesses spread over all 8 banks?

A. s = 1
B. s = 6
C. s = 7
D. s = 12

**Answer:** A, C

**Solution:** banks used = 8 / gcd(s, 8). s = 1: gcd 1 ⇒ 8. s = 6: gcd 2 ⇒ 4. s = 7: gcd 1 ⇒ 8. s = 12: gcd 4 ⇒ 2. So only A and C.

**Concept tested:** bank conflicts (NOTES §3.4).
**Difficulty:** Medium.
**Common trap:** assuming any stride that is not 8 uses all banks.

---

## Level 5 — Challenge

### Q23 — MCQ — Level 5

A two-level cache is accessed hierarchically (L2 only after an L1 miss). T1 = 1 cycle, T2 = 6 cycles, main memory 20 cycles (all access times). The L1 miss ratio is three times the **local** L2 miss ratio, and the AMAT is 1.8 cycles. The L1 and L2 miss ratios respectively are approximately:

A. 0.118 and 0.039
B. 0.039 and 0.118
C. 0.141 and 0.047
D. 0.060 and 0.020

**Answer:** A

**Solution:** AMAT = 1 + m1 (6 + m2 × 20) with m1 = 3 m2: 1 + 3 m2 (6 + 20 m2) = 1.8 ⇒ 60 m2² + 18 m2 − 0.8 = 0 ⇒ m2 = (−18 + √(324 + 192)) / 120 = 0.0393 ⇒ m1 = 0.1179. Check: 1 + 0.1179 × (6 + 0.786) = 1.80. B swaps the two; C is the solution of the simultaneous-access model (0.141, 0.047), which gives 1.98 here; D gives 1.38.

**Concept tested:** solving for miss ratios (NOTES §4.8).
**Difficulty:** Hard.
**Common trap:** wrong model; choosing the negative root.

### Q24 — NAT — Level 5

Two cache designs for the same program (base CPI 1.0 with hits included, 1.3 memory references per instruction). Memory miss time is 75 ns, converted to a **whole number of clock cycles (round up)**. Design X: clock 0.8 ns, miss ratio 4 %. Design Y: clock 0.9 ns, miss ratio 2.5 %. What is (time per instruction of X) / (time per instruction of Y), to 2 decimals?

**Answer:** 1.40

**Solution:** X: 75 / 0.8 = 93.75 ⇒ 94 cycles; CPI = 1.0 + 1.3 × 0.04 × 94 = 5.888; time = 5.888 × 0.8 = 4.7104 ns. Y: 75 / 0.9 = 83.33 ⇒ 84 cycles; CPI = 1.0 + 1.3 × 0.025 × 84 = 3.73; time = 3.73 × 0.9 = 3.357 ns. Ratio = 4.7104 / 3.357 = 1.403 ≈ 1.40. (Without the ceiling: 4.7 / 3.3375 = 1.408 ≈ 1.41.)

**Concept tested:** comparing designs by time, integer cycles (NOTES §5.2).
**Difficulty:** Hard.
**Common trap:** comparing CPI only; not rounding the penalty up.

### Q25 — NAT — Level 5

A program has base CPI 1.6 (hits included), instruction-cache miss ratio 4 %, 25 % loads/stores with data-cache miss ratio 10 %, miss penalty 40 cycles. A prefetcher removes 60 % of all misses (instruction and data) and has no other effect. What is the speedup (2 decimals)?

**Answer:** 1.59

**Solution:** stalls = 1 × 0.04 × 40 + 0.25 × 0.10 × 40 = 1.6 + 1.0 = 2.6; CPI = 4.2. After the prefetcher: stalls = 0.4 × 2.6 = 1.04; CPI = 2.64. Speedup = 4.2 / 2.64 = 1.59.

**Concept tested:** CPI with stalls, Amdahl-style improvement (NOTES §5.3).
**Difficulty:** Medium–Hard.
**Common trap:** applying the 60 % reduction to the whole CPI (that would give a speedup of 1 / 0.4 = 2.5) instead of only to the stall part.

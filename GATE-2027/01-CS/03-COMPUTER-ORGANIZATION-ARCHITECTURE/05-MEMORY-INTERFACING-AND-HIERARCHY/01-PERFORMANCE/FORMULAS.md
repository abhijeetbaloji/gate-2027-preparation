# Memory Hierarchy Performance and Interfacing — FORMULAS

Every formula: statement, symbols, when it applies, why, example (all examples script-verified), common misuse.
Conventions: sizes K = 2^10, M = 2^20; rates MHz = 10^6 Hz, MB/s = 10^6 B/s; h = hit ratio, m = 1 − h; lower-level hit ratios are **local** unless stated.
Details and derivations: [`NOTES.md`](NOTES.md). Cache address-split formulas (tag/index/offset) live in [`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/).

Contents: A. Time and bandwidth · B. Main-memory organisation · C. AMAT · D. Miss penalty and writes · E. Solving backwards · F. CPU time with memory stalls · G. Memory interfacing · H. DRAM refresh · I. VM bridge

---

## A. Time and bandwidth

### A1. Access time, cycle time, access rate
```
t_C ≥ t_A ;  maximum random-access rate = 1 / t_C ;  peak bandwidth = (bytes per access) / t_C
```
- Symbols: t_A access time (s), t_C cycle time (s). When: back-to-back random accesses to one bank.
- Why: a new access cannot start until the restore/precharge of the previous one has finished.
- Example: t_A = 60 ns, t_C = 80 ns, 4-byte word ⇒ 12.5 × 10^6 accesses/s ⇒ 50 MB/s.
- Misuse: using t_A for the rate (gives 66.7 MB/s, too high).

### A2. Burst block-transfer time
```
T_block = t_first + (W − 1) · t_next ;   W = block bytes / word bytes ;   BW_block = block bytes / T_block
```
- When: memory delivers the first word after a long latency and later words faster (burst/page mode).
- Example: W = 8, 40 ns, 10 ns ⇒ 110 ns ⇒ 32 B/110 ns = 290.9 MB/s.
- Misuse: using W instead of W − 1; using the word size in bits as bytes.

### A3. Cycles ↔ time, bandwidth in controller-cycles form
```
T = (cycles) / f ;  cycles per block = Σ non-overlapped stages ;  BW = block bytes / T
```
- Example: 1 (address) + 4 (fetch) + 16 (transfer) = 21 cycles at 100 MHz = 210 ns; 64 B ⇒ 304.76 MB/s.
- Misuse: counting overlapped stages twice; MB/s with 2^20.

### A4. Block transfer over a bus of width Bw words
```
transfers = ⌈ block words / Bw ⌉ ;  T = transfers × t_per_transfer
```
- Example: 8 words over a 4-word bus at 120 ns per transfer ⇒ 240 ns; 4 words over a 2-word bus at 15 ns ⇒ 30 ns; both moves in sequence ⇒ 270 ns.
- Misuse: using the block size of the wrong level; forgetting the ceiling.

---

## B. Main-memory organisation

### B1. Block read time: simple, wide, interleaved (non-overlapped rounds)
```
simple        : T = B (t_a + t_m + t_b)
wide (W words, W-word bus) : T = ⌈B/W⌉ (t_a + t_m + t_b)
wide, 1-word bus           : T = ⌈B/W⌉ (t_a + t_m + W·t_b)
m-bank low-order interleave: T = ⌈B/m⌉ (t_a + t_m + m·t_b)
```
- Example (cycles, t_a=1, t_m=6, t_b=1): B = 4: 32 / 8 / 11 / 11 ; B = 8 with 4 banks: 22 (simple 64, 2 banks 36).
- Misuse: using these when the question says the banks overlap (staggered) — use B2.

### B2. Staggered (overlapped) interleaving
```
m_min = ⌈ t_m / t_b ⌉ ;   T ≈ t_m + B · t_b   (m ≥ m_min) ;   sustained rate with m < m_min : one word per t_m / m
```
- Why: bank i+1 starts t_b after bank i; a bank is free again after t_m, so m·t_b ≥ t_m keeps the bus saturated.
- Example: t_m = 40, t_b = 10 ⇒ m_min = 4, B = 8 ⇒ 120 ns (simple: 400 ns).
- Misuse: ignoring address time when the question includes it; adding banks beyond m_min (no gain).

### B3. Banks touched by a constant stride
```
distinct banks = m / gcd(stride, m)           (low-order interleaving)
```
- Example: m = 8: strides 1,3,7 ⇒ 8 banks; 2 ⇒ 4; 4 ⇒ 2; 8 ⇒ 1.
- Misuse: using it for high-order interleaving (consecutive addresses stay in one bank).

---

## C. AMAT

### C1. One level — hierarchical, simultaneous, additive
```
hierarchical : T = T_c + m · T_m              (miss costs T_c + T_m)
simultaneous : T = h · T_c + m · T_m
additive     : T = T_c + m · P                P = miss penalty (extra)
equivalences : additive(P = T_m) = hierarchical ;  additive(P = T_m − T_c) = simultaneous ;  hierarchical − simultaneous = m · T_c
```
- When: pick by the wording (NOTES §4.2). "Takes X on a hit and Y on a miss" ⇒ T = h·X + m·Y.
- Example: T_c = 5, T_m = 50, h = 0.8 ⇒ 15.0 vs 14.0.
- Misuse: using a totals-style miss time (Y) as a penalty (adds T_c twice).

### C2. n levels
```
hierarchical : T = T1 + m1 ( T2 + m2 ( T3 + m3 T4 ) ) ;     simultaneous : T = h1 T1 + m1 h2 T2 + m1 m2 h3 T3 + m1 m2 m3 T4
hier − simul = Σ over non-last levels i of  T_i · (m1 … m_i)
```
- Why: hierarchical = every reference pays T1, only L1 misses pay T2, only L1-and-L2 misses pay T3.
- Example: T = (2, 20, 100 mem), h1 = 0.9, h2 = 0.8: 6.0 vs 5.4 (difference 0.6 = 0.1·2 + 0.1·0.2·20).
  3-level (1, 5, 30, 200 mem; 0.95, 0.8, 0.9): 1.75 vs 1.62.
- Misuse: evaluating outside-in; treating local ratios as global.

### C3. Local and global miss ratios
```
g_i = m1 · m2 · … · m_i  ;   hierarchical:  T = T1 + m1 T2 + g2 T3 + …
```
- Example: m1 = 0.08, m2 = 0.25 ⇒ g2 = 0.02; T1=2, T2=10, T_mem=100 ⇒ 2 + 0.8 + 2.0 = 4.8.
- Misuse: using g2 inside the bracket (double counting m1).

### C4. Penalty-style multi-level
```
T = T1 + m1 ( P12 + m2 · P2m )
```
- Example: 2 + 0.08 (12 + 0.25 × 150) = 5.96. Misuse: using local m2 as global.

### C5. Weighted over reference types
```
T = Σ f_type · T_type ,  Σ f_type = 1 ;   T_type = h_type · T_hit,type + m_type · T_miss,type  (totals)
```
- Example: I-fetch 70 %: 2.8 ns, data 30 %: 3.7 ns ⇒ 3.07 ns; trace 170 reads (2.5 ns) + 30 writes (3.85 ns) ⇒ 2.7025 ns.
- Misuse: weighting by 1/(number of types).

### C6. Speedup from the memory system
```
speedup = T_without / T_with ;   Amdahl: speedup = 1 / ( (1 − f) + f / s )
```
- Example: 100 / 5.6 = 17.86. Misuse: dividing AMATs of different reference streams.

---

## D. Miss penalty and write policy

### D1. Block-transfer miss penalty
```
P = t_first + (W − 1) t_next                       (CPU waits for the whole block)
P_critical-word-first = t_first                    (CPU restarts at the requested word)
```
- Example: W = 8, 30, 6 ⇒ P = 72; hierarchical 2 + 0.05·72 = 5.6; simultaneous 5.5; critical-word 3.5.
- Misuse: using the restart-penalty for a question that says the CPU waits for the block.

### D2. Write-back penalty
```
P_miss = P_fetch + d · P_writeback ,  d = fraction of victims that are dirty ;   T = T_c + m · P_miss
```
- Example: 2 + 0.04 (50 + 0.4 × 50) = 4.8 (d = 0 ⇒ 4.0; d = 1 ⇒ 6.0). Misuse: writing back clean victims; counting a write-back on write-through caches.

### D3. Write-through timing
```
no buffer   : each store takes t_w (memory write time) ;   ideal buffer : each store takes the cache write time
mixed T = f_read · T_read + f_write · T_write
```
- Example (25 % stores, reads 4.0, t_w = 50): 15.5 without buffer; 3.25 with ideal 1 ns buffer.
- Misuse: assuming a buffer never fills (valid only if stores are slow enough to drain).

---

## E. Solving backwards

### E1. Break-even hit ratio
```
T_c' + m' · P ≤ T_c + m · P   ⇒   m' ≤ m − (T_c' − T_c)/P  ,   h' ≥ 1 − m'
```
- Example: T_c 4→5, m = 0.1, P = 60 ⇒ m' ≤ 0.0833, h' ≥ 0.9167 (0.92 to 2 d.p.).
- Misuse: comparing the hit rates instead of AMATs.

### E2. Ratio-constrained miss ratios (hierarchical)
```
T = T1 + k·m2 ( T2 + m2 T_mem )   (m1 = k m2)  ⇒  k·T_mem·m2² + k·T2·m2 − (T − T1) = 0
```
- Example: T1=1, T2=6, T_mem=20, T=1.8, k=3 ⇒ 60 m2² + 18 m2 − 0.8 = 0 ⇒ m2 = 0.0393, m1 = 0.1179.
- Misuse: choosing the negative root; wrong model.

### E3. Table of sizes
Compute T for each size, apply the target with its strict/non-strict inequality (NOTES §4.8).

---

## F. CPU time with memory stalls

### F1. CPI and time
```
CPI_eff = CPI_base + stalls/instr ;   stalls/instr = (1)·m_I·P_I + (data refs/instr)·m_D·P_D
penalty cycles = penalty ns / T_clk (ceil if whole cycles required) ;   CPU time = IC · CPI_eff · T_clk
```
- Example: CPI_base 1.2, 2 GHz, I 1 %, D 4 %, 35 % ld/st, 80 ns ⇒ P = 160 cycles; stalls 3.84; CPI 5.04; 10^9 instr ⇒ 2.52 s.
- Misuse: base CPI that does not include hits; ns penalty used as cycles.

### F2. Two levels
```
stalls/instr = refs/instr · ( m1 · P12 + g2 · P2m )
```

### F3. Perfect cache speedup and Amdahl
```
speedup_perfect = CPI_eff / CPI_base ;   speedup after cutting stalls by s = (CPI_base + S) / (CPI_base + S/s)
```
- Example: CPI_base 2, S = 2.4: 2.2; halving S: 4.4/3.2 = 1.375. Misuse: using stall fraction of the wrong total.

### F4. Comparing designs
```
time/instr = (CPI_base + refs/instr · m · P_cycles) · T_clk ;   with a fixed ns penalty P_cycles = ⌈P_ns / T_clk⌉
```
- Example: A (0.50 ns, 3 %, 120 cycles) = 3.07 ns; B (0.55 ns, 2 %, 110 cycles) = 2.299 ns.

---

## G. Memory interfacing

### G1. Chip counts and address split
```
chips = ⌈M/K⌉ · ⌈W/N⌉ ;  chip address lines = log₂K (low bits) ;  decoder inputs = log₂M − log₂K (high bits) ;  decoder outputs = ⌈M/K⌉
```
- Example: 64 KB × 8 from 16 K × 4: 8 chips, 14 chip lines, 2-to-4 decoder; 256 K × 16 from 32 K × 4: 32 chips, 15 lines, 3-to-8.
- Misuse: byte vs word addressing; using total bits ÷ chip bits when the shapes do not divide.

### G2. Address ranges
```
row r (full decoding, top-bit select) : [ r·K , (r+1)·K − 1 ]          (word addresses; for bytes, multiply by bytes per location)
non-top select bits at positions p…q  : block i start = i << p  (other bits 0), blocks interleaved in 2^p-sized stripes
```
- Example: 4 blocks of 2 KB with select on A6A5 ⇒ starts 0, 32, 64, 96; 0x1A5 is in block 1.

### G3. Aliasing
```
images = 2^(number of unused upper select bits)
```
- Example: 16-bit, 8 K RAM, CS = A15 ⇒ 2² = 4 images in 8000–FFFF.

---

## H. DRAM refresh

```
overhead = rows · t_row / T_refresh ;  available = 1 − overhead ;  distributed interval = T_refresh / rows
```
- Example: 8192, 60 ns, 64 ms ⇒ 0.768 % ; 99.232 % ; 7.8125 µs. If 4 chips refresh sequentially: 3.072 %.
- Misuse: using number of chips instead of rows; ns vs ms.
- Address pins of a multiplexed DRAM: n/2 for a 2ⁿ-location one-bit chip with square array (24 ⇒ 12).

---

## I. Virtual-memory bridge (owned by the OS folder)

```
EAT = α (t_tlb + t_m) + (1 − α)(t_tlb + (k+1) t_m) ;  with page faults: (1 − p)·EAT + p·S  ;  inversion: p = (X − M)/(D − M) for measured average X, normal M, faulting D
```
- Example: t_tlb 5, t_m 80, k = 2, α = 0.9 ⇒ 101.0 ns; with t_tlb ignored 96.0; α needed for 110 ns: 0.84375; fault: 100 ns + 2×10^-6 × 8×10^6 ns = 116 ns.
- Misuse: forgetting the final data access; counting page-table levels from the TLB hit path.

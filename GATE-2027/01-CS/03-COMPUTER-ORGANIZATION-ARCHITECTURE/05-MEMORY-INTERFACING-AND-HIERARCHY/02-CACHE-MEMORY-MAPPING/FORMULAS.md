# Cache Memory Mapping — FORMULAS

Every formula: statement, symbols, when it applies, why, example (script-verified), common misuse.
Conventions: K = 2¹⁰, M = 2²⁰; byte-addressable unless stated; cache **capacity** = data bytes only unless the question says otherwise.
AMAT theory and memory-side bandwidth: [`../01-PERFORMANCE/FORMULAS.md`](../01-PERFORMANCE/FORMULAS.md). Full derivations: [`NOTES.md`](NOTES.md).

Contents: A. Address split · B. Tag relations · C. Storage and hardware · D. Mapping arithmetic · E. Reverse / max-cache · F. Tracing · G. Miss types · H. Write policies · I. AMAT bridge · J. Page colours (bridge)

---

## A. Address split (byte-addressable)

### A1. Field widths
```
offset o = log₂(block size in bytes)
#lines N = cache capacity C / block size B
#sets S = N / k          (k = associativity, ways per set)
index i  = log₂ S = log₂ N − log₂ k
tag t    = A − i − o     (A = physical address bits)
```
- **When:** any cache organisation; k = 1 → direct-mapped; k = N → fully associative (i = 0).
- **Why:** the offset picks a byte inside the block; the index picks the set; the tag distinguishes blocks sharing that set.
- **Example:** A = 32, C = 64 KB, B = 64 B, 4-way → o = 6, N = 1024, S = 256, i = 8, **t = 18**.
- **Misuse:** using C/k as the number of sets; forgetting that capacity is in bytes.

### A2. Word-addressable variant
```
offset = log₂(block size in address units)     (words if word-addressable)
tag, index, #lines unchanged if you convert capacity and block to the same unit first
```
- **Example:** 2¹⁴ words cache, 8-word blocks, 2²⁴-word address → index 11, offset 3, **tag 10** (same as the byte view: 26-bit byte address, 32-byte blocks).
- **Misuse:** mixing bytes in capacity with words in block size without converting.

### A3. Arithmetic extraction (hex-friendly)
```
block number = ⌊addr / B⌋ = addr >> o
index        = block mod S = (addr >> o) & (S − 1)
tag          = block >> i   = addr >> (o + i)
line number (DM) = index
```
- **Example:** addr = 0x00001F80, B = 32 B, 256 lines → line = (8064 >> 5) mod 256 = **252**.
- **Misuse:** using low bits of the address as the index without removing the offset first.

---

## B. Tag-bit relationships (fixed C, B, A)

### B1. Associativity adds log₂k to the tag
```
t_k = t_DM + log₂ k        (k′-way tag − k-way tag = log₂(k′/k))
t_FA = A − o               (no index)
t_k = A − log₂ C + log₂ k  (block size B cancels)
```
- **When:** comparing organisations at the same capacity and block size.
- **Why:** doubling k halves the number of sets, so one index bit moves into the tag.
- **Example:** 2²⁸ B memory, 2²⁰ B cache, 64 B blocks: DM tag 8; 2-way tag 9; 4-way 10; 8-way 11 → **N = M + L** when K = 2^L.
- **Misuse:** writing N = M + K or N = M − L (distractor forms).

### B2. Symbolic form (P, N, M, W, K notation)
```
block bytes = 2^(M+W) ;  tag = P − N + log₂ K
```
- **When:** question gives 2^P-byte addresses, 2^N-byte cache, 2^M-word blocks, word = 2^W bytes, K-way.
- **Example:** P = 32, N = 16, M = 3, W = 2, K = 4 → tag = 32 − 16 + 2 = **18**.
- **Misuse:** leaving M+W in the tag formula (M and W cancel).

### B3. Effect of block-size or cache-size change (k fixed)
```
block size ×2  →  index −1, offset +1, tag per line unchanged, #lines halved
cache size ×2  →  index +1, tag −1
address +1 bit →  tag +1, index and offset unchanged
```
- **Example:** 16 KB DM, A = 32: B = 32 → 512 lines × 18-bit tags = 9216 tag bits; B = 64 → 256 × 18 = 4608 tag bits.
- **Misuse:** assuming the tag width grows when the block grows (only total tag *storage* may change via #lines).

---

## C. Storage and hardware counts

### C1. Tag directory (tags only)
```
total tag bits = N × t
tag directory with status = N × (t + valid + dirty + …)
```
- **Example:** A = 28, 32 KB DM, 16 B blocks → t = 13, N = 2048 → 26 624 bits = **26 Kbit**.
- **Misuse:** multiplying by #sets instead of #lines in a set-associative cache.

### C2. Main memory and cache size from field widths
```
memory bytes  = 2^(t + i + o)
cache data    = 2^(i + o) × k     (DM: k = 1)
```
- **Example:** tag 6, index 9, offset 3 → memory 2¹⁸ B = 256 KB; cache 2¹² B = **4 KB**.
- **Misuse:** omitting the offset from the address width.

### C3. Total metadata (valid, dirty, LRU)
```
per-line meta = t + valid + dirty (+ …)
LRU per set (true LRU, k ways) = ⌈log₂ k!⌉
per-set meta  = k × per-line meta + LRU_bits
total meta    = S × per-set meta
```
- **Example:** 32-bit, 64 KB, 8-way, 64 B, WB, true LRU → meta = **23 552 bits** (data excluded).
- **Misuse:** using k·log₂k counters or k−1 tree bits when the question says true LRU.

### C4. Hardware comparators
```
k-way lookup : k comparators, each t bits wide
fully assoc. : N comparators, each (A − o) bits
```
- **Example:** 4 KB, 16 B blocks, fully associative → 256 comparators.
- **Misuse:** reporting 1 comparator for fully associative.

---

## D. Block-to-line mapping

### D1. Set-associative line range
```
set s = j mod v ;  lines for block j :  (j mod v)·k  through  (j mod v)·k + (k−1)
```
- **When:** lines numbered consecutively, all sets of size k placed in order.
- **Example:** v = 16, k = 2, block 37 → set 5 → lines **10–11**.
- **Misuse:** using (j mod k) or (j mod k)·v.

### D2. Direct-mapped
```
line = block mod N = index field of the address
```

---

## E. Reverse problems and maximum cache size

### E1. Unknown associativity from tag width
```
log₂ S = A − log₂ B − t  →  k = N / S
```

### E2. Maximum cache capacity from one address→line fact (DM)
```
line(a) = bits [o, o+i) of a  must equal L ;  maximise o + i subject to o ≥ 0, o + i ≤ A
capacity = 2^(o + i) bytes
```
- **Procedure:** find every alignment o where L fits in a; extend i upward while leading bits of the field in a are zero.
- **Example:** A = 19 (512 KB), a = 0x52CE8, L = 75 → max o+i = 18 → cache **256 KB**.
- **Misuse:** ignoring zero-extension above L; allowing i too small to represent L.

### E3. Set-associative max size
```
capacity = k × 2^(o + i)     (k fixed by the question)
```

---

## F. Hit/miss tracing

### F1. Conflict classification (same capacity)
```
miss in real cache AND hit in fully-associative reference  →  conflict miss
miss in both real and fully-associative reference of same size  →  capacity miss
first reference to block  →  compulsory miss
```

### F2. Miss count from a reference string
Simulate per set: on miss, evict by LRU (move hit to MRU) or FIFO (queue). Count hits/misses; write-backs on dirty eviction in WB mode.

### F3. Array / loop miss estimate (DM, two passes)
```
pass-1 compulsory misses ≈ # distinct blocks touched
pass-2 extra misses from lines reused with different blocks (capacity/conflict wrap)
```
- **Example:** 8-line cache, 11 distinct blocks in one pass, 8 lines → 11 + 6 = **17** total over two row-major passes (NOTES §11.3).

---

## G. Miss types and design trade-offs

### G1. Three C's
Compulsory (cold), capacity (working set > cache), conflict (set contention; removed by full associativity at same size).

### G2. LRU miss-ratio bound (associativity A, reuse distance ≤ k)
```
miss ratio ≤ k / N        (N = references, k = max gap between repeats of same block)
```
- **When:** LRU, A ≥ k, stream obeys the reuse bound (2014 Set-1 pattern).
- **Misuse:** using 1/A or n/N without checking the bound.

---

## H. Write policies

### H1. Write-through vs write-back
| Policy | Dirty bit | Write hit | Evict on miss |
|---|---|---|---|
| Write-through | no | writes memory | never write-back |
| Write-back | yes | may set dirty | write-back if dirty |

### H2. Write-allocate vs no-write-allocate
Write miss with no-write-allocate: write memory directly, block may stay absent. Write-allocate: fetch block first (may evict dirty victim).

---

## I. AMAT and CPI (bridge to 01-PERFORMANCE)

### I1. Single-level AMAT
```
AMAT = t_hit + m · P          (P = extra miss penalty)
     = h·t_hit + m·(t_hit + P)
block-fill penalty: P = t_first + (W − 1)·t_next ,  W = block bytes / word bytes
```
- **Example:** t_hit = 1.5 ns, m = 0.04, first word 30 ns, 7 more at 6 ns → AMAT = 1.5 + 0.04×72 = **4.38 ns**.
- **Misuse:** using 8×30 or 8×6 for the penalty.

### I2. Two-level hierarchical
```
T = t₁ + m₁·(t₂ + m₂·t_m)     (m₂ local to L2)
```
- **Example:** t₁=1, m₁=0.10, t₂=5, m₂=0.05, P_m=50 → T = 1 + 0.10×(5+2.5) = **1.75 ns**; solve for m₁ when T is given.

### I3. Simultaneous access
```
T = h₁·t₁ + (1−h₁)·h₂·t₂ + (1−h₁)(1−h₂)·t_m
```
- **Example:** h₁=0.85, t₁=2, h₂=0.70, t₂=10, t_m=80 → **6.35 ns** (not 7.10 hierarchical).

### I4. CPI with cache stalls
```
CPI_eff = CPI_base + m_I·P + (f_ld + f_st)·m_D·P
```
- **Example:** CPI_base=1.2, m_I=0.02, m_D=0.05, f_ld+f_st=0.35, P=40 → CPI = **2.70**.

---

## J. Page colours (OS bridge)

### J1. Minimum page colours (VIPT, direct-mapped or set-assoc)
```
index + offset bits that alias within a page = p + x  →  need 2^x page colours
x = (index bits + offset bits) − log₂(page size)
colours = 2^x
```
- **When:** virtually indexed, physically tagged cache; synonyms must not map to different sets.
- **Example:** 32 KB, 4-way, 64 B blocks, 4 KB pages → x = 1 → **2 colours** (NOTES §17).
- **Owner topic:** [`../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY`](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY).

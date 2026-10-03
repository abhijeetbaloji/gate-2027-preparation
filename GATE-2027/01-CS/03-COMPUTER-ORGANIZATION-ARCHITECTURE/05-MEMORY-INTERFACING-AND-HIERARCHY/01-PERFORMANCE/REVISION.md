# Memory Hierarchy Performance — REVISION (last-minute)

Full detail: [`NOTES.md`](NOTES.md) · formulas: [`FORMULAS.md`](FORMULAS.md) · cache mapping: [`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/).

## Definitions
- Hierarchy works because of **temporal** (reuse) and **spatial** (neighbours → blocks) locality. Down the hierarchy: bigger, cheaper per bit, slower.
- Miss kinds: compulsory (first touch), capacity (working set > cache; even fully associative), conflict (set contention).
- Access time t_A ≤ cycle time t_C. Latency ≠ bandwidth. Sizes K = 2^10; rates MHz, MB/s decimal.
- Miss penalty = EXTRA time. "Takes X on hit, Y on miss" = TOTAL times.
- Block size ↑: spatial locality ↑ at first, penalty ↑, more conflicts later. Inclusion needs L2 ≥ L1 (back-invalidation maintains it).

## Must-remember formulas
```
Hierarchical :  T = T1 + m1 (T2 + m2 (T3 + …))          Simultaneous : T = h1T1 + m1h2T2 + m1m2h3T3 + …
One level    :  hier T_c + m·T_m ;  simult h·T_c + m·T_m ;  difference = m·T_c ;  additive T_c + m·P
Global miss  :  g2 = m1·m2 ;  T = T1 + m1·T2 + g2·T3
Burst block  :  P = t_first + (W − 1)·t_next ,  W = block bytes / word bytes
Bus          :  transfers = ⌈block words / bus words⌉
Interleave   :  rounds ⌈B/m⌉ × (t_a + t_m + m·t_b) ;  staggered: m_min = ⌈t_m/t_b⌉ ,  T ≈ t_m + B·t_b ;  banks used = m / gcd(stride, m)
Write-back   :  P_miss = P_fetch + d·P_wb  (d = P(dirty victim))
CPU          :  CPI_eff = CPI_base + 1·m_I·P_I + (ld/st fraction)·m_D·P_D ;  time = IC·CPI·T_clk ;  P_cycles = P_ns × f
Interfacing  :  chips = ⌈M/K⌉⌈W/N⌉ ;  chip lines = log₂K (low) ;  decoder = log₂(M/K) high bits
Refresh      :  rows × t_row / T_refresh
VM bridge    :  EAT = α(t_tlb + t_m) + (1−α)(t_tlb + (k+1)t_m) ;  fault term p·S
```

## Tables to remember
| Write policy | Dirty bit | Evict | Read miss can write memory? |
|---|---|---|---|
| Write-through | no | never writes back | no |
| Write-back | yes | write back if dirty | yes (dirty victim) |

| Wording | Model |
|---|---|
| "X on hit, Y on miss" | h·X + m·Y |
| "hit time + miss penalty" | T_c + m·P |
| "first looks in L1, then L2, then memory" | hierarchical |
| "simultaneously / in parallel" | simultaneous |
| only access times given | ambiguous — compute both, read the options |

## Fast-solve checklist
1. State model (hier / simul / penalty) and local vs global. 2. Convert units (ns ↔ cycles, bytes ↔ words). 3. Nested AMAT: inside-out. 4. Mixed streams: per-type time, then count-weighted average.
5. CPI: stalls per instruction = refs × miss ratio × penalty cycles; one fetch per instruction. 6. Compare designs by **time**, not CPI. 7. Interfacing: columns = W/N, rows = M/K, low bits to chips, high bits to decoder. 8. NAT: check rounding direction.

## Top traps
- hit time added twice; hit/miss ratio swapped; penalty vs total time; local vs global; W vs W − 1; bits vs bytes in word size.
- MB/s decimal; ns vs cycles; assuming contiguous memory blocks when select bits are not the top bits; refresh uses rows not chips.
- Write buffer hides latency but does not remove writes; write-through needs no dirty bit; associativity does not fix capacity misses.

## High-frequency PYQ concepts (from the mapped evidence only)
Single/multi-level AMAT with numbers (2025, 2022, 2020, 2017, 2015, 2014 — all mapped in the cache folder); read/write/fetch weighted averages (2017, 2014); block-transfer time and memory bandwidth (2020, 2019, 2010); write policy statements (2024, 2022); block-size and inclusion statements (2014, 2008). See [`PYQ.md`](PYQ.md). No official answers are given in this repository.

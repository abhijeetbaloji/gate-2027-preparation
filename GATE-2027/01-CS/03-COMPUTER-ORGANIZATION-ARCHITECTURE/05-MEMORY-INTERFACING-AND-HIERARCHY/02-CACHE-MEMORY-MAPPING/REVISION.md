# Cache Memory Mapping — REVISION (last-minute)

Full detail: [`NOTES.md`](NOTES.md) · formulas: [`FORMULAS.md`](FORMULAS.md) · AMAT/interfacing: [`../01-PERFORMANCE`](../01-PERFORMANCE/).

## Definitions
- **Block/line:** unit of cache–memory transfer. **Hit/miss:** block present/absent. **Set:** group of k lines a block may use. **Tag:** high address bits stored to identify the occupant.
- **Locality:** temporal (reuse) + spatial (neighbours → whole block fetched). **3C misses:** compulsory, capacity, conflict.
- **DM:** k=1, one line per set. **Fully assoc.:** one set, no index. **Capacity** = data bytes unless question says otherwise.

## Must-remember formulas
```
o = log₂ B ;  N = C/B ;  S = N/k ;  i = log₂ S ;  t = A − i − o
t_k = t_DM + log₂ k ;  symbolic: t = P − N + log₂ K
block = addr >> o ;  index = (addr >> o) & (S−1) ;  tag = addr >> (o+i)
lines for block j: (j mod v)·k … (j mod v)·k + (k−1)
tag bits total = N × t ;  meta = S × (k·(t+status) + LRU_bits)
max DM cache from one mapping: maximise o+i with line(a)=L → 2^(o+i) bytes
AMAT (hier)  : t_hit + m·P ;  2-level: t₁ + m₁(t₂ + m₂·t_m)
AMAT (simul) : h₁t₁ + (1−h₁)h₂t₂ + … ;  gap one level = m·t_hit
CPI stalls   : m_I·P + (ld+st frac)·m_D·P
page colours : 2^((i+o) − log₂ page_size)   [VIPT bridge]
```

## Organisation table
| | DM (k=1) | k-way | Fully assoc. |
|---|---|---|---|
| Conflict misses | most | fewer | none (at same size) |
| Tag bits | smallest | +log₂k vs DM | A−o (largest) |
| Comparators | 1 | k | N |
| Replacement | none | LRU/FIFO per set | global LRU |

## Write-policy table
| | Write-through | Write-back |
|---|---|---|
| Dirty bit | no | yes |
| Write hit | writes memory | may set dirty only |
| Read-miss eviction | no write-back | dirty victim → memory |

## Fast-solve checklist
1. State **byte vs word** addressable and **block size unit**. 2. Compute o, N, S, i, t in order. 3. For hex: **shift by o** before index mask.
4. Tag storage: multiply by **lines**, not sets. 5. Trace: build per-set state; **same block** = hit without tag compare if only one block size.
6. P,Q,R,S loops: check **shared lines** and **shared blocks** first. 7. AMAT: name **hierarchical vs simultaneous** and **penalty vs total miss time**.
8. Max-cache: write address in binary; find L at each o; extend i with leading zeros of the field. 9. NAT: check **Kbit vs bit** and rounding.

## Top traps
- Tag width vs tag **storage**; index bits vs **line number**; using addr mod lines without >>o.
- Fully assoc. ⇒ **most** tag bits, not fewest; DM tag **unchanged** when B doubles (per line).
- Conflict vs capacity: FA same size **also misses** ⇒ capacity. Y/Z same block; W/X same line different tags.
- WB read miss **can** write memory; WT never needs dirty bit. LRU hit **refreshes** victim order (Q16 vs Q27 FIFO).
- AMAT: W−1 for subsequent words; local vs global L2 ratio; simultaneous ≠ hierarchical.
- Page colours need **page size** from the linked OS part of the question.

## High-frequency PYQ concepts (from mapped evidence only)
Tag/index/offset sizing and N=M+L relation (2026, 2025, 2023, 2018, 2017, 2016, 2014, 2012, 2007); hex→set/line and max cache size (2026, 2015, 2008, 2007); P,Q,R,S conflict loops (2026, 2022); LRU trace/final contents (2009, 2022); array traversal misses (2007, 2008); k-way line range (2013); tag directory size (2012, 2025); write-policy statements (2024, 2022); AMAT/CPI (2010, 2014–2017, 2019–2020, 2022, 2025); page colours (2013). See [`PYQ.md`](PYQ.md). **No official answers** in this repo.

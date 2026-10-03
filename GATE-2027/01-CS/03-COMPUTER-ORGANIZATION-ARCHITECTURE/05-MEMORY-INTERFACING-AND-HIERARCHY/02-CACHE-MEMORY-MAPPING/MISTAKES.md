# Cache Memory Mapping — MISTAKES

Typical errors for this topic, with the fix. The "My Mistakes" table at the end is for you; it is intentionally empty.
See [`NOTES.md`](NOTES.md), [`PRACTICE.md`](PRACTICE.md), and [`../01-PERFORMANCE/MISTAKES.md`](../01-PERFORMANCE/MISTAKES.md) for AMAT-specific traps.

---

## 1. Conceptual confusions

| # | Mistake | Why wrong | Fix |
|---|---|---|---|
| C1 | "Fully associative has the fewest tag bits." | No index field means the tag keeps all bits above the offset — the **widest** tag. | NOTES §3.2–3.3; Q1 trap. |
| C2 | "Conflict miss means fully associative would also miss." | Reversed: if FA of the **same size** would hit, your miss was conflict. | NOTES §12.1; Q5. |
| C3 | "Direct-mapped has no conflict misses." | DM has the **most** conflict misses; one line per set. | NOTES §3.3. |
| C4 | "A read miss never writes main memory." | Write-back may evict a **dirty** victim on a read miss. | NOTES §14; Q4. |
| C5 | "Write-through needs a dirty bit." | Memory is always up to date. | NOTES §14.1. |
| C6 | "Doubling block size always improves miss ratio." | Fewer lines, higher penalty, pollution — miss ratio can rise. | NOTES §12.2; Q2-C. |
| C7 | "Index bits are the high bits of the address." | Index sits **between** tag and offset. | NOTES §4.1 diagram. |
| C8 | "Cache size includes tag storage unless stated." | Capacity = **data** bytes by convention. | NOTES conventions. |
| C9 | "LRU always outperforms FIFO." | Belady anomaly: FIFO can do better on some traces. | Q35; NOTES §13. |
| C10 | Mixing **line number** with **set number** in k-way caches. | One set holds k lines; index picks the set only. | NOTES §9. |

## 2. Formula mistakes

| # | Mistake | Fix |
|---|---|---|
| F1 | #sets = C / (k·B) written as C/k or C/B. | S = (C/B)/k = N/k. |
| F2 | t_k = t_DM − log₂k or t_DM + k. | t_k = t_DM + **log₂k**; symbolic N = M + **L** when K = 2^L. |
| F3 | Tag storage = #sets × tag width. | Multiply by **#lines** = N. |
| F4 | Word-addressable: using byte block size in offset without converting. | Convert capacity and block to the **same unit** as the address. |
| F5 | Line = addr mod #lines (no shift). | line = (addr >> o) mod #lines. |
| F6 | Block j maps to lines j … j+k−1. | Lines **(j mod v)·k** … **(j mod v)·k + k−1**. |
| F7 | LRU bits = k·log₂k always. | True LRU = **⌈log₂ k!⌉** per set unless the question fixes another scheme. |
| F8 | AMAT simultaneous formula with t₁ added to every term. | Simultaneous: failed lookups do not pay t₁ again. |
| F9 | Block-fill penalty = W × t_next. | P = t_first + **(W−1)**·t_next. |
| F10 | CPI: data stalls on all instructions. | Only load/store fraction × m_D × P. |

## 3. Numerical / calculation mistakes

| # | Mistake | Fix |
|---|---|---|
| N1 | Kbit vs bit: reporting 26624 bits as 26624 Kbit. | Divide by 1024 for Kbit. |
| N2 | Hex index: using low 8 bits of address when offset is 5 bits. | Shift right by o first (Q11). |
| N3 | Max-cache: i too small to hold line number L. | Need 2^i > L and zero-extension of L in the field. |
| N4 | Array misses: second pass all hits. | Wrap-around evicts early blocks (Q17). |
| N5 | Column-major: counting 8 columns per block as "reuse". | Stride evicts before the next column (Q18). |
| N6 | Quadratic for miss ratio: negative root or reporting L2 ratio when L1 is asked. | Pick root in [0,1]; read which level (Q20). |
| N7 | PQRS: Y and Z treated as different blocks. | Same block if addresses differ only inside one block (Q15). |
| N8 | Write-back count includes final dirty line not flushed. | Count only write-backs **during** the sequence (Q22). |

## 4. PYQ-derived traps

Question kinds from the mapping (newest → oldest). **No official answers** are given or implied.

| Year / Q# | Question kind | Trap pattern |
|---|---|---|
| 2026 Q.38 | DM vs K-way tag relation | use L = log₂K, not K; N = M + L |
| 2026 Q.52 | P,Q,R,S loop | same line different tags; same block different offsets |
| 2026 Q.56 | Max cache size | binary search for field alignment; zero-extension |
| 2025 Q.36 | Total tag bits DM | lines × tag; MCQ may express as multiple of 2^10 |
| 2025 Q.39 | Size from field widths | offset bits from block size, not assumed 1 B |
| 2023 Q.64 | 8-way tag NAT | divide capacity by 8 only for sets, not for lines |
| 2022 Q.54 | P,Q,R,S (16-bit word) | word length vs byte address |
| 2021 Q.22, Q.18 | Tag / associativity NAT | scanned OCR; verify block size unit |
| 2020 Q.30 | Four hex addresses same set? | compute set index for each |
| 2019 Q.1 | Fully assoc. tag and index | index = 0, not "no tag" |
| 2018 Q.34 | Symbolic tag MCQ | P−N+log₂K form |
| 2017 Q.53 | DM tag NAT | 2^32 bytes / 32 B blocks |
| 2016 Q.32 | 40-bit addr, 512 KB 8-way | tag from formula, not guess |
| 2015 Q.34 | Tag and line in hex | consecutive bytes may share a block |
| 2014 Q.44 (Set-1) | LRU miss-ratio bound | k/N bound, not 1/A |
| 2014 Q.9 | Tag with block in words | convert 8 words × 32 bits to bytes |
| 2013 Q.20/6/18/8 | k-way line range | (j mod v)·k term |
| 2013 Q.53/55 (×4 booklets) | Page colours | needs page size from linked OS setup |
| 2012 Q.54–55 | Linked tag + directory | extra valid/modified/replacement bits per entry |
| 2009 Q.29 | LRU final absent block | simulate all 16 refs, 4 sets |
| 2008 Q.71–73 | Array + tag directory | double 8 B, row-major init; common data |
| 2007 Q.10 | Word-addressable fields | LINE vs SET naming; block in words |
| 2007 Q.80–81 | 50×50 array two passes | unaligned start 1100H; which lines replaced |
| 2025 Q.53, 2024 Q.53, 2022 Q.24/33, 2020 Q.21, 2019 Q.45, 2017 Q.29/45, 2016 Q.50, 2015 Q.18, 2014 Q.43/44, 2010 Q.48/49, 2008 Q.35 | Performance-type (see [`../01-PERFORMANCE/PYQ.md`](../01-PERFORMANCE/PYQ.md)) | AMAT model, WB/WT statements, bandwidth, inclusion |

## 5. Examination-time mistakes

1. Starting arithmetic before writing o, i, t and the organisation (k).
2. Not padding hex addresses to the full address width before bit-slicing.
3. Simulating the whole cache when a same-line / same-block shortcut exists.
4. For MSQ/TRUE-FALSE, not reading whether the stem asks for TRUE or **FALSE** statements.
5. Picking the first MCQ option that matches a partial calculation (distractors use wrong model or off-by-one).
6. Forgetting that **every instruction fetches** when adding CPI stalls.

## 6. How to check yourself

- [ ] Do t_DM + log₂k and the direct formula agree?
- [ ] Does line = (addr >> o) mod N match your bit-slice?
- [ ] Tag storage uses **lines**, metadata question uses the LRU scope stated?
- [ ] After a trace, does each set have at most k blocks?
- [ ] AMAT: stated hierarchical/simultaneous and penalty vs total?
- [ ] Max-cache: is 2^i > L and are high field bits of a zero where needed?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
| | | | | | |

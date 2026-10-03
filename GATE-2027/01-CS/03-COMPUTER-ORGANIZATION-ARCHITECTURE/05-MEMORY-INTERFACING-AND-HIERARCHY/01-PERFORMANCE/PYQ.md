# Memory Hierarchy Performance — PYQ analysis

**Answers:** the mapping files list **no verified answers** (every entry says "VERIFICATION REQUIRED"). None are given here; this file records only the concept, the skill and the solving method.
Work the questions from the papers and check against an official key.

## 1. What the mapping says for this folder

[`questions.md` for this topic](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/questions.md) says: "No GATE CS question from the local papers (2007–2026) was identified for this syllabus line." It has **no entries**.

The performance-type questions (AMAT, effective access time, hit-rate arithmetic, write-policy statements, block-transfer time, memory bandwidth) were mapped into the sibling file
[`02-CACHE-MEMORY-MAPPING/questions.md`](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/questions.md)
(read-only; I did not modify it). Rows below carry the marker **mapped under 02-CACHE-MEMORY-MAPPING**.

What I searched: the cache mapping file (all 66 entries); the extracted paper text in `/tmp/pyqtxt` for the keywords interleav, refresh, DRAM, memory chip, chip select, burst, write buffer, write-through/back, hit ratio/rate, miss rate/penalty, access time, TLB, page fault, effective access.
Limits: the text extraction is noisy, figures are missing, and 2007–2012, 2019–2021 papers are mostly scanned (little or no text), so absence of a hit is not evidence of absence.

## 2. Table: performance-type entries (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill tested (paraphrased) | On-topic? | Where mapped | Paper |
|---|---|---|---|---|---|---|
| 2025 | Q.53 (CS-1) | NAT | Two-level cache + memory AMAT from a figure of hit rates and times; the text says L1 is looked up first, then L2, then memory (figure not in the mapping — numbers unknown) | Yes (needs figure) | mapped under 02-CACHE-MEMORY-MAPPING | [set-01](../../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2024 | Q.53 (CS1) | MCQ | Write-back vs write-through set-associative caches with LRU: dirty eviction on read miss, write-hit dirty bit, write-miss victim handling (option text is merged/garbled in the mapping) | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [set-01](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2022 | Q.24 | MCQ | Which statements about WB vs WT are FALSE: dirty bits, data transfer on write hit, eviction, read miss evicting a dirty block | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2022 | Q.33 | NAT | Break-even hit rate after an optimisation that lowers miss ratio but raises hit latency | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2020 | Q.21 | NAT | AMAT with miss penalty = first word + subsequent words of a block (64-bit words, large block); model of the hit time to be decided | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2019 | Q.45 | NAT | Maximum memory bandwidth of a single-level-cache system from controller cycles (accept address, fetch, transfer at one word per cycle) and a clock in MHz (printed header Set-2) | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [2019](../../../12-PYQ/2019/question-paper.pdf) |
| 2017 | Q.29 (Session 2) | MCQ | Solve for L1 and L2 miss rates from a given AMAT, level access times, L2→memory penalty and a ratio between the miss rates | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2017 | Q.45 (Session 2) | NAT | Average read time with I-cache, D-cache and a shared L2 and memory; 60/40 instruction/operand mix; "referred-word-first", write-back, dirty bit always 0 | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2016 | Q.50 (CS-2) | NAT | Average read latency of a file-system buffer cache against a miss-rate-vs-size curve; smallest size meeting a latency target (figure missing in mapping) | Partly — AMAT arithmetic, but OS buffer-cache context and missing figure | mapped under 02-CACHE-MEMORY-MAPPING | [set-02](../../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.18 (7 Feb, Shift 2) | NAT | Basic average read time from hit time, miss time and hit fraction | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [set-02](../../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2014 | Q.44 (Set-3) | NAT | Average access time over a sequence with instruction fetches, operand reads and writes, with different hit/miss times for reads and writes | Yes | mapped under 02-CACHE-MEMORY-MAPPING | [set-03](../../../12-PYQ/2014/set-03/question-paper.pdf) |
| 2014 | Q.43 (Set-2) | MCQ | Effect of block size on spatial locality, tag overhead, hit time and miss penalty | Yes (conceptual) | mapped under 02-CACHE-MEMORY-MAPPING | [set-02](../../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2010 | Q.48 | MCQ | Time to move a block from L2 to L1 when L1 misses and L2 hits (common-data question; bus/figure partly garbled by OCR) | Yes (figure partly missing) | mapped under 02-CACHE-MEMORY-MAPPING | [2010](../../../12-PYQ/2010/question-paper.pdf) |
| 2010 | Q.49 | MCQ | Total block-transfer time when both caches miss (memory → L2, then L2 → L1) (same common data) | Yes (figure partly missing) | mapped under 02-CACHE-MEMORY-MAPPING | [2010](../../../12-PYQ/2010/question-paper.pdf) |
| 2008 | Q.35 | MCQ | Which conditions are necessary for the inclusion property between L1 and L2 | Yes (conceptual) | mapped under 02-CACHE-MEMORY-MAPPING | [2008](../../../12-PYQ/2008/question-paper.pdf) |

Counts (my own): 15 entries, 14 clearly on-topic and 1 partial (2016 Q.50), all in the cache file; no duplicates among them. By year: 2025 ×1, 2024 ×1, 2022 ×2, 2020 ×1, 2019 ×1, 2017 ×2, 2016 ×1, 2015 ×1, 2014 ×2, 2010 ×2, 2008 ×1.

### Related performance-type questions mapped elsewhere or unmapped (not duplicated here)

| Year | Q# | Concept (paraphrased) | Where it is | Paper |
|---|---|---|---|---|
| 2025 | Q.55 (CS-2) | Two-level cache AMAT with "miss penalty" values from L2→L1 and memory→L2 — penalty-form AMAT (NOTES §4.3 penalty-style) | **not found in any mapping** (found by text search of `/tmp/pyqtxt`) | [set-02](../../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.56 (CS1) | CPI with memory stalls: ideal CPI, load/store fraction, I/D miss rates, penalty; speedup with a perfect cache (NOTES §5) | mapped under `08-PIPELINE-HAZARDS` | [set-01](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2023 | Q.42 | Memory built from four small blocks with a decoder on two chosen address bits; starting addresses of blocks (NOTES §6.3) | mapped under `02-DIGITAL-LOGIC` combinational circuits (the extracted text places it near Q.41) | [2023](../../../12-PYQ/2023/question-paper.pdf) |
| 2020 | Q.20 | Decoder input/output counts to address a 1 KB byte-addressable RAM (NOTES §6.2) | mapped under `02-DIGITAL-LOGIC` combinational circuits | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2018 | Q.23 | DRAM memory built from wide chips; rows per chip, refresh time and period; % time available for read/write (NOTES §6.4) | **not found in any mapping** (found by text search) | [2018](../../../12-PYQ/2018/question-paper.pdf) |
| 2020 | Q.53 | Paging with TLB, page-table in memory, page faults: effective access time (NOTES §8) | mapped under OS `08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY` | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2018 | Q.10 | From a measured average access time (normal vs faulting time) find the page-fault rate (NOTES §8) | OS folder | [2018](../../../12-PYQ/2018/question-paper.pdf) |
| 2014 | Q.33 (Set-3) | EAT with TLB hit ratio, TLB search time and memory time (NOTES §8) | OS folder | [set-03](../../../12-PYQ/2014/set-03/question-paper.pdf) |
| 2011 | Q.20 | Page-fault service time and fault frequency added to a memory access time (NOTES §8) | OS folder (scanned paper; text from the mapping only) | [2011](../../../12-PYQ/2011/question-paper.pdf) |

Because these are owned elsewhere or unmapped, they are not in the 15-entry count above. The coordinator may want to add 2025 CS-2 Q.55 and 2018 Q.23 to a mapping.

## 3. What has been tested (concept list)

- Average memory access time: one level (2015), with weights for read/write/fetch (2014), three-way cache split (2017), two levels with figure (2025) or algebra (2017), unmapped two-level penalty form (2025 CS-2).
- AMAT with a block-fill penalty (2020) and block-transfer time between levels (2010 ×2).
- Memory bandwidth of a burst-style miss service (2019).
- Break-even / unknown-solving (2022 hit rate; 2017 miss rates; 2016 cache size vs miss-rate curve).
- Write policy statements (2024, 2022).
- Block-size effects (2014) and inclusion (2008).
- Indirectly: CPI with memory stalls (2024 CS1 in the pipeline-hazard folder), memory blocks + decoder (2023, 2020 in DL), DRAM refresh (2018, unmapped), TLB/page-fault EAT (OS folder).

## 4. Recurring patterns

| Kind | Patterns | NOTES section |
|---|---|---|
| Numerical | hit/miss weighted time; nested multi-level AMAT; block-fill penalty; solving for hit/miss rate; bandwidth from cycles; read/write/fetch mix | §4, §2 |
| Numerical (indirect) | CPI with stalls; decoder/address-range; refresh %; EAT with TLB/page faults | §5, §6, §8 |
| Conceptual | WB vs WT; block size; inclusion; locality | §4.7, §1 |

The year spread of the 15 mapped rows is 2008–2025, with the numerical AMAT items concentrated in 2014–2022 and 2025. I do not give frequencies beyond these counts.

## 5. Important numerical patterns (solving recipes, no answers)

1. **Event-time average** ("a read takes X on a hit, Y on a miss"): T = h·X + (1−h)·Y. For read/write/fetch mixes: per-type time, then weights by count. (2015, 2014)
2. **Multi-stream hierarchical** (I-cache, D-cache, shared L2, memory): compute each stream's nested time, then weight by stream fraction. (2017 Q.45)
3. **Block-fill penalty** (2020): W = block bytes / word bytes (64-bit word = 8 B), P = first + (W−1)·next, then AMAT in the model that fits the wording (hit time added or not — state it).
4. **Burst bandwidth** (2019): cycles per block = sum of the serial stages; time = cycles / f; bytes = words × word size; express in the unit asked (×10^6 B/s).
5. **Bus-width transfers** (2010): ⌈block words / bus words⌉ × access time per transfer, summed over the sequential moves (memory→L2 then L2→L1); use the block size of the correct level.
6. **Solve for miss rates** (2017 Q.29): write AMAT with the ratio relation, solve the quadratic, reject out-of-range roots, verify.
7. **Break-even hit rate** (2022 Q.33): old AMAT = new AMAT with the slower hit time; solve for m'; h' = 1 − m'; take care of rounding direction.
8. **Cache-size from a curve** (2016 Q.50): table of AMAT per size; choose the first size meeting the target with the stated inequality.
9. **Two-level penalty-style** (2025): T = T1 + m1 (P12 + m2 P2m) if "miss penalty" values are given; if full access times are given, use the hierarchical or simultaneous formula the wording implies.

## 6. Traps to expect in these question kinds (patterns, not answers)

Years name the question kinds in which the trap can occur, judged from the question wording; I did not see official solutions.

- Hit time counted twice or not at all (penalty vs total time) — 2015, 2020, 2022.
- Local vs overall hit rates in multi-level problems — 2025, 2017.
- Word size in bits vs block size in bytes; W vs W − 1 — 2020, 2019.
- Weighting mixed accesses by 1/(number of kinds) instead of by counts — 2014, 2017.
- "Referred-word-first" or critical-word-first changes what the CPU waits for — 2017.
- Statement questions that confuse "dirty victim" with "write hit" — 2024, 2022.
- Inclusion design choices vs logical requirements — 2008.
- Rounding direction in "minimum hit rate" — 2022.

## 7. How the existing practice file complements the PYQs

The existing [`practice.md`](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/practice.md) trains the additive AMAT form (hit time + miss rate × penalty), the extra-latency two- and three-level forms,
CPI with I/D stalls and a page-fault average. It does **not** cover: the choice between hierarchical and simultaneous models, local vs global ratios, block-transfer penalties, bandwidth, read/write/fetch mixes, memory interfacing,
refresh or interleaving. [`PRACTICE.md`](PRACTICE.md) fills those gaps.

## 8. Mapping notes (data limitations)

- This folder's mapping is empty; the performance items sit in the cache folder. Mapping decisions are not mine to change.
- The cache file has 66 entries: 15 are the performance-type rows above; 17 are misfiled or not performance (non-COA: 2026 Q.53 free-block list, 2024 Q.16 and 2023 Q.52 web/DNS, 2023 Q.62 and 2008 Q.70 indexing, 2022 Q.35 DNS,
  2020 Q.24 grammar + web, 2019 Q.42 inode, 2017 Q.49 / 2015 Q.39 / 2007 Q.63 B+ tree order, 2014 Q.20 FAT, 2014 Q.30 join, 2012 Q.53 grammar fragment, 2010 Q.47 IP netmask, 2007 Q.79 derivation trees; COA but not performance: 2025 Q.28 "what is part of the ISA");
  the other 34 are cache-mapping questions (tag/index/offset sizes, set mapping, conflict traces, page colouring, 2013 booklets duplicates) owned by [`../02-CACHE-MEMORY-MAPPING`](../02-CACHE-MEMORY-MAPPING/).
- Missing figures: 2025 Q.53 (hit rates and times), 2016 Q.50 (miss-rate curve), 2010 Q.48–49 (bus widths are only partly legible in the text).
- 2010 Q.48–49 share a common-data block that is OCR-garbled in the mapping; the paper itself should be consulted.
- 2024 Q.53 options are merged in the mapping (text of A–D runs together).
- Scanned papers (2007–2012, 2019–2021) have little extracted text, so some performance-type items may exist unmapped.
- 2014 Q.44 appears for Set-1 (a different, cache-mapping question) and Set-3 (the one above): only the Set-3 entry is performance-type.
- Booklet duplicates (2013 ×4) concern cache mapping and are not in the performance list.

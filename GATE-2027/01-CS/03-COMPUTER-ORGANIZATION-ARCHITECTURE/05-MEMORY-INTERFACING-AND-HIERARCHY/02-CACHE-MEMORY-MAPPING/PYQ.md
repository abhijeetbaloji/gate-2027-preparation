# Cache Memory Mapping — PYQ analysis

**Answers:** the mapping file lists **no verified answers** (every entry says "VERIFICATION REQUIRED"). None are given here; this file records only the concept, the skill and the solving method. Work the questions from the papers and check against an official key.

**Mapping source (read-only):** [`questions.md`](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/questions.md)

Performance-type rows are also analysed in [`../01-PERFORMANCE/PYQ.md`](../01-PERFORMANCE/PYQ.md) (same mapping file, different triage lens).

---

## Table: all mapped entries (newest → oldest)

Triage: **cache** = mapping/organisation/trace; **performance-type** = AMAT, bandwidth, write-policy timing (see sibling folder); **OS-bridge** = page colours / VIPT; **misfiled** = wrong subject or garbled OCR fragment.

| Year | Q# (paper/set) | Type | Concept / skill tested (paraphrased) | Triage | Paper |
|---|---|---|---|---|---|
| 2026 | Q.38 (CS-1) | MCQ | DM tag M vs K-way tag N when K = 2^L; relation N = M + L | cache | [set-01](../../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2026 | Q.52 (CS-2) | MSQ | P,Q,R,S repeated loop: which variables always hit/miss (16 MB, 4 KB DM, 16 B blocks) | cache | [set-02](../../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2026 | Q.53 (CS-2) | NAT | Free-block list for a 16 GB disk — file-system block count, not cache | misfiled | [set-02](../../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2026 | Q.56 (CS-2) | NAT | Given address → cache block 176, find maximum DM cache size (KB) | cache | [set-02](../../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2025 | Q.36 (CS-1) | MCQ | Total bits to store all DM tag values (1M mem, 16K cache, 16 B blocks, 20-bit addr) | cache | [set-01](../../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.53 (CS-1) | NAT | Two-level cache AMAT from hit rates and access times in a figure (figure missing in mapping) | performance-type | [set-01](../../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.28 (CS-2) | MSQ | Which items are part of the ISA (cache size, clock, cache levels, register count) | misfiled | [set-02](../../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2025 | Q.39 (CS-2) | MCQ | Main-memory and cache data sizes from DM tag/index and 1-byte blocks | cache | [set-02](../../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.16 (CS1) | MCQ | TCP/DNS/HTTP packet order when fetching a web page | misfiled | [set-01](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.53 (CS1) | MSQ | Write-back vs write-through set-associative caches with LRU — which statements are true (options merged in mapping) | performance-type | [set-01](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2023 | Q.52 | MSQ | DNS/HTTP RTT count for rendering a web page | misfiled | [2023](../../../12-PYQ/2023/question-paper.pdf) |
| 2023 | Q.62 | NAT | Primary-index file block accesses for a database record search | misfiled | [2023](../../../12-PYQ/2023/question-paper.pdf) |
| 2023 | Q.64 | NAT | Tag field width for 64 KB 8-way cache, 32-bit byte address | cache | [2023](../../../12-PYQ/2023/question-paper.pdf) |
| 2022 | Q.24 | MSQ | Which statements about WB vs WT set-associative caches are **FALSE** | performance-type | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2022 | Q.33 | NAT | Minimum hit rate after optimisation raises hit time but lowers miss ratio | performance-type | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2022 | Q.35 | NAT | DNS query-response count for iterative resolution | misfiled | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2022 | Q.54 | MSQ | P,Q,R,S loop on 2 KB DM cache, 16-bit word, four hex addresses | cache | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2021 | Q.22 (Set-1) | NAT | Tag field size for 2^32 B memory, 32 KB DM cache, 64 B blocks | cache | [set-01](../../../12-PYQ/2021/set-01/question-paper.pdf) |
| 2021 | Q.18 (Set-2) | NAT | Associativity from tag width (2 KB SA cache, 64 B blocks, 32-bit addr, tag 22 bits; OCR garbled with number-rep text) | cache | [set-02](../../../12-PYQ/2021/set-02/question-paper.pdf) |
| 2020 | Q.21 | NAT | AMAT with block-fill penalty (first word + subsequent words, 64-bit words) | performance-type | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2020 | Q.24 | NAT | Bottom-up parser reductions + HTTP TCP connections (two unrelated fragments merged) | misfiled | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2020 | Q.30 | MCQ | Which pair of four hex addresses map to the same cache set (4-way, 64 KB, 256 B blocks) | cache | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2019 | Q.1 (Set-2 header) | MCQ | Fully associative 16 KB cache, 16 B blocks, 32-bit addr — tag and index field widths | cache | [2019](../../../12-PYQ/2019/question-paper.pdf) |
| 2019 | Q.42 (Set-2 header) | NAT | Unix inode maximum file size | misfiled | [2019](../../../12-PYQ/2019/question-paper.pdf) |
| 2019 | Q.45 (Set-2 header) | NAT | Memory bandwidth from controller cycles and clock on a cache miss service | performance-type | [2019](../../../12-PYQ/2019/question-paper.pdf) |
| 2018 | Q.34 | MCQ | Symbolic tag length for K-way cache (P, N, M, W, K notation) | cache | [2018](../../../12-PYQ/2018/question-paper.pdf) |
| 2017 | Q.29 (Session 2) | MCQ | L1/L2 miss rates from AMAT, access times, penalty and ratio between miss rates | performance-type | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2017 | Q.45 (Session 2) | NAT | Average read time with I-cache, D-cache, shared L2 and memory; 60/40 mix | performance-type | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2017 | Q.49 (Session 2) | NAT | B+ tree maximum order from block and key sizes | misfiled | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2017 | Q.53 (Session 2) | NAT | Tag bits for 2^32-byte memory, 512-line DM cache, 32-byte blocks | cache | [set-02](../../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2016 | Q.32 (CS-2) | NAT | Tag width for 40-bit addresses, 512 KB 8-way cache | cache | [set-02](../../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2016 | Q.50 (CS-2) | NAT | Buffer-cache average read latency vs cache size from a miss-rate curve (figure missing; OS context) | performance-type | [set-02](../../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.18 (7 Feb Shift 2) | NAT | Average read time from hit time, miss time and hit fraction | performance-type | [set-02](../../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2015 | Q.34 (8 Feb Shift 1) | MCQ | Tag and cache-line address in hex for a DM cache (consecutive bytes E201F/E2020) | cache | [set-03](../../../12-PYQ/2015/set-03/question-paper.pdf) |
| 2015 | Q.39 (8 Feb Shift 1) | NAT | B+ tree max keys in a non-leaf node | misfiled | [set-03](../../../12-PYQ/2015/set-03/question-paper.pdf) |
| 2014 | Q.44 (Set-1) | MCQ | Miss ratio bound for LRU with associativity A and reuse distance ≤ k | cache | [set-01](../../../12-PYQ/2014/set-01/question-paper.pdf) |
| 2014 | Q.9 (Set-2) | NAT | Tag bits for 4-way 16 KB cache, 8-word blocks, 32-bit words, 4 GB physical | cache | [set-02](../../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2014 | Q.20 (Set-2) | NAT | Maximum file size on a FAT-based file system | misfiled | [set-02](../../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2014 | Q.30 (Set-2) | MCQ | Nested-loop join disk-access optimisation | misfiled | [set-02](../../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2014 | Q.43 (Set-2) | MCQ | Effect of cache block size on locality, tag overhead, hit time, miss penalty | performance-type | [set-02](../../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2014 | Q.44 (Set-3) | NAT | Weighted AMAT over instruction fetches, operand reads and writes with different hit/miss times | performance-type | [set-03](../../../12-PYQ/2014/set-03/question-paper.pdf) |
| 2013 | Q.20 (Booklet A) | MCQ | k-way cache: line range for memory block j — **same question in Booklets A–D (Q.20/6/18/8)** | cache | [set-01](../../../12-PYQ/2013/set-01/question-paper.pdf) |
| 2013 | Q.53 (Booklet A) | MCQ | Minimum page colours so synonyms do not map to different sets — **same in Booklets A–D (Q.53/55)** | OS-bridge | [set-01](../../../12-PYQ/2013/set-01/question-paper.pdf) |
| 2013 | Q.6 (Booklet B) | MCQ | Duplicate of Booklet A Q.20 (k-way line range) | cache | [set-02](../../../12-PYQ/2013/set-02/question-paper.pdf) |
| 2013 | Q.55 (Booklet B) | MCQ | Duplicate of Booklet A Q.53 (page colours) | OS-bridge | [set-02](../../../12-PYQ/2013/set-02/question-paper.pdf) |
| 2013 | Q.18 (Booklet C) | MCQ | Duplicate of Booklet A Q.20 | cache | [set-03](../../../12-PYQ/2013/set-03/question-paper.pdf) |
| 2013 | Q.53 (Booklet C) | MCQ | Duplicate of Booklet A Q.53 | OS-bridge | [set-03](../../../12-PYQ/2013/set-03/question-paper.pdf) |
| 2013 | Q.8 (Booklet D) | MCQ | Duplicate of Booklet A Q.20 | cache | [set-04](../../../12-PYQ/2013/set-04/question-paper.pdf) |
| 2013 | Q.55 (Booklet D) | MCQ | Duplicate of Booklet A Q.53 | OS-bridge | [set-04](../../../12-PYQ/2013/set-04/question-paper.pdf) |
| 2012 | Q.53 (Booklet A) | MCQ | Grammar-production choices (OCR merged with cache common-data header for Q.54–55) | misfiled | [2012](../../../12-PYQ/2012/question-paper.pdf) |
| 2012 | Q.54 (Booklet A) | MCQ | Tag field width (linked: 256 KB 4-way WB cache, 32 B blocks, 32-bit addr, extra status bits) | cache | [2012](../../../12-PYQ/2012/question-paper.pdf) |
| 2012 | Q.55 (Booklet A) | MCQ | Cache tag-directory size in Kbits (same linked data) | cache | [2012](../../../12-PYQ/2012/question-paper.pdf) |
| 2010 | Q.47 | MCQ | IP netmask question (OCR merged with L1/L2 common-data header for Q.48–49) | misfiled | [2010](../../../12-PYQ/2010/question-paper.pdf) |
| 2010 | Q.48 | MCQ | Block transfer time L2 → L1 on L1 miss, L2 hit (common data; bus widths partly garbled) | performance-type | [2010](../../../12-PYQ/2010/question-paper.pdf) |
| 2010 | Q.49 | MCQ | Total transfer time when both L1 and L2 miss (same common data) | performance-type | [2010](../../../12-PYQ/2010/question-paper.pdf) |
| 2009 | Q.29 | MCQ | LRU trace on 4-way cache with 16 blocks — which block is absent at the end | cache | [2009](../../../12-PYQ/2009/question-paper.pdf) |
| 2008 | Q.35 | MCQ | Necessary conditions for inclusion between L1 and L2 | performance-type | [2008](../../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.70 | MCQ | Multi-level index block counts for a file (OCR merged with cache array common data Q.71–73) | misfiled | [2008](../../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.71 | MCQ | Total tag bits in cache directory (2-way 64 KB, 16 B blocks, 32-bit virtual addr) | cache | [2008](../../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.72 | MCQ | Which array element shares the same cache index as ARR[0][0] (row-major double array) | cache | [2008](../../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.73 | MCQ | Cache hit ratio for zeroing a 1024×1024 double array (same common data) | cache | [2008](../../../12-PYQ/2008/question-paper.pdf) |
| 2007 | Q.10 | MCQ | 4-way cache: tag, LINE and WORD field widths (block size in words) | cache | [2007](../../../12-PYQ/2007/question-paper.pdf) |
| 2007 | Q.63 | MCQ | B+ tree leaf order | misfiled | [2007](../../../12-PYQ/2007/question-paper.pdf) |
| 2007 | Q.79 | MCQ | Number of derivation trees (OCR merged with cache array linked Q.80–81) | misfiled | [2007](../../../12-PYQ/2007/question-paper.pdf) |
| 2007 | Q.80 | MCQ | Total data-cache misses reading a 50×50 byte array twice (DM, 32 lines of 64 B) | cache | [2007](../../../12-PYQ/2007/question-paper.pdf) |
| 2007 | Q.81 | MCQ | Which cache lines are replaced on the second pass of the same array | cache | [2007](../../../12-PYQ/2007/question-paper.pdf) |

**Counts (66 mapped rows):** cache 30 · performance-type 15 · OS-bridge 4 · misfiled 17.
**Distinct on-topic questions (merging 2013 booklet duplicates):** cache 27 · performance-type 15 · OS-bridge 1 · **43** total distinct COA-relevant questions.

---

## What has been tested

- **Address split:** tag/index/offset sizing; DM vs k-way vs FA; symbolic P,N,M,W,K form; tag directory bit count.
- **Reverse mapping:** associativity from tag width; memory/cache size from field widths; max cache size from one address→line fact.
- **Hex arithmetic:** address → set/line/tag; which addresses share a set.
- **Block placement:** k-way line-range formula (2013); fully associative tag/index = 0.
- **Tracing:** P,Q,R,S conflict loops; LRU final contents (2009); write-policy traffic.
- **Arrays:** row/column traversal misses; same cache index elements; two-pass wrap-around.
- **Theory:** LRU miss-ratio bound; block-size trade-offs; inclusion.
- **Performance (also in 01-PERFORMANCE):** AMAT one/two level, read/write mix, CPI stalls, bandwidth, WB/WT statements.
- **OS bridge:** page colours for VIPT (2013).

## Recurring patterns

| Kind | Examples | NOTES |
|---|---|---|
| Numerical | tag bits, tag storage, associativity, set from hex | §4–§9 |
| Numerical | max cache size, memory size from fields | §7 |
| Numerical | hit/miss count, LRU trace, array misses | §10–§11 |
| Numerical | AMAT, CPI, bandwidth | §15; 01-PERFORMANCE |
| Conceptual | organisations, 3C misses, block size, WB/WT, inclusion | §3, §12–§14, §16 |
| Bridge | page colours | §17 |

## Important numerical patterns (recipes, no answers)

1. **Tag bits:** o = log₂B; N = C/B; S = N/k; i = log₂S; t = A−i−o. Check t_DM + log₂k.
2. **Tag storage:** N × t bits; watch Kbit vs bit and MCQ factors of 2^10.
3. **Line from hex:** (addr >> o) mod N; pad address to A bits first.
4. **k-way line range:** lines (j mod v)·k through (j mod v)·k + (k−1).
5. **P,Q,R,S loop:** table of block, line, tag per variable; check same block and same-line conflicts.
6. **LRU trace:** per-set stacks; hit moves block to MRU; evict LRU on miss when full.
7. **Max cache:** binary search for offset o where L fits; extend i with leading zeros; capacity = 2^(o+i).
8. **Array two-pass:** count distinct blocks pass 1; pass 2 conflicts from line wrap.
9. **AMAT block fill:** W = block_bytes/word_bytes; P = t_first + (W−1)·t_next; state hierarchical vs simultaneous.
10. **Page colours:** x = (i+o) − log₂(page_size); colours = 2^x (get page size from the linked OS setup).

## Traps seen

- N = M + **L** not +K (2026). Index vs line vs set. Tag per line unchanged when B doubles but total tag bits halve.
- P,Q,R,S: variables in same block vs same line (2026, 2022). Word-length vs byte address (2022).
- Max cache: zero-extension and o+i ≤ A (2026). Figure-dependent AMAT (2025 Q.53, 2016 Q.50).
- WB/WT: FALSE vs TRUE stem; dirty victim on read miss (2024, 2022). Inclusion: necessary vs design choices (2008).
- 2013 page colours: four booklet duplicates; page size not in the mapping excerpt alone.
- OCR merges: 2012 Q.53 grammar, 2010 Q.47 netmask, 2008 Q.70 indexing, 2007 Q.79 TOC — use the paper PDF.

## How the existing practice file complements the PYQs

The existing [`practice.md`](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/practice.md) (22 questions) drills DM/SA/FA tag widths, tag+valid metadata, hex line number, DM and 2-way LRU traces, and a cycle-count formula. It does **not** include: symbolic N=M+L, max-cache reverse problems, P,Q,R,S loops, array wrap-around, AMAT/CPI, write-back traffic, page colours, or FIFO vs LRU comparison. [`PRACTICE.md`](PRACTICE.md) in this folder fills those gaps with original questions.

## Mapping notes

- **66 entries** in the mapping file; **17 misfiled** (TCP/DNS, file systems, DB, TOC/grammar, ISA, B+ trees, joins, IP netmask, OCR fragments).
- **2013:** one k-way mapping question and one page-colour question each printed in four booklets → 8 rows, 2 distinct skills.
- **2014 Q.44** appears twice in the mapping (Set-1 = LRU theory cache row above; Set-3 = performance AMAT).
- **Missing figures:** 2025 Q.53, 2016 Q.50, 2010 Q.48–49 (bus widths partly illegible in extracted text).
- **Scanned papers** (2007–2012, 2019–2021): little text in `/tmp/pyqtxt`; rely on PDFs for wording.
- **2021 Set-2 Q.18:** OCR merges a number-representation question with the cache associativity item — treat the cache part using the visible SA parameters.
- Performance-type rows are owned conceptually by [`../01-PERFORMANCE`](../01-PERFORMANCE/) but remain in this mapping file; both folders cross-link.

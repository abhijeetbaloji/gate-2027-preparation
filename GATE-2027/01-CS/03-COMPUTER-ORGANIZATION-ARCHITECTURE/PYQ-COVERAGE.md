# COA — PYQ Coverage (2007–2026)

Summary from the validated PYQ topic mapping in [`../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/). Full per-question tables live in each topic's `PYQ.md`.

**Answers:** mapping files mark every entry "VERIFICATION REQUIRED". This document does not state official answers.

---

## Totals

| Metric | Value |
|--------|------:|
| Mapped rows (all COA topic `questions.md` files) | 150 |
| Raw rows in cache mapping alone | 66 |
| On-topic cache rows (after triage) | 30 rows → 27 distinct |
| Performance-type rows (in cache file, taught in Performance) | 15 |
| Misfiled rows (in cache file) | 17 |
| Years with at least one mapped COA row | 2007–2026 (gaps in individual topics) |
| Topic folders with **zero** mapped rows | Microprogrammed, Memory Performance (own file) |

**Search limits:** text extraction from PYQ PDFs works for many 2013–2026 papers. **2007–2012, 2019, 2021** are mostly scanned — absence of mapping entries for those years does **not** prove the topic was not examined.

---

## By topic (mapped rows → see `PYQ.md` for triage)

| Topic folder | Mapped rows | Coverage verdict |
|--------------|------------:|------------------|
| 01 Instruction Set | 17 | Good; encoding family repeats 2016–2026 |
| 02 Addressing Modes | 3 | **Thin**; auto-increment in ALU file |
| 03 ALU | 3 | **Thin**; arithmetic PYQs mostly in Digital Logic mapping |
| 04 Hardwired | 1 | **Very thin** |
| 04 Microprogrammed | 0 | **None mapped** |
| 05 Performance | 0 (own file) | Via cache file: 15 performance-type rows |
| 05 Cache Mapping | 66 | **Densest**; includes misfiled non-COA items |
| 06 Interrupt | 13 | Moderate; 2013×4 duplicates |
| 06 DMA | 6 | Thin but recent numerics |
| 07 Pipelining | 16 | Moderate; overlaps hazards mapping |
| 08 Pipeline Hazards | 25 | Good; includes misfiled CN/DS items |

---

## By year (mapped rows, all COA files combined)

Approximate row counts per year (sum across topic files; **not** distinct exam questions because one question can appear in multiple booklet entries):

| Year | Rows (approx.) | Notes |
|------|---------------:|-------|
| 2026 | 7+ | ISA×2, cache×4, hazards×1, interrupt×1 — verify Q numbers on PDF |
| 2025 | 8+ | ISA, cache×4, pipelining, performance (unmapped AMAT in paper text) |
| 2024 | 10+ | ISA, cache, hazards×4, DMA×2, pipelining |
| 2023 | 3 | cache, interrupt |
| 2022 | 7+ | cache×4, DMA, hazards, pipelining |
| 2021 | 2 | cache×2 |
| 2020 | 5+ | ISA, ALU, cache×3, DMA, hazards |
| 2019 | 3 | cache |
| 2018 | 3+ | hardwired, cache, performance (DRAM refresh — unmapped) |
| 2017 | 4 | cache |
| 2016 | 6+ | ISA×2, ALU, cache×2, pipelining×2 |
| 2015 | 6+ | ISA×2, cache×3, pipelining, hazards×3 |
| 2014 | 10+ | cache×6, pipelining×2, hazards×2 |
| 2013 | 12+ | ISA×8 (2 Qs × 4 booklets), cache×8, interrupt×4, pipelining×4 |
| 2012 | 3 | cache |
| 2011 | 2 | addressing, pipelining (DMA misfiled in pipelining) |
| 2010 | 3 | cache |
| 2009 | 2 | cache, interrupt |
| 2008 | 8+ | ALU, cache×5, interrupt, pipelining×2, hazards |
| 2007 | 6+ | cache×5, interrupt, hazards, pipelining |

Exact per-year counts per topic: each folder's `PYQ.md` table.

---

## Recurring concepts (evidence-based)

### Numerical (highest frequency in mapping)

1. **Cache tag / index / offset / tag storage** — almost every even year.
2. **AMAT and multi-level hit rates** — filed under cache; taught in Performance + Cache.
3. **Pipeline speedup and clock from stage delays** — pipelining + hazards folders.
4. **Stall counting with forwarding / load-use** — hazards folder.
5. **Instruction-field and opcode-space arithmetic** — instruction set (and related addressing-mode encoding).
6. **CPU fraction: polling vs interrupt vs DMA** — I/O folders.
7. **Hit/miss trace on a reference string** — cache (P,Q,R,S loops, LRU traces).

### Conceptual

1. Load–store vs register–memory ISA; RISC characteristics (ISA + hardwired).
2. Write-through vs write-back statements.
3. RAW/WAR/WAW classification (hazards).
4. Interrupt recognition timing and entry sequence.
5. Burst vs cycle-stealing DMA properties.

---

## Topics with sparse or no confidently mapped PYQs

| Syllabus area | Status |
|---------------|--------|
| Microprogrammed control | **No mapped row** in 2007–2026; syllabus-driven only |
| Memory performance (own folder) | **Empty mapping**; 15 related rows under cache |
| Hardwired control (beyond RISC MCQ) | **1 row**; micro-op sequencing cross-filed |
| Addressing modes (standalone) | **3 rows**; concepts tested via ISA encoding elsewhere |
| ALU (this folder) | **2 on-topic rows**; Booth/overflow/CLA often under Digital Logic |

---

## Mapping noise (known issues)

| Issue | Examples |
|-------|----------|
| Misfiled non-COA | TCP/DNS (2024), file-system free list (2026), C stack program (2015), B+ tree / heap (hazards) |
| Misfiled within COA | Auto-increment → ALU; ISA items → cache; AMAT → cache only |
| 2013 booklet duplicates | Same question listed 4× with different booklet Q numbers |
| Garbled / incomplete text | 2020 datapath (ALU), 2015 stack program, 2024 DMA options |
| Missing figures/tables | 2015 reservation table (pipelining), 2009 cycle table, 2007 interrupt listing |
| Trailing garbage | 2024 Q61 (regex fragment), 2016 page footers |

Do not solve from mapping text alone when a row is flagged above — open the PDF.

---

## Unmapped COA-related questions (found in paper text, not in mapping)

Reported by topic workers during preparation; **not counted** in mapping totals:

| Year | Q# | Skill | Suggested topic |
|------|-----|-------|-----------------|
| 2025 | CS1 Q11 | Interrupt event ordering | Interrupt |
| 2025 | CS1 Q27 | Partial datapath (MSQ) | Hardwired / ALU |
| 2025 | CS-2 Q55 | Two-level AMAT | Performance |
| 2022 | Q17 | Highest-throughput I/O method | DMA / Interrupt |
| 2018 | Q23 | DRAM refresh overhead | Performance |

Coordinator may add these to the mapping later.

---

## How to use this with study material

1. Pick a topic from [`TOPIC-PRIORITY.md`](TOPIC-PRIORITY.md).
2. Read `NOTES.md` → solve `PRACTICE.md`.
3. Open topic `PYQ.md` → solve linked papers from [`../12-PYQ/`](../12-PYQ/).
4. For cache performance questions filed only under cache mapping, also read [`05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/NOTES.md`](05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/NOTES.md).

---

## Source

- Mapping index: [`../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/)
- Papers: [`../12-PYQ/`](../12-PYQ/)

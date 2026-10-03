# COA — Topic Priority

Based on **mapped PYQ rows** in [`../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/`](../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/) (2007–2026). Counts are **raw mapping rows** (2013 booklet duplicates inflate some folders). "Distinct" counts merge same question across booklets where noted in each topic's `PYQ.md`.

**Caveat:** the mapping is noisy (misfiled CN/DBMS/OS questions, garbled OCR, missing figures). Priority reflects **repository mapping evidence**, not an official GATE frequency table. Scanned papers (2007–2012, 2019, 2021) may contain unmapped COA questions.

| Topic | Mapped rows | Distinct (approx.) | Recent (2024–2026) | Priority |
|-------|------------:|-------------------:|:-------------------:|:--------:|
| Cache Memory Mapping | 66 | 43 on-topic | Yes (2026×4) | **High** |
| Pipeline Hazards | 25 | 13 on-topic | Yes (2026) | **High** |
| Instruction Pipelining | 16 | 7–13 on-topic | Partial (2025) | **High** |
| Instruction Set | 17 | 10 on-topic | Yes (2026×2) | **High** |
| Interrupt (I/O) | 13 | 7 on-topic | Yes (2026) | **Medium** |
| DMA (I/O) | 6 | 6 on-topic | Yes (2024×2) | **Medium** |
| Memory Performance | 0* | 15† | Yes (2025) | **Medium** |
| Addressing Modes | 3 | 4‡ | Yes (2026) | **Medium** |
| ALU | 3 | 2 on-topic | 2020 | **Lower** |
| Hardwired Control | 1 | 1 | 2018 | **Lower** |
| Microprogrammed Control | 0 | 0 | — | **Lower (syllabus)** |

\* Own mapping file is empty; performance-type questions are filed under the cache mapping (15 rows). See [`05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/PYQ.md`](05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/PYQ.md).

† Distinct performance questions counted from cache-mapping triage, not raw rows.

‡ Includes 2008 auto-increment question mapped under ALU but conceptually addressing modes.

**Total mapped rows across all COA topic files: 150** (sum of per-file `### Q.` counts).

---

## Priority bands

### High — study first; most mapped evidence and heaviest numerics

| Topic | Why |
|-------|-----|
| **Cache Memory Mapping** | Largest mapped set (66 rows); tag/index/offset, tracing, AMAT, write policies recur every few years. |
| **Pipeline Hazards** | Stall counting, forwarding, branch CPI; 25 mapped rows, many adjacent ideal-pipeline items in same file. |
| **Instruction Pipelining** | Speedup, clock period, stage splitting; pairs with hazards; several items also mapped under hazards. |
| **Instruction Set** | Opcode/immediate field arithmetic is a recurring NAT/MCQ family (2016, 2020, 2024–2026). |

### Medium — regular marks; complete after High band

| Topic | Why |
|-------|-----|
| **Memory Performance** | AMAT, interleaving, chip sizing — 15 performance-type mapped rows (filed under cache); own folder has no mapping entries. |
| **Interrupt** | Conceptual sequencing + polling/interrupt CPU-fraction NATs; thin but steady. |
| **DMA** | Burst vs cycle-stealing, rate from bus fraction; small set but recent (2024). |
| **Addressing Modes** | Only 3 mapped rows here, but skills appear in encoding questions elsewhere; practice file is substantial. |

### Lower — syllabus-required; sparse or zero mapped PYQs in this repo

| Topic | Why |
|-------|-----|
| **ALU** | 2 on-topic mapped questions (2020 datapath, 2016 CLA); most arithmetic PYQs mapped under Digital Logic. Depth is practice- and syllabus-driven. |
| **Hardwired Control** | 1 mapped MCQ (2018 RISC characteristics); micro-operation sequencing appears in interrupt/ALU mappings. |
| **Microprogrammed Control** | **Zero** mapped rows in 2007–2026 mapping; keyword search of extractable papers found no hit. Still on official syllabus — study from notes + practice. |

---

## Skill clusters that cross topic folders

These appear in PYQs mapped to a different leaf than the "natural" owner:

| Skill | Often mapped under | Natural home |
|-------|-------------------|--------------|
| AMAT / memory hierarchy numerics | Cache mapping | Performance + Cache |
| ISA vs microarchitecture (registers vs cache size) | Cache mapping | Instruction Set |
| Opcode counting with mode field | Addressing modes | Instruction Set |
| CPI with cache stalls | Pipeline hazards | Performance + Cache |
| Auto-increment addressing | ALU | Addressing modes |
| Data-path micro-step order | ALU | Hardwired + ALU |
| Booth / overflow / ripple carry | Digital Logic fixed-point | ALU |

See [`PYQ-COVERAGE.md`](PYQ-COVERAGE.md) for the full cross-reference list.

---

## Suggested time split (first pass)

| Band | Share of COA study time |
|------|:-----------------------:|
| High (cache + pipeline + ISA) | ~55–60% |
| Medium (performance + I/O + addressing) | ~30% |
| Lower (ALU + control) | ~10–15% |

Adjust after solving your first full PYQ pass — your weak clusters matter more than raw counts.

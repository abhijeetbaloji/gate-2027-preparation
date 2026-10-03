# Pipeline Hazards — PYQ Analysis

**Answers:** the mapping file lists **no verified answers** (every entry says "VERIFICATION REQUIRED") and **none are given here**. This file records what is tested and the solving method only.

- Mapping (read-only): [`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/08-PIPELINE-HAZARDS/questions.md)
- Theory: [`NOTES.md`](NOTES.md) · Practice: [`PRACTICE.md`](PRACTICE.md)

Counted from the mapping: **25 entries, 2007–2026**. After triage: **13 on-topic**, **6 adjacent** (ideal-pipeline timing or cache-stall CPI filed here but owned by topic 07 or 05), **6 misfiled** (non-COA). No duplicate booklet rows inside this mapping (2013 multi-booklet duplicates sit in topic 07).

---

## 1. Entry table (newest → oldest)

Papers: `../../12-PYQ/…` (relative to this folder). **On-topic?** Yes = hazard skill; Partial/Adjacent = ideal pipe or cache CPI; Misfiled = wrong subject.

| Year | Q# (paper/set) | Type | Concept / skill tested (paraphrase) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.16 (CS-1) | MCQ | Which register dependence among RAR/RAW/WAR/WAW can cause a **data hazard** in a pipelined processor | **Yes** | [2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2025 | Q.56 (CS-2) | NAT | Total time for 1000 instructions on a pipeline with stage delays and latch delay, **no stalls** | Adjacent (topic 07) | [2025 set-02](../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.30 (CS-1) | MSQ | Correct statements about **operand forwarding** (paths, hardware, stalls it cannot remove) | **Yes** | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.56 (CS-1) | NAT | Speedup with perfect cache vs real I/D miss rates; ideal CPI 2 — **cache performance**, not pipeline hazards | Adjacent (topic 05) | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.58 (CS-1) | NAT | Longest-prefix match on an **IP router forwarding table** — packet counts per next hop | **Misfiled** (CN) | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.58 (CS-2) | NAT | Speedup of 5-stage pipeline over non-pipelined unit at same GHz with **data- and control-stall fractions** | **Yes** | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2023 | Q.33 | NAT | Execution time for 100 instructions on a **3-stage pipeline, no hazards** | Adjacent (topic 07) | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2023 | Q.65 | NAT | **Router forwarding table** — which interface matches a destination IP | **Misfiled** (CN) | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2022 | Q.61 | NAT | Speedup from a **branch predictor** (accuracy given) that removes stalls only on correct predictions | **Yes** | [2022](../../12-PYQ/2022/question-paper.pdf) |
| 2021 | Q.53 (Set-1) | NAT | Total time for 100 independent instructions with **stage delays + register delay, no stalls** | Adjacent (topic 07) | [2021 set-01](../../12-PYQ/2021/set-01/question-paper.pdf) |
| 2021 | Q.53 (Set-2) | NAT | **ADD/MUL** sequence with multi-cycle EX, operand read in EX, speedup with vs without **operand forwarding** | **Yes** | [2021 set-02](../../12-PYQ/2021/set-02/question-paper.pdf) |
| 2020 | Q.15 | MCQ | Truth of statements about **IP router** behaviour (modify packets, routing protocol, reassembly) | **Misfiled** (CN) | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2020 | Q.43 | NAT | Pipelined speedup with **different clocks**, memory-instruction miss stalls, and **branch stalls** | **Yes** (mixed hazard + cache) | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2020 | Q.54 | NAT | Minimum disk accesses to retrieve a record in a **B+ tree** index | **Misfiled** (DBMS) | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2018 | Q.50 | NAT | Cycle count with a **variable-cycle PO/EX stage**, explicitly **no data or control hazards** | Adjacent (topic 07) | [2018](../../12-PYQ/2018/question-paper.pdf) |
| 2015 | Q.55 (7 Feb, Shift 1) | NAT | Speedup from pipelining with **lower clock** and **no stalls** | Adjacent (topic 07) | [2015 set-01](../../12-PYQ/2015/set-01/question-paper.pdf) |
| 2015 | Q.53 (7 Feb, Shift 2) | NAT | **MUL/DIV/ADD/SUB** sequence, 4-stage pipe, multi-cycle PO, **forwarding from PO to OF** | **Yes** | [2015 set-02](../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2015 | Q.49 (8 Feb, Shift 1) | MCQ | **Anti-dependence** (WAR) identification and whether it always stalls in a pipeline | **Yes** | [2015 set-03](../../12-PYQ/2015/set-03/question-paper.pdf) |
| 2014 | Q.43 (Set-1) | NAT | Speedup of 6-stage balanced pipeline when **25 % of instructions incur 2 stall cycles** | **Yes** | [2014 set-01](../../12-PYQ/2014/set-01/question-paper.pdf) |
| 2014 | Q.43 (Set-3) | NAT | **Stage split** redesign: new clock, branch fraction, IF stalls until next-IP — ratio of execution times old/new | **Yes** | [2014 set-03](../../12-PYQ/2014/set-03/question-paper.pdf) |
| 2012 | Q.20 (Booklet A) | MCQ | Purpose of **register renaming** in pipelined processors | **Yes** | [2012](../../12-PYQ/2012/question-paper.pdf) |
| 2009 | Q.60 | MCQ | **Heap/array** content after delete operations (C programming) | **Misfiled** (Programming) | [2009](../../12-PYQ/2009/question-paper.pdf) |
| 2008 | Q.36 | MCQ | Which statements are **NOT** true: bypassing all RAW, renaming all WAR, prediction eliminates all control penalty | **Yes** | [2008](../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.75 | MCQ | **C functions** f1/f2 return values (linked-answer preamble mentions delayed branching) | **Misfiled** (Programming; garbled OCR) | [2008](../../12-PYQ/2008/question-paper.pdf) |
| 2007 | Q.37 | MCQ | **ADD/MUL/SUB** with multi-cycle EX and **operand forwarding** — total clock cycles | **Yes** | [2007](../../12-PYQ/2007/question-paper.pdf) |

**Counts:** 25 entries · 13 on-topic · 6 adjacent · 6 misfiled · **21 distinct question texts** (2024 CS-1 has two Q.58 entries for different papers).

---

## 2. What has been tested (on-topic concepts)

1. RAW as the only in-order data hazard; RAR/WAR/WAW discrimination (2026, 2015 Set-3).
2. Operand forwarding: what it does, MEM→EX path, cannot remove every stall, needs hardware (2024 CS-1).
3. Stall counting with multi-cycle EX and forwarding vs no forwarding (2021 Set-2, 2015 Set-2, 2007).
4. CPI and speedup with data-stall and control-stall fractions (2024 CS-2, 2020, 2014 Set-1).
5. Branch predictor accuracy → CPI speedup (2022).
6. Pipeline redesign: stage split, branch penalty stage moves, clock changes (2014 Set-3).
7. Register renaming purpose; absolute claims on bypassing/prediction (2012, 2008).
8. Mixed memory-miss and branch stalls in one CPI (2020).

## 3. Recurring patterns

**Conceptual:** dependence type vs hazard (2026); forwarding capabilities (2024); anti-dependence statements (2015); renaming / "all/always" traps (2012, 2008).

**Numerical (dominant):** schedule a dependent sequence with variable EX latency (2007, 2015 Set-2, 2021 Set-2); `CPI = 1 + Σ f_i s_i` and speedup (2024 CS-2, 2020, 2014 Set-1); predictor speedup (2022); execution-time ratio after microarchitectural change (2014 Set-3).

## 4. Important numerical patterns (recipes, no answers)

| Pattern | Recipe |
|---|---|
| Variable-latency EX + forwarding | Schedule instruction by instruction; producer's **last** EX cycle gates the consumer; forwarding removes register-file wait, not serial EX occupancy (NOTES §5.6). |
| Speedup with stall fractions | `CPI_pipe = 1 + Σ f_i s_i`; `Speedup = (CPI_np × τ_np)/(CPI_pipe × τ_pipe)`; state whether ideal CPI is 1 or given (NOTES §8). |
| Branch predictor | `CPI_old = 1 + f_b P`; `CPI_new = 1 + f_b (1−a) P`; ratio (NOTES §7.6, E15). |
| Stage-split branch penalty | Recompute `P = r − 1` for the **new** resolution stage; recompute `τ = max stage + latch`; time = IC × CPI × τ (NOTES §7, 2014 Set-3 pattern). |
| Balanced k-stage, stall fraction, same clock | Asymptotic `Speedup = k/(1 + s)` where `s` = average stall cycles per instruction (2014 Set-1). |
| Mixed cache + branch stalls | One CPI sum: `1 + f_mem × m × M + f_b × q × P`; miss penalty only on memory instructions (2020). |

## 5. Traps seen

- Answering "all except RAR" for hazard MCQs — WAR/WAW are not hazards in-order (2026).
- "Forwarding needs no hardware" (2024).
- Treating forwarding as zero stalls for multi-cycle EX (2021 Set-2, 2007).
- Using branch fraction where instruction fraction is needed (2024 CS-2, 2022).
- Forgetting clock ratio when pipelined frequency drops (2020, 2014 Set-3).
- Calling WAW "anti-dependence" (2015 Set-3).
- Accepting "anti-dependence always stalls" (2015 Set-3).
- Absolute claims: all RAW / all WAR / all control (2008, 2012).
- Applying ideal-pipeline formulas to hazard questions without adding stalls (adjacent entries).

## 6. How the existing practice file complements the PYQs

The repository practice file (`14-PRACTICE-QUESTIONS/.../08-PIPELINE-HAZARDS/practice.md`, 18 questions) drills: RAW/WAR/control/structural definitions; no-forwarding chain (RF-A); load-use cycle count; branch flush count; predict-not-taken + load-use combined; structural CPI; stall-always CPI; compiler scheduling; delay-slot CPI; execution time from CPI; independent filler + taken branch. [`PRACTICE.md`](PRACTICE.md) in this folder adds original questions at the same skills with different numbers, including multi-cycle EX, predictor traces, BTB CPI, unified memory, and forwarding clock tradeoffs.

## 7. Mapping notes

| Issue | Entries |
|---|---|
| **Misfiled — Computer Networks (IP forwarding)** | 2024 CS-1 Q.58, 2023 Q.65, 2020 Q.15 |
| **Misfiled — other subjects** | 2020 Q.54 (B+ tree / DBMS), 2009 Q.60 (heap/C), 2008 Q.75 (C functions; OCR garbled) |
| **Adjacent — ideal pipeline (topic 07)** | 2025 Q.56, 2023 Q.33, 2021 Set-1 Q.53, 2018 Q.50, 2015 Set-1 Q.55 |
| **Adjacent — cache CPI (topic 05)** | 2024 CS-1 Q.56 |
| **OCR / text quality** | 2008 Q.75 mixes delayed-branch preamble with unrelated C code; 2015 Set-3 options garbled |
| **No figure/table missing** among on-topic entries | Variable-latency questions give EX times explicitly |

**Data sufficiency:** PYQ evidence for hazards is **SUFFICIENT** for data/control/structural stalls, forwarding, CPI algebra, and predictor concepts. Ideal-pipeline timing appears mainly in **adjacent** mapped entries (see topic 07). **Precise exceptions** and **BTB** have no direct mapped question but are syllabus-standard extensions of control hazards.

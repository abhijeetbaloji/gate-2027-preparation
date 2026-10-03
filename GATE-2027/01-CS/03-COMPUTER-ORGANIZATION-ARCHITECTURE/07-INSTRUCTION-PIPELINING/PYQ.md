# Instruction Pipelining — PYQ Analysis

**Answers:** the mapping file lists **no verified answers** (every entry says "VERIFICATION REQUIRED") and **none are given here**. This file records what is tested and the solving method only.

- Mapping (read-only): [`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/07-INSTRUCTION-PIPELINING/questions.md)
- Sibling mapping that also contains ideal-pipeline timing questions: [`08-PIPELINE-HAZARDS/questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/08-PIPELINE-HAZARDS/questions.md)
- Theory: [`NOTES.md`](NOTES.md) · Practice: [`PRACTICE.md`](PRACTICE.md)

Counted from the mapping: **16 entries, 13 distinct questions** (the 2013 five-stage question appears four times, once per booklet). Years with entries: 2025, 2024, 2016, 2015, 2014, 2013, 2011, 2009, 2008. No entries for 2007, 2010, 2012, 2017–2023 or 2026 in this folder's mapping.

---

## 1. Entry table (newest → oldest)

Papers: `../../12-PYQ/…` (relative to this folder). "On-topic?": **Yes** = ideal-pipeline model; **Partial** = shares ground with another topic (named); **Misfiled** = belongs elsewhere.

| Year | Q# (paper/set) | Type (per mapping) | Concept / skill tested (paraphrase) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2025 | Q.61 (CS-2) | NAT | Iron law: given instruction types with CPI and counts and total run time, find the clock period (no pipeline involved) | Partial (CPI/performance) | [2025 set-02](../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.31 (CS2) | MCQ in mapping; wording "is/are TRUE" | Classify register dependences (RAW/WAR/WAW) among four instructions | Partial (hazards sibling) | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2016 | Q.32 (CS-1) | NAT | Throughput increase (%) after replacing the slowest stage by two shorter stages | Yes | [2016 set-01](../../12-PYQ/2016/set-01/question-paper.pdf) |
| 2016 | Q.33 (CS-2) | NAT | New clock frequency after splitting the longest of three stages; stage latencies defined by ratio equalities | Yes | [2016 set-02](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.48 (8 Feb, Shift 1) | NAT | Minimum average latency from a reservation table — **table missing in mapping** | Yes (non-linear pipeline) | [2015 set-03](../../12-PYQ/2015/set-03/question-paper.pdf) |
| 2014 | Q.55 (Set-1) | NAT | Frequency of a second processor from "less time, more CPI" relative to the first | Partial (iron law) | [2014 set-01](../../12-PYQ/2014/set-01/question-paper.pdf) |
| 2014 | Q.9 (Set-3) | MCQ | Which of four pipelines (different depths, zero-delay registers) has the highest peak clock frequency | Yes | [2014 set-03](../../12-PYQ/2014/set-03/question-paper.pdf) |
| 2013 | Q.45 (A) / Q.28 (B) / Q.39 (C) / Q.33 (D) — same question in Booklets A–D | MCQ | Five-stage pipeline, unequal stage delays plus buffer delay, 12 instructions, one taken branch with no prediction: total time | Yes (shares control-hazard timing with sibling) | [set-01](../../12-PYQ/2013/set-01/question-paper.pdf) · [set-02](../../12-PYQ/2013/set-02/question-paper.pdf) · [set-03](../../12-PYQ/2013/set-03/question-paper.pdf) · [set-04](../../12-PYQ/2013/set-04/question-paper.pdf) |
| 2011 | Q.41 (Booklet A) | MCQ | Steady-state speedup of a four-stage pipeline with registers (delay in a figure) versus non-pipelined implementation; text OCR-garbled | Yes | [2011](../../12-PYQ/2011/question-paper.pdf) |
| 2011 | Q.28 (Booklet A) | NAT in mapping; options printed in text | Speedup of DMA transfer over an interrupt-driven byte-copy loop | **Misfiled** (DMA / I-O) | [2011](../../12-PYQ/2011/question-paper.pdf) |
| 2009 | Q.28 | MCQ | Cycles for a loop of four instructions through a four-stage pipeline given a table of cycles per stage — **table incomplete in mapping** | Yes | [2009](../../12-PYQ/2009/question-paper.pdf) |
| 2008 | Q.77 | MCQ | Which instruction can legitimately fill a single branch-delay slot; text has trailing unrelated text from another question | Partial (hazards sibling) | [2008](../../12-PYQ/2008/question-paper.pdf) |
| 2008 | Q.38 | MCQ | Earliest point in an instruction pipeline at which the data TLB can be accessed | Partial (memory/TLB bridge) | [2008](../../12-PYQ/2008/question-paper.pdf) |

(The 2013 row stands for four mapped entries; the 13 rows above plus the three extra 2013 copies make the 16 mapped entries.)

Counts by year (entries / distinct / on-topic for this folder): 2025 1/1/partial · 2024 1/1/partial · 2016 2/2/yes · 2015 1/1/yes (table missing) · 2014 2/2/(1 yes, 1 partial) · 2013 4/1/yes · 2011 2/2/(1 yes, 1 misfiled) · 2009 1/1/yes (table incomplete) · 2008 2/2/partial.

---

## 2. What has been tested (concepts)

1. Clock period/frequency from stage delays (max stage), frequency comparison across designs.
2. Effect of splitting the slowest stage: throughput gain %, new frequency.
3. Steady-state (asymptotic) speedup = non-pipelined time / pipelined clock, with a register delay.
4. Total time for N instructions on an unbalanced pipeline with buffer delay, including a taken branch.
5. Cycle count from a table of cycles per stage (multi-cycle stages, in-order).
6. Iron law: CPI × clock × IC; mix with per-class CPI; CPI/time/frequency algebra.
7. Non-linear pipeline: reservation table → minimum average latency.
8. Register dependence classes; delay-slot legality; TLB access ordering (borderline topics shared with other folders).

## 3. Recurring patterns

**Numerical (dominant):** stage-delay/split/frequency (2016 ×2, 2014 S3), steady-state speedup with register delay (2011), full time computation with branch (2013), CPI/frequency (2025, 2014 S1), table of cycles (2009), MAL (2015).
**Conceptual:** dependence labelling (2024), delay slot (2008), TLB position (2008).
The sibling mapping adds many more numerical items of the same ideal-model type (see §5), so the numerical skills of NOTES §4–§8 are the highest return.

## 4. Important numerical patterns (recipes, no answers)

| Pattern | Recipe |
|---|---|
| Highest frequency / new frequency | T_p = max(stage delays) + d; f = 1/T_p. After a split recompute the max over all stages (NOTES §6.1). |
| Throughput increase % after a redesign | (T_p,old / T_p,new − 1) × 100. |
| Stage latencies given as ratio equalities (e.g. τ1 = aτ2 = bτ3) | Choose a unit, express all stage latencies, identify the longest, then apply the split rule. |
| Steady-state speedup, figure with register delay | S_∞ = Σ stage delays / (max stage delay + register delay) assuming the non-pipelined version has no registers; read the figure to confirm where registers are. |
| Taken-branch timing, no prediction | T = max stage + buffer; cycles = p + r + m + k − 2 (NOTES §9.1); time = cycles × T. |
| Cycle table | Blocking schedule (NOTES §7.2); loop iterations repeat the instruction sequence; overlap across iterations is allowed only if stages are free. |
| CPI/time/frequency | T = IC·CPI/f; compare ratios; f_2 = f_1 (CPI_2/CPI_1)(T_1/T_2). |
| Mix → clock period | Σ count × CPI = cycles; T_clk = time / cycles; keep 10^8 factors. |
| MAL | Forbidden latencies → collision vector → state diagram → cheapest cycle (NOTES §7.3). |

## 5. Ideal-pipeline questions that are filed in the sibling mapping (not rows of this folder)

These belong to the model taught here and are in [`08-PIPELINE-HAZARDS/questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/08-PIPELINE-HAZARDS/questions.md). Skills only:

| Year | Q# | Skill |
|---|---|---|
| 2025 | Q.56 (CS-2) | total time for N instructions with stage delays and inter-stage latch delay |
| 2024 | Q.58 (CS2) | speedup with data- and control-stall fractions versus a multi-cycle baseline at the same frequency |
| 2023 | Q.33 | total time on a three-stage unbalanced pipeline |
| 2022 | Q.61 | speedup from removing branch stalls (CPI algebra) |
| 2021 | Q.53 (Set-1) | total time with stage delays plus register delay |
| 2021 | Q.53 (Set-2) | EX stage with different cycles for different instructions (forwarding comparison) |
| 2020 | Q.43 | speedup with different clocks and stall classes |
| 2018 | Q.50 | cycles with a variable-cycle PO stage (one multi-cycle stage) |
| 2015 | Q.55 (Shift 1) | speedup from CPI and frequency with no stalls |
| 2015 | Q.53 (Shift 2) | variable-cycle PO stage with forwarding |
| 2014 | Q.43 (Set-1) | balanced pipeline speedup with stall fraction |
| 2014 | Q.43 (Set-3) | splitting stages, branch fraction, execution time ratio old/new |
| 2007 | Q.37 | variable-cycle EX with forwarding |

Found in the text extraction but **in neither mapping**: GATE 2026 CS-2 — a pipelined versus non-pipelined (1.6 GHz, 5 cycles) comparison with a pipelined clock of 1.2 GHz and a stall fraction (appears near the Q.57 marker in `/tmp/pyqtxt/2026_set-02_question-paper.txt`; confirm the number in [2026 set-02](../../12-PYQ/2026/set-02/question-paper.pdf)); GATE 2026 CS-1 Q.60 — structural-hazard stalls from a variable-latency EX stage ([2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf)). Both are covered by NOTES §4, §7 and §8.

## 6. Traps seen

- Splitting the slowest stage but forgetting that another stage is now the slowest (2016).
- Ratio-defined stage latencies requiring a unit (2016 CS-2).
- Deeper pipelines are not automatically faster (2014 Set-3).
- Register or buffer delay in a figure: whether it enters the non-pipelined time (2011, 2013).
- Non-pipelined time vs pipelined time in "speedup" (2011).
- Branch with no prediction: skipped instructions and resolution stage (2013).
- Percent-change algebra for CPI and time (2014 Set-1).
- Powers of ten and unit conversion (2025).
- Table-driven cycle counts: overlap between loop iterations and blocking (2009).
- Forbidden latencies include non-adjacent marks in the same row (2015).

## 7. How the existing practice file complements the PYQs

The existing [`practice.md`](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/07-INSTRUCTION-PIPELINING/practice.md) covers k + N − 1, same-clock and different-clock speedup, asymptotic speedup, register overhead, replacing a stage by two, smallest k for a speedup, completed-by-cycle counting and one multi-cycle EX stage. It does **not** cover: frequency comparison across designs, ratio-defined stage latencies, taken-branch timing, multi-cycle tables with two slow stages, instruction-mix to clock period, non-linear pipelines/MAL, or utilisation. [`PRACTICE.md`](PRACTICE.md) adds those.

## 8. Mapping notes (noise and limitations)

- **Misfiled:** 2011 Q.28 (DMA vs interrupt-driven I/O) belongs to [`../06-IO-INTERFACE/02-DMA`](../06-IO-INTERFACE/02-DMA/). The question text in the mapping also prints its options inside the body while the mapping's "Type" says NAT.
- **Duplicates:** the 2013 question appears four times (Booklets A–D); counted once. The two 2014 entries (Set-1 Q.55 and Set-3 Q.9) are *different* questions, not duplicates.
- **Missing figure/table:** 2015 Q.48 (reservation table not captured, only some column numbers); 2009 Q.28 (cycle table partly missing: some cells blank); 2011 Q.41 (figure text garbled; stage delays and register delay are recoverable from the text but verify against the PDF).
- **Contaminated text:** 2008 Q.77 ends with the header of an unrelated linked-answer question (binary strings); the code listing in the mapping is also partly garbled (a branch line without a label). 2008 Q.38's text is clean.
- **Mis-typed:** 2024 Q.31 is typed MCQ but the wording "is/are TRUE" suggests a multiple-select item.
- **Partly other topics:** 2025 Q.61 and 2014 Q.55 are iron-law/CPI questions; 2024 Q.31 and 2008 Q.77 are hazard questions; 2008 Q.38 is a TLB/address-translation ordering question.
- **Coverage gaps:** this folder's mapping has no entries for 2007, 2010, 2012, 2017–2023, 2026. Several of those years do contain ideal-pipeline questions that were mapped to the hazards folder (see §5). Scanned papers (2007–2012, 2019–2021) give little or no extractable text, so unmapped questions there could not be searched.

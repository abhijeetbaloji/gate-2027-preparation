# PYQ Analysis — I/O Interface and Interrupts

**Answers:** the mapping file lists **no verified answers** (every entry is marked "VERIFICATION REQUIRED"), so **none are given here**.
This file paraphrases what each question tests and how to approach it; for solving methods see [`NOTES.md`](NOTES.md).

- Mapping source (read-only): [`questions.md`](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/01-INTERRUPT/questions.md)
- Papers: `../../../12-PYQ/<year>/…/question-paper.pdf` (links in the table)

## 1. Table of mapped entries (newest → oldest)

13 mapped entries = 10 distinct questions (the 2013 question appears in all four booklets A–D).

| Year | Q# (paper / set) | Type | Concept / skill tested (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.18 (CS-2) | MCQ | Two-statement truth test: time to start the ISR in non-vectored vs vectored interrupts; whether a daisy-chain scheme means the CPU polls every device | Yes | [PDF](../../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2024 | Q.25 (CS2) | MSQ | Which of four events (blocking read call, page fault on a swapped-out page, another process's disk interrupt, timer interrupt) always make the running process leave the running state | Partial (OS context-switch view of interrupts/exceptions) | [PDF](../../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2024 | Q.40 (CS1) | MCQ | Possible final values of two shared variables updated by two threads with arbitrary interleaving | **No — misfiled (OS concurrency)** | [PDF](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2023 | Q.34 (CS) | NAT | Ratio of CPU time (fraction of a second) for a keyboard handled by interval polling (poll cost + processing on a key) vs by interrupts; one decimal place | Yes | [PDF](../../../12-PYQ/2023/question-paper.pdf) |
| 2018 | Q.9 (CS) | MCQ | Order of five events after a device controller interrupts a running process (finish instruction, push status, load new PC, run ISR, pop status) | Yes | [PDF](../../../12-PYQ/2018/question-paper.pdf) |
| 2013 | Q.28 (A), Q.45 (B), Q.34 (C), Q.39 (D) — **same question in Booklets A–D** | MCQ | Identify what operation a four-line register-transfer sequence (copy PC into a buffer register, load MAR, overwrite PC, write buffer to memory) could be: fetch / operand fetch / branch / interrupt-service initiation | Yes | [A](../../../12-PYQ/2013/set-01/question-paper.pdf) · [B](../../../12-PYQ/2013/set-02/question-paper.pdf) · [C](../../../12-PYQ/2013/set-03/question-paper.pdf) · [D](../../../12-PYQ/2013/set-04/question-paper.pdf) |
| 2011 | Q.11 (CS, Booklet A) | MCQ | Which of four interrupt sources (CPU temperature sensor, mouse, keyboard, hard disk) is served at the highest priority | Yes | [PDF](../../../12-PYQ/2011/question-paper.pdf) |
| 2009 | Q.8 (CS) | MCQ | When a CPU actually services an interrupt (immediately / end of fetch / after the current instruction finishes / at fixed intervals) | Yes | [PDF](../../../12-PYQ/2009/question-paper.pdf) |
| 2008 | Q.64 (CS) | MCQ | Which statement about synchronous vs asynchronous I/O is false (ISR invocation on completion; whether the process waits; who wakes the waiting process) | Partial (OS I/O semantics; the ISR/interrupt link is the COA part) | [PDF](../../../12-PYQ/2008/question-paper.pdf) |
| 2007 | Q.73 (CS) | MCQ | Return address pushed when an interrupt occurs during a given instruction (byte-addressable memory, 32-bit word) | Yes — **but the instruction listing is missing in the mapping** | [PDF](../../../12-PYQ/2007/question-paper.pdf) |

Totals: on-topic distinct = **7** (2026, 2023, 2018, 2013, 2011, 2009, 2007); partial = **2** (2024 CS2, 2008); misfiled = **1** (2024 CS1 Q.40).

By year: 2026 → 1; 2024 → 2; 2023 → 1; 2018 → 1; 2013 → 4 copies (1 distinct); 2011 → 1; 2009 → 1; 2008 → 1; 2007 → 1.
No mapped entries for 2010, 2012, 2014–2017, 2019–2022, 2025.

### Questions found in the paper text but **not** in the mapping (for the coordinator)
Found by searching `/tmp/pyqtxt` for "interrupt" / "DMA" / "polling" (text extraction; 2007–2012, 2019–2021 are mostly scanned so this
search is blind there):

| Year | Where | Topic | Note |
|---|---|---|---|
| 2025 | CS1 (set-01) Q.11 | Order of three steps when an external device interrupts a non-pipelined CPU (save PC, load ISR address, finish instruction) | Same pattern as 2018 Q.9; not in the mapping |
| 2022 | Q.17 | Which I/O method gives the highest throughput for bulk disk-to-memory transfer (DMA / interrupt / polling / programmed) | Belongs more to DMA; not in the mapping |

I did not use them in the counts above.

## 2. What has been tested (concept list)

1. When an interrupt is recognised (end of current instruction) — 2009.
2. Order of events in interrupt handling (finish instruction → save state → load new PC → ISR → restore) — 2018 (and unmapped 2025).
3. Return address pushed to the stack — 2007 (listing missing).
4. Interrupt-entry micro-operations (saving the PC to memory while loading a new PC) — 2013.
5. Priority among interrupt sources — 2011.
6. Polling vs interrupt-driven CPU cost — 2023.
7. Vectored vs non-vectored speed; daisy chain vs polling — 2026.
8. Synchronous vs asynchronous I/O and the ISR's role — 2008.
9. Context-switch consequences of system calls, page faults, interrupts — 2024 CS2.

## 3. Recurring patterns

| Kind | Entries | Comment |
|---|---|---|
| **Conceptual one-liners** (when, order, priority, vectored/daisy) | 2026, 2018, 2013, 2011, 2009, 2008, 2007 (method-type) | The overwhelming majority; each is decided by one or two facts from NOTES §6, §8–§10 |
| **Numerical** | 2023 (NAT); 2007 (needs listing) | Single-step fraction arithmetic or address addition |
| **OS-flavoured** | 2024 CS2, 2008 | Require the "interrupt ≠ context switch" distinction (NOTES §13) |

## 4. Important numerical patterns (recipes, no answers)

1. **Polling vs interrupt ratio (2023).** Compute polls per second = 1/interval; polling fraction = polls × poll cost + (events per second) × processing;
   interrupt fraction = (events per second) × (total per-interrupt cost). Divide at the end and round once.
   See NOTES E6 and PRACTICE Q13.
2. **Return address (2007).** Needs the listing (not available in the mapping). Method: after the instruction completes the pushed PC is
   address + length in bytes of the interrupted instruction (or the target if a taken branch). NOTES E9, PRACTICE Q7, Q19.
3. **Event order (2018, unmapped 2025).** Three anchors: finish instruction first, save before load-PC, restore last. PRACTICE Q5.

## 5. Traps seen

- Choosing a "faster" reading of when interrupts are handled (immediately / end of fetch / at a fixed interval).
- Swapping the save-state and load-PC steps.
- Treating the interrupt-entry micro-operations as a branch or call without noticing the old PC is written to memory.
- Counting only successful polls; mixing ms and μs (2023-type).
- Ranking priority by user-visible importance rather than consequence of delay (2011-type).
- Equating a daisy chain with CPU polling (2026-type).
- Equating "any interrupt" with "process switch" (2024 CS2-type).
- Reading a mapped entry whose figure/listing is missing as if numbers were given (2007).

## 6. How the existing practice file complements the PYQs

The existing practice file (14 questions, in `../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/01-INTERRUPT/practice.md`) is heavier
on numerics (6 of 14 are CPU-fraction / cycle-count / maximum-rate questions) and on vectored vs non-vectored / daisy-chain statements,
while the PYQs are mostly sequencing and recognition. The new [`PRACTICE.md`](PRACTICE.md) adds the PYQ-style items that the existing
file lacks: event ordering (Q5), return address (Q7, Q19), priority by principle (Q11), polling-vs-interrupt ratio (Q13) and
the OS-flavoured context-switch distinction (Q21); it also adds I/O-fundamentals (Q1–Q4, Q6) that the existing file does not cover.

## 7. Mapping notes (noise and data limitations)

- **Misfiled:** 2024 CS1 Q.40 (shared-variable interleaving) is an OS concurrency question; excluded from pattern analysis.
- **Partly COA:** 2024 CS2 Q.25 and 2008 Q.64 are operating-system questions that touch interrupts; included only for the OS bridge (NOTES §13).
- **Duplicates:** 2013 appears four times (Booklets A–D at Q.28, 45, 34, 39); counted as one distinct question.
- **Missing listing:** 2007 Q.73 refers to a program of instructions (addresses and sizes) that is not reproduced in the mapping; the options alone are
  insufficient. The 2007 text extraction in `/tmp/pyqtxt` is essentially empty (scanned paper), so the listing could not be recovered. Use the PDF.
- **OCR garbage:** 2011 Q.11 option D carries stray page-header text; 2008 Q.64 prints "1/O" for I/O; 2007 Q.73 option D is followed by the heading of an unrelated
  Common Data question (TOC finite automaton) — not part of this question.
- **Unmapped but relevant:** 2025 CS1 Q.11 and 2022 Q.17 (above).
- Sets/booklets of 2014–2017 and 2019–2021 could not be searched reliably (scanned or not extracted); absence of entries there is **not** evidence of absence.

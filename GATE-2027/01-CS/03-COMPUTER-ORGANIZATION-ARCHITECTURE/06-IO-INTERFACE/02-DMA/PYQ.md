# DMA — Previous Year Questions

**Answers:** the mapping file lists no verified answers (every entry is marked "VERIFICATION REQUIRED"), and none are given
here. Solve from the linked papers and the methods in [NOTES.md](NOTES.md).

Mapping source: [questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/questions.md)
(6 entries, 2016-2024). Question text is not reproduced; each row is a paraphrase of what is tested.

## Table (newest -> oldest)

| Year | Q# (paper/set) | Type | Concept / skill tested | On-topic? | Paper |
|---|---|---|---|---|---|
| 2024 | Q.15 (CS1) | MCQ | Which statement is false among: cycle stealing moves one word per stolen cycle; burst vs stealing throughput; programmed vs interrupt-driven CPU utilisation; vectored vs non-vectored interrupt start-up | Yes (partly interrupt: see sibling) | [2024 Set-1](../../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.11 (CS2) | MCQ | Data transfer rate in bits/s from processor clock, bytes per cycle and percent of cycles used (cycle stealing) | Yes | [2024 Set-2](../../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2022 | Q.17 (CS) | MCQ | Which I/O mechanism gives the highest throughput for bulk disk-to-memory transfer | Yes | [2022](../../../12-PYQ/2022/question-paper.pdf) |
| 2021 | Q.20 (CS Set-2) | NAT | Data rate in bits/s from clock, percent of cycles, character moved per cycle | Yes | [2021 Set-2](../../../12-PYQ/2021/set-02/question-paper.pdf) |
| 2020 | Q.3 (CS) | MCQ | Four statements: daisy chain priority, vectored interrupt and polling, polling definition, CPU and DMA bus mastership | Partly (3 of 4 statements are interrupt-side; one is DMA) | [2020](../../../12-PYQ/2020/question-paper.pdf) |
| 2016 | Q.31 (CS-1) | NAT | Minimum number of bus takeovers to move a file given the count register width, KB file size, byte-addressable memory | Yes | [2016 Set-1](../../../12-PYQ/2016/set-01/question-paper.pdf) |

No duplicates across booklets were found in the mapping. Counts: 2016: 1, 2020: 1, 2021: 1, 2022: 1, 2024: 2; total 6 mapped, 6 distinct, 6 on-topic (1 partly).

## What has been tested

- Rate/percent-of-cycles calculations in cycle-stealing DMA (2 entries; clock, percent, bytes per cycle).
- Bus acquisitions needed for a large file, given the count register size (1 entry).
- DMA mode definitions and comparison (cycle stealing, burst) within a mixed true/false statement (1 entry).
- Choice of I/O mechanism for bulk transfer (1 entry).
- Bus mastership during DMA combined with interrupt-side statements (1 entry).

Not tested in the mapped entries: transparent mode, bus-arbitration numerics, synchronous/asynchronous bus numerics, DMA and
cache coherence, setup/completion break-even calculations.

## Recurring patterns

- Numerical (3 of 6): rate from clock × fraction × unit (2); file size to bus acquisitions via register capacity (1).
- Conceptual (3 of 6): statement sets and mechanism choice (3).

## Important numerical patterns (recipes, no answers)

1. Rate from percent of cycles: cycles/s = clock × percent; × bytes per cycle; × 8 for bits; units checked last (NOTES 8.2).
2. Bus acquisitions for a file: file bytes = size (KB) × 1024; capacity per programming = 2^m × unit; ceil of the ratio; state the 2^m convention (NOTES 8.9).

## Traps seen

- Bytes vs bits; character (8 bits) vs word; percent vs fraction (rate questions).
- KB vs 1000 bytes; ceiling vs floor; unit width (acquisition question).
- Statement questions mixing DMA with interrupt-handling topics, and CPU utilisation with throughput.
- A statement about bus mastership that sounds plausible but contradicts the one-master-at-a-time rule.

## How the existing practice file complements the PYQs

[Existing practice](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/practice.md)
covers the same rate, register size and mode-definition skills (Q2, Q3, Q5, Q7, Q8, Q10, Q11) and adds overhead and stall-limit
numerics (Q9, Q12). It does not contain a count-register/bus-acquisition question, arbitration, bandwidth, or coherence;
those are covered in [PRACTICE.md](PRACTICE.md) (Q9, Q8, Q11-Q12, Q16).

## Mapping notes

- All six entries are I/O/DMA questions; none is misfiled. The 2020 entry is mostly interrupt-side and also relevant to
  [../01-INTERRUPT](../01-INTERRUPT/NOTES.md).
- The mapping text for 2024 CS1 Q.15 is garbled: the stem line and the options are merged and the option letters do not
  line up with the question text (words of option A sit in the stem, and option text runs into the next line). Read the
  full text in the paper PDF. The 2024 CS2 Q.11 stem in the mapping omits the processor clock and the bytes per cycle (only
  the tail of the question is shown); read the paper. The 2021 and 2016 NAT entries have no options.
- Scanned years (2019, 2021 Set-1, 2007-2012) give no usable text, so absence of DMA entries there cannot be concluded.
- Related entries in the sibling mapping (not copied here): interrupt-polling overhead calculations (2023), vectored interrupts (2018, 2026).
- Data limits: 6 entries over 2016-2024; no mapped entry for 2007-2015, 2017-2019, 2023, 2025, 2026.

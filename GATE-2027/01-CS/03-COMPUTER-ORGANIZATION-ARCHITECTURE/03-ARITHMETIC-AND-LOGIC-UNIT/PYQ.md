# Arithmetic and Logic Unit — PYQ Analysis

> **No verified answers.** The mapping file marks every answer "VERIFICATION REQUIRED". This file gives no official answer for any past question; it records what each question tests and how to solve that kind of question (method and traps). Confirm answers from the official key.

* Mapping file (read only): [questions.md](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/03-ARITHMETIC-AND-LOGIC-UNIT/questions.md)
* Theory: [NOTES.md](NOTES.md) · Practice: [PRACTICE.md](PRACTICE.md)

## 1. Mapped entries (newest → oldest)

| Year | Q# (paper/set) | Type | Concept / skill tested (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2020 | Q.4 (CS) | MCQ | Correct order of the micro-steps that execute a register-to-register add on a single-bus data path with temporary registers; fetch chain, operand staging, ALU, write-back | Yes (data path); figure garbled in the mapping | [2020 paper](../../12-PYQ/2020/question-paper.pdf) |
| 2016 | Q.33 (CS-1) | MCQ | Asymptotic time of a carry-lookahead adder when gates have fan-in at most two | Yes | [2016 set-01](../../12-PYQ/2016/set-01/question-paper.pdf) |
| 2008 | Q.33 (CS) | MCQ | Statements about the auto-increment addressing mode (self-relocating code, extra ALU for effective address, increment depends on operand size) | **No — misfiled; addressing-modes concept** | [2008 paper](../../12-PYQ/2008/question-paper.pdf) |

Entry count: **3 mapped entries** (2020: 1, 2016: 1, 2008: 1); **2 distinct on-topic** questions, 1 misfiled, 0 duplicates.

## 2. What has been tested (from the mapped entries)

* Data-path register-transfer sequencing (2020 Q.4).
* Asymptotic delay of lookahead adders with bounded fan-in (2016 CS-1 Q.33).
* (Misfiled) auto-increment addressing semantics (2008 Q.33): a question about *addressing modes*, covered in [../02-ADDRESSING-MODES](../02-ADDRESSING-MODES), not here.

## 3. Related ALU-skill PYQs that the mapping files under Digital Logic (read-only pointers)

The ALU skills that GATE examines most are mapped in the Digital Logic number-representation file, [01-FIXED-POINT/questions.md](../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT/questions.md). They are **not counted** in the entry counts above (they are not in this topic's mapping) but they use the methods of this folder. Verified to exist in that file:

| Year | Q# | Skill (paraphrased) | Method in NOTES |
|---|---|---|---|
| 2025 | Q.32 (CS-2) | Number of additions and subtractions when two 16-bit 2's-complement numbers are multiplied with Booth's algorithm (NAT) | §10.3: count bit changes of the multiplier with an appended 0 |
| 2024 | Q.13 | Which operation on two 5-bit 2's-complement numbers overflows or underflows | §7.2 sign rule; check the `2 * B` option with a left shift (§9.2) |
| 2022 | Q.18 | Which pair of 4-bit 2's-complement operands overflows when added | §7.2 sign rule / carries XOR |
| 2016 | Q.7 (CS-2) | For a given A in an 8-bit ripple-carry adder, which B gives the longest latency (NAT) | §4.1 longest carry chain |
| 2010 | Q.8 | 2's-complement representation of 8 × P for a 16-bit P given in hex | §9.2 left shift as ×2ᵏ with overflow check |

Floating-point ALU questions (IEEE 754 operations) are mapped in the sibling file [02-FLOATING-POINT/questions.md](../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT/questions.md); NOTES §12 gives the ALU-level steps.

### Found by text search of `/tmp/pyqtxt`, absent from this and the Digital Logic mapping (not counted, not verified)

* 2026 set-01, Q.22 and 2026 set-02, Q.28: overflow of arithmetic operations on short signed numbers (sign-magnitude in one, 2's complement in the other). Method: NOTES §2 (sign-magnitude overflow is a magnitude carry-out) and §7.2.
* 2025 set-01 (CS-1), Q.27: select-the-correct-statements question about arithmetic operations possible with a partial data path (registers RA, RB, RZ). The figure is not present in the extracted text, so the exact structure is unknown; the concept is NOTES §13.4 (operand-select multiplexers).

Limits of this search: the 2007–2012, 2019, 2020 and 2021 papers are mostly scanned images and gave almost no text, so questions there could not be searched.

## 4. Recurring patterns

| Pattern | Kind | Where in NOTES |
|---|---|---|
| Delay/complexity class of an adder (ripple, lookahead, skip/select) | Conceptual | §5.5, §6.3 |
| Ripple adder worst-case input / latency | Numerical (NAT) | §4.1 |
| Overflow vs carry detection in fixed-width add/subtract | Numerical/conceptual | §7.2–§7.5 |
| Booth's algorithm operation count or trace | Numerical (NAT) | §10.3–§10.4 |
| Shift as multiplication/division and 2's-complement left shift | Numerical | §9.2 |
| Data-path micro-step ordering / counting | Conceptual-ordering | §13 |

## 5. Important numerical patterns (recipes, no answers)

1. **Adder delay with a stated gate model.** Draw the critical path: P/G → (block G*/P*) → carries → sum. Use the per-level numbers from the question; the path that matters goes through the top-level carry, not through the first section.
2. **Longest ripple latency for a given A.** The chain begins at the lowest set bit of A and must propagate to the MSB; choose B = −A (NOTES §4.1). Chain length n − k.
3. **Overflow.** Convert the patterns; apply the sign rule (addition: same-sign operands and different-sign result; subtraction: different-sign operands and a result whose sign differs from the minuend's).
4. **Booth.** Append 0 to the multiplier; count adjacent differences; do not count shifts.
5. **Left shift multiplication.** Hex → signed → ×2ᵏ → check the representable range, or shift the bit pattern directly and compare the top k + 1 bits.
6. **Register-transfer ordering.** Build the dependency graph from the labels of each step (what it reads, what it writes), starting from PC → MAR → MDR → IR; eliminate options that violate an edge.

## 6. Traps seen

* **2016 Q.33 type:** Θ(1) (unbounded fan-in thinking), Θ(√n) (skip/select), Θ(n) (ripple) all appear as options; the phrase "fan-in at most two" is the deciding assumption.
* **2020 Q.4 type:** operand order and the temporary-register staging; the memory read must complete before the IR is loaded; the result passes through a temporary before it reaches the destination register.
* **2008 Q.33 type:** (misfiled) mixing addressing-mode semantics with ALU hardware.

## 7. How the existing practice file complements the PYQs

The existing [practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/03-ARITHMETIC-AND-LOGIC-UNIT/practice.md) (14 original questions) is aimed at the arithmetic and flag skills: full-adder equations, flags for specific additions, ripple delay, subtraction by 2's complement, sequential-vs-array multiplication time, two-level CLA timing and signed/unsigned comparison by flags. It has **no** question on the data-path ordering skill (2020) or on the fan-in-2 asymptotics (2016), Booth, division, shifters or floating point; those are covered in this folder's [PRACTICE.md](PRACTICE.md) (Q5, Q22 for the CLA asymptotics; Q14, Q15 for the data path; Q8, Q16, Q23 for Booth; Q12 for division; Q2, Q3, Q9, Q18 for shifts; Q20, Q21 for floating point).

## 8. Mapping notes (data quality)

* **2008 Q.33 is misfiled.** It is an addressing-mode (auto-increment) question; the ALU mention in one statement is why it landed here. Excluded from the ALU pattern analysis. Its concept belongs to [../02-ADDRESSING-MODES](../02-ADDRESSING-MODES).
* **2020 Q.4: figure and notation garbled.** The data-path diagram is only a jumble of component labels in the mapping (bus, TEMP1, TEMP2, MAR, MDR, IR, PC, R0…R7, ALU, "to memory"); the connections are lost. The step notation also has OCR damage (stray characters instead of subscripts, a missing line break between two options, option C rendered with a stray symbol). The register-transfer *method* is independent of the figure (NOTES §13.2), but to answer the actual question use the PDF. Nothing was guessed about the diagram.
* **2016 Q.33:** option text is partly damaged (a square-root sign missing from one option, a page-footer fragment glued to the last option, a stray tick mark beside one option). The tick is an extraction artefact, not evidence of the key.
* No duplicates exist in this topic's mapping.
* **Data sufficiency:** PYQs — THIN (2 genuine entries). Syllabus sub-areas of this topic with no mapped ALU-folder PYQ: flags and conditional branches, ALU function select, shifters/barrel shifters, multiplication/division hardware, floating-point arithmetic (these appear, if at all, under Digital Logic), carry-select/skip.

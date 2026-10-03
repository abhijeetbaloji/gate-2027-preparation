# Hardwired Control — PYQ Analysis

**Answers:** the mapping lists **no verified answers** (every entry says "VERIFICATION REQUIRED"), and **none are given here**. Check the official key before relying on any answer.

- Mapping file (read only): [questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/questions.md)
- Existing practice file (read only): [practice.md](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/practice.md)
- Study material: [NOTES.md](NOTES.md) · [PRACTICE.md](PRACTICE.md) · sibling [../02-MICROPROGRAMMED](../02-MICROPROGRAMMED)

## 1. Mapped entries of this topic (newest → oldest)

| Year | Q# (paper/set) | Type | Concept / skill tested (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2018 | Q.5 (CS) | MCQ | Decide which of three listed design features — register-to-register arithmetic only, fixed-length instruction format, hardwired control unit — belong to RISC design; answer options are combinations of the features | Yes (RISC characteristics; hardwired control is one of the features) | [2018 paper](../../../12-PYQ/2018/question-paper.pdf) |

Entries in the mapping for this topic: **1**. Distinct on-topic questions: **1**. Years with no mapped entry: every other year 2007–2026.

## 2. Cross-filed questions that use the same skills (not in this folder's mapping; mapping files not modified)

| Year | Q# | Where filed | Type | Skill | Relevance | Paper |
|---|---|---|---|---|---|---|
| 2020 | Q.4 (CS) | `03-ARITHMETIC-AND-LOGIC-UNIT/questions.md` | MCQ | Arrange a shuffled list of register-transfer steps for one register-register ALU instruction on a bus-based data path (fetch steps included) into a valid order | Directly the "control signals sequence data-path steps" skill (NOTES §5.6) | [2020 paper](../../../12-PYQ/2020/question-paper.pdf) |
| 2013 | Q.28 (Booklet A), Q.45 (B), Q.34 (C), Q.39 (D) | `06-IO-INTERFACE/01-INTERRUPT/questions.md` | MCQ | Interpret a four-line micro-operation sequence written with MBR, MAR, PC and memory and decide what kind of operation it performs | Register-transfer / micro-operation reading skill (NOTES §5); same question in four booklets | [Booklet A](../../../12-PYQ/2013/set-01/question-paper.pdf), [B](../../../12-PYQ/2013/set-02/question-paper.pdf), [C](../../../12-PYQ/2013/set-03/question-paper.pdf), [D](../../../12-PYQ/2013/set-04/question-paper.pdf) |

Unmapped candidate noticed (not counted anywhere): GATE 2025 CS1 (set-01) Q.27, "a partial data path with registers RA, RB, RZ — which arithmetic operand combinations can it implement" (MSQ). The figure is missing from the extracted text, and the question appears in none of the COA mapping files I checked, so it may be unmapped. It exercises *reading a data-path figure* (NOTES §5.7), not hardwired control as such; flag for the coordinator. Paper: [2025 set-01](../../../12-PYQ/2025/set-01/question-paper.pdf).

## 3. What has been tested

- Which processor design features are characteristic of RISC, including the hardwired-control feature (2018).
- (Cross-filed) ordering of micro-operations on a bus-based data path with temporary registers (2020).
- (Cross-filed) interpreting a micro-operation sequence in register-transfer notation (2013).
- Not tested in any mapped entry: step-counter/state-register sizing, control-signal equations, ROM sizing, clock-period computation, CPI from control steps, hardwired-vs-microprogrammed speed numerics. These appear only in the existing practice file.

## 4. Recurring patterns

| Pattern | Kind | Evidence | NOTES section |
|---|---|---|---|
| Classify design features as RISC / not RISC | Conceptual, statement-by-statement | 2018 Q.5 | §12.2, §15 P1 |
| Order or interpret register-transfer micro-operations | Procedural / reading | 2020 Q.4, 2013 Q.28 family (cross-filed) | §5, §5.6, §15 P2–P3 |

## 5. Important numerical patterns (with recipes; no answers)

The mapping contains no numerical hardwired-control PYQ. The numerical skills in the existing practice file, and where to learn them:

| Skill | Recipe | NOTES |
|---|---|---|
| Counter / state bits | N from the design described, then ⌈log₂ N⌉ (or N flip-flops for one-hot) | §6, §8 |
| Execute steps of an instruction | Draw the micro-op table; count steps | §5, Shortcut S2 |
| ROM size | 2^(opcode + step bits) × signals; ÷ 8 for bytes | §8.4 |
| Clock period | clk→Q + max(parallel decoders) + logic (+ datapath) + setup | §10 |
| CPI / time | Σ fraction × cycles; time = IC × CPI / f | §9 |

## 6. Traps seen

- 2018 Q.5 kind: judging a combination question by the one feature you remember. Check all three features individually and combine afterwards; confirm against the official key (not provided in the mapping).
- 2020 Q.4 kind (cross-filed): operand order for a non-commutative operation, and fetch steps that must come before execute steps; the mapped text is garbled (see Mapping notes), so work from the PDF figure.
- 2013 Q.28 kind (cross-filed): reading the micro-operations by what they *do* (what is saved, which address is formed, what is loaded into the PC), not by register names.

## 7. How the existing practice file complements the PYQs

The 10-question existing file is mostly small numerical counting (bits, ROM size, cycles, clock period) and statements about hardwired control. It gives almost nothing on the RISC-characteristic pattern that is the actual mapped PYQ; [PRACTICE.md](PRACTICE.md) adds Q4 and Q21 for that, and Q19 for the data-path ordering skill. See the coverage map in NOTES §19.

## 8. Mapping notes (data limitations)

- The mapping for this folder is a single, clean entry; its text matches the 2018 paper's extracted text near Q.5.
- The 2020 entry in the ALU folder is OCR-garbled: step labels such as "R21, TEMP1r, ALUadd, TEMP2w" and "PC,, MAR, MEM," are damaged, one option line is mangled ("() 3,5,2,1,4"), and the data-path figure appears only as a list of box names. Do not trust the mapping text for that question; use the PDF. The paper itself is scanned, and the plain-text extraction in `/tmp/pyqtxt/2020_question-paper.txt` has no text for it.
- The 2013 micro-operation question appears four times (Booklets A–D) in the Interrupt folder; it is one question.
- Search performed in `/tmp/pyqtxt` (2013–2026 extractions; the 2007–2012, 2019, 2020, 2021 papers are mostly scanned and yield almost no text): "hardwired" and "control unit" occur only in 2018; "microprogram", "control word", "control store", "microinstruction", "CISC" occur nowhere; "micro-operation" occurs only in the four 2013 booklets; "RISC" occurs in 2018 (the entry above and a pipeline question) and in 2022 (pipeline wording only); "control signal" occurs once, in a 2014 set-02 memory-bus question (not a control-unit question); "data path" occurs in 2025 set-01 (the unmapped candidate above). Because the scanned years give no text, **absence of hits for 2007–2012, 2019–2021 is not evidence of absence**.

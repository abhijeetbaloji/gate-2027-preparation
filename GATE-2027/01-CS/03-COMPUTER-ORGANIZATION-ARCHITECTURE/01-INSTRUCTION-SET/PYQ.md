# Instruction Set — PYQ Analysis

**Answers:** the mapping file lists **no verified answers** (every entry says "VERIFICATION REQUIRED"); none are given in this repository folder.
This file paraphrases what each question tests; it never reproduces question text.

- Mapping (read-only): [`questions.md`](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/01-INSTRUCTION-SET/questions.md)
- Method notes: [`NOTES.md`](NOTES.md) (section numbers below refer to it) · practice: [`PRACTICE.md`](PRACTICE.md)
- Counts: **17 mapped entries** = **11 distinct questions** (2013 appears as 8 entries of 2 questions across 4 booklets). **1 misfiled** (2015 Q52). **10 distinct on-topic or partly on-topic questions.**

## Table (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill tested (paraphrase) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.15 (CS-1, forenoon) | MCQ | Choose the instruction sequence that realises `Z = X + Y` on a load–store ISA with destination-first operands (NOTES §4.4) | Yes | [PDF](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2026 | Q.44 (CS-2, afternoon) | MCQ | Three fixed-length formats with different operand layouts; maximum unique opcodes of the third given counts of the other two (variable-sized opcodes) (NOTES §6.4) | Yes | [PDF](../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2025 | Q.37 (CS-1) | MCQ | Maximum immediate bits in a fixed 32-bit word given register count, instruction-type count and an add-immediate form (NOTES §6.1) | Yes | [PDF](../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2024 | Q.61 (CS2) | NAT | Two instruction formats (R-type, I-type) separated by one opcode bit; equal split of the instruction count; compute UNUSED, opcode and immediate widths and combine them (NOTES §6.3) | Yes (the entry also carries an unrelated regular-expression sentence at its end) | [PDF](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2020 | Q.44 (CS) | NAT | 16-bit word, 64 registers, I-type (register + 4-bit immediate) and R-type (two registers); maximum R-type opcodes given the number of I-type opcodes (NOTES §6.4) | Yes | [PDF](../../12-PYQ/2020/question-paper.pdf) |
| 2016 | Q.10 (CS-2) | NAT | Bits left for the immediate: 32-bit word with opcode, two register fields, immediate; instruction and register counts not both powers of two (NOTES §6.1) | Yes (page-footer garbage in text) | [PDF](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2016 | Q.31 (CS-2) | NAT | Byte-aligned program size: five-field instruction (opcode, three register ids, 12-bit immediate), fixed program length (NOTES §6.2) | Yes | [PDF](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.22 (CS, 7 Feb shift 1) | MCQ | What the address fields of a three-address instruction can specify (memory operand, register, implied accumulator) (NOTES §3.2) | Yes | [PDF](../../12-PYQ/2015/set-01/question-paper.pdf) |
| 2015 | Q.52 (CS, 7 Feb shift 2) | NAT | Output of a C program with array-based stack functions | **No — misfiled** (programming / data structures); excluded from analysis | [PDF](../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2013 | Booklets A Q.48, B Q.50, C Q.49, D Q.51 (same question) | MCQ | Minimum number of spills with only two registers when code motion is the only optimisation (NOTES §7) | Partly (compiler register allocation seen through the ISA's register count); **code segment missing from the mapping text** | [A](../../12-PYQ/2013/set-01/question-paper.pdf) · [B](../../12-PYQ/2013/set-02/question-paper.pdf) · [C](../../12-PYQ/2013/set-03/question-paper.pdf) · [D](../../12-PYQ/2013/set-04/question-paper.pdf) |
| 2013 | Booklets A Q.49, B Q.51, C Q.48, D Q.50 (same question) | MCQ | Minimum number of architectural registers so the code compiles with no spill, register allocation only (NOTES §7) | Partly; **code segment missing from the mapping text** | same four papers |

Years 2007–2012, 2014, 2017–2019, 2021–2023 have no entries in this topic's mapping (see "Mapping notes" for what that does and does not mean).

## Related questions filed under other leaves (found by searching the extracted paper text; **not counted above**)

These test skills from this folder but are mapped elsewhere. Concepts only; no answers.

| Year | Q# | Where it is mapped | Skill | Notes section |
|---|---|---|---|---|
| 2025 | Q.28 (CS-2) | cache-memory-mapping leaf | Which items belong to the ISA (cache size, clock, cache levels, register count) | §1 |
| 2024 | Q.57 (CS2) | addressing-modes leaf | Maximum opcodes per addressing mode, with a mode field, two register fields and a scalar field | §6.4.12 |
| 2024 | Q.56 (CS1) | pipeline-hazards leaf | Speedup of a perfect cache using CPI with memory stalls | §8.6 |
| 2018 | Q.51 | **floating-point leaf** (misfiled there) | Opcode counting with 16 integer and 64 floating-point registers (different field widths) in 2-byte instructions with four instruction categories | §6.4.11 |
| 2018 | Q.5 | hardwired-control leaf | Which of three listed features (register-to-register arithmetic, fixed-length format, hardwired control) are RISC design characteristics | §5.2 |
| 2014 | Q.55 (CS, set 1) | instruction-pipelining leaf | Relative time, CPI and clock frequency of two processors with the same ISA (ratio method) | §8.4 |

## What has been tested (concept list)
1. Instruction-field arithmetic in fixed-length encodings: opcode, register, immediate/offset widths (2016 ×2, 2024, 2025, 2020, 2026).
2. Variable-length / expanding opcodes: maximum number of opcodes left for a format (2020, 2026; related: 2018, 2024 CS-2 Q57).
3. Byte-aligned instruction storage and program size (2016).
4. Load–store architecture and operand-order convention (2026).
5. Address-field semantics of n-address instructions (2015).
6. Register allocation / spills as seen from the ISA register count (2013).

## Recurring patterns
- **Numerical (6 of 10 distinct questions):** field widths and opcode space. Every instance is solvable from ⌈log₂⌉, subtraction, and the opcode-space fraction rule.
  Mapped entries of this family appear in 2016, 2020, 2024, 2025 and 2026 (two in 2026 CS-sets and two in 2016), plus a related one filed under addressing modes (2024 CS-2 Q57) and one under floating point (2018).
- **Conceptual (4 of 10):** load–store sequence, address-field semantics, spill/register allocation (2 distinct 2013 questions).
- Question formats in the mapping: NAT (2016 ×2, 2020, 2024) and MCQ (2013, 2015, 2025, 2026 ×2).

## Important numerical patterns — solving recipes (no answers)

| Pattern | Recipe |
|---|---|
| Max immediate bits (2016 Q10, 2025 Q37) | opcode ⌈log₂ types⌉; each register field ⌈log₂ r⌉; count register fields from the instruction shape; subtract from L |
| Byte-aligned program size (2016 Q31) | b = Σ fields; bytes per instruction ⌈b/8⌉; multiply by program length |
| R/I format with format bit (2024 Q61) | per-type operations n/2 → ⌈log₂(n/2)⌉ + 1 = opcode bits; X, Z by subtraction; combine as the question asks |
| Max opcodes of a format (2020 Q44, 2026 Q44) | o_t = L − operand bits for each format; N = ⌊2^(o_T) − Σ n_i·2^(o_T − o_i)⌋; the shorter-opcode format creates fractions |
| Load–store sequence (2026 Q15) | four-question test: no memory operand in ALU instructions, sources loaded, result stored, operand order per convention |
| Address fields (2015 Q22) | decide for each operand style whether it is named by an address field or implied by the opcode |
| Spills (2013) | live ranges → peak pressure → interference graph → with code motion minimise peak; spill ≥ peak − k |

## Traps seen
- Treating the number of registers as bits; forgetting the ceiling when the count is not a power of two.
- Wrong number of register fields (the instruction shape is part of the question).
- Rounding program size once instead of per instruction.
- Using a flat opcode size when a format bit exists; subtracting opcode counts without scaling.
- Accepting a sequence with a memory operand inside an ALU instruction as load–store.
- Confusing an implied register with an address field.

## How the existing practice file complements the PYQs
The existing [`practice.md`](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/01-INSTRUCTION-SET/practice.md) covers field widths (Q4, Q9, Q10, Q16), one-level expanding opcodes (Q11, Q14), instruction-count machines (Q1, Q6, Q8, Q15) and the iron law (Q5, Q13, Q17) —
which matches the dominant PYQ families. It has no byte-aligned program-size, format-bit, three-format opcode-space or register-pressure question; [`PRACTICE.md`](PRACTICE.md) adds those (Q6, Q12–Q14, Q17, Q18, Q23–Q25).

## Mapping notes (data limitations)
- **Misfiled:** 2015 Q52 is a C stack-program question (programming/data structures) with OCR damage; excluded.
- **2013 entries:** four booklets × two questions = 8 entries; question numbers differ per booklet (Booklet C lists the two in swapped order). The mapping stores only the stems ("this code segment") and
  **omits the code segment**, so the mapping alone cannot solve them. Trailing text in several 2013 entries belongs to *other* questions (find-and-replace common data, a DBMS linked-answer statement).
  The code segment exists in the paper itself; no answer is asserted here.
- **2024 Q61** carries an unrelated regular-expression sentence appended to the stem (TOC question); the instruction-format part is complete.
- **2016 Q10** has a page-footer fragment ("Set B, 2/18") inside the stem; the data are complete.
- **2026 Q15** options are flattened onto single lines by the extraction; the four sequences are readable but check the PDF for line breaks.
- **Duplicates:** none within a single paper other than the booklet repeats of 2013.
- **Search limits:** I searched the extracted paper text (`/tmp/pyqtxt`, 2013–2026) for: opcode, address instruction, accumulator, RISC/CISC, instruction set/format, endian, byte-aligned, MIPS, stack machine, load–store, ISA, spill, CPI.
  Papers 2007–2012, 2019 and 2021 are mostly scanned and yielded almost no text, so the absence of entries for those years does **not** show that the topic was not examined; it only shows that this repository holds no mapped text for them. Booklet/set naming of 2014/2015 shifts follows the mapping.
- **Marks:** the mapping does not state marks; verify on the PDFs.

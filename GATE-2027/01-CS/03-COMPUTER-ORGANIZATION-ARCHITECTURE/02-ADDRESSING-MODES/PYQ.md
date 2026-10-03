# Addressing Modes — PYQ analysis

> **Answers:** the mapping lists **no verified answers** (every entry says "VERIFICATION REQUIRED"). None are given here. Solve each question with the
> method in [NOTES.md](NOTES.md) and check the official answer key yourself.

Mapping file (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/02-ADDRESSING-MODES/questions.md).
One additional on-topic entry (2008) is filed by the mapping under the ALU topic:
[ALU questions.md](../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/03-ARITHMETIC-AND-LOGIC-UNIT/questions.md). I have not modified either mapping file.

## 1. Question table (newest → oldest)

| Year | Q# (paper / set) | Type | Concept / skill tested (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.14 (CS-1, forenoon) | MCQ | Match four addressing modes (immediate, indirect, base with index, base with offset) to four data constructs (constant, pointer, array element, record field) | Yes | [2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2024 | Q.57 (CS2) | NAT | Instruction-field budget: fixed-length instruction with opcode, mode field (8 modes), two register fields (16 registers) and a 16-bit literal; find opcodes available per mode | Yes (encoding ↔ modes) | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2011 | Q.21 (CS, Booklet A) | MCQ | Name the addressing mode of a load whose EA is a constant plus a register's contents, from four named modes | Yes | [2011](../../12-PYQ/2011/question-paper.pdf) |
| 2008 | Q.33 (CS) — **mapped under ALU** | MCQ | Statement-style: which of three claims about auto-increment mode are true (relocation, extra ALU for EA, increment = operand size) | Yes (addressing mode, mis-filed under ALU) | [2008](../../12-PYQ/2008/question-paper.pdf) |

Entries in the ALU mapping file that are **not** addressing-mode questions (excluded from analysis): 2020 Q.4 (datapath micro-step ordering — control unit / datapath topic, partially related only through MAR/MDR sequencing) and 2016 Q.33 (carry-lookahead adder delay — ALU/adder topic).

Counts: 3 mapped entries in this topic's own file (2026, 2024, 2011) + 1 on-topic entry in the ALU file (2008) = **4 distinct on-topic questions**; no duplicates across booklets/sets in these four. Years with no mapped entries: all others from 2007–2025 (including 2013–2023).

## 2. What has been tested (from the 4 entries)

- Mapping of high-level data elements to modes: constant, pointer, array element, record field (2026).
- Counting bits in a fixed-length instruction to decide how many opcodes remain (2024).
- Recognising a displacement-style instruction and naming it among similar-sounding modes (2011).
- Properties of auto-increment mode (relocation, hardware needs, increment amount) (2008).

## 3. Recurring patterns

| Kind | Entries | Comment |
|---|---|---|
| Conceptual / naming | 2026, 2011, 2008 | No arithmetic; discriminate modes by their EA formula and properties |
| Numerical | 2024 | Bit-budget arithmetic that shares an instruction word between opcode, mode, register and literal fields |

## 4. Important numerical pattern and solving recipe

**Field budget (2024-style).** Recipe: (1) add up the bits of all fields except opcode: mode bits (given or ⌈log₂ #modes⌉ if the mode field is sized to fit the modes), register fields (count × ⌈log₂ #registers⌉), literal bits; (2) opcode bits = instruction length − that sum; (3) opcodes per mode = 2^(opcode bits) when the mode field is separate; total (opcode, mode) pairs multiply by the number of modes. Original practice in [PRACTICE.md](PRACTICE.md) Q12 and Q16. NOTES §9.1–9.2.

**Naming (2011-style).** Recipe: write the EA formula; count registers; look for a constant; look for a scale; check whether a memory pointer is read. Then pick the option whose structure matches; if two options seem to fit, the one with the *same number of registers* wins. NOTES §4.9; PRACTICE Q21.

**Matching (2026-style).** Recipe: pair certain items (constant ↔ immediate, pointer ↔ indirect), then separate array element (changing subscript ⇒ index) from record field (fixed offset ⇒ displacement). NOTES §5; PRACTICE Q5.

**Statement truth-test (2008-style).** Recipe: for each statement find the EA formula, the register side effect, whether the code holds absolute addresses, and what the stride is. NOTES §8. The auto-increment concepts are in §4.7.

## 5. Traps seen

- Confusing "indirect" (pointer in memory) with "register indirect" (pointer in register) when the list uses a short name (2026).
- Swapping the roles of "base with index" (array subscript) and "base with offset" (record field) (2026).
- Textbook name differences: "index", "base", "displacement" overlap; the options distinguish one-register + constant from two-register and scaled forms (2011).
- Forgetting a register field when computing opcode bits, or dividing opcode space by the number of modes though the mode field is separate (2024).
- Assuming auto-increment gives relocation or requires an EA adder, or stepping by one rather than the operand size (2008).

## 6. How the existing practice file complements the PYQs

The existing [practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/02-ADDRESSING-MODES/practice.md) is calculation-heavy (EA from snapshots, PC-relative targets, auto-inc/dec traces, access counts, chained modes). The PYQs are
mostly conceptual (matching, naming, statements) plus one encoding-budget item. The existing file has no field-budget question, no matching/naming question and no relocation question, so
this folder's NOTES §5, §9, §7.6 and PRACTICE Q5, Q12, Q16, Q21, Q24 cover those gaps.

## 7. Mapping notes

- **2008 Q.33 is filed under the ALU topic** though it is about an addressing mode; it is listed here because the instructions ask to cover its concepts. Not modified.
- **2020 Q.4 and 2016 Q.33** in the ALU file are not addressing-mode questions (see §1).
- **2011 Q.21 text:** the mapped text has dropped letters ("xecution", "ddress") from OCR; the meaning is intact. Options are complete in the mapping.
- **2024 Q.57:** the mapping prints no options (NAT) — correct for this question; the paper PDF is the source.
- **2026 Q.14:** the List I/List II table text is fully present in both the mapping and the extracted paper text.
- **Search limits:** keyword search over `/tmp/pyqtxt` (best-effort text of 2013–2026; 2007–2012, 2019–2021 mostly scanned) found no further addressing-mode questions, but scanned years give almost no text, so absence there is not proof.
- **Data sufficiency:** PYQ evidence for this topic is **THIN** (4 questions). Depth in NOTES is therefore driven also by the existing practice file's skills and by prerequisites for pipeline/control-unit questions.

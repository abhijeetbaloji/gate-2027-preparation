# Microprogrammed Control — PYQ analysis

**Answers:** the mapping lists no verified answers (every answer elsewhere in the mapping is marked "VERIFICATION REQUIRED"). No official answers are given in this file, and none are asserted anywhere in this folder.

**Mapping file:** [questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/questions.md)

## 1. Status: NONE mapped

The mapping file for this leaf contains **no entries** ("No GATE CS question from the local papers (2007–2026) was identified for this syllabus line"). This file therefore has an empty table and does not invent any question.

| Year | Q# (paper/set) | Type | Concept/skill tested | On-topic? | Paper link |
|---|---|---|---|---|---|
| 2026 → 2007 | — | — | **No mapped entry** | — | — |

Count of mapped entries for this topic: **0** (all years). Distinct on-topic questions: **0**.

## 2. What was searched, and the limits of the search

| Corpus | What was done | Result |
|---|---|---|
| Text extraction of the 2013–2026 papers (noisy, figures missing) | Case-insensitive search for: microprogram, microinstruction (and "micro-instruction"/"micro instruction"), control word, control store, control memory, nanoprogram, microcode, horizontal, vertical, hardwired / hard-wired, control unit, micro-operation | **No microprogram / microinstruction / control-word / control-store / control-memory / nanoprogram / microcode hit in any paper.** "Horizontal"/"vertical" hit once, in 2023, in a non-COA (geometry reflection) question: not related. "Hardwired control unit" hit once in 2018 (a RISC design-characteristics item, mapped to the [hardwired sibling](../01-HARDWIRED/)). "Micro-operations" hit in four 2013 booklets (same register-transfer-sequence question, mapped to the [interrupt topic](../../06-IO-INTERFACE/01-INTERRUPT/)). |
| Repository per-paper `.md` stubs in the PYQ archive | Same keyword search | Stubs are about 0.4–0.9 KB (no question text): no information. |

**Limits:**
- Papers for **2007–2012** and for **2019–2021** are scanned images; the text extraction gives almost nothing (a few hundred bytes), so those years **could not be searched at all**. A microprogramming question in those years would not have been detected by this method.
- Even for text years, **figures and tables are missing** in the extraction; a question presented with a figure (for example a control-word layout or a microprogram listing) may be hidden.
- Some years are only **partly extracted** (2015 sets, 2016 sets and 2017 set 2 are much shorter than the full-text papers), so text may be missing.
- The archive holds only set 2 for 2017; any other 2017 set is not covered at all.
- The search is keyword-based; a question using unusual wording ("ROM-based control", "control signals stored in memory") could slip through.

Therefore "no PYQ" means "none found by this search", not a proof that the topic has never been asked.

## 3. How depth was decided

Depth in [NOTES.md](NOTES.md) is **syllabus-driven, no mapped PYQ**:
- The official syllabus line names "Design of control unit – hardwired and microprogrammed".
- The existing 12-question practice file sets the skills: control memory, CAR width, horizontal vs vertical, encoded field with a "none" code, control-store size, absolute-address range, mapping ROM/sequencing, timing vs hardwired.
- No frequency or weight is claimed.

## 4. Adjacent real PYQs (in other folders; listed only so you know where the nearest contact is)

These are **not** mapped to this topic. They are listed for orientation and are not analysed or answered here.

| Year | Q# | Where mapped | What is tested (paraphrase) | Paper link |
|---|---|---|---|---|
| 2018 | Q.5 | [01-HARDWIRED](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/questions.md) | Which of three design characteristics (including the control-unit style) belong to RISC design: a conceptual comparison that also needs the micro-vs-hardwired tendencies in [NOTES 8.3](NOTES.md#83-microprogrammed-vs-hardwired). | [2018](../../../12-PYQ/2018/question-paper.pdf) |
| 2013 | Q.28 (set 1), Q.45 (set 2), Q.34 (set 3), Q.39 (set 4) | [06-IO-INTERFACE/01-INTERRUPT](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/01-INTERRUPT/questions.md) | Identify what a short register-transfer ("micro-operation") list accomplishes; same question appears in all four 2013 booklets (the mapping labels the first as Booklet A). The skill is reading a micro-operation list: [NOTES 4.3](NOTES.md#43-reading-a-micro-operation-sequence-skill). | [set 1](../../../12-PYQ/2013/set-01/question-paper.pdf), [set 2](../../../12-PYQ/2013/set-02/question-paper.pdf), [set 3](../../../12-PYQ/2013/set-03/question-paper.pdf), [set 4](../../../12-PYQ/2013/set-04/question-paper.pdf) |

For their answers, verify against the official key; this folder does not give them.

## 5. What has been tested / recurring patterns / numerical patterns / traps seen

- **What has been tested (this leaf):** nothing found.
- **Recurring patterns:** none can be reported without evidence.
- **Important numerical patterns:** none from PYQs. The syllabus-derived numerical shapes (width, control-store size, nano pointer, timing) are in [NOTES Section 10](NOTES.md#10-question-patterns-for-this-topic-syllabus-derived-no-pyq-evidence); treat them as practice shapes, not as exam statistics.
- **Traps seen:** none from PYQs. Likely traps are in [MISTAKES.md](MISTAKES.md).

## 6. How the existing practice file complements the (absent) PYQs

The repository's separate practice file (12 questions) is the only concrete skill list for this leaf: concept MCQs, width arithmetic, control-store size, mapping/sequencing statements and one timing comparison. [PRACTICE.md](PRACTICE.md) here adds 22 new original questions that also exercise the topics the 12 do not stress: bus-legality of a listing, group-conflict encoding, nanoprogramming, subroutines, variable format, overlapped timing and a looping microroutine.

## 7. Mapping notes

- The mapping for this leaf is intentionally empty; the empty state is consistent with the keyword search above.
- The 2018 RISC-characteristics item sits in the hardwired mapping and the 2013 micro-operation item in the interrupt mapping; neither is a microprogramming-format question.
- A data limitation: scanned years (2007–2012, 2019–2021) could not be checked, and figures are absent in the text extraction.

# Theory of Computation — Topic Priority

Priority here is based on stems in `../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/` whose question text is actually about that syllabus fragment. It is not a prediction about GATE 2027, and it is not a percentage of any paper.

## Counting rule

- A row counts when the stored question text is about the topic.
- Rows about compilers, caches, pipelines, probability, NP-completeness, or similar are mapping noise. They are excluded. Each topic `PYQ.md` lists them.
- The four 2013 booklets repeat the same questions. The table below gives **rows** and **distinct questions**.
- The `Paper` line is used for the year.
- Stored answers are `VERIFICATION REQUIRED`. Priority is about what was asked, not about a verified key.
- “Latest paper” means the newest paper among the counted stems.
- Several extracts are OCR-damaged. A damaged but still recognizable TOC stem is counted; a destroyed stem is not treated as extra evidence.

| Topic | Recognizable rows | Distinct questions | Latest paper | Priority |
|-------|------------------:|-------------------:|--------------|----------|
| Finite automata | 34 | 31 | 2026 | High |
| Undecidability | 21 | 15 | 2026 | High |
| Regular languages | 10 | 10 | 2026 | High |
| Regular expressions | 8 | 8 | 2024 | High |
| Context-free grammars | 7 | 7 | 2026 | High |
| Context-free languages | 4 | 4 | 2025 | Medium |
| Turing machines | 3 | 3 | 2026 | Medium |
| Push-down automata | 0 | 0 | — | Lower |
| Pumping lemma | 1 | 1 | 2019 | Lower |

**Finite automata.** Counted rows are the DFA/NFA/ε-NFA constructions, min-state NATs, subset-construction bounds, distinguishability, and DFA→RE matches in that mapping file. Excluded: 2015 CS Shift-2 Q.27 (compiler matching). The 2013 DFA-property question is one question printed in four booklets (4 rows, 1 distinct). The 34 = 31 distinct + 3 extra 2013 reprints.

**Undecidability.** Counted rows are decidability / Rice / reduction stems, plus the 2026 grammar question whose last option is a decidability claim, and the 2025 “accepted by a DPDA” classification. Excluded: 2025 CS1 Q.13 (liveness), 2014 Q.38 (2SAT), 2009 Q.14 (NP), 2008 Q.11 (LR handle), 2008 Q.37 (register windows). The 2013 pair (RE-closure statements; CFG/TM decidability) is two questions printed in four booklets (8 rows, 2 distinct). 21 rows = 15 distinct + 6 extra reprints.

**Regular languages.** All ten stored stems are about regularity or closure. 2007 Q.53 (regular grammar vs LL(1)/LR(1)) is counted because it is a fact about regular sets.

**Regular expressions.** All eight stored stems are RE reading, RE counting, or RE↔automaton matching.

**Context-free grammars.** Counted: 2026 Q.52, 2025 Q.19, 2024 Q.59, 2024 Q.52, 2023 Q.39, 2016 CS-1 Q.42, 2007 Q.77 (linked CFG; extract damaged, PDF required). Excluded: LALR/SLR, LL(1) tables, IR/AST/compiler matching.

**Context-free languages.** Counted: 2025 Q.45, 2021 Set-1 Q.1, 2017 Session-2 Q.4, 2011 Q.24. 2021 Set-2 Q.12 is stored but the extract is unreadable; it is not in the 4. If the PDF is a CFL-closure question, the distinct count becomes 5 and the band stays Medium.

**Turing machines.** Counted: 2026 CS-2 Q.13 (decides), 2011 Q.26 (which machine recognizes which language), 2008 Q.9 (`{a^p | p prime}`). Excluded: 2011 Q.18 (a probability stem with leftover machine options).

**Push-down automata.** The only two stored blocks are 2009 Q.17 (compiler matching) and 2008 Q.30 (first-order logic). Neither is a PDA construction. Counted recognizable PDA rows: 0. A 2025 DPDA classification is filed under undecidability and is counted there.

**Pumping lemma.** One stored stem: 2019 Q.15 (which integer can be a pumping length of a given regular language). The extract is OCR-damaged; the PDF is required.

## Why these bands

**High.** A repeated modern pattern, or a whole syllabus machine/family with a double-digit (or high single-digit, still current) recognizable set.

- Finite automata is the thick file: min-state NATs, NFA-to-DFA bounds, and “what does this DFA accept?” appear from 2007 through 2026.
- Undecidability is the other thick file: a decidability table by model is asked in some form in most recent years.
- Regular languages: closure and “which of these is regular?” is a current MSQ/MCQ pattern (2024–2026).
- Regular expressions: fewer rows than automata, but the same skill (read the language exactly) is also how many automata questions are solved. 2024 is a counting NAT.
- Context-free grammars: language-of-`G` and letter-count invariants are the 2023–2026 pattern; CNF step-count is 2024.

**Medium.** A real syllabus line with a short but nonempty mapped set, still needed to solve High-band questions.

- Context-free languages: five recognizable closure/classification stems. The *skill* (one stack vs two agreements) is also how 2025 Q.45 and several undecidability options are solved.
- Turing machines: only three clean mapped stems, but 2026 asks the definition of “decides”, and the RE-vs-decidable distinction is the prerequisite for the undecidability table.

**Lower.** The mapping file for that folder is almost empty. The *idea* is not optional.

- Pumping lemma: one 2019 stem. Non-regularity and non-CFL arguments in the other folders use it. Study it from `07-PUMPING-LEMMA/NOTES.md` and from the regular/CFL practice files.
- Push-down automata: no construction stem is stored in that mapping file. CFG↔PDA and DPDA vs NPDA still appear (2025 DPDA question; CFL proofs). Study the machine from the notes and from `14-PRACTICE-QUESTIONS`.

## What this file does not say

- It does not say a Lower topic will be absent in 2027.
- It does not convert these rows into marks. The extracts do not consistently record marks.
- It does not treat mapping noise as TOC frequency.
- It does not invent a percentage of the paper.
- A DFA→RE question is counted under finite automata, not again under regular expressions. A “is this regular?” question is counted under regular languages, not again under automata.

# Theory of Computation — PYQ Coverage (2007–2026)

Counts come from the question text in `../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/`. Papers are in `../12-PYQ/`. A row is “recognizable” when the stem is about that TOC syllabus fragment. Mapping noise is counted separately and is not a TOC question.

The year headings inside several `questions.md` files may not match the `Paper` line. Coverage below follows `Paper`. Stored answers are `VERIFICATION REQUIRED`.

This file does **not** duplicate the questions. Each topic `PYQ.md` points at the mapping file and names the PDF.

## Totals

| Metric | Value |
|--------|------:|
| Topic files with a `questions.md` | 9 of 9 |
| Recognizable rows counted in `TOPIC-PRIORITY.md` | 88 |
| Distinct questions among those 88 | 79 |
| Other stored blocks (noise, unreadable, or off-folder) | see below |

The 88 is \(34+21+10+8+7+4+3+0+1\). The distinct count is 79 because the four 2013 booklets reprint one finite-automata question (3 extra rows) and two undecidability questions (6 extra rows).

These are counts of **mapped extracts**, not a claim that every TOC question from 2007–2026 was filed. Absence from a mapping file is not a claim that the paper had no such question.

## Which syllabus topics have PYQs

| Official fragment | Folder | Mapped PYQs? | What the recognizable stems actually ask |
|-------------------|--------|--------------|------------------------------------------|
| Regular expressions | `01-REGULAR-EXPRESSIONS` | Yes | Read an RE; count strings outside a union of REs; match an RE to an ε-NFA or NFA |
| Finite automata | `02-FINITE-AUTOMATA` | Yes, thick | Min DFA size; NFA→DFA state bounds; language of a drawn DFA; DFA→RE; ε-closure / subset; distinguishability |
| Context-free grammars | `03-CONTEXT-FREE-GRAMMARS` | Yes | Language of `G`; letter-count invariants; CNF derivation length `2n−1` |
| Push-down automata | `04-PUSH-DOWN-AUTOMATA` | No clean construction stem | The two stored blocks are compiler matching and first-order logic |
| Regular languages | `05-REGULAR-LANGUAGES` | Yes | Which languages are regular; closure / non-closure; prefix, suffix, `ww^R` |
| Context-free languages | `06-CONTEXT-FREE-LANGUAGES` | Yes, thinner | Which of two counting languages is CFL; CFL vs regular closures |
| Pumping lemma | `07-PUMPING-LEMMA` | One stem (2019) | Which integer can be a pumping length of a given regular language |
| Turing machines | `08-TURING-MACHINES` | Yes, thin | What “decides” means; which machine class accepts which language; `{a^p \| p prime}` |
| Undecidability | `09-UNDECIDABILITY` | Yes, thick | Decidability table by model; Rice; bounded-step TM properties; CFG emptiness vs universality |

A 2025 “accepted by a DPDA” stem is stored under undecidability, not under PDA.

## Recurring concepts

These are the jobs the recognizable stems actually set.

**Regular expressions and finite automata**

- Min-state DFA for a modular count, a forbidden run, a required suffix/substring, or a product of two independent conditions.
- Upper bound `2^n` after subset construction; a 1-state DFA is possible; an equivalent DFA need not have at least `n` states.
- Trace a DFA / NFA on short strings and name the language, or pick the matching RE.
- Distinguishability of states (Myhill–Nerode in all but name).
- Read an RE exactly: odd number of `1`s, at least two `0`s, both `00` and `11`, multiples of 3.

**Grammars, PDAs, CFLs**

- What a grammar generates, by tracking what each production adds.
- CNF: a string of length `n ≥ 1` needs `2n−1` steps.
- One unbounded agreement (or two *nested* agreements) is CFL; three equal counts, or two *crossed* agreements, is not.
- CFL closed under union and under intersection with regular; not closed under intersection or complement.

**Turing machines and undecidability**

- Decides = accept every yes-instance **and** reject every no-instance.
- Regular / DFA problems (membership, emptiness, finiteness, equivalence, universality) are decidable.
- CFG membership, emptiness, finiteness are decidable; CFG equivalence, universality, ambiguity are not.
- TM language properties (empty, regular, `Σ*`, equivalent to another TM) are undecidable.
- “Runs more than `k` steps on every / some input”, for a fixed `k`, is decidable.
- Rice applies to nontrivial properties of `L(M)`, not to “`M` has five states”.

## Topics with sparse or no confidently mapped PYQs

| Folder | Gap |
|--------|-----|
| Push-down automata | No construction, acceptance-mode, or DPDA-vs-NPDA stem is stored *in this folder*. Study PDA from the notes, from CFL proofs, and from the 2025 DPDA question filed under undecidability. |
| Pumping lemma | One 2019 stem, OCR-damaged. The lemma is still the written argument for “not regular / not CFL” in other folders. |
| Turing machines | Three recognizable stems. The definition of “decides” (2026) and the RE-vs-decidable distinction are the load-bearing parts. |
| Context-free languages | Four readable stems. 2021 Set-2 Q.12 is stored and unreadable. |
| Context-free grammars | Language-of-`G` is well covered. The mapping also contains several parser-table stems that belong to Compiler Design. |
| Regular expressions | No mapped row for 2025–2026 in this folder. DFA→RE questions from those years sit under finite automata. |

## Mapping noise (not TOC frequency)

| Kind | Where it is stored |
|------|--------------------|
| Compiler matching, LL(1)/LALR tables, AST vs CFG, live-variable analysis, LR handle | CFG mapping; undecidability mapping; one FA matching row (2015) |
| First-order logic “every FSA has an equivalent PDA” | PDA mapping (2008 Q.30) |
| Probability / variance stem with leftover machine options | TM mapping (2011 Q.18) |
| NP / 2SAT / “πA is in NP” | Undecidability mapping (2015 Q.20 is partly TOC — NP ⊆ decidable — and is counted; 2014 Q.38 and 2009 Q.14 are excluded) |
| Register windows | Undecidability mapping (2008 Q.37) |
| 2013 booklet reprints | FA mapping (one question × 4); undecidability mapping (two questions × 4) |

## How to use a row

Open the PDF named in the source line of the mapping file. The extract is enough to see the pattern and not always enough to solve: figures are flattened, and several option lists are visually corrupted. Do not grade yourself from a reconstructed figure. Do not use a stored `VERIFICATION REQUIRED` field as a key.

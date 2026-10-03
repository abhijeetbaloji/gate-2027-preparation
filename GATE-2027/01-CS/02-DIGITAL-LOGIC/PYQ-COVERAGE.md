# Digital Logic — PYQ Coverage (2007–2026)

Counts come from the question text in `../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/`. Papers are in `../12-PYQ/`. A row is “recognizable” when the stem is about that Digital Logic syllabus line. Mapping noise is counted separately and is not a Digital Logic question.

The year headings inside several `questions.md` files do not match the `Paper` line. Coverage below follows `Paper`. Stored answers are `VERIFICATION REQUIRED`.

## Totals

| Metric | Value |
|--------|------:|
| Topic files with a `questions.md` | 7 of 7 |
| Stored blocks, all files | 123 |
| Recognizable rows counted in `TOPIC-PRIORITY.md` | 88 |
| Distinct questions among those 88 | 82 |
| Other stored blocks | 35 |

The 88 is \(27+18+13+14+11+4+1\). The distinct count is 82 because the four 2013 booklets repeat one fixed-point question and one combinational encoder question (each set of four rows contributes one question, so six extra rows are not extra questions).

The other 35 blocks are:

| Kind | Blocks |
|------|-------:|
| Unrelated subjects (parsers, caches, pipelines, OS, databases, and similar) | 25 |
| Memory diagrams that use a decoder or a mux | 8 |
| Combinational questions filed under sequential circuits | 2 |

Unrelated-subject blocks are not Digital Logic frequency. The eight memory diagrams are listed in the combinational `PYQ.md`. The two misfiled combinational questions are GATE 2014 CS SET-3 Q.8 (a 2-to-1 mux) and GATE 2007 CS Q.34 (mux size), both stored in the sequential file.

2017 Session 1 is the archive gap already recorded for other subjects: where a paper is missing from `12-PYQ`, it is also missing here.

## Recurring patterns

These are the jobs the recognizable stems actually set.

**Boolean algebra and minimization**

- Equivalent expressions, including XOR with a product or a constant.
- Minimal sum of products of a minterm list. Sometimes more than one minimal form (MSQ). Sometimes don’t-cares.
- Minimum product of sums, which is the map of the 0s, not the SOP with bars copied on.
- Number of essential prime implicants, and (2015) the number of prime implicants.
- How many Boolean functions, and how many self-dual functions.
- A small gate circuit, or an AND/XOR of known minterm lists, written back as a minterm list.
- NOR-only gate counts, with or without complements supplied.

**Combinational**

- Mux trees and the SOP of a small mux.
- How many small decoders build a wide decoder.
- Carry delay through a half-adder/full-adder chain.
- An encoder truth table with a valid bit.

**Sequential**

- Next state of a D, T, or JK circuit from a given start.
- Minimum flip-flops for a sequence that repeats outputs. The count is states, not distinct integers.
- Johnson sequence from a stated initial value.
- Saturating counter excitation.
- Ripple-counter waveform period versus clock frequency. The two differ by \(2^n\) on a binary counter.
- How many distinct states a clocked circuit actually reaches.

**Fixed point**

- Two’s-complement range, especially the most negative value.
- Which patterns represent a given negative integer.
- Signed overflow, as distinct from carry-out.
- Decimal value of a long two’s-complement bit string.
- Booth: number of additions and subtractions on a given multiplier.
- One unsigned fixed-point format with the binary point not at the LSB.
- A left shift that multiplies a two’s-complement hex value by 8.

**Floating point**

- IEEE-754 single precision only, in the stored stems.
- Decode a hex word, or compare several words.
- Add or multiply two hex values.
- Largest encoding, which requires infinity and NaN to be recognised before any magnitude comparison.
- Smallest positive normalised value.

## Where the mapping is thin or noisy

| Topic | Gap |
|-------|-----|
| Tabular method | One stem, 2015. No other year is stored. Prime counts that do exist are often filed under algebraic technique. |
| Karnaugh map | Four stems (2025, 2017, 2012, 2008). Drawn maps in the extract are incomplete; use the PDF. Many grouping questions sit in the algebraic file. |
| Combinational | No recognizable adder/mux/decoder stem stored for 2025, 2021, 2019, 2018, 2017, 2012, 2010, 2009, 2008. A 2007 mux-size question is filed under sequential circuits. |
| Sequential | No recognizable flip-flop stem stored for 2024, 2022, 2020, 2019, 2013, 2012, 2010, 2008. The file contains a large amount of pipeline, cache, and OS text. |
| Fixed point | No row for 2026, 2023, 2021, 2020, 2017, 2015, 2014, 2012, 2011, 2009, 2008, 2007. Ones’-complement addition is not its own stored stem. |
| Floating point | No row for 2019, 2016, 2015, 2013, 2011, 2010, 2009, 2007. Double precision is not stored. One 2018 row is an instruction format. |

Absence from a mapping file is not a claim that the paper had no such question. It is a claim about this repository’s extract.

## How to use a row

Open the PDF named in the source line. The extract is enough to see the pattern and not always enough to solve: figures are flattened, and a few option lists are visually corrupted. Do not grade yourself from a reconstructed figure.

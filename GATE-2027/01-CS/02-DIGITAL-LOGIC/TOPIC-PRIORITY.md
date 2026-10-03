# Digital Logic — Topic Priority

Priority here is based on stems in `../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/` whose question text is actually about that syllabus line. It is not a prediction about GATE 2027, and it is not a percentage of any paper.

## Counting rule

- A row counts when the stored question text is about the topic.
- Rows about parsers, caches, pipelines, databases, operating systems, or similar are mapping noise. They are excluded. Each topic `PYQ.md` lists them.
- The four 2013 booklets repeat the same questions. The table below gives **rows** and **distinct questions**.
- The `Paper` line is used for the year. Several year headings inside `questions.md` disagree with that line.
- Stored answers are `VERIFICATION REQUIRED`. Priority is about what was asked, not about a verified key.
- “Latest paper” means the newest paper among the counted stems.

| Topic | Recognizable rows | Distinct questions | Latest paper | Priority |
|-------|------------------:|-------------------:|--------------|----------|
| Algebraic technique | 27 | 27 | 2026 | High |
| Sequential circuits | 18 | 18 | 2026 | High |
| Floating point | 13 | 13 | 2026 | High |
| Fixed point | 14 | 11 | 2025 | High |
| Combinational circuits | 11 | 8 | 2026 | High |
| Karnaugh map | 4 | 4 | 2025 | Medium |
| Tabular method | 1 | 1 | 2015 | Lower |

The algebraic count includes GATE 2014 CS SET-2 Q.53, a propositional tautology question that uses Boolean connectives and is not a minimization. Without it, the recognizable algebra count is 26. Either figure is well above the other topics.

The combinational count is the mux, adder-delay, encoder, and decoder-construction stems only. Further rows in that file use a decoder or a mux inside a memory diagram (chip select, RAM built from smaller chips). Those are recorded in that topic’s `PYQ.md` and are not in the 11.

## Why these bands

**High.** A double-digit recognizable set, or a smaller set that still appears in 2024–2026 and is a whole syllabus line with its own numerical technique. Algebra, sequential circuits, and floating point are the thick files. Fixed point is slightly thinner only because 2013 is one question printed four times; 2024 and 2025 both have stems (overflow, Booth, representations of a negative integer). Combinational circuits have fewer distinct questions than algebra, but 2024 and 2026 both ask mux circuits, and decoder construction is a repeated older pattern.

**Medium.** Karnaugh map has four recognizable stems, one of them in 2025 (an MSQ: which expressions match a drawn map). The file is thin because many minimal-SOP and don’t-care questions were stored under algebraic technique. The map is how those questions are solved. The priority of the *file* is medium; the priority of the *skill* is the same as algebraic minimization.

**Lower.** The tabular-method file has a single stem: GATE 2015 CS, 8 February Shift 1, Q.62, a prime-implicant count. No later paper is stored there. Prime and essential-prime counts also appear under algebraic technique (GATE 2018 CS Q.49). The method is part of the syllabus and is the reliable way to answer a prime count. It is not, on this mapping, a high-frequency folder of its own.

## What this file does not say

- It does not say a Lower topic will be absent in 2027.
- It does not convert these rows into marks. The extracts do not consistently record marks.
- It does not treat mapping noise as Digital Logic frequency.
- The 100-day plan’s days 22–27 are a calendar. They are not this ranking.

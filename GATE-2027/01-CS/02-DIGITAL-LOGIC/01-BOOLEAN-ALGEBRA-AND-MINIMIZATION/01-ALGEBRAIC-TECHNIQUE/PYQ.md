# Boolean Algebra (Algebraic Technique) — Previous Year Questions

The question text stays in the mapped file. Do not treat the year headings inside that file as authoritative: several of them disagree with the `Paper` line. This page uses the `Paper` line. Every stored answer is marked `VERIFICATION REQUIRED`, so no official key is copied here.

Mapping file: `../../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/01-ALGEBRAIC-TECHNIQUE/questions.md`

Papers: `../../../12-PYQ/`.

## What the recognizable stems test

About 26 of the 35 stored blocks have a Boolean-algebra stem. They recur as:

- Equivalent form of an expression, including XOR with a product (2026 CS-1).
- Minimal sum of products of a minterm list, sometimes with more than one minimal form in an MSQ (2026, 2025, 2024, 2014).
- Which equation is or is not a Boolean identity (2026 CS-2, 2025 CS-2).
- Majority (“at least two inputs are 1”) versus other three-variable functions (2025 CS-1).
- A small gate circuit whose output must be written as a minterm list (2020, 2019, 2008).
- Minimum 2-input NOR count, with complements available in the 2019 stem.
- Number of essential prime implicants, with don’t-cares (2018).
- Number of minterms of a complemented expression (2015, 7 February Shift 2).
- Absorption on \(PQ + PQR + PQRS\) (2014 SET-1).
- Count of self-dual functions (2014 SET-2).
- Minimal SOP with don’t-cares (2014 SET-3).
- XOR simplification on two variables (2014 SET-3).
- Truth table to expression (2012), SOP simplification (2011), minterm expansion (2010).
- NOR realization of \(AB+C\) (2009).
- Number of Boolean functions of \(n\) variables (2007).
- A structural property of a listed 4-variable function (2007): independent of a variable, or self-dual, or linear. The stem in the mapping is truncated after “The function is”, so the property names are in the paper, not in the extract.

K-map grouping is the practical tool for the minterm-list items. They are filed here because the stem asks for an algebraic form rather than for a picture of the map. The Karnaugh-map folder holds the stems that show a map.

## Rows whose text is not this topic

These blocks are in the mapping file. Their stems are parsers, grammars, or relational algebra. They are not counted above.

| Paper | Question | Why it is not this topic |
|-------|----------|--------------------------|
| GATE 2026 CS-2 | Q.41 | Canonical LR(0) items |
| GATE 2025 CS-2 | Q.21 | Backpatching in a compiler |
| GATE 2021 CS Set-1 | Q.26 | Syntax-directed translation |
| GATE 2021 CS Set-2 | Q.51 | LR closure and GOTO |
| GATE 2017 CS Session 2 | Q.6 | Power of SLR, LALR, canonical LR |
| GATE 2015 CS, 8 February Shift 1 | Q.15 | SLR versus canonical LR versus LALR |
| GATE 2014 CS SET-1 | Q.34 | Canonical set of LR items |
| GATE 2014 CS SET-3 | Q.21 | Relational-algebra optimization |

GATE 2014 CS SET-2 Q.53 asks which Boolean expression is not a tautology. That is propositional logic. It uses the same connectives, and the mapping placed it here. A tautology checker is the one-row counterexample method in `NOTES.md`. It is not a minimization question.

## Recognizable rows, newest paper first

| Paper | Question | Type | Pattern |
|-------|----------|------|---------|
| GATE 2026 CS-1 | Q.21 | MCQ | XOR of a sum and a product; equivalent expressions |
| GATE 2026 CS-1 | Q.48 | MCQ | Minimal SOP of a 4-variable minterm list |
| GATE 2026 CS-2 | Q.16 | MCQ | Which statement is not a Boolean-algebra property |
| GATE 2026 CS-2 | Q.40 | MCQ | Minimal SOP of \(\sum m(0..3, 8..11)\) |
| GATE 2025 CS-1 | Q.24 | MCQ | Function that is 1 when at least two inputs are 1 |
| GATE 2025 CS-1 | Q.42 | MCQ | 4-variable SOP and a numeric reading of the inputs |
| GATE 2025 CS-2 | Q.50 | MCQ | Which Boolean equations hold |
| GATE 2024 CS1 | Q.47 | MCQ | Statements about \(\sum(3,5,6,7)\) |
| GATE 2024 CS2 | Q.50 | MCQ | Four minterm-list functions in one circuit |
| GATE 2021 CS Set-1 | Q.42 | MCQ | Equivalent forms of a product of sums, including the complement |
| GATE 2020 CS | Q.28 | MCQ | Minterm list of a drawn circuit |
| GATE 2019 CS | Q.30 | MCQ | AND and XOR of three minterm-list functions |
| GATE 2019 CS | Q.50 | NAT | Minimum 2-input NOR gates; complements available |
| GATE 2018 CS | Q.49 | NAT | Number of essential prime implicants, with don’t-cares |
| GATE 2015 CS, 7 February Shift 2 | Q.55 | NAT | Minterm count of a complemented expression |
| GATE 2014 CS SET-1 | Q.7 | MCQ | Minimal SOP by absorption |
| GATE 2014 CS SET-2 | Q.6 | MCQ | Number of self-dual functions |
| GATE 2014 CS SET-2 | Q.53 | MCQ | Boolean expression that is not a tautology |
| GATE 2014 CS SET-3 | Q.7 | MCQ | Minimal SOP with don’t-cares |
| GATE 2014 CS SET-3 | Q.55 | MCQ | Two-variable XOR nest |
| GATE 2012 CS | Q.6 | MCQ | Expression for a given truth table |
| GATE 2011 CS | Q.14 | MCQ | Simplified SOP of a product of sums |
| GATE 2010 CS | Q.6 | MCQ | Minterm expansion of \(PQ+QR+PR\) |
| GATE 2009 CS | Q.6 | MCQ | Minimum 2-input NOR gates for \(AB+C\) |
| GATE 2008 CS | Q.8 | MCQ | Recover one function from a gate and two minterm lists |
| GATE 2007 CS | Q.3 | MCQ | Number of Boolean functions of \(n\) variables |
| GATE 2007 CS | Q.9 | MCQ | Property of \(\sum(1,3,4,6,9,11,12,14)\) |

2013 has no row in this file. 2016 and 2022 have no recognizable Boolean-algebra stem here. That is a statement about this mapping file, not a statement that those papers contain no such question.

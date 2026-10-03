# Regular Expressions — PYQ analysis

> **Answers:** every stored answer in the mapping is `VERIFICATION REQUIRED`. None are given here. Solve from the paper PDF named in the source line.

Mapping (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/01-REGULAR-EXPRESSIONS/questions.md).
Papers: [12-PYQ](../../12-PYQ/).

## 1. Question table (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2024 | Q.61 (CS1) | NAT | Count binary strings of length ≤ 5 in neither `0* + 1*` nor `01* + 10*` | Yes | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2023 | Q.19 (CS) | MCQ | Which ε-NFA accepts the token `letter (letter \| digit)*` | Yes (RE → ε-NFA) | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2021 | Q.47 (CS Set-2) | MCQ | Which REs denote binary numbers divisible by 3 (`ε` counted as divisible) | Yes | [2021 set-02](../../12-PYQ/2021/set-02/question-paper.pdf) |
| 2020 | Q.7 (CS) | MCQ | Which RE denotes binary strings with an odd number of `1`s | Yes | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2016 | Q.18 (CS-1) | MCQ | Which RE denotes strings that contain both `00` and `11` | Yes | [2016 set-01](../../12-PYQ/2016/set-01/question-paper.pdf) |
| 2009 | Q.15 (CS) | MCQ | Language of `(0+1)*0(0+1)*0(0+1)*` | Yes | [2009](../../12-PYQ/2009/question-paper.pdf) |
| 2008 | Q.52 (CS) | MCQ | Match four NFAs to four REs | Yes (NFA ↔ RE) | [2008](../../12-PYQ/2008/question-paper.pdf) |
| 2007 | Q.74 (CS) | MCQ | Language of a drawn automaton as an RE | Yes (FA → RE) | [2007](../../12-PYQ/2007/question-paper.pdf) |

The 2021 extract is OCR-corrupted: option (C) is garbled and a page-table question is concatenated after option (D). Use the PDF. The 2008 and 2007 extracts drop the figures; the PDF is required.

Years with no row in this mapping file: 2026, 2025, 2022, 2019, 2018, 2017, 2015, 2014, 2013, 2012, 2011, 2010. Absence from the extract is not a claim that those papers had no RE question. Some RE-looking stems sit in the finite-automata mapping (DFA → RE options).

## 2. What has been tested

- Read an RE and name its language in English (2009).
- Pick the unique correct RE among near-miss options (odd number of `1`s; both `00` and `11`; multiples of 3).
- Count strings of bounded length outside a union of simple REs (2024).
- Match an ε-NFA to a token RE (2023).
- Match a drawn NFA/DFA to an RE (2008, 2007).

## 3. Recurring patterns

| Pattern | Entries |
|---|---|
| English description ↔ RE | 2021, 2020, 2016, 2009 |
| Automaton / token ↔ RE or ε-NFA | 2023, 2008, 2007 |
| Counting strings of length ≤ n | 2024 |

The common job is **reading** an RE exactly: what it includes, what it misses, and whether `ε` is a member.

## 4. Constructions and theorem applications

- Kleene equivalence is used implicitly: an RE option is checked by tracing a DFA, or an ε-NFA is checked against a token RE.
- The 2021 “divisible by 3” family is the state-elimination RE of the mod-3 remainder DFA, including `ε`.
- 2024 is inclusion–exclusion per length, after identifying `L(r)` and `L(s)` and their overlap.

## 5. Traps seen in the stems

- “Contains `00` and `11`” is not “contains `0011` or `1100`”. Adjacent-block options miss `001011`.
- “At least two `0`s” is not “contains `00`”: `010` is a member of `(0+1)*0(0+1)*0(0+1)*`.
- Odd number of `1`s: options that cannot produce `10`, or that include `ε` / `11`.
- Token ε-NFA: a machine that accepts a lone digit, or that cannot accept a single letter, is wrong.
- Counting: `ε` belongs to both `0*` and `1*`; do not omit length 0.

## 6. How the existing practice file complements the PYQs

[14-PRACTICE practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/01-REGULAR-EXPRESSIONS/practice.md) drills precedence, even/odd `1`s, no-`00`, Arden orientation, and unambiguous-star counting. This folder’s [PRACTICE.md](PRACTICE.md) adds `∅`/`ε` algebra, inclusion–exclusion of the 2024 shape, mod-3 remainder REs, and powers `L^k`.

## 7. Mapping notes

- Stored answers are all `VERIFICATION REQUIRED`.
- Figures are missing from the 2008 and 2007 extracts.
- 2021 Q.47 options are damaged in the extract; the PDF is the source.
- DFA-to-RE questions from 2024 CS2, 2023, 2022 and 2014 live in the finite-automata mapping, not here.

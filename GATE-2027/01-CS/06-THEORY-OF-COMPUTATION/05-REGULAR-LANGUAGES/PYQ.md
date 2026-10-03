# Regular Languages — PYQ analysis

> **Answers:** every stored answer in the mapping is `VERIFICATION REQUIRED`. None are given here. Solve from the paper PDF named in the source line.

Mapping (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/05-REGULAR-LANGUAGES/questions.md).
Papers: [12-PYQ](../../12-PYQ/).

## 1. Question table (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.51 (CS-1) | MCQ | `L1 ∩ L2` and `L2` regular: which of regularity / CFL-ness of `L1`, of `L1 ∪ L2`, of `L2` is always true | Yes | [2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2025 | Q.44 (CS-1) | MCQ | `αβα` with `α ∈ {a, b}+` versus `α ∈ {a}+` | Yes | [2025 set-01](../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.52 (CS-2) | MSQ | Which of `a^m b^n`, a no-`c` slice of `a^m b^n c^{m−n}`, modular counts, modular-and-equal counts are regular | Yes | [2025 set-02](../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.23 (CS1) | MCQ | Regular `L1, L2`, non-regular `L3`: equality vs `L1 ∩ L̄2 = ∅`; union with `L3`; complement of `L3`; `L̄1 ∪ L̄2` | Yes | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2020 | Q.8 (CS) | MCQ | Union regular ⇒ both regular? Closed under infinite union? | Yes | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2019 | Q.7 (CS) | MCQ | `L` regular: which of `L · L^R`, `{ww^R \| w ∈ L}`, Prefix(`L`), Suffix(`L`) is not necessarily regular | Yes | [2019](../../12-PYQ/2019/question-paper.pdf) |
| 2014 | Q.15 (CS SET-2) | MCQ | `{a^n} · {b^n}` regular? Equal to `{a^n b^n}`? | Yes | [2014 set-02](../../12-PYQ/2014/set-02/question-paper.pdf) |
| 2008 | Q.53 (CS) | MCQ | Which of `a^n b^m`, `n = 2m`, `n ≠ m`, `{xcy}` are regular | Yes | [2008](../../12-PYQ/2008/question-paper.pdf) |
| 2007 | Q.7 (CS) | MCQ | Subsets of regular; finite subsets of non-regular; union of two non-regular; infinite union of finite | Yes | [2007](../../12-PYQ/2007/question-paper.pdf) |
| 2007 | Q.53 (CS) | MCQ | Every regular grammar LL(1)? Every regular set has an LR(1) grammar? | Yes (regular grammars; compilers vocabulary) | [2007](../../12-PYQ/2007/question-paper.pdf) |

The 2024 stem is worded “which is/are always TRUE”; the mapping records type MCQ. Use the PDF for the official item type. Several extracts are OCR-damaged (`L1 U Lz`, `2 = {a,b)`); the PDF is the source.

Years with no row in this mapping file: 2023, 2022, 2021, 2018, 2017, 2016, 2015, 2013, 2012, 2011, 2010, 2009. Absence from the extract is not a claim that those papers had no regular-language question. Some “is this regular?” stems sit in the finite-automata or pumping-lemma mappings.

## 2. What has been tested

- Closure yes/no, including infinite union and complement of a non-regular language.
- Independent exponents versus equal / doubled / unequal exponents.
- Modular counts versus modular-plus-equal counts.
- Copy `αβα` with mixed versus unary `α`.
- Concatenation of two unary regular sets versus `{a^n b^n}`.
- Prefix, suffix, `L · L^R` versus `{ww^R \| w ∈ L}`.
- Finite ⇒ regular, subset ⇏ regular.
- Regular grammar versus LL(1) / LR(1).

## 3. Recurring patterns

| Pattern | Entries |
|---|---|
| Closure arithmetic (“always true?”) | 2026, 2024, 2020, 2019, 2007 Q.7 |
| Independent vs dependent counts | 2025 CS2, 2014, 2008 |
| Copy / reverse / concatenation distinction | 2025 CS1, 2019, 2014 |
| Regular grammars | 2007 Q.53 |

The common job is: name the family, apply one closure rule, and refuse to cancel a regular operand.

## 4. Constructions and theorem applications

- Product DFA for independent modular counts (2025 CS2).
- Complement-closure both directions (2024).
- Reverse + concatenation ⇒ `L · L^R` regular; prefix/suffix constructions (2019).
- Right-linear / left-linear grammars; left recursion vs LL(1); DCFL ⇒ LR(1) (2007 Q.53).
- Myhill–Nerode or pumping is the implicit non-regularity engine for `{a^n b^n}`-type options; the stems themselves usually only ask the classification.

## 5. Traps seen in the stems

- Regular intersection does not regularise the other factor (2026).
- Unary `αβα` looks like a copy (2025 CS1).
- Intersecting with `{a, b}*` can still leave `{a^n b^n}` (2025 CS2).
- `L1 ∩ L̄2 = ∅` is inclusion (2024).
- Infinite union is not a closure operation of the family (2020, 2007).
- `{ww^R \| w ∈ L}` is not `L · L^R` (2019).
- The same letter `n` in `{a^n}{b^n}` is not shared (2014).
- `n ≠ m` is not “free exponents” (2008).
- Finite pieces of a non-regular set are still regular (2007).

## 6. How the existing practice file complements the PYQs

[14-PRACTICE practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/05-REGULAR-LANGUAGES/practice.md) drills Myhill–Nerode, the closure table, reverse of `a*b*`, `ww` versus `L · L`, `L*` regular while `L` is not, and min-DFA sizes for “starts with `b` and even `#a`”, no `11`, and `a^i b^j` with `i+j` even. This folder’s [PRACTICE.md](PRACTICE.md) adds unary-versus-mixed `αβα`, modular-versus-equal counts, quotient / homomorphism, regular grammars vs LL(1)/LR(1), and complement/inclusion arithmetic, without repeating those items.

## 7. Mapping notes

- Stored answers are all `VERIFICATION REQUIRED`.
- 2019 Q.7 and 2020 Q.8 extracts are OCR-corrupted; use the PDF.
- 2008 Q.53 extract uses `a"b'™` for exponentiation; the four languages are the ones in the table above.
- Min-DFA *numeric* questions live in the finite-automata mapping even when the language is regular.
- Pumping-length questions live in [07-PUMPING-LEMMA/PYQ.md](../07-PUMPING-LEMMA/PYQ.md).

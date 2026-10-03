# Context-Free Grammars — PYQ analysis

> **Answers:** every stored answer in the mapping is `VERIFICATION REQUIRED`. None are given here. Solve from the paper PDF named in the source line.

Mapping (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/03-CONTEXT-FREE-GRAMMARS/questions.md).
Papers: [12-PYQ](../../12-PYQ/).

## 1. Question table (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.52 (CS1) | mapping says MCQ; stem is “which of the following statements is/are true?” | Count invariant on `S → abaABAbba`, `A → aaBBAb \| bBabaa`, `B → aBb \| ab`: compare `#a` and `#b` | Yes | [2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2025 | Q.19 (CS1) | MCQ | Language of `S → aaB \| Abb`, `A → a \| aA`, `B → b \| bB` | Yes | [2025 set-01](../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.40 (CS2) | MCQ | LALR(1) vs SLR(1) vs CLR(1) for a tiny grammar | **No — compiler noise** | [2025 set-02](../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.59 (CS1) | NAT | CNF, `\|V\| = 10`, `w = a^{30} b^{30} c^{30}` derivable; number of steps in `S ⇒* w` | Yes | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.40 (CS2) | MCQ | Fill cells of an LL(1) table | **No — compiler noise** | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2024 | Q.52 (CS2) | mapping says MCQ; stem is “which … is/are TRUE?” | Counts `n_a, n_b, n_c` for `S → aS \| aSbS \| c` | Yes | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2023 | Q.39 (CS) | MCQ | Language of `S → aSb \| X`, `X → aX \| Xb \| a \| b`; regular or not | Yes | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2021 | Q.31 (CS Set-1) | MCQ | LL(1) table cells; extract OCR-destroyed | **No — compiler noise** | [2021 set-01](../../12-PYQ/2021/set-01/question-paper.pdf) |
| 2021 | Q.13 (CS Set-2) | MCQ | Which is **not** an intermediate representation (AST / CFG as control-flow graph / …) | **No — compiler noise** (`CFG` here is control-flow graph) | [2021 set-02](../../12-PYQ/2021/set-02/question-paper.pdf) |
| 2016 | Q.42 (CS-1) | MCQ | Languages of two CFGs; `and`/`or` and `≥`/`>` | Yes | [2016 set-01](../../12-PYQ/2016/set-01/question-paper.pdf) |
| 2016 | Q.19 (CS-2) | MCQ | Match lexical analysis / top-down parsing / semantic analysis / runtime to RE, leftmost derivation, type checking, activation records | **No — compiler noise** | [2016 set-02](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.28 (CS, 7 Feb shift 2) | MCQ | AST vs control-flow graph | **No — compiler noise** | [2015 set-02](../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2007 | Q.77 as stored | mapping says NAT; body is not a CFG question | Extract concatenates an unrelated “average length of Q.76” stem with the **linked** CFG statement for Q.78–79 | Extract damaged | [2007](../../12-PYQ/2007/question-paper.pdf) |

The mapping file has **no separate rows** for 2007 Q.78 and Q.79. Their common grammar is visible inside the Q.77 dump (`S → aB | bA`, `B → b | bS | aBB`, `A → a | aS | bAA`, with OCR damage `A→as`, `{S, 4, B}`). PDF required for the actual questions (generated string / number of derivation trees).

Years with no row in this mapping file: 2022, 2020, 2019, 2018, 2017, 2014, 2013, 2012, 2011, 2010, 2009, 2008, and 2026 CS2 / 2025 CS2 TOC-other-slots. Absence from the extract is not a claim that those papers had no CFG question.

## 2. What has been tested (on-topic rows only)

- Name `L(G)` as a union of two `{a^p b^q}` families, including the `and`/`or` distinction (2025 Q.19, 2016 Q.42).
- Prove or refute letter-count relations from the productions, without writing a closed form (2026 Q.52, 2024 Q.52).
- Decide whether a wrap `aSb` around an inner variable makes the language non-regular (2023 Q.39).
- Derivation length in CNF (2024 Q.59).
- Linked equal-count grammar (2007 Q.78–79, PDF).

## 3. Recurring patterns

| Pattern | Entries |
|---|---|
| Read `L(G)` | 2025 Q.19, 2016 Q.42, 2023 Q.39 |
| Count invariant / production accounting | 2026 Q.52, 2024 Q.52 |
| CNF combinatorics | 2024 Q.59 |
| Compiler keyword collision | 2025 Q.40, 2024 Q.40, 2021 Q.31, 2021 Q.13, 2016 Q.19, 2015 Q.28 |

## 4. Constructions and theorem applications

- 2024 Q.59 is the CNF identity “`n` letters ⇒ `2n − 1` steps”. `|V| = 10` is unused. `n = |a^{30} b^{30} c^{30}| = 90`.
- 2023 Q.39 is wrap-absorption: `L(X) = a*(a+b)b*` already, so `{ a^i w b^i | w ∈ L(X) }` is the same regular language.
- 2026 Q.52 is an invariant on `B` (`n_a = n_b`), lifted through `A` and `S`. Confirm the first `A`-production against the PDF (`aaBBAb` in the extract).
- 2024 Q.52 is live-`S` accounting: `aSbS` increases the `S`-count by 1, `c` decreases it by 1.

No stored official key is reproduced here.

## 5. Traps seen in the stems

- Options that replace a union of two independent families by a single linked exponent (`a^n b^{2n}` instead of `a^2 b^n ∪ a^n b^2`).
- Swapping `and`/`or` and `m ≥ 0` vs `m > 0`.
- Claiming the 2023 language is not regular because of the wrap `aSb`.
- Using `|V|` in the CNF step count.
- Strict `n_a > n_b` when a member with equality exists (`c`, `acbc` for `S → aS | aSbS | c`).
- Treating “CFG” in 2021 Q.13 / 2015 Q.28 as a context-free grammar.

## 6. How the existing practice file complements the PYQs

[14-PRACTICE practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/03-CONTEXT-FREE-GRAMMARS/practice.md) drills leftmost vs any derivation, useless symbols in the generating-then-reachable order, CNF/GNF recognition, Dyck vs equal counts, and inherent ambiguity. This folder’s [PRACTICE.md](PRACTICE.md) adds production-count invariants, wrap-absorption vs a rigid centre, CNF step arithmetic, and `and`/`or` grammar pairs that are not the 2016 stem.

## 7. Mapping notes

- Stored answers are all `VERIFICATION REQUIRED`.
- 2026 Q.52 and 2024 Q.52 are labelled MCQ in the mapping and read as MSQ from the stem; the PDF decides.
- 2007 Q.77 row is not a usable CFG question; Q.78–79 live only as a damaged tail of that row.
- 2021 Q.31 options are OCR-destroyed.
- FIRST/FOLLOW and parse tables are compiler design; they are listed only so they are not studied as TOC.

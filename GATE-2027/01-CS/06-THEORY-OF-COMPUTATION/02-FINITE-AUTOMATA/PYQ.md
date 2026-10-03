# Finite Automata — PYQ analysis

> **Answers:** the mapping lists **no verified answers** (every entry says “VERIFICATION REQUIRED”). None are given here. Solve each question with the method in [NOTES.md](NOTES.md) and check the official answer key yourself. Figures are omitted from many extracts; **do not invent them** — open the paper PDF named in the source line.

Mapping file (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/02-FINITE-AUTOMATA/questions.md).
Papers: [12-PYQ](../../12-PYQ/).

## 1. Question table (newest → oldest)

Distinct on-topic questions only. The four 2013 booklets reprint one stem; it is one row. Mapping noise is Section 7, not this table.

| Year | Q# (paper / set) | Type | Concept / skill tested (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2026 | Q.26 (CS-1, forenoon) | MCQ | 6-state NFA: which of 32, 65, 1, 128 **cannot** be the min equivalent DFA size | Yes (powerset bound) | [2026 set-01](../../12-PYQ/2026/set-01/question-paper.pdf) |
| 2026 | Q.47 (CS-2, afternoon) | MCQ | Two drawn DFAs `D1`, `D2`: equality / proper subset / intersection `{ε}` / star of the union vs lengths `≡ 0 (mod 3)` | Yes (identify languages; **figure missing** in the extract) | [2026 set-02](../../12-PYQ/2026/set-02/question-paper.pdf) |
| 2025 | Q.28 (CS-1) | MCQ | `n`-state NFA for regular `L`: which claim(s) are **false** (smaller NFA/DFA possible; some DFA `≤ 2^n`; every DFA has `> 2^n`) | Yes | [2025 set-01](../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.50 (CS-1) | MCQ | Language(s) of a drawn DFA over `{a, b}` (even `#b` / contains `bab` / ends with `bab` / avoids `aba`) | Yes (**figure missing**) | [2025 set-01](../../12-PYQ/2025/set-01/question-paper.pdf) |
| 2025 | Q.60 (CS-2) | NAT | `Σ = {1,2,3,4}`, `prod(x) mod 7`, `prod(ε) = 1`, `L = {prod = 2}`; min DFA states | Yes (multiplicative monoid) | [2025 set-02](../../12-PYQ/2025/set-02/question-paper.pdf) |
| 2024 | Q.50 (CS1) | MCQ | 5-state DFA: which claims are **false** (distinguishability of numbered states; every `n0 = n1` string is in `L`) | Yes (**figure missing**) | [2024 set-01](../../12-PYQ/2024/set-01/question-paper.pdf) |
| 2024 | Q.22 (CS2) | MCQ | Which RE equals a drawn DFA over `{0, 1}` | Yes (**figure missing**; option text is present) | [2024 set-02](../../12-PYQ/2024/set-02/question-paper.pdf) |
| 2023 | Q.14 (CS) | MCQ | RE for a 4-state DFA `{s, p, q, r}`, start `s`, accept `p` | Yes (**figure damaged** in the extract) | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2023 | Q.63 (CS) | NAT | Min DFA states for binary strings with **no three consecutive `1`s** | Yes | [2023](../../12-PYQ/2023/question-paper.pdf) |
| 2022 | Q.12 (CS) | MCQ | RE for a drawn FA over `{a, b}` (OCR-garbled options) | Yes (**figure missing**; PDF required) | [2022](../../12-PYQ/2022/question-paper.pdf) |
| 2021 | Q.38 (CS Set-1) | MCQ | Which drawn DFA accepts strings that **end with `011`** | Yes (**figure missing** / options destroyed in the extract) | [2021 set-01](../../12-PYQ/2021/set-01/question-paper.pdf) |
| 2020 | Q.51 (CS) | NAT | Min DFA states: `#a` divisible by 2 **but not** by 3 | Yes | [2020](../../12-PYQ/2020/question-paper.pdf) |
| 2019 | Q.48 (CS, printed header Set-2) | NAT | Bijections of `{1,…,5}`, composition `n(x)`, `L = {n(x) = id}`; min DFA states | Yes (group DFA) | [2019](../../12-PYQ/2019/question-paper.pdf) |
| 2018 | Q.6 (CS) | MCQ | `n`-state NFA, `k` = min DFA size: which of `k ≥ 2^n`, `k ≥ n`, `k ≤ n^2`, `k ≤ 2^n` is **necessarily** true | Yes | [2018](../../12-PYQ/2018/question-paper.pdf) |
| 2017 | Q.25 (CS Session 2) | NAT | Min DFA for `{ w1 a w2 | \|w1\| = 2, \|w2\| ≥ 3 }` over `{a, b}` | Yes (OCR-damaged stem; PDF required) | [2017 set-02](../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2017 | Q.39 (CS Session 2) | MCQ | `ε`-NFA table; compute `δ̂(q2, aba)` (mapping type line says NAT; options (A)–(D) are sets of states — use the PDF) | Yes (OCR-damaged table) | [2017 set-02](../../12-PYQ/2017/set-02/question-paper.pdf) |
| 2016 | Q.16 (CS-2) | NAT | Min DFA size for `(0+1)*(0+1)(0+1)*` | Yes | [2016 set-02](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2016 | Q.42 (CS-2) | MCQ | (I) all NFA states accepting ⇒ `L = Σ*` (II) exists regular `A` with `A ∩ B` regular for every `B` | Yes | [2016 set-02](../../12-PYQ/2016/set-02/question-paper.pdf) |
| 2015 | Q.49 (7 Feb Shift 1) | NAT | Min DFA for `L(M) ∩ L(N)` of two drawn DFAs | Yes (**figures missing**) | [2015 set-01](../../12-PYQ/2015/set-01/question-paper.pdf) |
| 2015 | Q.45 (7 Feb Shift 2) | NAT | Min DFA for `(0+1)*(10)` | Yes | [2015 set-02](../../12-PYQ/2015/set-02/question-paper.pdf) |
| 2015 | Q.32 (8 Feb Shift 1) | MCQ | Min DFA states for the **complement** of `L((0+1)*0011(0+1)*)` (options 4, 5, 6, 8) | Yes | [2015 set-03](../../12-PYQ/2015/set-03/question-paper.pdf) |
| 2014 | Q.16 (SET-1) | MCQ | Reachable NFA-state set on input `0011` for a drawn machine | Yes (**figure missing**) | [2014 set-01](../../12-PYQ/2014/set-01/question-paper.pdf) |
| 2014 | Q.36 (SET-1) | MCQ | Which of three REs denote a drawn DFA (I `0*1(1+00*1)*`, II a broken union, III `(0+1)*1`) | Yes (DFA figure missing; RE text present) | [2014 set-01](../../12-PYQ/2014/set-01/question-paper.pdf) |
| 2013 | Q.33 / Q.40 / Q.29 / Q.44 (Booklets A–D, **same stem**) | MCQ | Drawn DFA `A`: which of four claims are **false** (complement is CFL; a given RE; `A` is minimal; all strings of length `≥ 2`) | Yes (**figure missing**). Four mapping entries, one question | [2013 set-01](../../12-PYQ/2013/set-01/question-paper.pdf) |
| 2012 | Q.12 (Booklet A) | MCQ | Complement of the language of a drawn unary NFA with `ε`-edges (options `∅`, `{ε}`, `a*`, `{a, ε}`) | Yes (**figure missing**) | [2012](../../12-PYQ/2012/question-paper.pdf) |
| 2012 | Q.46 (Booklet A) | MCQ | Complete missing DFA arcs: every length-3 window has at most two `0`s (no `000`); states named by last two bits plus a dead state | Yes (**figure / option tables damaged**) | [2012](../../12-PYQ/2012/question-paper.pdf) |
| 2011 | Q.42 (Booklet A) | MCQ | Unary `L = { a^{kn} | k > 0 }`, `n` a fixed positive integer; min DFA states (options `k+1`, `n+1`, `2^n+1`, `2k+1`; OCR) | Yes | [2011](../../12-PYQ/2011/question-paper.pdf) |
| 2011 | Q.45 (Booklet A) | MCQ | Which drawn machine is a valid **minimal** DFA equivalent to a given DFA | Yes (**figures missing**) | [2011](../../12-PYQ/2011/question-paper.pdf) |
| 2010 | Q.41 (CS) | MCQ | `w` of length `n` over `{0, 1}`; min **NFA** states for the language of all substrings of `w` (options `n−1`, `n`, `n+1`, `2^{n−1}`; OCR) | Yes | [2010](../../12-PYQ/2010/question-paper.pdf) |
| 2009 | Q.41 (CS) | MCQ | Language of a drawn DFA (begin 0 or 1 / end with 0 / end with 00 / contain 00) | Yes (**figure missing**) | [2009](../../12-PYQ/2009/question-paper.pdf) |
| 2007 | Q.29 (CS) | MCQ | Min DFA for `#0` divisible by 3 **and** `#1` divisible by 5 (options 15, 11, 10, 9) | Yes | [2007](../../12-PYQ/2007/question-paper.pdf) |

**Counts:** 31 distinct on-topic questions in this table (2013 counted once). Mapping file rows for 2013 booklets B–D are reprints, not extra questions. Years 2007–2026 with **no** row in this mapping file: **2008** (the 2008 NFA↔RE matching question is filed under regular expressions). Absence from the extract is not proof that a paper had no FA question.

## 2. What has been tested

- Write the min complete DFA *size* from a one-line description (consecutive runs, residue conditions, `Σ+`, group action, product of symbols, a distinguished position plus a length floor).
- Apply the powerset bound without building the DFA (`k ≤ 2^n`; 1 possible; `k ≥ n` not necessary; `> 2^n` impossible).
- Read a drawn DFA: name `L(M)`, decide distinguishability of two states, or pick the matching RE.
- Compute one `ε`-NFA extended transition, or the set of NFA states reached by a given string.
- Complement of an NFA language; fill missing arcs of a window-constraint DFA; minimise a drawn machine.
- NFA size for all substrings of a fixed word.

## 3. Recurring patterns

| Kind | Entries | Comment |
|---|---|---|
| NAT min DFA size from a description | 2025 Q.60, 2023 Q.63, 2020 Q.51, 2019 Q.48, 2017 Q.25, 2016 Q.16, 2015 Q.49, 2015 Q.45 | Recipe in [NOTES.md](NOTES.md) §7, §13, §14; [FORMULAS.md](FORMULAS.md) §5 |
| MCQ min DFA size (options) | 2015 Q.32, 2011 Q.42, 2007 Q.29 | Complement-of-contains; unary `a^{kn}`; product of moduli |
| NFA → DFA bounds | 2026 Q.26, 2025 Q.28, 2018 Q.6 | Same three facts, three wordings |
| Identify language / distinguishability of a drawn DFA | 2026 Q.47, 2025 Q.50, 2024 Q.50, 2013, 2009 Q.41 | PDF required |
| DFA → RE options | 2024 Q.22, 2023 Q.14, 2022 Q.12, 2014 Q.36 | Short-string filter; [NOTES.md](NOTES.md) §15 |
| `ε`-NFA / NFA reachability | 2017 Q.39, 2014 Q.16 | Close–consume–close; subset on one word |
| NFA complement / missing arcs / minimization / substring NFA | 2012 Q.12, 2012 Q.46, 2011 Q.45, 2010 Q.41 | One of each |
| True/false about NFAs and `A ∩ B` | 2016 Q.42 | Incomplete NFA; `A = ∅` |

No frequency percentages are claimed. Several of the highest-value NATs have **no figure** and can be practised from the stem alone; the identify/RE/minimization cluster cannot.

## 4. Constructions and theorem applications (how to attempt; not keys)

Recipes only. Official keys remain `VERIFICATION REQUIRED`.

- **Powerset bound (2026 Q.26, 2025 Q.28, 2018 Q.6).** `k ≤ 2^n` is the one necessary inequality. For `n = 6`, anything `> 64` is impossible. `k = 1` occurs for `∅` and `Σ*`. `k ≥ n` is not necessary. “Every DFA has `> 2^n` states” contradicts subset construction. NOTES §5; PRACTICE Q14.
- **No `k` consecutive `1`s (2023 Q.63).** Trailing-`1` counts `0 … k−1` plus a dead sink: `k + 1` complete states. For `k = 3` that is 4. NOTES Example 5; PRACTICE Q17.
- **Even `#a` but not divisible by 3 (2020 Q.51).** Residues mod 6, accept `{2, 4}`. All six distinguishable. NOTES Example 6; PRACTICE Q18.
- **`(0+1)*(0+1)(0+1)*` (2016 Q.16).** Language `Σ+`. Two states. NOTES Example 8; PRACTICE Q8.
- **Ends with `10` (2015 Q.45).** Prefixes of `10`: 3 states. PRACTICE Q7 is the distinguishability form for `11`.
- **Complement of contains `0011` (2015 Q.32).** Progress DFA on `0011` has 5 states; flipping accept/reject keeps 5 if those states stay distinguishable. NOTES §7 contains-`w` row.
- **Product of moduli (2007 Q.29).** Independent counters: `3 × 5 = 15`. NOTES §6.
- **Unary `{a^{kn} : k > 0}` (2011 Q.42).** Start is a rejecting residue 0; accepting residue 0 is a different state: `n + 1`. PRACTICE Q16 (`n = 3`).
- **`w1 a w2` with `|w1| = 2`, `|w2| ≥ 3` (2017 Q.25).** Waiting + branch + `|w2|` counter + dead: `p + q + 3 = 8`. PRACTICE Q19 uses different `p, q`.
- **Product of symbols mod 7 (2025 Q.60).** Multiplicative group of order 6; residue 0 unreachable. NOTES §13.
- **Bijections of `{1,…,5}` (2019 Q.48).** States = `S_5`, `|G| = 120`. PRACTICE Q20 uses `S_3`.
- **All substrings of `w`, `|w| = n` (2010 Q.41).** NFA with `n + 1` states; tight on `w = a^n`. NOTES §12.
- **All NFA states accepting (2016 Q.42 I).** False without completeness. **II:** `A = ∅` works. PRACTICE Q9.
- **NFA complement (2012 Q.12).** Typical unary `a+` trap → `{ε}`. Figure required to confirm the accepted language. PRACTICE Q4 is the existential-run analogue, not a copy of the figure.
- **DFA → RE (2014 Q.36).** Options I and III are the standard pair for “ends with `1`”; II is the usual broken union. Confirm on the PDF figure. NOTES §15.

## 5. Traps seen in the stems

- `2^n + 1` or `2^{n+1}` offered as a possible min DFA size after an `n`-state NFA.
- `k ≥ n` offered as “necessary”.
- Extra start state on “no three consecutive `1`s”.
- `prod(ε) = 0` or an extra residue `0` in a product-of-nonzero-digits DFA.
- `5` or `25` in place of `5!` for `S_5`.
- `Σ+` counted as 1.
- NFA complement by flipping `F`.
- Intersection of two count conditions added (`3+5`) or replaced by `lcm` instead of the product.
- Ends-with vs contains vs avoids, decided from the picture’s *shape*.
- OCR: 2017 Q.25/Q.39, 2011 Q.42, 2010 Q.41, 2022 Q.12 options. Trust the PDF.

## 6. How the existing practice file complements the PYQs

The existing [practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/02-FINITE-AUTOMATA/practice.md) already drills ends-with-`01`, a two-state “contains `1`” NFA and its subset construction, even `#a` and even `#b`, contains-`ab`, exactly two `1`s, third-from-start vs third-from-end, and a 4-state DFA that minimises to 2.

This folder’s [PRACTICE.md](PRACTICE.md) does **not** repeat those questions. It adds the bound-MSQ, `Σ+`, incomplete all-accepting NFA, no-consecutive and exactly-three counts, `ε`-NFA `δ̂`, second-from-end, unary `a^{3k}` (`k ≥ 1`), the 2020-style mod-6 language, a `w1 a w2` variant, and an `S_3` group DFA — the PYQ shapes that the existing file does not isolate.

Figure-based PYQs (2026 Q.47, 2025 Q.50, 2024 Q.50/Q.22, 2023 Q.14, 2022 Q.12, 2021 Q.38, 2017 Q.39 table, 2015 Q.49, 2014 Q.16, 2013, 2012 Q.12/Q.46, 2011 Q.45, 2009 Q.41) still have to be done from the paper. Short-string tracing in NOTES §15 and PRACTICE Q1, Q7, Q13 is the transferable skill.

## 7. Mapping notes and noise

**Mapping noise (not counted in §1):**

| Year | Q# | Why it is listed here as noise |
|---|---|---|
| 2015 | Q.27 (7 Feb Shift 2) | Match-the-following: lexical analysis / parsing / register allocation / expression evaluation. Lexical analysis is paired with DFA minimization, but the stem is a **compiler-design** matching question, not an FA construction. |

**2013 reprints.** Mapping rows Q.40 (Booklet B), Q.29 (Booklet C), Q.44 (Booklet D) are the same question as Q.33 (Booklet A). One distinct item.

**Type-line glitch.** 2017 Q.39 is stored as NAT in the mapping but prints four set-valued MCQ options. Use the PDF.

**OCR / missing figures.** Stems for 2022 Q.12, 2021 Q.38, 2017 Q.25/Q.39, 2014 Q.16, 2012 Q.12/Q.46, 2011 Q.42/Q.45, 2010 Q.41, 2009 Q.41, and every “drawn DFA/NFA” row above, drop or scramble the figure. Nothing in NOTES or PRACTICE reconstructs those figures.

**RE-folder overlap.** DFA→RE option questions live **here**; English-description RE questions live in [`01-REGULAR-EXPRESSIONS/PYQ.md`](../01-REGULAR-EXPRESSIONS/PYQ.md). 2008 Q.52 (match NFAs to REs) is in the RE mapping.

**Stored answers.** Every mapping answer field is `VERIFICATION REQUIRED`. This file does not invent keys.

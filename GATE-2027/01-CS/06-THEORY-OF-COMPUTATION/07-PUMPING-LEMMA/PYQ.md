# Pumping Lemma — PYQ analysis

> **Answers:** every stored answer in the mapping is `VERIFICATION REQUIRED`. None are given here. Solve from the paper PDF named in the source line.

Mapping (read-only): [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/07-PUMPING-LEMMA/questions.md).
Papers: [12-PYQ](../../12-PYQ/).

## 1. Question table (newest → oldest)

| Year | Q# (paper) | Type | Concept / skill (paraphrased) | On-topic? | Paper |
|---|---|---|---|---|---|
| 2019 | Q.15 (CS) | MCQ | Which of 3, 5, 9, 24 can be a pumping length of a given regular unary-ish language | Yes | [2019](../../12-PYQ/2019/question-paper.pdf) |

The mapping extract is OCR-corrupted (`L=(2l2=a23kr=1012k`). The standard reconstruction, to be checked on the PDF, is: for `Σ = {a, b}`,

`L = { x | x = a^{2+3k} or x = b^{10+12k}, k ≥ 0 }`,

with those four numeric options. Do not treat the reconstruction as a substitute for the paper.

Years with no row in this mapping file: every year other than 2019. That is not a claim that those papers had no pumping question. Non-regularity of `{a^n b^n}`-type languages is asked inside the [regular-languages mapping](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/05-REGULAR-LANGUAGES/questions.md) without naming the lemma.

## 2. What has been tested

- The **constant** in the regular pumping lemma: which integers are legal pumping lengths of a *regular* language presented as two arithmetic progressions, one on `a` and one on `b`.
- Not tested in this mapping: write-a-proof that a named language is not regular / not CFL; CFL `uvwxy` conditions; converse of the lemma.

## 3. Recurring patterns

| Pattern | Entries |
|---|---|
| Pumping length of a regular language with two unary components | 2019 Q.15 only, in this mapping |

The skill the stem actually uses: a number `p` is a pumping length only if **every** word of `L` of length ≥ `p` has a legal split. Sparse words such as `b^{10}` kill small `p`. Any integer at least as large as some DFA’s state count (or large enough that those sparse words fall below the threshold) works, and every larger integer then works too.

## 4. Constructions and theorem applications

- Existence of a DFA for `L` (two unary cycles plus a dead sink for mixed strings) guarantees that some integer is a pumping length.
- The lemma does not require `p` to equal the min-DFA size.
- Official keyed option: `VERIFICATION REQUIRED`. Work the PDF.

## 5. Traps seen in the stems

- Choosing 3 because of the `a`-cycle `2 + 3k`, without checking whether `b^{10}` can be pumped inside a window of size 3.
- Thinking that only one integer qualifies.
- Thinking a larger option is illegal once a smaller option fails.

## 6. How the existing practice file complements the PYQs

[14-PRACTICE practice.md](../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/07-PUMPING-LEMMA/practice.md) drills the quantifiers, `|y| ≥ 1`, CFL `uvwxy` bounds, defeating every legal split, `{a^n b^{n+1}}`, smallest pumping length of `(aa+bb)*`, `{a^n b^{2n}}` as CFL-not-regular, invalid arguments, the `a^p b^p c^p` window, and `{a^{n^2}}`. This folder’s [PRACTICE.md](PRACTICE.md) adds `|xy| ≤ p` via pigeonhole, `(aba)*` and odd-length unary pumping lengths, `{a^{n!}}`, marked-copy intersection before pumping, and the `q > p` fact, without repeating those items.

## 7. Mapping notes

- Stored answer is `VERIFICATION REQUIRED`.
- The 2019 extract is not usable as a stem; the PDF is required.
- CFL pumping has no mapped GATE row in this folder. Depth on `{a^n b^n c^n}` comes from the notes and from CFL-folder stems that need the lemma.

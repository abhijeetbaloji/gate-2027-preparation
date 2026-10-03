# Pumping Lemma — Notes

Syllabus line: *Regular and context-free languages, pumping lemma* (GATE CS 2027, Section 6). This folder is the **necessary-condition** test. It proves that a language is *not* regular, or *not* context-free. It never proves that a language *is* regular or *is* CFL. Those proofs live in [regular languages](../05-REGULAR-LANGUAGES/) and [context-free languages](../06-CONTEXT-FREE-LANGUAGES/).

## What the PYQs actually test

From the mapped questions (`../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/07-PUMPING-LEMMA/questions.md`):

| Pattern | Seen in |
|---|---|
| Which integers can be a **pumping length** of a given regular (unary-ish) language | 2019 Q.15 |

The mapping has a single stem, and the extract is OCR-garbled. The standard reconstruction (verify against [the PDF](../../12-PYQ/2019/question-paper.pdf)) is: over `{a, b}`,

`L = { a^{2+3k} | k ≥ 0 } ∪ { b^{10+12k} | k ≥ 0 }`,

and the options are `3, 5, 9, 24`. The skill is not “apply pumping to prove non-regularity”; it is “what the constant in the lemma actually is”. Section 5 works this shape without recording an official key.

Absence of other years from the mapping is not a claim that those papers never used pumping. Non-regularity arguments also sit inside the regular-language mapping.

---

## 1. Regular pumping lemma, with the quantifiers

If `L` is regular, then **there exists** an integer `p ≥ 1` (a **pumping length**) such that **for every** `s ∈ L` with `|s| ≥ p`, **there exists** a split `s = xyz` satisfying

1. `|xy| ≤ p`,
2. `|y| ≥ 1`,
3. `xy^k z ∈ L` for **every** `k ≥ 0` (including deletion `k = 0`).

Read the quantifiers in that order. They are the lemma.

| Who chooses | What |
|---|---|
| The lemma (existence) | the integer `p` |
| You, the prover of non-regularity | one long string `s ∈ L` |
| The adversary / the lemma | the split `xyz` among those with `|xy| ≤ p` and `|y| ≥ 1` |
| You again | a pump power `k` that throws `xy^k z` out of `L` |

Because the split is existential, a non-regularity proof must defeat **every** legal split, not one favourite split.

The converse is false: satisfying the conclusion of the lemma does not make `L` regular. Give a DFA, an NFA, an RE, a right-linear grammar, or a finite Myhill–Nerode index ([regular languages](../05-REGULAR-LANGUAGES/)).

---

## 2. Why `|xy| ≤ p` and `|y| ≥ 1`

Let `A` be a DFA for `L` with `p` states (any DFA, not necessarily minimal). Take `s = a1 a2 … an ∈ L` with `n ≥ p`. The run on the **prefix of length `p`** visits `p + 1` states (the start state, then one state per symbol). By the pigeonhole principle two of those states are the same, say after `i` symbols and after `j` symbols, `0 ≤ i < j ≤ p`.

- `x` = the prefix up to the first visit,
- `y` = the portion that walks the cycle (`j − i ≥ 1` symbols),
- `z` = the rest.

Then `|xy| = j ≤ p`, `|y| ≥ 1`, and pumping `y` is walking the cycle `k` times. Accepting is preserved because the machine is in the same state at both ends of `y`.

**Why `|y| ≥ 1`.** If `y` could be empty, pumping would not change the string, and the condition would be true of every language. The nonempty cycle is what makes the lemma capable of producing a *different* string.

**Why the window is the first `p` symbols, not an arbitrary block.** The pigeonhole is applied to a prefix of length `p`. A split that takes `y` from the *middle* of a long string may have `|xy| > p` and is **not** a split the lemma is obliged to honour. Failing an illegal split proves nothing.

The number of states of **some** DFA is therefore a pumping length. The number of states of the *minimal* DFA is a pumping length. It need not be the *smallest* one (Section 4).

---

## 3. Proving `L` is not regular

Assume, for a contradiction, that `L` is regular. Let `p` be a pumping length given by the lemma. Choose one `s ∈ L` with `|s| ≥ p`. Then let `s = xyz` be an **arbitrary** split with `|xy| ≤ p` and `|y| ≥ 1`, and produce a `k` (often `k = 0` or `k = 2`) such that `xy^k z ∉ L`.

The length bound is what makes the case analysis short: if `s` begins with `p` letters of one block, every legal `y` lies inside that block.

### `{ a^n b^n | n ≥ 0 }`

Take `s = a^p b^p`. Then `|xy| ≤ p` forces `y = a^t` with `1 ≤ t ≤ p`. Deleting `y` gives `a^{p−t} b^p`. This is in the language only if `p − t = p`, i.e. `t = 0`, which is forbidden. Every legal split fails.

### `{ a^n b^{n+1} | n ≥ 0 }`

Take `s = a^p b^{p+1}`. Again `y = a^t`, `1 ≤ t ≤ p`. Then `xy^0 z = a^{p−t} b^{p+1}`, and `p + 1 = (p − t) + 1` would need `t = 0`.

### `{ a^n b^{2n} | n ≥ 0 }` — not regular, but context-free

The grammar `S → aSbb | ε` generates exactly this language, so it is CFL. It is not regular: `s = a^p b^{2p}`, `y = a^t`, `xy^0 z = a^{p−t} b^{2p}`, and `2p = 2(p − t)` needs `t = 0`. Failure of *regular* pumping does not touch the grammar.

### `{ a^{n^2} | n ≥ 0 }`

Take `s = a^{p^2}`. Then `y = a^t` with `1 ≤ t ≤ p`. The pumped-up string `xy^2 z` has length `p^2 + t`. The next square is `(p+1)^2 = p^2 + 2p + 1`. Because `1 ≤ t ≤ p`,

`p^2 < p^2 + t ≤ p^2 + p < p^2 + 2p + 1`,

so the length sits strictly between two consecutive squares. Not regular. This argument says nothing about whether the language is CFL.

### `{ a^{n!} | n ≥ 0 }`

Take `n ≥ max(2, p)` and `s = a^{n!}`. Then `y = a^t` with `1 ≤ t ≤ p ≤ n!`. Length `n! + t` lies strictly between `n!` and `(n+1)! = (n+1) n!`, because `n! + t ≤ n! + n! = 2 n! < (n+1) n!` for `n ≥ 2`.

---

## 4. Pumping length

An integer `p ≥ 1` **is a pumping length** of a regular language `L` when every `s ∈ L` with `|s| ≥ p` has *some* legal split that pumps inside `L`.

Facts that follow from the definition (and from Section 2):

| Fact | Why |
|---|---|
| If `p` is a pumping length, so is every `q > p` | a string of length `≥ q` already has length `≥ p`, and its `p`-window split also satisfies `|xy| ≤ q` |
| The number of states of **any** DFA for `L` is a pumping length | Section 2 |
| The min-DFA size is a pumping length | it is *a* DFA |
| The **smallest** pumping length can be strictly smaller than the min-DFA size | the lemma only needs some cycle in the first `p` letters, not a full set of distinguishable states |
| `p` is not a pumping length as soon as **one** long word has **no** legal split that stays in `L` | the definition is universal over long words |

**Example: `(aa + bb)*`.** The language is concatenations of the blocks `aa` and `bb`. The min DFA has 4 states (aligned at a block boundary; just read one `a`; just read one `b`; rejecting sink). The smallest pumping length is **2**: every nonempty member begins with `aa` or `bb`, and pumping that first block stays in the language. The integer `1` fails: `aa` has only the split `y =` first `a`, and `xy^0 z = a` is not in the language. So 2, 3, 4, … are all pumping lengths, and 2 is already smaller than the min-DFA size.

**Example: `(aba)*`.** Strings have lengths `0, 3, 6, …`. The integer `2` fails on `aba`: every split with `|xy| ≤ 2` produces `ba`, `a`, `aa`, or `abba` after pumping, none of which is `(aba)*`. The integer `3` works: pump the first block `aba`. Smallest pumping length 3.

### 2019-style: which option *can* be a pumping length

Let `L = { a^{2+3k} | k ≥ 0 } ∪ { b^{10+12k} | k ≥ 0 }` (standard reconstruction of the mapped 2019 stem; confirm the exponents on the PDF). Members are

`a^2, a^5, a^8, …` and `b^{10}, b^{22}, b^{34}, …`.

The dangerous short word is `b^{10}`. If `p ≤ 10`, this word must be pumped with `|y| ≤ p`. Deleting `y` leaves a strictly shorter all-`b` string. No length in `{0, 1, …, 9}` is `10 + 12k`, and the string is not an `a`-word, so **every** legal split of `b^{10}` fails. In particular `3`, `5` and `9` are not pumping lengths.

If `p = 24`, the words `b^{10}` and `b^{22}` are shorter than 24, so the lemma does not constrain them. The next `b`-word is `b^{34}`: pump a block of 12 `b`s (`12 ≤ 24`); deletion lands on `b^{22} ∈ L`, and adding 12 preserves the residue `10 (mod 12)`. Every `a`-word of length ≥ 24 has the form `a^{2+3k}` with `2+3k ≥ 24`; pump a block of 3 `a`s. So 24 **is** a pumping length.

Among options of this shape, the large multiple of both cycle lengths is the one that is *guaranteed*. A number smaller than the shortest exceptional word in a residue class typically fails. Do not treat “min DFA size” as the unique legal option: every integer larger than a pumping length is still a pumping length. The official keyed option is not recorded here (`VERIFICATION REQUIRED` in the mapping).

The smallest pumping length of this `L` is in fact 12 (`b^{10}` becomes exempt, and `b^{22}` can pump 12 `b`s down to `b^{10}`), which is already smaller than the min DFA (the `b`-chain plus the `a`-cycle plus a dead sink). The 2019 options do not include 12.

---

## 5. Invalid arguments (all appear as wrong options)

| Argument | Why it is invalid |
|---|---|
| “This one split of `a^p b^p` fails, so `L` is not regular” | another legal split might work; you must quantify over every `y = a^t`, `1 ≤ t ≤ p` |
| “A string shorter than `p` leaves `L` when pumped” | the lemma is silent on `|s| < p` |
| “I pumped `y` from the `b`-block of `a^p b^p`” | that split can have `|xy| > p`; the adversary is not required to give it to you |
| “Some pumped string stays in `L`, therefore `L` is regular” | converse of the lemma; also, *some* `k` staying in is not the same as *every* `k` |
| “`p` must equal the number of min-DFA states” | it is *a* pumping length, not always the smallest, and not the only one |
| “If 5 is not a pumping length, 24 cannot be one” | larger integers can succeed after short exceptional words drop below the threshold |

A repaired `{a^n b^n}` argument is one sentence longer than the invalid one: *every* legal `y` is `a^t` for some `t ≥ 1`, and *every* such `t` breaks the equality. The extra sentence is the proof.

---

## 6. Context-free pumping lemma

If `L` is context-free, then **there exists** `p` such that **for every** `s ∈ L` with `|s| ≥ p`, **there exists** a split `s = uvwxy` satisfying

1. `|vwx| ≤ p` (the pumped window is local),
2. `|vx| ≥ 1` (`v` and `x` may each be empty, but not both),
3. `u v^k w x^k y ∈ L` for every `k ≥ 0`.

The two copies `v` and `x` are pumped **together**. The bound is on `vwx`, not on `uv`. Copying the regular condition `|uv| ≤ p` onto a CFL split is a standard wrong option.

Why the window is local: in a Chomsky-normal-form parse tree of a long string, some non-terminal repeats on a path; the portion between the two occurrences has yield-length at most `p`, and pumping that portion is pumping `v` and `x`.

Regular pumping is *not* the CFL lemma. A language can fail regular pumping and still be CFL (`{a^n b^n}`, `{a^n b^{2n}}`). A language can fail CFL pumping and therefore fail to be CFL (`{a^n b^n c^n}`). Failure of regular pumping never proves “not CFL”.

Pumping does **not** prove that a language is context-free. Give a CFG or a PDA ([context-free grammars](../03-CONTEXT-FREE-GRAMMARS/), [push-down automata](../04-PUSH-DOWN-AUTOMATA/)).

---

## 7. Why the window cannot hit both `a` and `c` in `a^p b^p c^p`

Let `s = a^p b^p c^p` and `s = uvwxy` with `|vwx| ≤ p`. The last `a` and the first `c` have `p` letters `b` between them. Any substring that contains at least one `a` and one `c` therefore has length at least `p + 2`. A window of length ≤ `p` cannot cover that gap. So `vwx` lies in `a*b*`, or in `b*c*`, or in a single block. It never contains both an `a` and a `c`.

That is the whole case analysis for `{ a^n b^n c^n | n ≥ 0 }`:

- only `a`s (or only `b`s, or only `c`s) in `vx`: one count changes, the other two stay `p`;
- `a`s and `b`s in `vx`: the `c`-count stays `p`, and at least one of the first two counts changes;
- `b`s and `c`s in `vx`: the `a`-count stays `p`, and at least one of the other two changes.

In every case `u v^2 w x^2 y` leaves the language. Hence not context-free (and, a fortiori, not regular — but regular pumping on the same string already shows “not regular” with a weaker conclusion, because `|xy| ≤ p` plants `y` entirely in the `a`s).

The same separation works for `{ 0^n 1^n 0^n }` and for `{ a^n b^n a^n }`.

---

## 8. Intersect with a regular language first

Pumping a messy language is painful. Regular languages are closed under intersection, and the intersection of a CFL with a regular language is a CFL. So:

- to prove `L` is not regular, it is enough to prove that `L ∩ R` is not regular for some regular `R`;
- to prove `L` is not CFL, it is enough to prove that `L ∩ R` is not CFL for some regular `R`.

**Examples.**

- `{ ww | w ∈ {a, b}* } ∩ a*ba*b = { a^n b a^n b | n ≥ 0 }`, then pump (or use MN on `a^i b`).
- `{ wcw | w ∈ {a, b}* } ∩ a* c a* = { a^n c a^n | n ≥ 0 }`.
- `{ a^n b^n c^n | n ≥ 0 } ∪ {a, b, c}* {d} {a, b, c, d}*`: intersect with `a*b*c*` to recover the triple-equality core.

Choosing `R = ∅` is useless: `L ∩ ∅ = ∅` is regular for every `L`.

---

## GATE problem-solving approach

1. **Decide what you are proving.** Not regular? Regular pumping or Myhill–Nerode. Not CFL? CFL pumping (or Ogden / intersection). Regular / CFL? A machine or a grammar, never pumping.
2. **Fix `p` as an adversary’s constant.** Do not pick a numeric `p` unless the question asks which integers *are* pumping lengths.
3. **Pick one long `s`** whose block lengths are `p` (or `p^2`, or `p!`) so that `|xy| ≤ p` (or `|vwx| ≤ p`) cannot see two far-apart blocks.
4. **Case-analyse every legal position of `y` (or of `vwx`)**. The length bound should leave one or two cases, not six.
5. **Pump down (`k = 0`) when a count would have to stay matched; pump up when a gap between polynomial / factorial lengths is needed.**
6. **Pumping-length MCQ.** Strike every option `p` for which a *specific* word of length ≥ `p` has no good split (usually a short unary word in a sparse arithmetic progression). Keep every option that is at least as large as a DFA size, or large enough that the sparse words fall below the threshold. If `p` works, every larger option works too.

## Common traps (summary)

- Converse of the lemma.
- Checking one split.
- Pumping a string shorter than `p`.
- Taking `y` outside the first `p` symbols.
- Copying `|xy| ≤ p` onto a CFL split, or `|uv| ≤ p` onto `uvwxy`.
- Concluding “not CFL” from regular pumping.
- Claiming the unique pumping length equals the min-DFA size.
- Treating a number smaller than a pumping length as automatically a pumping length (the opposite of the `q > p` fact).

## Edge cases

- `k = 0` is legal and often the cheapest contradiction.
- `ε` is never a string the lemma forces you to pump: `|ε| = 0 < p`.
- Unary languages: `y` is a block of the unique letter; the argument becomes arithmetic on lengths.
- A finite language has a pumping length (any `p` larger than every word: there are then no words of length ≥ `p` to constrain). That does not make pumping a regularity test in the useful direction.

## Connections

- **Regular languages** (05): Myhill–Nerode *characterises* regularity; pumping does not. Use MN when the prefixes `a^i` are obvious; use pumping when a length-arithmetic gap is obvious (`n^2`, `n!`).
- **Finite automata** (02): `p` can be taken as the number of DFA states. Min-DFA size is a pumping length, not always the smallest.
- **Context-free languages** (06) / **CFGs** (03) / **PDAs** (04): CFL pumping is the matching necessary condition. `{a^n b^n}` and `{a^n b^{2n}`} pass it and have grammars; `{a^n b^n c^n}` fails it.
- **Undecidability** (09): “is `L(M)` regular?” is undecidable for TMs. Pumping is not an algorithm for that question; it is a hand proof for a *fixed* language you can write down.

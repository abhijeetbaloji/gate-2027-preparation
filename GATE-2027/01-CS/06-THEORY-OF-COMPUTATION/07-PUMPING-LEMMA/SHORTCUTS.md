# Pumping Lemma — Shortcuts

Each shortcut below is a valid rule, not a guess. The limitation line says exactly where it stops working.

## 1. Independent exponents ⇒ regular; equal exponents ⇒ not

- **Solves**: first-pass classification before writing a pumping proof.
- **Why**: `a*b*` has a DFA; `{a^n b^n}` does not.
- **Example**: `{a^n b^m}` regular; `{a^n b^n}`, `{a^n b^{2n}}`, `{a^n b^{n+1}}` not regular.
- **Limitation**: `{a^n b^{2n}}` is still CFL. Never “if it pumps it is regular”.

## 2. Finite ⇒ regular; then pumping is optional

- **Solves**: finite languages, and finite subsets of non-regular languages.
- **Why**: a trie DFA exists, so the lemma applies but you do not need it.
- **Limitation**: infiniteness is not a non-regularity proof.

## 3. Plant `y` in the first block

- **Solves**: `{ a^p b^{f(p)} }` arguments.
- **When**: `|xy| ≤ p` and `s` starts with `p` letters `a`.
- **Why**: the window cannot reach the `b`s, so every legal `y` is `a^t`, `t ≥ 1`.
- **Example**: `{a^n b^{2n}}` with `s = a^p b^{2p}`, then `k = 0`.
- **Limitation**: if you chose a string whose first `p` letters mix two blocks, the case analysis grows. Choose `s` so that it does not.

## 4. If `p` is a pumping length, so is every larger integer

- **Solves**: “which of 3, 5, 9, 24 can be a pumping length?” after one option is known to work.
- **Why**: the same split that satisfies `|xy| ≤ p` satisfies `|xy| ≤ q` for `q > p`.
- **Example**: `(aa+bb)*` has smallest `p = 2`, so 3 and 4 work; 1 does not.
- **Limitation**: a *smaller* option is not automatic. Short sparse words (`b^{10}` in the 2019-shape language) kill small `p`.

## 5. Min-DFA size is *a* pumping length, not *the* pumping length

- **Solves**: options that assume a unique constant equal to the number of states.
- **Why**: the lemma only needs some cycle in a prefix; distinguishable states can outnumber that cycle.
- **Example**: `(aa+bb)*` — smallest `p = 2`, min DFA has 4 states.
- **Limitation**: you may still use min-DFA size as a *safe* pumping length when the question asks for one integer that works.

## 6. Window cannot see `a` and `c` in `a^p b^p c^p`

- **Solves**: CFL pumping of three equal blocks.
- **Why**: `|vwx| ≤ p` and the `b`-block has length `p`.
- **Example**: `{a^n b^n c^n}` is not CFL; `{a^n b^n}` is CFL (regular pumping only).
- **Limitation**: this geometry is special to three (or more) consecutive blocks of length `p`. It is not a reason that `vwx` contains only one alphabet symbol in an arbitrary CFL.

## 7. Intersect with a regular language, then pump

- **Solves**: `{ww}`, `{wcw}`, a non-regular core hidden in extra junk.
- **Why**: regular ∩ regular = regular; CFL ∩ regular = CFL. A bad core infects the original.
- **Example**: `{ wcw | w ∈ {a, b}* } ∩ a*ca* = { a^n c a^n }`.
- **Limitation**: a regular core (`L ∩ ∅`, `L ∩ {ε}` when `ε ∈ L`) proves nothing.

## 8. Never use the converse

- **Solves**: options of the form “this string pumps, hence regular / CFL”.
- **Why**: the lemmas are implications one way.
- **Example**: exhibiting a pumping length of a language you already know is regular is consistent with the lemma; it is not a regularity proof.
- **Limitation**: none — this prohibition is absolute in GATE.

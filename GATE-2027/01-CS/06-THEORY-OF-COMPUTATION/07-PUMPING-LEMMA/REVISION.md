# Pumping Lemma — Revision

Last-minute sheet. Every line is explained in `NOTES.md`.

## Regular lemma (quantifiers)

If `L` is regular, **∃** `p ≥ 1` such that **∀** `s ∈ L` with `|s| ≥ p`, **∃** `s = xyz` with

- `|xy| ≤ p`
- `|y| ≥ 1`
- `xy^k z ∈ L` for **every** `k ≥ 0`

Converse is false. Pumping never proves regularity.

## Why the bounds

Prefix of length `p` on a `p`-state DFA visits `p+1` states. A repeated state gives a nonempty cycle `y` inside the first `p` letters. Empty `y` would not change the string.

## Non-regularity proof

Adversary picks `p`. You pick one long `s`. You must kill **every** split with `|xy| ≤ p`, `|y| ≥ 1`. Usually `s` begins with `p` letters of one block, so every legal `y` sits in that block. Pump `k = 0` or `k = 2`.

## Pumping length

- If `p` works, every `q > p` works.
- Any DFA’s number of states is a pumping length.
- Min-DFA size is a pumping length, **not** always the smallest. `(aa+bb)*` has smallest `p = 2` and a 4-state min DFA.
- `p` fails as soon as one long word has no good split.

2019-shape: `L = { a^{2+3k} } ∪ { b^{10+12k} }`. Options `3, 5, 9` fail on `b^{10}` (cannot delete 1–9 `b`s and stay in `L`). A large multiple such as `24` exempts `b^{10}` and `b^{22}` and can pump 3 `a`s / 12 `b`s. Official key: verify on the PDF.

## CFL lemma

∃ `p` ∀ long `s` ∃ `s = uvwxy` with `|vwx| ≤ p`, `|vx| ≥ 1`, and `u v^k w x^k y ∈ L` for all `k ≥ 0`. Pump `v` and `x` together. Not `|uv| ≤ p`.

## `{a^n b^n c^n}`

Window length ≤ `p` cannot cover `a`…`c` because `p` letters `b` sit between them. Pumping changes at least one count and leaves at least one count equal to `p`. Not CFL.

## Classification

| Language | Regular? | CFL? | Tool |
|---|---|---|---|
| `{a^n b^n}` | no | yes | regular pumping / MN; grammar `S → aSb \| ε` |
| `{a^n b^{n+1}}` | no | yes | same |
| `{a^n b^{2n}}` | no | yes | `S → aSbb \| ε` |
| `{a^n b^n c^n}` | no | no | CFL pumping |
| `{a^{n^2}}`, `{a^{n!}}` | no | — | length gap after pumping |

## Invalid

One split only · string shorter than `p` · `y` outside the first `p` letters · converse · “not CFL” from regular pumping · unique `p` = min-DFA size.

## Intersect first

`L` not regular if `L ∩ R` is not, for regular `R ≠ ∅` chosen to expose `{a^n b^n}` or a copy. Same for CFL, because CFL ∩ regular = CFL.

# Pumping Lemma — Formulas, Equivalences and Rules

TOC has few numerical formulas. This sheet lists the lemma statements, pumping-length facts, and the regular-language closure table used before pumping.

## 1. Regular pumping lemma

| Piece | Statement | Condition | Limitation |
|---|---|---|---|
| hypothesis | `L` regular | | converse is false |
| constant | ∃ pumping length `p ≥ 1` | `L` regular | `p` is not unique |
| string | ∀ `s ∈ L` with `|s| ≥ p` | | not for `|s| < p` |
| split | ∃ `s = xyz` with `|xy| ≤ p`, `|y| ≥ 1` | | you do not choose the split when proving non-regularity |
| pump | `xy^k z ∈ L` for every `k ≥ 0` | the split above | `k = 0` is allowed |

Origin of the bounds: a DFA with `p` states, prefix of length `p`, pigeonhole, nonempty cycle.

## 2. Pumping-length facts

| Fact | When | Example | Limitation |
|---|---|---|---|
| `p` works ⇒ every `q > p` works | always | `(aa+bb)*`: 2 works, so 3 and 4 work | a *smaller* integer may fail |
| #states of some DFA is a pumping length | `L` regular | | not always the smallest |
| min-DFA size is a pumping length | `L` regular | `(aa+bb)*` min DFA has 4 states | smallest `p` can be 2 |
| `p` fails if one long word has no good split | definition | `b^{10}` in `{a^{2+3k}} ∪ {b^{10+12k}}` kills `p ∈ {3, 5, 9}` | |

## 3. Context-free pumping lemma

| Piece | Statement | Condition | Limitation |
|---|---|---|---|
| hypothesis | `L` context-free | | converse is false |
| split | `s = uvwxy` | `|s| ≥ p` | |
| window | `|vwx| ≤ p` | | **not** `|uv| ≤ p` |
| nonempty pump | `|vx| ≥ 1` | `v` or `x` may be `ε` | not both empty |
| pump | `u v^k w x^k y ∈ L` for all `k ≥ 0` | | `v` and `x` move together |

On `s = a^p b^p c^p`, `|vwx| ≤ p` implies `vwx` cannot contain both an `a` and a `c` (they are `p` letters apart).

## 4. Worked length arithmetic

| Language | `s` | Legal `y` / `vx` | Contradiction |
|---|---|---|---|
| `{a^n b^n}` | `a^p b^p` | `y = a^t`, `1 ≤ t ≤ p` | `k = 0` breaks equality |
| `{a^n b^{n+1}}` | `a^p b^{p+1}` | `y = a^t` | `k = 0` |
| `{a^n b^{2n}}` | `a^p b^{2p}` | `y = a^t` | `k = 0`; still CFL |
| `{a^{n^2}}` | `a^{p^2}` | `y = a^t`, `1 ≤ t ≤ p` | `p^2 + t` sits between squares |
| `{a^{n!}}` | `a^{n!}`, `n ≥ max(2, p)` | `y = a^t` | `n! < n!+t < (n+1)!` |
| `{a^n b^n c^n}` | `a^p b^p c^p` | `vwx` in `a*b*` or `b*c*` | some count changes, some stays `p` |

## 5. Closure table for regular languages (used before pumping)

| Operation | Closed? | Use with pumping |
|---|---|---|
| union, concat, star | yes | a regular slice of a union can be pumped |
| complement | yes | `L` not regular ⇔ `L̄` not regular |
| intersection | yes | if `L ∩ R` is not regular and `R` is, then `L` is not |
| reverse, homomorphism, inverse hom, prefix, suffix | yes | simplify, then pump |
| infinite union, subset, `{ww \| w ∈ L}` | no | do not claim these stay regular |

CFL ∩ regular = CFL. Intersect first, then apply CFL pumping.

Limitation: `L ∩ ∅ = ∅` is regular for every `L`; a useless slice proves nothing.

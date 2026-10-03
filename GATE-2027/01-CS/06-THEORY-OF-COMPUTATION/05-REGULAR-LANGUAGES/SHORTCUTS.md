# Regular Languages — Shortcuts

Each shortcut below is a valid rule, not a guess. The limitation line says exactly where it stops working.

## 1. Finite ⇒ regular

- **Solves**: any language presented as a finite list, or “all strings of length ≤ k”.
- **When**: the set is finite, even if it sits inside a non-regular language.
- **Why**: a trie DFA plus a rejecting sink.
- **Example**: every finite subset of `{a^n b^n}` is regular.
- **Limitation**: an *infinite* subset of a regular language need not be regular.

## 2. Independent exponents ⇒ regular; equal/crossed ⇒ not

- **Solves**: `{ a^n b^m \| … }` classification.
- **When**: the condition on `(n, m)` is a finite-memory predicate (independent, or modular) versus an unbounded equality.
- **Why**: `a*b*` is regular; a DFA cannot compare two unbounded counters.
- **Example**: `a*b*` and `#a ≡ 2 (mod 7)` are regular; `{a^n b^n}`, `{a^n b^{2n}}`, `{a^n b^m \| n ≠ m}` are not.
- **Limitation**: `{a^n b^{2n}}` is still context-free. “Not regular” is not “not CFL”. Modular *and* equal (`#_a ≡ 2 (mod 7)` and `#_a = #_b`) stays non-regular.

## 3. Do not cancel a regular operand

- **Solves**: “`L ∪ R` / `L ∩ R` is regular, `R` is regular, hence `L` is?”
- **Rule**: union (or a too-large intersection) with a regular language does **not** force `L` regular. Contrapositive of intersection: if `L ∩ R` is *not* regular and `R` is, then `L` is not.
- **Example**: `{a, b}* ∪ {a^n b^n} = {a, b}*`. If `L2 = ∅`, then `L1 ∩ L2` is regular for every `L1`.
- **Limitation**: if `L ∩ R` *fails* to be regular, you *may* conclude `L` is not regular.

## 4. Complement flips regularity both ways

- **Solves**: “`L` is not regular; what about `L̄`?”
- **Why**: regular languages are closed under complement, so `L` regular ⇔ `L̄` regular.
- **Example**: `L3` not regular ⇒ `L̄3` not regular. `L̄1 ∪ L̄2` is regular whenever `L1, L2` are.
- **Limitation**: CFLs are not closed under complement; do not use this one level up. Also `L1 ∩ L̄2 = ∅` is `L1 ⊆ L2`, not `L1 = L2`.

## 5. Unary `α` collapses; mixed `α` copies

- **Solves**: `{ αβα \| α ∈ Γ, β nonempty }` for `Γ = {a}+` versus `Γ = {a, b}+`.
- **Why**: if `α` must be `a^k`, the choice `k = 1` is always legal as soon as the string starts and ends with `a` and has a nonempty middle.
- **Example**: `{ αβα \| α ∈ {a}+, β ∈ {a, b}+ } = a(a+b)+a`.
- **Limitation**: if `α` may contain both letters, `|α| = 1` only covers first-symbol = last-symbol. The rest is a copy language; intersect with `ab*ab*` to expose `{ab^i ab^j \| i > j}`.

## 6. Concatenation is not a copy

- **Solves**: `L · L`, `L · L^R`, `{a^n}{b^n}` versus `{ww}`, `{ww^R}`, `{a^n b^n}`.
- **Why**: concatenation picks *two* (possibly different) members.
- **Example**: `{a^n} · {b^n} = a*b*`. If `L` is regular then `L · L^R` is regular, but `{ ww^R \| w ∈ L }` need not be.
- **Limitation**: if `L` is finite then `{ww \| w ∈ L}` is finite, hence regular. The failure needs an infinite `L` with enough variety.

## 7. Intersect with `a*b*` (or a similar regular slice) before classifying

- **Solves**: messy languages that mix a non-regular core with extra junk.
- **Why**: regular ∩ regular = regular, so a non-regular slice proves the original was not regular.
- **Example**: `{a, b}* ∩ { a^m b^n c^{m−n} \| m ≥ n }` = `{a^m b^m}`. `{ ww \| w ∈ {a, b}* } ∩ a*ba*b` = `{ a^n b a^n b }`.
- **Limitation**: a *regular* slice proves nothing: every language intersects `∅` in a regular set.

## 8. Myhill–Nerode instead of pumping when prefixes are obvious

- **Solves**: “show not regular” in one line.
- **When**: the candidate prefixes are `a^i`, or `a^i b`, or `(ab)^i`.
- **Why**: each pair needs its own DFA state.
- **Example**: for `{a^n b^{n+1}}`, `a^i` is distinguished from `a^j` by `b^{i+1}`.
- **Limitation**: MN also *proves* regularity when the index is finite. Pumping never does. For CFL-ness, MN is the wrong theorem.

# Regular Languages — Revision

Last-minute sheet. Every line is explained in `NOTES.md`.

## Kleene equivalence

Regular ⇔ RE ⇔ DFA ⇔ NFA ⇔ right-linear grammar ⇔ left-linear grammar ⇔ finitely many Myhill–Nerode classes.

Pumping is **not** on this list.

## Closure (two regular languages)

Yes: union, concat, star, complement (complete DFA, flip accepts), intersection (product), difference, reverse, homomorphism, inverse homomorphism, prefix, suffix, quotient.

No: infinite union, infinite intersection, subset, `{ww \| w ∈ L}`, `{ww^R \| w ∈ L}`.

## Always / not always

- Finite ⇒ regular. Finite subset of a non-regular set ⇒ regular.
- Subset of a regular set ⇏ regular.
- `L` not regular ⇒ `L̄` not regular.
- `L ∪ R` regular and `R` regular ⇏ `L` regular.
- `L ∩ R` not regular and `R` regular ⇒ `L` not regular.
- `L*` regular ⇏ `L` regular.
- Every regular language is CFL; not conversely.

## Counts

| Form | Regular? |
|---|---|
| independent exponents `a^n b^m` | yes, `a*b*` |
| equal / doubled `a^n b^n`, `a^n b^{2n}` | no (`a^n b^{2n}` is CFL) |
| `n ≠ m` inside `a*b*` | no (`a*b*` minus that is `{a^n b^n}`) |
| `#a ≡ r (mod p)` (and `#b ≡ s (mod q)`) | yes, product DFA |
| `#a = #b`, even with a modular constraint on `#a` | no |
| `{xcy \| x, y ∈ {a, b}*}` | yes |

## Copy languages

- `αβα` with `α ∈ {a}+`: shortest `α = a` always works → `a(a+b)+a`, regular.
- `αβα` with mixed `α ∈ {a, b}+`: genuine copy, not regular. Intersect with `ab*ab*` to get `{ab^i ab^j \| i > j}`.

## Concatenation vs copy

`L · L` and `L · L^R` regular if `L` is. `{ww \| w ∈ L}` and `{ww^R \| w ∈ L}` need not be. `{a^n} · {b^n} = a*b* ≠ {a^n b^n}`.

## Myhill–Nerode

`x ≡_L y` iff every continuation treats them the same. Finite index ⇔ regular. Index = min-DFA size. Infinitely many pairwise distinguishable prefixes ⇒ not regular.

## Regular grammars

Right-linear *or* left-linear: regular. Mixing both sides: can generate `{a^n b^n}`. Left-recursive ⇒ not LL(1). Every regular *set* has an LR(1) grammar.

## High-value PYQ concepts

- Intersection regular + one factor regular does not regularise the other factor; the regular factor is CFL.
- Complement of non-regular is non-regular; `L1 ∩ L̄2 = ∅` is inclusion, not equality.
- Infinite union of regular / finite sets need not be regular.
- Prefix and suffix of a regular language are regular; `{ww^R \| w ∈ L}` is not always.

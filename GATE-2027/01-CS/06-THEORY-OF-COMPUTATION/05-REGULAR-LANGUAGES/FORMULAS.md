# Regular Languages — Formulas, Equivalences and Rules

TOC has few numerical formulas. This sheet lists the equivalences and constructions you apply, each with its condition, a small example and its limitation.

## 1. Kleene equivalence

| Presentation | Condition | Example | Limitation |
|---|---|---|---|
| `L = L(r)` for an RE `r` | always equivalent to the others | `a*b*` | RE reading errors are in folder 01 |
| accepted by a DFA / NFA | always | parity DFA | min-DFA *size* is folder 02 |
| right-linear or left-linear grammar | one orientation throughout | `S → aS \| b` | mixing left and right can leave the family |
| finitely many MN classes | iff regular | even `#a`: 2 classes | infinite index proves non-regularity only |

Limitation of the table: the pumping lemma is a *necessary* condition, not an equivalent presentation.

## 2. Closure constructions

| Operation | Construction | Condition | Limitation |
|---|---|---|---|
| `L ∪ M` | NFA union, or product accept-either | `L, M` regular | not for an infinite family of languages |
| `L ∩ M` | product, accept-both | `L, M` regular | CFLs are not closed under ∩ |
| `Σ* − L` | complete DFA, swap accepts | `L` regular | swapping accepts of an NFA is wrong |
| `L^R` | reverse NFA edges; new start from old accepts | `L` regular | `(a*b*)^R = b*a*`, not `{b^n a^n}` |
| `h(L)` | replace each `a`-edge by a path for `h(a)` | `L` regular | a regular image does not imply a regular source |
| `h^{-1}(L)` | `p --a--> q` iff `h(a)` takes `p` to `q` in a DFA for `L` | `L` regular | |
| `Prefix(L)` | accept every DFA state that can reach an old accept | `L` regular | |
| `Suffix(L)` | reverse, prefix, reverse | `L` regular | |
| `L / a` | `{ x \| xa ∈ L }`; retarget accepts | `L` regular | also works for quotient by a regular language |

## 3. Non-closure, with the exact counter-example

| Claim | Counter-example | What the claim confused |
|---|---|---|
| closed under infinite union | `⋃_n {a^n b^n} = {a^n b^n}` | finite union *is* closed |
| closed under subset | `{a^n b^n} ⊂ {a, b}*` | finite subsets *are* regular |
| `L ∪ M` regular ⇒ both regular | `M = {a, b}*`, `L = {a^n b^n}` | cannot cancel a regular summand |
| `L*` regular ⇒ `L` regular | `{a^n b^n \| n ≥ 1} ∪ {a, b}` | star can fill `Σ*` |
| `{ww \| w ∈ L}` regular if `L` is | `L = a*b` | that is not `L · L` |
| `{ww^R \| w ∈ L}` regular if `L` is | `L = {a, b}*` | palindromes |

## 4. Myhill–Nerode

| Rule | When it applies | Example | Limitation |
|---|---|---|---|
| `x ≡_L y` iff `∀z (xz ∈ L ⇔ yz ∈ L)` | always | | |
| `L` regular ⇔ finite index | always | | the classes must be *pairwise* distinguishable |
| index = states of min complete DFA | `L` regular | | unreachable or equivalent extra states do not add classes |
| `a^i ≇ a^j` via `z = b^i` | `{a^n b^n}` and similar | also `{a^n b^{n+1}}`, `{a^n b^{2n}}` | need `|z|` to match *that* `i` |

## 5. Finite and complement

| Rule | Condition | Example | Limitation |
|---|---|---|---|
| finite ⇒ regular | always | `{ w \| \|w\| ≤ 3 }` | infinite regular languages exist too |
| finite subset of a non-regular set is regular | always | `{ab, aabb} ⊂ {a^n b^n}` | infinite subsets need not be |
| `L` regular ⇔ `L̄` regular | always | | CFLs are not closed under complement |
| `L` not regular ⇒ `L̄` not regular | always | | |

## 6. Count languages

| Language | Regular? | Witness |
|---|---|---|
| `{ a^n b^m \| n, m ≥ 0 }` | yes | `a*b*` |
| `{ a^n b^m c^k \| n, m, k ≥ 0 }` | yes | `a*b*c*` |
| `{ a^n b^n \| n ≥ 0 }` | no | MN on `a^i` |
| `{ a^n b^{2n} \| n ≥ 0 }` | no (CFL yes) | `S → aSbb \| ε` |
| `{ a^n b^m \| n ≠ m }` | no | `a*b* −` this `= {a^n b^n}` |
| `{ a^n b^m \| n = 2m }` | no | MN / pumping |
| `{ xcy \| x, y ∈ {a, b}* }` | yes | `(a+b)*c(a+b)*` |
| `#_a ≡ r (mod p)` and `#_b ≡ s (mod q)` | yes | `p × q` product |
| `#_a ≡ r (mod p)` and `#_a = #_b` | no | `{ a^{pk+r} b^{pk+r} }` |

## 7. Copy / collapse

| Language | Equals | Regular? |
|---|---|---|
| `{ αβα \| α ∈ {a}+, β ∈ {a, b}+ }` | `a(a+b)+a` | yes: shortest `α = a` always works |
| `{ αβα \| α ∈ {a, b}+, β ∈ {a, b}+ }` | genuine binary copy | no: intersect `ab*ab*` |

Limitation: the collapse needs a *unary* `α`. It fails as soon as `α` can contain both letters.

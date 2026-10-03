# Regular Expressions — Formulas, Equivalences and Rules

TOC has few numerical formulas. This sheet lists the equivalences and construction rules you apply, each with its condition, a small example and its limitation.

## 1. Language algebra

| Rule | When it applies | Example | Limitation |
|---|---|---|---|
| `∅L = L∅ = ∅` | always | `∅ · {a}* = ∅` | do not confuse with `{ε}L = L` |
| `{ε}L = L{ε} = L` | always | `{ε}{ab} = {ab}` | |
| `∅* = {ε}` | always | `∅* ∪ ∅ = {ε}` | the star is never empty |
| `L+ = L*` | iff `ε ∈ L` | `{ε, a}+ = a*` | `{a}+ = a+ ≠ a*` |
| `L^k ⊆ L^{k+1}` | when `ε ∈ L` | `L = {ε, a}` | if `ε ∉ L` the powers need not be nested |
| `(LM)^R = M^R L^R` | always | `({ab}{c})^R = {cba}` | order reverses |

## 2. RE identities

| Identity | Condition | Example check | Limitation |
|---|---|---|---|
| `(r*)* = r*` | always | `(a*)* = a*` | |
| `r*r* = r*` | always | | |
| `(ε + r)* = r*` | always | `(ε + a)* = a*` | |
| `rr* = r*r = r+` | always | | `r+ = r*` only if `ε ∈ L(r)` |
| `(r + s)* = (r*s*)* = (r* + s*)*` | always | `(a+b)* = (a*b*)*` | not equal to `r* + s*` or `r*s*` |
| `r(sr)* = (rs)*r` | always | `a(ba)* = (ab)*a` | |
| `r(s + t) = rs + rt` | always | | concatenation does **not** distribute over `*`: `(rs)* ≠ r*s*` |

## 3. Arden's theorem

| Form | Solution | Condition | Example |
|---|---|---|---|
| `X = Q + XP` | `X = QP*` | `ε ∉ L(P)` for uniqueness | `X = b + Xa ⇒ X = ba*` |
| `X = Q + PX` | `X = P*Q` | `ε ∉ L(P)` | `X = b + aX ⇒ X = a*b` |

Limitation: if `ε ∈ L(P)`, `QP*` is still *a* solution but not the only one; the method can then give a wrong "unique" answer.

## 4. State elimination rule

Removing state `q` with self-loop `S`, incoming `p --R1--> q`, outgoing `q --R2--> t`:

`new(p → t) = old(p → t) + R1 S* R2`

- Apply for **every** in/out pair, including `p = t` (that creates or extends a self-loop on `p`).
- If `q` has no self-loop, use `R1 R2`.
- Limitation: the final RE depends on the elimination order in form, never in language.

## 5. Thompson construction sizes

Each symbol occurrence contributes 2 states; each `+` and each `*` adds 2 states; concatenation adds none. The ε-NFA for `r` therefore has at most `2|r|` states, where `|r|` counts symbols and operators. Use only to estimate; GATE asks for languages, not exact sizes.

## 6. Counting rules

| Count | Formula | Condition |
|---|---|---|
| strings of length `n` over `k` symbols | `k^n` | |
| strings of length `≤ n` | `(k^{n+1} − 1)/(k − 1)` | `k ≥ 2` |
| binary strings of length `n` with no `00` | `F(n + 2)` with `F(1) = F(2) = 1` | `1, 2, 3, 5, 8, 13, …` for `n = 0, 1, 2, …` |
| strings over `{a,b}` of length `n` with no `ab` | `n + 1` | they are `b^i a^{n−i}` |
| `|A ∪ B|` at a fixed length | `|A| + |B| − |A ∩ B|` | count the overlap explicitly |
| strings of length `n` in an unambiguous star `(p1 + … + pm)*` | `t(n) = Σ_i t(n − |p_i|)`, `t(0) = 1` | only if every string has one parse (prefix-free pieces suffice) |

## 7. Standard equivalences used in options

| Description | RE | Note |
|---|---|---|
| at least one `0` and one `1` | `(0+1)*(01+10)(0+1)*` | adjacency argument |
| no `00` | `(1+01)*(ε+0)` = `(ε+0)(1+10)*` | |
| even number of `a` over `{a,b}` | `(b + ab*a)*` = `b*(ab*ab*)*` | `(b*ab*a)*` is wrong: it cannot end in `b` unless empty |
| binary multiple of 3 | `(0+1(01*0)*1)*` | includes `ε` |

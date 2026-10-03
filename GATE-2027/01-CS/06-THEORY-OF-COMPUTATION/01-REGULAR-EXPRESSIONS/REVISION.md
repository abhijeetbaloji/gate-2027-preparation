# Regular Expressions — Revision

Last-minute sheet. Every line is explained in `NOTES.md`.

## Definitions

- Alphabet: finite non-empty set. String: finite sequence. `ε`: empty string, `|ε| = 0`.
- Language: any subset of `Σ*`. `Σ+ = Σ* − {ε}`.
- `L^0 = {ε}`, `L* = ∪_{k≥0} L^k`, `L+ = LL*`. `L+ = L*` iff `ε ∈ L`.
- RE grammar: `∅ | ε | a | r+s | rs | r* | (r)`. Precedence: `*` > concatenation > `+`.

## ∅ and ε

| | Value |
|---|---|
| `∅ · L` | `∅` |
| `{ε} · L` | `L` |
| `∅*` | `{ε}` |
| `{ε}*` | `{ε}` |
| `∅ + L` | `L` |

## Identities that hold

`(r*)* = r*` · `r*r* = r*` · `(ε + r)* = r*` · `rr* = r*r = r+` · `r* = ε + rr*` · `(r+s)* = (r*s*)* = (r*+s*)* = (r*s)*r*` · `r(sr)* = (rs)*r`

## Identities that fail

`(r+s)* ≠ r*+s*` · `(rs)* ≠ r*s*` · `r*r ≠ r*` (differs on `ε`) · `(r+s)* ≠ r*s*`

## Arden (needs `ε ∉ L(P)`)

- `X = Q + XP ⇒ X = QP*` (state "reaching" equations)
- `X = Q + PX ⇒ X = P*Q` (state "accepted-from" equations)

## Conversions

- FA → RE: state elimination; new edge `p → t` is `R1 S* R2` for each in/out pair through the removed state with loop `S`.
- RE → ε-NFA: Thompson; star needs a bypass edge (for `ε`) and a back edge (for repetition).

## Standard REs (binary)

| Language | RE |
|---|---|
| even # of 1s | `(0*10*1)*0*` = `(0 + 10*1)*` |
| odd # of 1s | `0*1(0*10*1)*0*` |
| at least two 0s | `(0+1)*0(0+1)*0(0+1)*` |
| no `00` | `(1 + 01)*(ε + 0)` |
| contains `00` and `11` | `(0+1)*(00(0+1)*11 + 11(0+1)*00)(0+1)*` |
| value ≡ 0 mod 3 | `(0 + 1(01*0)*1)*` |
| value ≡ 1 mod 3 | `(0 + 1(01*0)*1)* 1 (01*0)*` |

## Fast techniques

- Test `ε`, single symbols and the shortest member in every option first.
- "Not containing `ab`" over `{a, b}` = `b*a*`.
- Count strings with complement, inclusion–exclusion, or DFA path tables; never count RE parses of an ambiguous RE.
- Shortest string not in `r`: enumerate by length; use the forced structure of `r`.

## High-value PYQ concepts

- English description → RE (odd 1s, both `00` and `11`, at least two 0s, divisible by 3).
- Automaton / token definition → RE or ε-NFA.
- Counting strings of length `≤ n` in or outside a union of REs.
- `∅` / `{ε}` algebra.
- Powers `L^k` and when they stabilise (check whether `ε ∈ L`).

# Finite Automata — Revision

Last-minute sheet. Every line is explained in `NOTES.md`.

## Definitions

- DFA: `δ : Q × Σ → Q` **total**. Unique run of length `|w| + 1`. Accept iff last state `∈ F`. `ε` accepted iff `q0 ∈ F`.
- NFA: `δ : Q × Σ → 2^Q`. Accept iff **some** run reads all of `w` and ends in `F`. A dead run does not kill other runs.
- `ε`-NFA: `ε`-edges consume no input. `E(q)` = `{q}` plus states on `ε`-paths. `δ̂(q, xa) = E(move on `a` from `δ̂(q, x))`.

## Conversions

- NFA / `ε`-NFA → DFA: subset construction, **reachable** subsets only. `∅` is a rejecting sink **if reached**.
- `|Q'| ≤ 2^n`. Not automatically minimal. `k ≥ n` is not required. `k = 1` is possible (`∅` or `Σ*`). `k > 2^n` is impossible.
- Product of complete DFAs: `≤ |Q1| · |Q2|` states. Accept `F1 × F2` for intersection.
- Complement: flip `F` of a **complete DFA**. Never flip an NFA.
- DFA → RE: short-string filter first; Arden / elimination only if needed ([`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS)).

## Myhill–Nerode

`x ∼_L y` iff `∀z (xz ∈ L ⇔ yz ∈ L)`. Number of classes = number of states of the min complete DFA. To prove minimality, give one distinguishable representative per state.

## Minimization

Delete unreachable. Partition accept vs reject. Split a block when a symbol sends its members into different blocks. Stable partition = min DFA.

## State-count table (complete DFA)

| Language | States |
|---|---|
| ends with `w`, `\|w\| = m` | `m + 1` |
| contains `w`, `\|w\| = m` | `m + 1` |
| exactly `k` ones | `k + 2` (need sink) |
| no `k` consecutive `1`s | `k + 1` (need sink) — `k = 3` → **4** |
| `#a ≡ r (mod m)` | `m` |
| two independent moduli `m, n` | `mn` |
| `#a` even but not div by 3 | **6** (`≡ 2 or 4 (mod 6)`) |
| `Σ+` | **2** |
| `k`-th from the end | `2^k` |
| `k`-th from the start | `k + 2` |
| `w1 a w2`, `\|w1\| = p`, `\|w2\| ≥ q` | `p + q + 3` |
| unary `{a^{tn} : t ≥ 1}` | `n + 1` |
| product of symbols `≡ t (mod p)`, `p` prime, `0` unreachable | `p − 1` |
| group DFA, letters = `G`, accept identity | `\|G\|` |
| NFA: all substrings of `w`, `\|w\| = n` | `n + 1` |

## Distinguishability micro-proofs

- Ends with `01`: `ε`, `0`, `01`. `z = ε` splits `01`; `z = 1` splits `ε` from `0`.
- Exactly two `1`s: `ε, 1, 11, 111`.
- No three consecutive `1`s: `ε, 1, 11, 111`.

## High-value PYQ concepts

- Min DFA size from a description (moduli, consecutive run, `Σ+`, group, product of digits, `w1 a w2`).
- NFA → DFA bounds (`≤ 2^n`, not `≥ n`, 1 possible, `> 2^n` impossible).
- Identify a drawn DFA / which states are distinguishable (trace; figures live in the paper PDF).
- DFA → RE by killing options on short strings.
- `ε`-NFA `δ̂(q, w)`: close, consume, close.
- NFA complement ≠ flip `F`. All-accepting NFA ≠ `Σ*` unless the NFA is complete.

## Fast checks in the hall

1. Is `δ` total? If you used a partial machine, add a dead state before counting.
2. Test `ε`.
3. One illegal prefix (too many `1`s, a `111`, a failed start) → dead state, distinguishable from the start.
4. Independent letter-counts → multiply. Same letter twice → `lcm` / one counter.
5. From-the-end vs from-the-start: exponential vs linear.

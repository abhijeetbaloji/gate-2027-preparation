# Finite Automata — Formulas, Equivalences and Rules

TOC has few numerical formulas. This sheet lists the constructions and state-count rules you apply, each with its condition, a small example and its limitation. Theory: [NOTES.md](NOTES.md).

## 1. Machine equivalences

| Rule | When it applies | Example | Limitation |
|---|---|---|---|
| DFA language = NFA language = `ε`-NFA language = RE language | always | any RE has a DFA | state counts need not match |
| Subset construction | any NFA / `ε`-NFA with `n` states | Example 2 in NOTES: 2 NFA states → 2 reachable DFA states | the DFA need not be minimal; `\|Q'\| ≤ 2^n` |
| `ε`-closure `E(q)` | `ε`-NFA | `E(q)` always contains `q` | forgetting `q` itself is wrong even if `q` has no `ε`-loop |
| Complete a partial DFA | add a rejecting sink for missing arcs | “exactly two `1`s” | the sink counts in the *complete* minimum |
| Complement | complete DFA: swap `F` with `Q − F` | `Σ+` ↔ `{ε}` | **not** valid on an NFA |
| Product `\|Q1\| · \|Q2\|` | two complete DFAs, same `Σ` | even `#0` and `#1 ≡ 0 (mod 5)` → `2 · 5 = 10` | only reachable pairs; minimization may shrink; conditions must be independent |

## 2. Extended transition

| Machine | `δ̂(q, ε)` | `δ̂(q, xa)` |
|---|---|---|
| DFA | `q` | `δ(δ̂(q, x), a)` |
| NFA | `{q}` | `⋃_{p ∈ δ̂(q, x)} δ(p, a)` |
| `ε`-NFA | `E(q)` | `E( ⋃_{p ∈ δ̂(q, x)} δ(p, a) )` |

Acceptance: DFA iff `δ̂(q0, w) ∈ F`; NFA / `ε`-NFA iff `δ̂(q0, w) ∩ F ≠ ∅`.

## 3. NFA → DFA size

Let `N` have `n` states and let `k` be the number of states of a **minimal complete** DFA for `L(N)`.

| Claim | True? | Why |
|---|---|---|
| `k ≤ 2^n` | always | powerset, then drop unreachable / merge equivalent |
| `k ≥ n` | **no** | NFA for `Σ*` with `n > 1` states still has `k = 1` |
| `k ≥ 2^n` | **no** | most languages sit strictly below the powerset |
| `k = 1` is possible | yes | `L = ∅` or `L = Σ*` |
| `k = 2^n` is possible | yes | `k`-th bit from the end, `n = k` in the usual NFA |
| `k = 2^n + 1` | **impossible** | exceeds the powerset |
| some DFA with `≤ 2^n` states exists | always | subset construction |
| every DFA for `L` has `> 2^n` states | **false** | contradicts the previous row |
| an NFA with `< n` states may exist | yes | the given NFA need not be NFA-minimal |

For `n = 6`: always `1 ≤ k ≤ 64`. In particular 32 is possible (fifth-bit-from-the-end language: 6-state NFA, 32-state min DFA); 65 and 128 are not possible. Not every integer in `1 … 64` need arise for some `n`-state NFA; every integer *outside* that interval is forbidden.

## 4. Myhill–Nerode

`x ∼_L y` iff for all `z`, `xz ∈ L ⇔ yz ∈ L`.

| Rule | Condition | Example | Limitation |
|---|---|---|---|
| `#` classes = `#` states of the min complete DFA | `L` regular | ends with `01`: 3 classes (`ε`, `0`, `01`) | infinite classes ⇔ not regular (folder 05) |
| one distinguishable string per state ⇒ minimality | the strings land in different states | `ε, 1, 11, 111` for “exactly two `1`s” | you must actually exhibit a `z` for every pair |
| unreachable DFA states are not classes of `L` | always | delete, do not count | a reachable dead sink **is** a class |

## 5. State-count recipes (complete DFA)

| Language | Count | Condition | Example | Limitation |
|---|---|---|---|---|
| ends with fixed `w`, `\|w\| = m` | `m + 1` | complete | ends with `01` → 3 | overlaps change arcs, not the prefix count |
| contains fixed `w`, `\|w\| = m` | `m + 1` | complete; accepting sink | contains `001` → 4 | same |
| starts with `w` | typically `m + 2` | dead sink on first mismatch | starts with `1` → 3 | if mismatch is impossible (unary `a*` starts with `a`), no extra dead |
| exactly `k` ones | `k + 2` | complete (need `≥ k+1` sink) | exactly two `1`s → 4 | “at least `k`” is `k + 1` |
| `#a ≡ r (mod m)` | `m` | `a` occurs in `Σ` | `#b ≡ 2 (mod 3)` → 3 | all residues reachable |
| `#0 ≡ 0 (mod m)` and `#1 ≡ 0 (mod n)` | `mn` | independent counters, `{0,1}` | `#0` div by 3 and `#1` div by 5 → 15 | do not multiply a single shared counter |
| `#a` even but not div by 3 | 6 | `≡ 2 or 4 (mod 6)` | 2020-style | accept set `{2,4}` still needs all 6 residues |
| no `k` consecutive `1`s | `k + 1` | include the `k`-run sink | no three consecutive `1`s → **4** | not `k + 2` |
| `Σ+` | 2 | reject only `ε` | `(0+1)*(0+1)(0+1)*` | not 1 |
| `{ε}` | 2 | dead sink on any letter | | |
| `∅` or `Σ*` | 1 | | | |
| `k`-th from the **end** is a fixed letter | `2^k` | complete | third from the end → 8 | NFA size is `k + 1`, not the DFA size |
| `k`-th from the **start** is a fixed letter | `k + 2` | yes-sink and no-sink; short strings reject | third symbol is `a` → 5 | |
| `w1 a w2` with `\|w1\| = p`, `\|w2\| ≥ q` | `p + q + 3` | complete | `p = 2, q = 3` → 8 | |
| `{ a^{tn} | t ≥ 1 }`, unary, `n` fixed | `n + 1` | `ε` rejected | `n = 3` → 4 | `t ≥ 0` (include `ε`) is `n` states |
| all substrings of a fixed `w`, **NFA** | `n + 1` | `\|w\| = n`; `ε` included | `w = a^n` proves tightness | DFA can be larger; the question is usually NFA |
| `prod(x) ≡ t (mod p)`, `p` prime, `Σ ⊆ {1,…,p−1}` | `p − 1` | `0` unreachable; `Σ` generates `(ℤ/pℤ)*` | `p = 7`, `Σ = {1,2,3,4}`, `t = 2` → 6 | do not add residue `0` |
| `n(x) = id` in a finite group `G` of letters | `\|G\|` | states = group elements | bijections of `{1,…,5}` → `5! = 120` | composition order changes arcs, not `\|G\|` |

## 6. Product and complement identities for machines

| Construction | Accept set / rule | Limitation |
|---|---|---|
| intersection DFA | `F1 × F2` | complete DFAs |
| union DFA | `(F1 × Q2) ∪ (Q1 × F2)` | |
| DFA complement | swap `F` | must be complete; dead sink of `L` becomes an accepting sink of the complement |
| NFA complement | determinize, complete, then swap | flipping `F` of the NFA is wrong |

## 7. Minimization invariants

- Deleting unreachable states first does not change `L`.
- Initial partition is always accept vs reject.
- The quotient by the stable partition is the unique min complete DFA (up to renaming).
- Subset construction followed by this quotient is a correct NFA → min DFA pipeline.

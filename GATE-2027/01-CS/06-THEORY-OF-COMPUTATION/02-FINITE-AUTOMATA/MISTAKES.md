# Finite Automata — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| NFA accepts only if every run accepts | Acceptance is existential: one successful run is enough |
| A dying NFA run rejects the string | It rejects *that run*. Other runs may still accept |
| `δ` of a DFA may skip a symbol | DFA `δ` is total; missing arcs belong to NFAs (or to incomplete machines that must be completed with a dead state) |
| `ε`-closure of `q` is only the `ε`-successors | `E(q)` always contains `q` |
| `ε` is a tape symbol | An `ε`-edge consumes nothing; `ε` is not in `Σ` |
| Flipping an NFA's accept states gives the complement | Determinize, complete, then flip. Counterexample: NFA for `a+`; complement is `{ε}` |
| All NFA states accepting ⇒ `L = Σ*` | Only if every state has a transition on every symbol. Otherwise strings with no run are rejected |
| Subset construction is already the min DFA | Reachable subsets can still be equivalent |
| `k ≥ n` after an `n`-state NFA | A large NFA can denote `Σ*` or `∅`; `k` can be 1 |
| Min DFA for `Σ+` has 1 state | 1-state complete DFAs are only `∅` and `Σ*`; `Σ+` needs 2 |
| No three consecutive `1`s → 5 states | Trailing-`0` is the start. Four states: `0, 1, 2` trailing plus dead |
| Exactly `k` ones → `k + 1` states | Complete DFA needs the `≥ k+1` sink: `k + 2` |
| `k`-th from the end → `k + 1` DFA states | That is the NFA size. The DFA has `2^k` |
| `k`-th from the start → `2^k` | Linear: `k + 2` (yes-sink and no-sink) |
| Product of digits mod `p` has `p` states | Residue `0` is unreachable if no factor is `0 mod p` |
| Unreachable states change the language if deleted | They do not; they are not Myhill–Nerode classes |
| Two rejecting states are always equivalent | Only if neither can reach an accept state. `c0` and `d` in “exactly two `1`s” are both rejecting and distinguishable |

## 2. Construction / algebra mistakes

- Subset construction: forgetting to take the union over every member of the current subset; dropping `∅` when a missing NFA arc actually reaches it; keeping all `2^n` subsets when the question asks for reachable ones.
- `ε`-NFA `δ̂`: closing only at the start, or consuming `ε` as an input letter. The loop is close → consume one real symbol → close.
- Product: accepting `F1 × Q2` when the operation is intersection; multiplying two moduli of the *same* letter.
- Minimization: skipping the accept/reject split; merging two states because they have the same outgoing *labels* without checking the *target blocks*; counting unreachable states in the minimum.
- Arden / DFA→RE: using `P*Q` on a left-linear equation (see [`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS)).

## 3. State-count mistakes

- Drawing a start state *and* a “trailing-0” state for “no `k` consecutive `1`s”. They are the same class.
- Omitting the dead state, then reporting the size of a *partial* machine.
- Using `m + n` instead of `mn` for two independent letter counts (or the reverse).
- “Even and not divisible by 3” counted as 4 (mod-2 × mod-3 with illegal merges) or as 2 (parity only). Residues `2` and `4` mod 6 are distinguishable by `aa`.
- Group DFA counted as `n` rather than `n!` for bijections of `{1,…,n}`.
- Substring-NFA counted as `n` or `2^n`. For `|w| = n` the tight NFA size is `n + 1`.

## 4. PYQ-derived traps (mapped stems only; figures often missing)

| Year / Q# | Trap pattern |
|---|---|
| 2026 CS1 Q.26 | Treating 65 or 128 as legal for a 6-state NFA (`2^6 = 64`); or rejecting 1 and 32 |
| 2026 CS2 Q.47 | Comparing two drawn DFAs by shape instead of tracing `ε` and short strings (figure required) |
| 2025 CS1 Q.28 | Marking “there exists a DFA with `≤ 2^n` states” as false; or believing every DFA has `> 2^n` states |
| 2025 CS1 Q.50 | Ends-with vs contains vs “even `#b`” vs “avoids `aba`” — one short string kills three options (figure required) |
| 2025 CS2 Q.60 | Adding unreachable residue `0` to the product-mod-7 DFA; or taking `prod(ε) = 0` |
| 2024 CS1 Q.50 | Calling two states equivalent because both reject `ε`; `n0 = n1` need not put `w` in `L(M)` (figure required) |
| 2024 CS2 Q.22, 2023 Q.14, 2022 Q.12 | Picking an RE that agrees on length 1 but fails on a loop (figure required) |
| 2023 Q.63 | Counting five states for “no three consecutive `1`s” |
| 2021 Q.38 | A DFA that *contains* `011` rather than *ends with* `011` (figure required) |
| 2020 Q.51 | Product 2×3 with the wrong accept set, or merging residues `2` and `4` |
| 2019 Q.48 | Counting 5 or 25 instead of `5! = 120` |
| 2018 Q.6 | Choosing `k ≥ n` or `k ≥ 2^n` or `k ≤ n^2` |
| 2017 Q.25 | Forgetting the dead sink when the distinguished position fails, or forgetting to count `|w2|` |
| 2017 Q.39 | `ε`-closure without the seed state; consuming symbols before closing |
| 2016 Q.16 | Answering 1 (`Σ*`) instead of 2 (`Σ+`) |
| 2016 Q.42 | Believing statement I (all NFA states accepting ⇒ `Σ*`); missing `A = ∅` for statement II |
| 2015 Q.45 | Ends with `10` counted as 2, or as “contains `10`” with a wrong sink |
| 2015 Q.32 | Complement of “contains `0011`” counted as `2^4` or as 4 after an illegal merge |
| 2014 Q.36 | Accepting a broken RE that misses alternating strings ending in `1` |
| 2012 Q.12 | Complements `∅` or `a*` for an NFA that accepts `a+` |
| 2012 Q.46 | Filling a last-two-bits table so that `000` does not enter the dead state (figure required) |
| 2011 Q.42 | `k + 1` instead of `n + 1` for `{a^{kn} : k ≥ 1}` |
| 2011 Q.45 | A “minimal” option that still has equivalent states or that changes the language (figure required) |
| 2010 Q.41 | DFA size `2^n`, or NFA size `n`, for all substrings of a word of length `n` |
| 2009 Q.41 | “Ends with `0`” vs “ends with `00`” vs “contains `00`” (figure required) |
| 2007 Q.29 | Adding `3 + 5` or taking `lcm(3, 5)` instead of the product 15 |

## 5. Examination-time mistakes

- Answering a NAT with the size of a partial DFA.
- Tracing an NFA as if a missing arc rejected the whole string.
- Not testing `ε` on a drawn DFA.
- Building all `2^n` subsets when only the reachable ones are asked.
- Inventing a missing figure instead of opening the paper PDF.

## 6. How to check yourself

1. Is `δ` total? Did I include a dead sink if an illegal prefix is reachable?
2. Did I test `ε`, a shortest member, and a just-illegal string?
3. For minimality: do I have one distinguishing `z` per pair of representatives?
4. For NFA bounds: is my number `≤ 2^n`? Did I claim `k ≥ n` without cause?
5. For `ε`-NFA: did `E(q)` include `q`, and did I close after every real symbol?
6. For products: independent letters → multiply; same letter → one modulus / `lcm`.
7. Complement: am I looking at a complete DFA?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |

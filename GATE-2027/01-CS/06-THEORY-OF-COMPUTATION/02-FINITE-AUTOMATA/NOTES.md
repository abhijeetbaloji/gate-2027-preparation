# Finite Automata — Notes

Syllabus line: *Regular expressions and finite automata* (GATE CS 2027, Section 6). This folder owns the machines. Regular expressions live in [`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS); the algebra of the family they both describe lives in [`05-REGULAR-LANGUAGES`](../05-REGULAR-LANGUAGES).

Convention used throughout: unless a question says otherwise, a DFA is **complete** (`δ` is a total function). GATE numerical answers for “minimum number of states in a DFA” are the size of the unique (up to renaming) minimal complete DFA.

## What the PYQs actually test

From the mapped questions (`../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/02-FINITE-AUTOMATA/questions.md`). Figures are often missing from the extract; those stems are listed as *identify / complete-the-figure* jobs, not as invented diagrams. Stored answers are all `VERIFICATION REQUIRED`; none are treated as official keys here.

| Pattern | Seen in |
|---|---|
| Min complete DFA state count from an English / RE / modular description | 2025 CS2 Q.60, 2023 Q.63, 2020 Q.51, 2019 Q.48, 2017 Q.25, 2016 Q.16, 2015 (intersection; ends with `10`; complement of “contains `0011`”), 2011 unary `a^{kn}`, 2007 product of two moduli |
| NFA → DFA size bounds (`k ≤ 2^n`; 1 is possible; `k ≥ n` is not forced) | 2026 CS1 Q.26, 2025 CS1 Q.28, 2018 Q.6 |
| Identify the language of a drawn DFA, or which states are distinguishable | 2025 CS1 Q.50, 2024 CS1 Q.50, 2009 Q.41 |
| DFA → equivalent RE (options; figure required) | 2024 CS2 Q.22, 2023 Q.14, 2022 Q.12, 2014 Q.36 |
| `ε`-NFA extended transition `δ̂(q, w)` | 2017 Q.39 |
| NFA reachable-state set on a given string | 2014 Q.16 |
| Complement of an NFA language (do **not** flip NFA accept states) | 2012 Q.12 |
| Fill missing DFA arcs for a local substring constraint | 2012 Q.46 |
| Minimization of a drawn DFA | 2011 Q.45 |
| NFA for all substrings of a fixed `w` | 2010 Q.41 |
| True/false about NFAs and regularity of `A ∩ B` | 2016 Q.42 |

The common thread is **what a state must remember**, plus the powerset bound. Drawing a machine is the means, not the end.

---

## 1. Intuitive intro

A finite automaton is a machine with a **finite** set of internal configurations (states) and a **one-way** read of the input. After each symbol it is in some state; at the end it says yes or no.

Why “finite” matters: the state is the entire memory. If two prefixes `x` and `y` leave the machine in the same state, then for every continuation `z` the machine will accept `xz` if and only if it accepts `yz`. So a DFA with `n` states can distinguish at most `n` kinds of prefix. That observation is Myhill–Nerode (Section 8), and it is the reason min-DFA questions have unique numerical answers.

Two views you will keep switching between:

- **DFA:** no choice. One run per string. Easy to complement (swap accept / reject) and to intersect (product). Harder to design when the language is “guess where the pattern starts”.
- **NFA:** choice and (optionally) `ε`-moves. A string is accepted if **some** run succeeds. Easy to design; converting to a DFA may explode to `2^n` states.

They accept exactly the same family of languages (the regular languages). The blow-up is in the number of states, not in what can be recognised.

---

## 2. Deterministic finite automaton

A **DFA** is a 5-tuple `M = (Q, Σ, δ, q0, F)` where

- `Q` is a finite nonempty set of states,
- `Σ` is a finite nonempty alphabet,
- `δ : Q × Σ → Q` is a **total** function (exactly one next state for every pair `(state, symbol)`),
- `q0 ∈ Q` is the start state,
- `F ⊆ Q` is the set of accept (final) states.

**Run.** On `w = a1 a2 … an` the unique run is the sequence of `n + 1` states

`q0,  δ(q0, a1),  δ(δ(q0, a1), a2),  …`

**Acceptance.** `M` accepts `w` iff the last state of that run is in `F`. Equivalently `δ̂(q0, w) ∈ F`, where the **extended transition** `δ̂ : Q × Σ* → Q` is

- `δ̂(q, ε) = q`,
- `δ̂(q, xa) = δ(δ̂(q, x), a)` for `x ∈ Σ*`, `a ∈ Σ`.

There is always exactly one run, including on `ε` (the run is just `q0`). So `ε` is accepted iff `q0 ∈ F`.

**Complete vs incomplete.** Some texts allow `δ` to be partial: a missing arc aborts the run and rejects. Completing the machine means adding a **dead (sink) reject state** `d` with `δ(d, a) = d` for every `a`, and sending every missing arc to `d`. The language does not change. The *minimal complete* DFA may therefore have one more state than a partial machine. GATE state-count questions use the complete machine.

**Unreachable states.** A state `q` is unreachable if no `w` has `δ̂(q0, w) = q`. Deleting unreachable states does not change the language (no run from `q0` can visit them). They never survive minimization.

### Worked example 1 — DFA for “ends with `01`”

Over `{0, 1}`, let `L = { w | w ends with 01 }`. The machine remembers the longest suffix of the input that is a prefix of `01`.

| State | Meaning (suffix) | on `0` | on `1` | Accept? |
|---|---|---|---|---|
| `qε` (start) | not `0` and not `01` (empty, or ends in `1`) | `q0` | `qε` | no |
| `q0` | ends in `0` (and not in `01`) | `q0` | `q01` | no |
| `q01` | ends in `01` | `q0` | `qε` | **yes** |

Traces (every transition used at least once):

| `w` | run | accept? |
|---|---|---|
| `ε` | `qε` | no |
| `0` | `qε → q0` | no |
| `1` | `qε → qε` | no |
| `01` | `qε → q0 → q01` | yes |
| `10` | `qε → qε → q0` | no |
| `011` | `qε → q0 → q01 → qε` | no |
| `010` | `qε → q0 → q01 → q0` | no |
| `0101` | `qε → q0 → q01 → q0 → q01` | yes |

Why `q01 --1--> qε` and not a new state: the suffix of `…011` is `1`, which is the same information as `qε`. Why `q01 --0--> q0`: the suffix of `…010` is `0`. Why `q0 --0--> q0`: the suffix of `…00` is still `0`.

**These three states are necessary** (distinguishability, Section 8). The strings `ε`, `0`, `01` are pairwise distinguishable for `L`:

- `01 ∈ L`, while `ε ∉ L` and `0 ∉ L`, so `z = ε` separates `q01` from the other two.
- `ε · 1 = 1 ∉ L` and `0 · 1 = 01 ∈ L`, so `z = 1` separates `qε` from `q0`.

A complete DFA needs at least one state per distinguishable string, so 3 is minimal. This is the template for every “ends with `w`” question: `|w| + 1` states, one per prefix of `w`.

---

## 3. Nondeterministic finite automaton

An **NFA** is a 5-tuple `N = (Q, Σ, δ, q0, F)` where now

`δ : Q × Σ → 2^Q`

(`2^Q` is the powerset of `Q`). From a state on a symbol the machine may have **zero, one, or many** successors. Missing means `δ(q, a) = ∅`: that run **dies**. It does not accept, but other runs on the same string may still accept.

**Extended `δ` (no `ε`-moves).** For `S ⊆ Q`:

- `δ̂(q, ε) = {q}`,
- `δ̂(S, a) = ⋃_{p ∈ S} δ(p, a)`,
- `δ̂(q, xa) = δ̂(δ̂(q, x), a)`.

**Acceptance is existential.** `N` accepts `w` iff `δ̂(q0, w) ∩ F ≠ ∅`: *at least one* computation reads all of `w` and ends in `F`. A rejecting computation on the same `w` is irrelevant. There is no “majority” rule, and uniqueness of the run is not required.

`ε` is accepted iff `q0 ∈ F`. (Without `ε`-moves the only state reachable on `ε` is `q0` itself.)

A DFA is an NFA in which every `δ(q, a)` is a singleton. So every DFA language is an NFA language.

---

## 4. `ε`-NFA and `ε`-closure

An **`ε`-NFA** allows transitions on the empty string: `δ : Q × (Σ ∪ {ε}) → 2^Q`. An `ε`-edge changes state **without consuming an input symbol**. The letter `ε` is not a symbol of `Σ`.

**`ε`-closure.**

- `E(q)` is `{q}` together with every state reachable from `q` by a path of **one or more** `ε`-edges.
- `E(S) = ⋃_{q ∈ S} E(q)`.

The state itself is always in its closure, even if it has no `ε`-loop. Forgetting `q ∈ E(q)` is the standard closure error.

`E` is the reflexive-transitive closure of the `ε`-graph, so if `p ∈ E(q)` and `r ∈ E(p)` then `r ∈ E(q)`. Compute it by DFS/BFS on `ε`-edges only, starting from the set, never deleting the seeds.

**Extended transition of an `ε`-NFA.**

- `δ̂(q, ε) = E(q)`,
- `δ̂(q, xa) = E( ⋃_{p ∈ δ̂(q, x)} δ(p, a) )`.

In words: close, consume one real symbol from every currently occupied state, close again. Never consume `ε` from the input tape; `ε`-edges are taken “for free” before the first symbol and after every symbol.

**Acceptance.** `w` is accepted iff `δ̂(q0, w) ∩ F ≠ ∅`. In particular `ε` is accepted iff `E(q0) ∩ F ≠ ∅` — the start state need not itself be accepting if an `ε`-path reaches an acceptor.

Worked micro-example. States `q0, q1, q2`; `ε`-edges `q0 → q1` and `q1 → q2` only. Then `E(q0) = {q0, q1, q2}`, `E(q1) = {q1, q2}`, `E(q2) = {q2}`. Dropping `q0` from `E(q0)` is wrong; stopping at `{q0, q1}` is wrong.

---

## 5. Subset construction (NFA / `ε`-NFA → DFA)

**Idea.** A DFA state is a *set* of NFA states: “the set of all NFA states I could be in after reading this prefix”.

**For an NFA without `ε`.** DFA `M' = (Q', Σ, δ', q0', F')` with

- `Q' = 2^Q` (or just the reachable part),
- `q0' = {q0}`,
- `δ'(S, a) = ⋃_{p ∈ S} δ(p, a)`,
- `F' = { S ⊆ Q | S ∩ F ≠ ∅ }`.

**For an `ε`-NFA.** Same, except `q0' = E(q0)` and `δ'(S, a) = E( ⋃_{p ∈ S} δ(p, a) )`.

**Reachable subsets only.** There are `2^n` subsets of an `n`-state NFA, but many are never visited from `q0'`. The DFA you actually build is the part reachable from `q0'`. Unreachable subsets, including often the empty set, are discarded.

**The empty set.** `δ'(∅, a) = ∅` for every `a`. `∅` is never accepting (`∅ ∩ F = ∅`). If some reachable subset has no `a`-successor in the NFA, `∅` **is** reached and must be kept as a rejecting sink. If every reachable subset has a nonempty successor on every symbol, `∅` is not a DFA state of the reachable machine.

**The construction is not automatically minimal.** Two reachable subsets can be equivalent (same future). Minimization (Section 9) may merge them. Upper bound: reachable DFA size `≤ 2^n`; after minimization still `≤ 2^n`.

### Worked example 2 — two-state NFA “contains a `1`”

NFA over `{0, 1}`: states `{p, q}`, start `p`, accept `{q}`.

| | `0` | `1` |
|---|---|---|
| `p` | `{p}` | `{p, q}` |
| `q` | `{q}` | `∅` |

From `q`, the symbol `1` has no edge, so a *run that is already in `q`* dies on `1`. The other run can have stayed in `p`.

Subset construction, starting at `{p}`:

| DFA state | on `0` | on `1` | Accept? |
|---|---|---|---|
| `{p}` (start) | `{p}` | `{p, q}` | no |
| `{p, q}` | `{p} ∪ {q} = {p, q}` | `{p, q} ∪ ∅ = {p, q}` | **yes** |

`∅` is not reached. `{q}` is not reached (every time `q` is entered, `p` is still occupied). Exactly **two** reachable DFA states.

Language: `{p}` is “no `1` yet”; the first `1` moves to the accepting sink `{p, q}`. So `L = (0+1)*1(0+1)*` (contains at least one `1`). Check: `ε` stays in `{p}` (reject); `0` stays in `{p}`; `1` and `10` and `11` sit in `{p, q}` (accept). It is **not** “ends with `1`”: `10` is accepted.

### Why NFAs and DFAs have the same language power

1. Every DFA is already an NFA, so every DFA language is an NFA language.
2. Subset construction produces, from any NFA / `ε`-NFA, a DFA with the same language: after reading `w`, the DFA occupies exactly `δ̂_N(q0, w)`, and it accepts iff that set meets `F`.
3. Therefore NFA = `ε`-NFA = DFA = regular languages.

Thompson’s construction ([`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS) §9) turns any RE into an `ε`-NFA, so REs sit in the same class (Kleene).

What is *not* preserved is the number of states. The language “the `k`-th symbol from the end is `1`” has a `(k+1)`-state NFA (guess the position, then verify `k` symbols) and needs `2^k` DFA states (Section 11). So `2^n` is tight infinitely often, but many NFAs collapse far below `2^n`.

**Bound facts that GATE actually asks** (stems of 2026 Q.26, 2025 Q.28, 2018 Q.6):

- If an NFA has `n` states, **some** equivalent DFA has `≤ 2^n` states. Hence a *minimal* equivalent DFA has `k ≤ 2^n` states.
- `k ≥ n` is **not** necessary: a bloated NFA for `Σ*` minimises to 1.
- `k = 1` **is** possible: the minimal complete DFAs with one state are `Σ*` (the unique state accepting) and `∅` (the unique state rejecting). Both are NFA languages.
- `k > 2^n` is **impossible**. For `n = 6`, `2^6 = 64`, so 65 and 128 cannot occur; 32 can; 1 can.
- An equivalent DFA with **fewer** than `n` states may exist, and an equivalent NFA with fewer than `n` states may exist (the given NFA need not be state-minimal even among NFAs).
- “Every DFA for `L` has more than `2^n` states” is false: it contradicts the powerset construction.

---

## 6. Product automaton (intersection, union, difference)

Let `M1 = (Q1, Σ, δ1, s1, F1)` and `M2 = (Q2, Σ, δ2, s2, F2)` be complete DFAs.

The **product** `M1 × M2` has

- states `Q1 × Q2`,
- start `(s1, s2)`,
- `δ((p, q), a) = (δ1(p, a), δ2(q, a))`,
- accept states chosen according to the Boolean operation:

| Operation | Accept `F` |
|---|---|
| `L(M1) ∩ L(M2)` | `F1 × F2` |
| `L(M1) ∪ L(M2)` | `(F1 × Q2) ∪ (Q1 × F2)` |
| `L(M1) − L(M2)` | `F1 × (Q2 − F2)` |
| symmetric difference | the union of the two difference sets |

Only the **reachable** pairs are needed. The product has at most `|Q1| · |Q2|` states; after minimization it may have fewer, never more.

Complement of a complete DFA: keep `δ`, swap `F` with `Q − F`. Do this on a DFA, never on an NFA (Section 18).

### Worked example 3 — even `#a` and even `#b`

Over `{a, b}`, `L = { w | #a(w) even and #b(w) even }`. Independent parities: product of a 2-state “parity of `a`” DFA with a 2-state “parity of `b`” DFA.

States `(p_a, p_b)` with `p_a, p_b ∈ {0, 1}` (0 = even). Start `(0, 0)`, accept `{(0, 0)}`.

| | on `a` | on `b` |
|---|---|---|
| `(0,0)` | `(1,0)` | `(0,1)` |
| `(1,0)` | `(0,0)` | `(1,1)` |
| `(0,1)` | `(1,1)` | `(0,0)` |
| `(1,1)` | `(0,1)` | `(1,0)` |

All four pairs are reachable (`ε, a, b, ab`). They are pairwise distinguishable:

- `(0,0)` is the only state that accepts `ε`.
- From `(1,0)`, the continuation `a` is accepted; from `(0,1)` and from `(1,1)`, `a` is not.
- From `(0,1)`, the continuation `b` is accepted; from `(1,1)`, `b` is not.

Minimal complete DFA: **4** states. No dead state: every pair can still reach `(0,0)`.

**Independent moduli in general.** “`#0 ≡ 0 (mod m)` and `#1 ≡ 0 (mod n)`” is the product of an `m`-state counter with an `n`-state counter, hence **`mn` states**, all reachable over `{0, 1}` (read enough `0`s to set the first track, enough `1`s to set the second). Pairwise distinguishability: from residue `(i, j)` the continuation `0^{m-i} 1^{n-j}` is accepted, and it is accepted from `(i', j')` only if `(i', j') = (i, j)` (when working mod `m` and `n`). So the product is already minimal. This is the 2007 pattern (`m = 3`, `n = 5` → 15).

---

## 7. Standard min-DFA recipes

Each row is a *complete* DFA. “Sink” means a state that stays put on every symbol. Conditions are part of the rule: changing “exactly” to “at least”, or dropping completeness, changes the count.

| Language over `{0, 1}` unless noted | Min complete DFA | Why | Limitation |
|---|---|---|---|
| ends with a fixed `w`, `\|w\| = m` | `m + 1` | states = prefixes of `w` (KMP failure function on the last symbol) | alphabet does not matter for the count; overlaps change *arcs*, not the number of prefixes |
| contains a fixed `w`, `\|w\| = m` | `m + 1` | prefixes of `w`, plus an accepting sink once `w` is seen | same overlap warning; the sink **is** the “`w` already seen” prefix |
| starts with `w`, `\|w\| = m` | `m + 2` typically | `m` progress states + accepting sink after `w` + **dead** if the first mismatch can occur | “starts with `1`”: 3 states (`ε`, success sink, fail sink) |
| exactly `k` ones | `k + 2` | counts `0, 1, …, k` plus a rejecting sink for `≥ k+1` | **at least** `k` ones drops the sink (`k + 1` states); incomplete machines may hide the sink |
| `#a ≡ r (mod m)` | `m` | residues `0 … m−1`; other letters self-loop | all `m` are reachable if `a` occurs; accept only residue `r` |
| `#0 ≡ 0 (mod m)` **and** `#1 ≡ 0 (mod n)` | `mn` | product; all pairs reachable | if the conditions are **not** independent (e.g. a single counter) do not multiply |
| `#a` even but not divisible by 3 | `6` | even and not `≡ 0 (mod 3)` iff `#a ≡ 2 or 4 (mod 6)`; all 6 residues distinguishable | “even **or** not div by 3” is a different accept set and still uses 6 |
| no `k` consecutive `1`s | `k + 1` | trailing-`1` counts `0, 1, …, k−1` (accept) plus a rejecting sink for `k` in a row | `k = 3` → **4**, not 5; “no `k` consecutive” includes the shorter strings |
| `(0+1)*(0+1)(0+1)*` i.e. `Σ+` | `2` | reject only `ε`; one rejecting start, one accepting sink | a 1-state complete DFA is only `∅` or `Σ*`, never `Σ+` |
| `k`-th symbol **from the end** is `1` | `2^k` | last `k` bits | **not** `k + 1` (that is the NFA size); strings shorter than `k` reject |
| `k`-th symbol **from the start** is `1` | `k + 2` | positions `0 … k−1`, then a yes-sink and a no-sink | strings shorter than `k` reject; the two sinks are distinguishable |

### Worked example 4 — exactly two `1`s (need a sink)

States: `c0` (zero `1`s, start), `c1` (one `1`), `c2` (two `1`s, **only accept**), `d` (three or more `1`s, reject sink). Zeros self-loop on each.

| | `0` | `1` |
|---|---|---|
| `c0` | `c0` | `c1` |
| `c1` | `c1` | `c2` |
| `c2` | `c2` | `d` |
| `d` | `d` | `d` |

Traces: `ε` in `c0`; `10` in `c1`; `11` in `c2` (accept); `110` stays in `c2` (accept); `111` in `d` (reject).

The strings `ε`, `1`, `11`, `111` are pairwise distinguishable, so **4** states are necessary. A 3-state complete DFA has nowhere legal to send `c2` on `1` without colliding with `c0` or `c1`, and those collisions are distinguished by a further `1` or `11`. Dropping `d` makes `δ` partial; the *complete* minimum is 4.

### Worked example 5 — no three consecutive `1`s

`L = { w ∈ {0,1}* | w` does not contain `111` `}`. States remember the current run of trailing `1`s, until it hits 3.

| State | trailing `1`s | on `0` | on `1` | Accept? |
|---|---|---|---|---|
| `t0` (start) | 0 (empty, or last symbol `0`) | `t0` | `t1` | **yes** |
| `t1` | 1 | `t0` | `t2` | **yes** |
| `t2` | 2 | `t0` | `d` | **yes** |
| `d` | `≥ 3` (seen `111`) | `d` | `d` | no |

Traces: `ε, 0, 1, 11, 110, 1011` stay in `{t0, t1, t2}` (accept). `111` reaches `d` and stays (reject). `110111` also dies.

Distinguishability:

- `d` rejects `ε`; `t0, t1, t2` accept `ε`.
- From `t2`, `z = 1` dies; from `t0` and `t1` it does not.
- From `t1`, `z = 11` dies; from `t0`, `11` lands in `t2` (still accepting).

Four pairwise-distinguishable states, so the minimum is **4**. (A fifth state is a common overcount: “start” is the same as “trailing-0”.)

### Worked example 6 — `#a` even but not divisible by 3

Let `n = #a(w)` over `{a, b}`. `n` even and `n` not divisible by 3 ⇔ `n ≡ 2 (mod 6)` or `n ≡ 4 (mod 6)`. (`n ≡ 0 (mod 6)` is even *and* divisible by 3; odd residues are not even.)

DFA: residues of `n` modulo 6. `b` self-loops. Start `0`. Accept `{2, 4}`.

All six residues are reachable (`a^i` for `i = 0 … 5`). Pairwise distinguishability of residues `i ≠ j`: there exists `t` such that `i + t ≡ 2 (mod 6)` but `j + t ≢ 2` and `j + t ≢ 4`, or vice versa. Concretely:

- `2` accepts `ε`, `4` does not; `z = aa` sends `2` to `4` (accept) and `4` to `0` (reject), so `2 ≁ 4` as well.
- A non-accept residue `i` is separated from a different non-accept residue `j` by `a^{2-i \bmod 6}` (the unique shortest move of `i` onto `2`).

So **6** states, not 4 (the product of mod-2 with mod-3 also has 6 pairs, and the accept set `(even, not 0 mod 3)` does not let you merge any pair). Equivalently: build the 2-state even/odd DFA and the 3-state mod-3 DFA, take the product (6), accept the pairs `(even, r)` with `r ∈ {1, 2}`.

### Worked example 8 — `(0+1)*(0+1)(0+1)*`

The RE is `Σ Σ* = Σ+`: every nonempty binary string, not `ε`.

DFA: `s` (start, reject) `--0,1-->` `t` (accept sink) `--0,1--> t`.

`ε` is rejected; any nonempty string is accepted. `ε` and `0` are distinguishable (`z = ε`), so at least two states. A 1-state complete DFA cannot realise `Σ+`. Minimum: **2**.

---

## 8. Distinguishability and Myhill–Nerode

Fix a language `L ⊆ Σ*`. Strings `x, y ∈ Σ*` are **equivalent** (`x ∼_L y`) iff

for every `z ∈ Σ*`, `xz ∈ L  ⇔  yz ∈ L`.

They are **distinguishable** when some one continuation `z` puts exactly one of `xz`, `yz` in `L`. Equivalence is an equivalence relation. The classes are the **Myhill–Nerode classes** of `L`.

**Theorem.** `L` is regular iff `∼_L` has finitely many classes. If `L` is regular, the number of classes equals the number of states of the unique (up to renaming) minimal complete DFA for `L`. Each class is “all strings that land in this state”, and the start state is the class of `ε`.

**How GATE uses this.** To prove a constructed DFA is minimal, exhibit one string per state such that the strings are pairwise distinguishable. You never need to compare every pair of *states* if you have one distinguishing continuation per pair of *representatives*.

The continuation can be `ε` (that just asks whether the two strings themselves differ on membership). Always try `ε` first, then a single symbol, then the short string that finishes a pattern.

**States of a given DFA** `p` and `q` are distinguishable when there exists `z` such that `δ̂(p, z) ∈ F` xor `δ̂(q, z) ∈ F`. If no such `z` exists they are equivalent and minimization merges them. Unreachable states are not classes of `L` at all; they are deleted, not merged into a class of `L`.

---

## 9. Partition minimization (Hopcroft / marking table)

Input: a complete DFA, possibly with unreachable states.

1. **Delete unreachable states** from `q0` (BFS on the transition graph).
2. **Initial partition:** `F` vs `Q − F`. (Accepting / rejecting is the 0-equivalence.)
3. **Split:** while some block `B` and some symbol `a` send two states of `B` into *different current blocks*, split `B` accordingly.
4. Stop when no block splits. Each remaining block is an equivalence class. The quotient DFA is minimal.

Marking-table form (pairs): list every unordered pair `{p, q}`. Mark a pair if one is accepting and the other is not. Repeatedly: if `{p, q}` is unmarked and for some `a` the pair `{δ(p, a), δ(q, a)}` is already marked, mark `{p, q}`. Unmarked pairs are equivalent.

### Worked table

DFA over `{a, b}`:

| | `a` | `b` | Accept? |
|---|---|---|---|
| `q0` (start) | `q1` | `q2` | **yes** |
| `q1` | `q0` | `q3` | no |
| `q2` | `q3` | `q0` | **yes** |
| `q3` | `q2` | `q1` | no |

All four states are reachable: `ε → q0`, `a → q1`, `b → q2`, `ab → q3`.

Initial marks (accept vs reject): mark `{q0, q1}`, `{q0, q3}`, `{q2, q1}`, `{q2, q3}`. Unmarked: `{q0, q2}` and `{q1, q3}`.

Check `{q0, q2}`: on `a` go to `{q1, q3}` (unmarked); on `b` go to `{q2, q0}` (same pair). Check `{q1, q3}`: on `a` go to `{q0, q2}`; on `b` go to `{q3, q1}`. No new marks.

Quotient: `{q0, q2}` (accept) and `{q1, q3}` (reject). Language: even number of `a`s (`b` only swaps equivalent copies). Minimal DFA: **2** states.

The given 4-state machine is *not* minimal even though every state is reachable. Reachability and minimality are different tests.

---

## 10. Dead states and unreachable states

| Kind | Definition | Language effect if deleted | In the min complete DFA? |
|---|---|---|---|
| Unreachable | no path from `q0` | none | no |
| Dead / rejecting sink | no path from here to any accept state; usually `δ(d, a) = d` | deleting it makes `δ` partial | **yes**, whenever some illegal prefix is reachable (exactly-`k`, “no `k` in a row”, “starts with”, complement of `Σ*` minus a pattern, …) |
| Accepting sink | `δ(f, a) = f` and `f ∈ F` | — | yes, for “contains `w`”, `Σ+`, “already seen the pattern” |

A rejecting sink and an accepting sink are distinguishable (`z = ε`). Two rejecting sinks from which *no* accept state is reachable *are* equivalent (nothing ever accepts), so they merge into one dead state.

---

## 11. `k`-th symbol from the end

**NFA (easy).** Guess the symbol that will be `k` from the end, check it is the desired letter, then take exactly `k − 1` more symbols and halt. `k + 1` states.

**DFA (forced `2^k`).** The state is the last `k` bits (pad the start with a dummy letter that is *not* accepting: e.g. start at `0^k` when the distinguished letter is `1`). On bit `c`, shift: `b1 b2 … bk  ↦  b2 … bk c`. Accept iff the oldest remembered bit is the one you want.

All `2^k` strings of length `k` are pairwise distinguishable: if `x` and `y` differ in position `i` (1-indexed from the left), the continuation `0^{i-1}` makes that bit sit in the `k`-from-end place.

For `k = 1` (ends with `1`): 2 states. For `k = 2`: 4. For `k = 3` (third from the end): **8**.

**Contrast: `k`-th from the start.** You only wait `k` steps, then branch to a yes-sink or a no-sink. That is linear: `k + 2` complete states (the two sinks plus `k` waiting states), not exponential. Mixing the two up is a high-value trap.

---

## 12. NFA for all substrings of a fixed `w`

Let `|w| = n`, `L = { x | x is a substring of w }` (including `ε` and `w`).

**An `(n+1)`-state NFA.** States `q0, q1, …, qn`, all accepting, start `q0`. The spine is

`q0 --w[1]--> q1 --w[2]--> … --w[n]--> qn`.

Add `ε`-edges from `q0` to every `qi`. Then a substring `w[i+1 … j]` is accepted by jumping to `qi` and walking to `qj`. Prefixes use the spine from `q0` without a jump. `ε` is accepted at `q0`.

**Why `n+1` is tight.** Take `w = a^n`. Then `L = { a^0, a^1, …, a^n }`. An NFA with `n` states that accepts `a^n` has a run of length `n`, hence a repeated state on that run (or a cycle usable after some point); pumping that cycle accepts some `a^{n+t}` with `t ≥ 1`, which is not a substring of `a^n`. So at least `n+1` NFA states are required, and the construction matches. This is the 2010 pattern (OCR often writes the length as `n`).

A DFA for the same `L` can be much larger (it must reject every string that is *not* a substring of this particular `w`). The question asked for an NFA.

---

## 13. Monoid / group DFAs, products of symbols

### Worked example 7 — binary value modulo `m`

Read `w` as an unsigned integer (leading zeros allowed), `val(ε) = 0`. State = current value mod `m`.

`δ(r, b) = (2r + b) \bmod m` for `b ∈ {0, 1}`.

Start `0`. For “value `≡ 0 (mod 3)`” accept `{0}`: 3 states, all reachable (`ε, 1, 10`). Distinguishable because `{0, 1, 2}` is a group under the transitions. RE via state elimination: `(0 + 1(01*0)*1)*` ([`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS) §8).

### Product of symbols modulo a prime

Let `Σ ⊆ {1, 2, …, p−1}`, `p` prime, `prod(ε) = 1`, `prod(xa) = (prod(x) · a) \bmod p`. States are residues in `{1, 2, …, p−1}` (the multiplicative group `(ℤ/pℤ)*`). Residue `0` is **unreachable** because no factor is `0 mod p`.

If the generators `Σ` generate the whole group (they do when `Σ = {1, 2, 3, 4}` and `p = 7`), all `p − 1` nonzero residues are reachable. Accept the unique residue `t` asked for. Distinguishability: from residue `r` the continuation whose product is `t · r^{-1}` reaches `t`, and from `s ≠ r` it does not. Min DFA: **`p − 1`** states.

For `p = 7`, `Σ = {1, 2, 3, 4}`, `L = { x | prod(x) = 2 }`: start `1`, never `0`, six reachable residues, accept `{2}` → **6** states. (Including an unused `0` would be an unreachable extra state.)

### Group of bijections (permutations)

Let `G` be a finite group, written as a set of letters (e.g. all bijections `{1,…,n} → {1,…,n}`, so `|G| = n!`). For a word `x = g1 g2 … gm` let `n(x) = g1 ∘ g2 ∘ … ∘ gm`, and `n(ε) = id`. Let `L = { x | n(x) = id }`.

DFA: states = elements of `G`, start `id`, accept `{id}`, `δ(h, g) = h ∘ g`.

Every state is reachable (each group element is a letter). Distinguishability: from `h` the continuation `h^{-1}` is accepted, and from `h' ≠ h` it is not. Min DFA: **`|G|`** states.

For bijections of `{1,…,5}`, `|S_5| = 120`. For `{1, 2, 3}`, `|S_3| = 6`. The composition convention (`f ∘ g` vs `g ∘ f`) changes the *arcs*, not the state count.

---

## 14. Position constraints of the form `w1 a w2`

`L = { w1 a w2 | w1, w2 ∈ Σ*, |w1| = p, |w2| ≥ q }` means: the `(p+1)`-st symbol is `a`, and the length is at least `p + 1 + q`.

Complete DFA:

- `p + 1` waiting states for the first `p` symbols (`0, 1, …, p` read),
- then branch: if the next symbol is `a`, count `q` further symbols (`0, 1, …, q−1` of `w2`, then an accepting sink); if not, a rejecting sink.

Count: `(p + 1) + (q + 1) + 1 = p + q + 3`. For `p = 2`, `q = 3`: **8** states. For `p = 1`, `q = 2`: **6**.

All of these are reachable, and the waiting / counting / dead states are pairwise distinguishable by how many extra symbols they still need, or by whether the distinguished position already failed.

---

## 15. DFA → RE (exam method)

Full algorithms (state elimination, Arden) are in [`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS) §7–8. In GATE you almost never derive; you **check options**.

1. List `ε` and all strings of length 1, 2, 3 that the DFA accepts / rejects.
2. Kill every RE that disagrees on one of them.
3. If two REs survive, find a longer distinguishing string (a loop taken twice is the usual source) and trace it.

**Ends with `1`,** a recurring option-set (2014-style):

- `(0+1)*1` is exactly “ends with `1`”.
- `0*1(1 + 00*1)*` is the Arden form of the 2-state DFA (`A` non-accept `--1-->` `B` accept; `B --1--> B`; `B --0--> A`; `A --0--> A`) and equals `(0+1)*1`.
- A broken union such as `0*1*1 + 11*0*1` misses strings with more than one `0`/`1` alternation after the first block (e.g. `10101` ends with `1` but is in neither summand).

---

## 16. NFA complement, “all states accepting”, regularity of `A ∩ B`

**Complement.** For a *complete DFA*, flip `F`. For an NFA this is illegal:

- a string may have both an accepting run and a rejecting run — flipping `F` still accepts it;
- a string with **no** complete run is rejected by the NFA; flipping `F` does not create a run, so the string stays rejected, but it may need to be *accepted* by the complement.

Correct procedure: determinize (and complete), then flip. Classic unary trap: an NFA for `a+` (nonempty strings of `a`s). Complement relative to `{a}*` is `{ε}`, not `∅` and not `a*`.

**“Every NFA state is accepting ⇒ `L = Σ*`” is false.** Counterexample: one accepting state, alphabet `{a, b}`, a self-loop on `a` only. The machine is an NFA for `a*`, not `{a, b}*`. Strings with a `b` have no complete run, hence are rejected.

If the NFA is **complete** (`δ(q, a) ≠ ∅` for every pair) **and** every state is accepting, then every string has a run and every run accepts, so `L = Σ*`. Completeness is the missing hypothesis.

**“There exists a regular `A` such that `A ∩ B` is regular for every language `B`” is true.** Take `A = ∅`: `∅ ∩ B = ∅`. (Any finite `A` also works: `A ∩ B` is finite, hence regular.) `A = Σ*` does **not** work.

---

## 17. GATE problem-solving approach

1. **Name the finite memory.** Parity, residue, trailing run, longest prefix of a pattern, last `k` bits, group element, pair of residues. That name *is* the state set.
2. **Draw the complete DFA** (include a dead sink whenever an illegal prefix is reachable). Trace `ε`, a shortest member, and a just-illegal string.
3. **Prove minimality** by pairwise distinguishable representatives, one per state. If two states look mergeable, try `z = ε` then a single symbol then the finishing suffix of the pattern.
4. **For NFA → DFA size**, do not build `2^n` subsets. Argue the bound, or build *reachable* subsets only.
5. **For DFA → RE options**, do not eliminate states unless two options survive the short-string filter.
6. **For a missing-arc figure**, the state name is usually the last `k` symbols or the progress on a forbidden word. Complete every row of the transition table; the dead state is the row that has nowhere legal to go.

---

## 18. Common traps

- Counting “no `k` consecutive `1`s” as `k + 2` (an extra copy of the start). It is `k + 1` including the sink; `k = 3` → 4.
- Forgetting the dead state on “exactly `k` ones” (`k + 1` instead of `k + 2`).
- Using the NFA size `k + 1` for “`k`-th from the **end**” instead of `2^k`. Using `2^k` for “`k`-th from the **start**”.
- Flipping accept states of an NFA and calling that the complement.
- Claiming `k ≥ n` after subset construction; claiming a min DFA can have `2^n + 1` states.
- Including unreachable `0` in a product-mod-`p` DFA when `0` cannot appear as a factor.
- Treating `(0+1)*(0+1)(0+1)*` as `Σ*` (that would be 1 state) instead of `Σ+` (2 states).
- Believing subset construction is already minimal (Example 2 vs “contains `10`” in practice: 4 reachable subsets, 3 after merge).
- `ε`-closure without the state itself.
- Product of moduli when the two conditions are **not** independent (they share the same counter).
- “All NFA states accepting ⇒ `Σ*`” on an incomplete NFA.
- Identifying a DFA language from a figure by the *shape* instead of tracing `ε`, `0`, `1`, `00`, `01`.

---

## 19. Edge cases

- `ε`: accepted by a DFA iff `q0 ∈ F`; by an `ε`-NFA iff `E(q0)` meets `F`.
- `∅` and `Σ*`: unique 1-state complete DFAs.
- `Σ+`: 2 states. `{ε}`: 2 states (start accept, dead reject sink on any letter).
- Unary `L = { a^{kn} | k ≥ 1 }` (`n` a fixed positive integer): `n + 1` states (start is residue `0` but rejecting; the accepting residue-`0` is a different state). For `k ≥ 0` (include `ε`): `n` states.
- Incomplete NFA runs: “no next state” rejects *that run only*.
- Two DFAs can have different state names and extra unreachable states but the same language; compare by minimization or by Myhill–Nerode, not by drawing.

---

## 20. Connections

- **Regular expressions** ([`01-REGULAR-EXPRESSIONS`](../01-REGULAR-EXPRESSIONS)): Kleene, Thompson, Arden, state elimination. DFA → RE options in this folder; RE reading in that one.
- **Regular languages** ([`05-REGULAR-LANGUAGES`](../05-REGULAR-LANGUAGES)): closure, Myhill–Nerode as a *proof that a language is not regular* (infinitely many classes), pumping. Min-DFA *constructions* stay here; “is this regular?” goes there.
- **Regular grammars** ([`03-CONTEXT-FREE-GRAMMARS`](../03-CONTEXT-FREE-GRAMMARS) will not own them; right-linear grammars sit with regular languages): an NFA is a right-linear grammar with a production per arc.
- **Pumping lemma** ([`07-PUMPING-LEMMA`](../07-PUMPING-LEMMA)): a DFA with `n` states that accepts a word of length `≥ n` has a cycle; that is the regular pumping lemma.
- **Compiler design**: lexical analysis compiles an RE to an NFA, determinizes, minimises. The 2015 match-the-following stem that pairs “lexical analysis” with “DFA minimization” is a compiler question filed in this mapping; the construction is this folder’s.
- **Undecidability** ([`09-UNDECIDABILITY`](../09-UNDECIDABILITY)): emptiness, finiteness, equivalence of FAs are **decidable** (minimize and compare; or check reachability of an accept state). Do not quote Rice on a DFA.

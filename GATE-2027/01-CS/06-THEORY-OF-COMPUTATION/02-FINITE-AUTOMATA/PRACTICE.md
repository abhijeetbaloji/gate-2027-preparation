# Finite Automata — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/02-FINITE-AUTOMATA/practice.md`; do both sets.

Conventions: a DFA is complete unless the question says otherwise. An NFA accepts a string when at least one computation reads the whole string and ends in an accept state. `ε` is the empty string. Every numerical answer below was checked by tracing the machine or by a Myhill–Nerode argument on named representatives.

Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

In a complete DFA, the computation on a string `w` of length `n`

- (A) may have zero, one, or many runs, depending on `w`
- (B) consists of exactly `n + 1` states, uniquely determined by `w`
- (C) exists if and only if `w` is accepted
- (D) can die on a missing arc and then be rescued by another branch

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** `δ` is a total function, so there is exactly one successor at every step. The run is `q0` followed by one state per symbol, hence `n + 1` states, whether or not the last one is accepting. (A) and (D) describe NFAs. (C) confuses existence of the run with acceptance: rejected strings still have a unique run.

**Concept tested:** DFA `δ` is total; unique run.
**Difficulty:** Level 1
**Common trap:** treating a DFA like an NFA with missing arcs.
</details>

### Q2 · MCQ

In an `ε`-NFA, the `ε`-closure of a state `p` that has a single `ε`-edge `p → q` and no other `ε`-edge is

- (A) `{q}`
- (B) `{p, q}`
- (C) `{p}`
- (D) `∅`, because `ε` is not an input symbol

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** `E(p)` is `p` itself together with every state reachable from `p` by a path of one or more `ε`-edges. Here that adds `q`. (A) drops the seed state — the standard closure error. (D) confuses “`ε` is not in `Σ`” (true) with “`ε`-closure is empty” (false).

**Concept tested:** `ε`-closure includes the state itself.
**Difficulty:** Level 1
**Common trap:** returning only the `ε`-successors.
</details>

### Q3 · NAT

Over `{0, 1}`, the number of states in the minimal complete DFA for the language of strings that **start with `1`** is ____. (`ε` is rejected.)

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** Three states suffice: `s` (nothing read, start, reject), `yes` (first symbol was `1`, accepting sink), `no` (first symbol was `0`, rejecting sink).

`s --1--> yes --0,1--> yes`, `s --0--> no --0,1--> no`.

They are necessary. Representatives `ε`, `1`, `0`:

- `1 ∈ L`, `ε ∉ L`, `0 ∉ L`.
- `ε · 1 = 1 ∈ L` while `0 · 1 = 01 ∉ L`.

A 2-state complete DFA cannot keep a rejecting start, an accepting sink, and a rejecting sink that is distinguishable from the start.

**Concept tested:** “starts with” template; dead sink on the first mismatch.
**Difficulty:** Level 1
**Common trap:** answering 2 by omitting the dead sink, or answering 1 by confusing the language with `Σ*`.
</details>

### Q4 · MCQ

An NFA over `{0, 1}` has start `s`, an accept state `f`, a non-accept state `g`, and only the transitions `s --0--> p`, `s --0--> r`, `p --1--> f`, `r --1--> g`. On the input `01` this NFA

- (A) rejects, because the run through `g` rejects
- (B) accepts, because the run `s → p → f` reads all of `01` and ends in an accept state
- (C) is illegal, because `s` has two `0`-transitions
- (D) accepts only if `p` is also an accept state

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Two runs exist: `s -0→ p -1→ f` (accept) and `s -0→ r -1→ g` (reject). Existential acceptance keeps the string. Two transitions on the same symbol are exactly what an NFA is allowed. `p` need not be accepting; only the *end* of some complete run must be.

**Concept tested:** NFA acceptance is existential.
**Difficulty:** Level 1
**Common trap:** (A) — a rejecting branch does not veto an accepting branch.
</details>

---

## Level 2 — Standard GATE

### Q5 · NAT

Consider the NFA over `{0, 1}` with states `{p, q, r}`, start `p`, only accept state `r`, and

- `δ(p, 0) = {p}`, `δ(p, 1) = {p, q}`
- `δ(q, 0) = {r}`, `δ(q, 1) = ∅`
- `δ(r, 0) = {r}`, `δ(r, 1) = {r}`

The number of **reachable** states in the subset-construction DFA (including the start subset) is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** Start `{p}`.

- `{p} --0--> {p}`, `{p} --1--> {p, q}`
- `{p, q} --0--> {p} ∪ {r} = {p, r}`, `{p, q} --1--> {p, q} ∪ ∅ = {p, q}`
- `{p, r} --0--> {p, r}`, `{p, r} --1--> {p, q} ∪ {r} = {p, q, r}`
- `{p, q, r} --0--> {p, r}`, `{p, q, r} --1--> {p, q, r}`

Reachable subsets: `{p}`, `{p, q}`, `{p, r}`, `{p, q, r}`. The empty set is not reached. (The language is “contains `10`”; minimization later merges `{p, r}` with `{p, q, r}` into an accepting sink, leaving 3 states. The question asked for reachable subsets, not the minimum.)

**Concept tested:** subset construction; reachable subsets only.
**Difficulty:** Level 2
**Common trap:** reporting `8 = 2^3`, or reporting 3 after silently minimising.
</details>

### Q6 · NAT

The number of states in the minimal complete DFA for

`{ w ∈ {0, 1}* | #0(w) is even and #1(w) is odd }`

is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** Product of a 2-state parity-of-`0` DFA with a 2-state parity-of-`1` DFA. States `(e/o of 0, e/o of 1)`. Start `(E, E)`. Accept `{(E, O)}`. All four pairs are reached by `ε, 0, 1, 01`.

Distinguishability:

- only `(E, O)` accepts `ε`;
- from `(E, E)`, the continuation `1` is accepted; from `(O, E)` and from `(O, O)` it is not;
- from `(O, E)`, the continuation `01` is accepted; from `(O, O)`, `01` lands in `(E, E)` (reject).

Four classes. No dead state.

**Concept tested:** product of independent parities; accept set is one cell of the product.
**Difficulty:** Level 2
**Common trap:** answering 2 (remembering only one parity) or 3 (dropping a reachable pair).
</details>

### Q7 · MSQ

Let `L` be the binary language of strings that **end with `11`**. Which pairs are distinguishable with respect to `L`?

- (A) `ε` and `1`
- (B) `1` and `01`
- (C) `11` and `011`
- (D) `0` and `1`

<details><summary>Answer and solution</summary>

**Answer:** (A), (D)

**Solution:** `x ≁ y` iff some `z` puts exactly one of `xz`, `yz` in `L`.

- (A) `ε · 1 = 1 ∉ L`, `1 · 1 = 11 ∈ L`. Distinguishing continuation `1`.
- (B) both strings end in `1`. For every `z`, `1z` and `01z` have the same last two symbols whenever `|z| ≥ 1`, and on `z = ε` both are out of `L`. Equivalent: both sit in the “suffix `1`” class.
- (C) both already end in `11`, so they sit in the accepting class.
- (D) `0 · 1 = 01 ∉ L`, `1 · 1 = 11 ∈ L`.

**Concept tested:** Myhill–Nerode on an ends-with language; the three prefixes of `11`.
**Difficulty:** Level 2
**Common trap:** marking (B) because the strings look different; membership of the prefixes themselves is not the test — continuations are.
</details>

### Q8 · NAT

The number of states in the minimal complete DFA for `L((0+1)*(0+1)(0+1)*)` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** The RE is `Σ Σ* = Σ+`: every nonempty binary string, not `ε`. DFA: rejecting start `s --0,1-->` accepting sink `t --0,1--> t`. `ε ∉ L` and `0 ∈ L`, so at least two states. A 1-state complete DFA realises only `∅` or `Σ*`. Hence 2.

**Concept tested:** `Σ+` vs `Σ*`; one-state check.
**Difficulty:** Level 2
**Common trap:** answering 1 by reading the RE as `Σ*`.
</details>

---

## Level 3 — Multi-step reasoning / construction

### Q9 · MCQ

Every state of an NFA over `{a, b}` is accepting. Which statement is true?

- (A) The language is `{a, b}*` for every such NFA
- (B) The language is `{a, b}*` if `δ(q, x) ≠ ∅` for every state `q` and every symbol `x`
- (C) `ε` is never in the language
- (D) The language need not be regular

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** If every state is accepting *and* every state has at least one successor on every symbol, every string has a complete run and every run accepts, so `L = Σ*`. Without completeness, strings that die are rejected: the one-state NFA with an `a`-loop only (state accepting) denotes `a*`, not `{a, b}*`. (C) is false: the start state is accepting, so `ε ∈ L`. (D) is false: every NFA language is regular.

**Concept tested:** all-accepting NFA vs completeness; 2016-style statement I.
**Difficulty:** Level 3
**Common trap:** (A) — the incomplete counterexample.
</details>

### Q10 · NAT

The number of states in the minimal complete DFA for the binary language of strings with **no two consecutive `0`s** is ____.

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** Trailing-`0` count: `t1` (no trailing `0`: start, or last symbol `1`), `t0` (exactly one trailing `0`), `d` (seen `00`, reject sink). `t1` and `t0` accept.

`t1 --0--> t0 --0--> d`, `t1 --1--> t1`, `t0 --1--> t1`, `d --0,1--> d`.

Representatives `ε`, `0`, `00`: `00 ∉ L` while the other two are in `L`; `ε · 0 ∈ L` while `0 · 0 ∉ L`. Three classes. (Start is `t1`, not a fourth state.)

**Concept tested:** “no `k` consecutive” with `k = 2` → `k + 1 = 3` states.
**Difficulty:** Level 3
**Common trap:** answering 4 by splitting “start” from “last was `1`”.
</details>

### Q11 · NAT

The number of states in the minimal complete DFA for the binary language of strings with **exactly three `1`s** is ____.

<details><summary>Answer and solution</summary>

**Answer:** 5

**Solution:** Counts `c0, c1, c2, c3` (only `c3` accepting) plus a rejecting sink `d` for four or more `1`s. Zeros self-loop. The strings `ε, 1, 11, 111, 1111` are pairwise distinguishable (`ε` splits `c3` from the rest; a suitable number of extra `1`s splits every pair of the others). Completeness forces `d`: from `c3` the symbol `1` cannot return to `c0`, `c1`, or `c2` without identifying two distinguishable classes. Total `3 + 2 = 5`.

**Concept tested:** exactly-`k` ones → `k + 2` complete states.
**Difficulty:** Level 3
**Common trap:** answering 4 by omitting the sink.
</details>

### Q12 · NAT

A DFA over `{a, b}` has start `q0`, accept states `{q0, q2}`, and

| | `a` | `b` |
|---|---|---|
| `q0` | `q1` | `q2` |
| `q1` | `q0` | `q3` |
| `q2` | `q3` | `q0` |
| `q3` | `q2` | `q1` |

The number of states in the minimal equivalent complete DFA is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** All four states are reachable (`ε, a, b, ab`). Initial partition: accept `{q0, q2}`, reject `{q1, q3}`.

- `q0` and `q2` both go to the reject block on `a` and to the accept block on `b`.
- `q1` and `q3` both go to the accept block on `a` and to the reject block on `b`.

The partition is stable, so the two blocks are the Myhill–Nerode classes. Language: even number of `a`s (`b` only swaps equivalent copies). Reachability did not prevent the merge.

**Concept tested:** marking / partition minimization; reachable ⇏ minimal.
**Difficulty:** Level 3
**Common trap:** answering 4 because every state is reachable.
</details>

---

## Level 4 — Tricky / trap-based

### Q13 · MCQ

An `ε`-NFA has states `{A, B, C, D}`, start `A`, and transitions

| | `ε` | `a` | `b` |
|---|---|---|---|
| `A` | `{B}` | `{A}` | `{C}` |
| `B` | `∅` | `{C}` | `{B}` |
| `C` | `{D}` | `{B}` | `∅` |
| `D` | `∅` | `∅` | `{A}` |

Let `δ̂` be the extended transition. Then `δ̂(A, b)` equals

- (A) `{C}`
- (B) `{B, C, D}`
- (C) `{A, B, C}`
- (D) `{A, B, C, D}`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Closures: `E(A) = {A, B}`, `E(B) = {B}`, `E(C) = {C, D}`, `E(D) = {D}`.

Start `δ̂(A, ε) = {A, B}`. Consume `b`: `δ(A, b) ∪ δ(B, b) = {C} ∪ {B} = {B, C}`. Close: `E(B) ∪ E(C) = {B} ∪ {C, D} = {B, C, D}`.

`A` is not recovered: the only edge into `A` is `D --b--> A`, and that `b` has already been consumed. (A) forgot the run that stayed in `B` on `b` and forgot `E(C)`. (D) closed as if `A` were still occupied.

**Concept tested:** `ε`-NFA extended `δ`: close, consume, close.
**Difficulty:** Level 4
**Common trap:** skipping the seed of a closure, or taking `ε`-edges after the wrong symbol.
</details>

### Q14 · MSQ

Let `N` be an NFA with `n ≥ 1` states, and let `k` be the number of states of a minimal complete DFA equivalent to `N`. Which statements are true?

- (A) `k ≤ 2^n` always
- (B) `k ≥ n` always
- (C) there exists such an `N` with `k = 1`
- (D) there exists such an `N` with `k = 2^n + 1`

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** Subset construction yields some DFA with at most `2^n` states, so the *minimal* DFA satisfies `k ≤ 2^n`. For `k = 1`: take a complete NFA with every state accepting and a self-loop on every symbol (`L = Σ*`), or with no state accepting (`L = ∅`); extra states may be unreachable. Then the min DFA has one state, even if `n > 1`. So (B) is false. (D) exceeds the powerset, hence is impossible.

**Concept tested:** NFA → DFA bounds.
**Difficulty:** Level 4
**Common trap:** (B), which feels true because “determinizing adds states”.
</details>

### Q15 · NAT

Over `{0, 1}`, the number of states in the minimal complete DFA for the language of strings whose **second symbol from the end is `0`** is ____. (Strings of length less than 2 are rejected.)

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** The state is the last two bits, starting from the pad `11` (or any pad whose first bit is not `0`, so that `ε` rejects). On bit `c` shift `xy ↦ yc`. Accept the states whose *older* bit is `0`, i.e. `00` and `01`.

The four length-2 strings are pairwise distinguishable:

- `00 ∈ L`, `10 ∉ L` (`z = ε`); `01 ∈ L`, `11 ∉ L`.
- `00` vs `01` (both in): `z = 1` gives `001 ∈ L` (second-from-end `0`) and `011 ∉ L` (second-from-end `1`).
- `10` vs `11` (both out): `z = 1` gives `101 ∈ L` and `111 ∉ L`.

So 4 classes. (This is `2^k` for `k = 2`. An NFA with 3 states exists; the question asks for a DFA.)

**Concept tested:** `k`-th from the end; `2^k` vs the NFA size `k + 1`.
**Difficulty:** Level 4
**Common trap:** answering 3 (the NFA size) or 8 (mixing up `k = 3`).
</details>

### Q16 · NAT

Over `{a}`, let `L = { a^{3t} | t ≥ 1 }`. The number of states in the minimal complete DFA for `L` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** Residues modulo 3 are not enough: residue `0` must reject `ε` and accept `a^3, a^6, …`. So keep a rejecting start `s0` (zero `a`s) separate from an accepting `s3` (positive multiples of 3), plus `s1` and `s2`.

`s0 --a--> s1 --a--> s2 --a--> s3 --a--> s1`.

Representatives `ε, a, aa, aaa`: `aaa ∈ L`, the others are not; `ε · aaa ∈ L` while `a · aaa = a^4 ∉ L`; `aa · a ∈ L` while `ε · a ∉ L`. Four classes. (If `t ≥ 0` were allowed, `ε` would sit in `s3` and the count would drop to 3.)

**Concept tested:** unary `{a^{n t} : t ≥ 1}` → `n + 1` states.
**Difficulty:** Level 4
**Common trap:** answering 3 by accepting `ε`.
</details>

---

## Level 5 — Challenge

### Q17 · NAT

The number of states in the minimal complete DFA for

`{ w ∈ {0, 1}* | w does not contain three consecutive 1s }`

is ____.

<details><summary>Answer and solution</summary>

**Answer:** 4

**Solution:** Trailing-`1` counts `t0` (start / last was `0`), `t1`, `t2`, and a rejecting sink `d` for `111`. `t0, t1, t2` accept. A `0` from any of `t0, t1, t2` returns to `t0`; a `1` advances `t0 → t1 → t2 → d`; `d` stays in `d`.

Representatives `ε, 1, 11, 111`:

- `111 ∉ L`; the other three are in `L`.
- from `11`, `z = 1` dies; from `ε` and from `1` it does not.
- from `1`, `z = 11` dies; from `ε`, `11` is still in `L`.

Four classes. There is no fifth “start-only” state: after a `0` the machine is back at `t0`.

**Concept tested:** no `k` consecutive `1`s → `k + 1` states; `k = 3` → 4.
**Difficulty:** Level 5
**Common trap:** answering 5.
</details>

### Q18 · NAT

The number of states in the minimal complete DFA for

`{ w ∈ {a, b}* | #a(w) is even and #a(w) is not divisible by 3 }`

is ____.

<details><summary>Answer and solution</summary>

**Answer:** 6

**Solution:** Even and not a multiple of 3 ⇔ `#a ≡ 2 (mod 6)` or `#a ≡ 4 (mod 6)`. DFA: residues of `#a` modulo 6; `b` self-loops; start `0`; accept `{2, 4}`. All six residues are reached by `a^i`.

Both `a^2` and `a^4` are in `L`, so `z = ε` does not split residues `2` and `4`. Use `z = aa`: `a^2 · aa = a^4 ∈ L` while `a^4 · aa = a^6 ∉ L`.

A rejecting residue `i` is taken onto `2` by `a^{(2-i) \bmod 6}`; a different rejecting residue is not. So no two residues merge. Equivalently: product of mod-2 with mod-3 (6 pairs), accept `(even, r)` for `r ∈ {1, 2}`; the pair `(even, 0)` is `≡ 0 (mod 6)` and stays.

**Concept tested:** a single letter with two modular constraints; `lcm(2, 3) = 6`.
**Difficulty:** Level 5
**Common trap:** answering 4 by illegally merging residues `2` and `4`, or answering 2 (parity only).
</details>

### Q19 · NAT

Over `{a, b}`, let

`L = { w1 a w2 | w1, w2 ∈ {a, b}*, |w1| = 1, |w2| ≥ 2 }`.

The number of states in the minimal complete DFA for `L` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 6

**Solution:** The second symbol must be `a` and the length must be at least 4. Complete DFA:

- `u0`, `u1`: 0 or 1 symbol read;
- `a0`, `a1`: second symbol was `a`, then 0 or 1 symbol of `w2`;
- `acc`: second was `a` and `|w2| ≥ 2` (accepting sink);
- `dead`: second symbol was `b` (rejecting sink).

That is `p + q + 3` with `p = 1`, `q = 2`, hence 6.

Representatives `ε, a, aa, aab, aaaa, bb`:

- `ε` vs `a`: `z = aaa` — `aaa` has 2nd symbol `a` but length 3, so `∉ L`; `aaaa ∈ L`.
- `a` vs `aa`: `z = aa` — `aaa ∉ L`, `aaaa ∈ L`.
- `aa` vs `aab`: `z = a` — `aaa ∉ L`, `aaba ∈ L`.
- `aab` vs `aaaa`: `z = ε`.
- `bb` vs `ε`: `z = aaaa` — `aaaa ∈ L`, `bbaaaa` has 2nd symbol `b`, so `∉ L`.

Six classes.

**Concept tested:** distinguished position plus a length floor; dead sink when the position fails.
**Difficulty:** Level 5
**Common trap:** dropping `dead`, or merging `u0` with `u1`.
</details>

### Q20 · NAT

Let `G` be the set of all bijections `{1, 2, 3} → {1, 2, 3}`, and let `∘` be composition. For `x = g1 g2 … gm ∈ G*` write `n(x) = g1 ∘ g2 ∘ … ∘ gm`, and `n(ε) = id`. Let `L = { x ∈ G* | n(x) = id }`. The number of states in the minimal complete DFA for `L` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 6

**Solution:** `|G| = 3! = 6`. DFA: states = elements of `G`, start `id`, accept `{id}`, `δ(h, g) = h ∘ g`. Every letter is a group element, so every state is reachable. From `h`, the continuation `h^{-1}` is accepted, and from `h' ≠ h` it is not. Six distinguishable states. (Left vs right composition only permutes the transition table.)

**Concept tested:** group DFA; states = group elements.
**Difficulty:** Level 5
**Common trap:** answering 3 (the set `{1, 2, 3}` instead of the symmetric group).
</details>

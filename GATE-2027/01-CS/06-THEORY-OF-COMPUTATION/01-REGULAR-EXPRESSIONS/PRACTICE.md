# Regular Expressions — Practice

Original GATE-style questions written for this repository. They are not previous-year questions. They do not repeat the questions in `../../14-PRACTICE-QUESTIONS/TOPIC-WISE/06-THEORY-OF-COMPUTATION/01-REGULAR-EXPRESSIONS/practice.md`; do both sets.

Conventions: `+` is union, juxtaposition is concatenation, `*` is Kleene star; star binds tightest, then concatenation, then union. Every numerical answer below was checked by enumerating all strings up to the stated length.

Open the answer block only after attempting the question.

---

## Level 1 — Conceptual

### Q1 · MCQ

Let `L = ∅`. The language `(L* · {a, b}) ∪ (L · {a}*)` equals

- (A) `∅`
- (B) `{ε}`
- (C) `{a, b}`
- (D) `{ε, a, b}`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** `L* = ∅* = {ε}`, so `L* · {a, b} = {a, b}`. `L · {a}* = ∅` because concatenation with `∅` is empty. Union: `{a, b}`.

**Concept tested:** `∅` is the zero of concatenation; `∅*` is `{ε}`.
**Difficulty:** Level 1
**Common trap:** writing `∅* = ∅` gives (A); treating `∅ · {a}*` as `{a}*` gives a larger set.
</details>

### Q2 · MCQ

Which identity is **false** for all regular expressions `r`, `s`?

- (A) `(r*)* = r*`
- (B) `(r + s)* = (r*s*)*`
- (C) `(rs)* = r*s*`
- (D) `r(sr)* = (rs)*r`

<details><summary>Answer and solution</summary>

**Answer:** (C)

**Solution:** With `r = a`, `s = b`: `a ∈ L(a*b*)` but `a ∉ L((ab)*)`. The other three are standard identities: (B) both sides produce any sequence of `r`- and `s`-pieces; (D) both sides are `r s r s … r`.

**Concept tested:** RE identities and non-identities.
**Difficulty:** Level 1
**Common trap:** "distributing" the star over concatenation.
</details>

### Q3 · NAT

The number of strings of length exactly 4 in `(a + b)*bb(a + b)*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 8

**Solution:** The RE denotes strings containing `bb`. Complement: length-4 strings over `{a, b}` with no `bb`. These follow the Fibonacci count `1, 2, 3, 5, 8` for lengths `0 … 4`, so 8 avoid `bb`. `16 − 8 = 8`.

**Concept tested:** reading "contains" REs; complement counting.
**Difficulty:** Level 1
**Common trap:** counting placements of `bb` (3 positions × 4) double-counts `bbbb`, `abbb`, `bbba`, `bbbb`-type overlaps.
</details>

### Q4 · MCQ

The regular expression `ab* + c` denotes

- (A) `{ a b^n | n ≥ 0 } ∪ {c}`
- (B) `{ a b^n c | n ≥ 0 }`
- (C) `{ (ab)^n | n ≥ 0 } ∪ {c}`
- (D) `{ a b^n | n ≥ 0 } ∪ { a c }`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Star binds to `b` only, concatenation binds before union: `(a(b*)) + c`.

**Concept tested:** precedence.
**Difficulty:** Level 1
**Common trap:** (C) attaches the star to `ab`; (D) distributes `a` over the union.
</details>

---

## Level 2 — Standard GATE

### Q5 · MSQ

Over `{a, b}`, which REs denote exactly the strings in which every `a` is immediately followed by `b`?

- (A) `(b + ab)*`
- (B) `b*(abb*)*`
- (C) `(ab + b)*a`
- (D) `(a + b)*ab`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B)

**Solution:** (A): each piece is `b` or `ab`, so every `a` is followed by `b`; conversely a valid string splits uniquely into such pieces. (B): a leading block of `b`s, then blocks `a b b*`; each `a` is followed by at least one `b`, and every valid string decomposes this way. (C) ends in `a`, which is never followed by anything. (D) contains `aab`, whose first `a` is followed by `a`.

**Concept tested:** writing/recognising pattern REs.
**Difficulty:** Level 2
**Common trap:** (D) only constrains the end of the string.
</details>

### Q6 · NAT

Over `{0, 1}`, the number of strings of length at most 3 that are in **neither** `0*1*` nor `1*0*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** At length `n ≥ 1`, `0*1*` has `n + 1` strings, `1*0*` has `n + 1`, and they share `0^n` and `1^n`. Union sizes: `1` (length 0), `2`, `4`, `6`. Totals: `1, 2, 4, 8`. Outside: only at length 3, namely `010` and `101`.

**Concept tested:** inclusion–exclusion per length.
**Difficulty:** Level 2
**Common trap:** forgetting that `ε` is in both, or subtracting the overlap twice.
</details>

### Q7 · MCQ

The unique solution of `X = b + Xa` is

- (A) `a*b`
- (B) `ba*`
- (C) `(a + b)*`
- (D) `b*a`

<details><summary>Answer and solution</summary>

**Answer:** (B)

**Solution:** Arden with the unknown on the left of the coefficient: `X = Q + XP ⇒ X = QP*`, here `Q = b`, `P = a`, and `ε ∉ L(a)`. Check: `b ∈ X`; then `ba`, `baa` by repeated substitution; `ab` is never produced.

**Concept tested:** Arden's theorem, orientation.
**Difficulty:** Level 2
**Common trap:** (A) is the solution of `X = b + aX`.
</details>

### Q8 · MSQ

Which REs denote exactly the binary strings that contain at least one `0` and at least one `1`?

- (A) `(0+1)*0(0+1)*1(0+1)* + (0+1)*1(0+1)*0(0+1)*`
- (B) `(0+1)*01(0+1)* + (0+1)*10(0+1)*`
- (C) `0*1* + 1*0*`
- (D) `(0+1)*(01 + 10)(0+1)*`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** (A) says some `0` occurs before some `1` or vice versa. (B) and (D) are the same language: a string containing both symbols has an adjacent `01` or `10` somewhere (walk from a `0` to a `1`; the symbol changes at some step). (C) contains `ε` and `000`, and misses `010`.

**Concept tested:** adjacency argument; equivalent forms.
**Difficulty:** Level 2
**Common trap:** rejecting (B)/(D) because they "require adjacency".
</details>

### Q9 · NAT

The number of strings of length 5 in `(a + b)*a(a + b)(a + b)` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 16

**Solution:** The RE denotes strings whose third symbol from the end is `a`. At length 5 that position is fixed and the other four are free: `2^4 = 16`.

**Concept tested:** positional REs.
**Difficulty:** Level 2
**Common trap:** counting decompositions of `(a+b)*` as different strings.
</details>

---

## Level 3 — Multi-step reasoning / construction

### Q10 · MSQ

A DFA over `{a, b}` has states `P` (start, only accept) and `Q` with `P --a--> Q`, `P --b--> P`, `Q --a--> P`, `Q --b--> Q`. Which REs denote its language?

- (A) `(b + ab*a)*`
- (B) `(b*ab*a)*`
- (C) `b*(ab*ab*)*`
- (D) `(ab*a)*b*`

<details><summary>Answer and solution</summary>

**Answer:** (A), (C)

**Solution:** `a` toggles between `P` and `Q`; `b` keeps the state. The language is "even number of `a`s". Eliminating `Q` gives the loop `b + ab*a` on `P`: (A). (C) starts with any `b`s and then pairs `a b* a b*`, covering every even-`a` string. (B) cannot end with `b` unless it is empty, so it misses `b`. (D) misses `ba a` = `baa`: the first block must start with `a`, and the `b*` tail cannot contain `a`.

**Concept tested:** DFA → RE by state elimination; checking candidate REs.
**Difficulty:** Level 3
**Common trap:** (B) looks like (A) but forces every block to end in `a`.
</details>

### Q11 · NAT

Treat each binary string as an unsigned number (leading zeros allowed). The number of strings of length exactly 4 whose value is divisible by 3 is ____.

<details><summary>Answer and solution</summary>

**Answer:** 6

**Solution:** Values 0–15 divisible by 3: `0, 3, 6, 9, 12, 15`. The strings are `0000, 0011, 0110, 1001, 1100, 1111`. Each is accepted by the mod-3 DFA, equivalently matched by `(0 + 1(01*0)*1)*`.

**Concept tested:** mod-3 automaton / RE.
**Difficulty:** Level 3
**Common trap:** forgetting `0000` (value 0).
</details>

### Q12 · MCQ

An ε-NFA has start state `s` with ε-edges to `p` and `u`. `p` is accepting; `p --a--> q`, `q --a--> p`. `u` is not accepting; `u --b--> v`, `v --b--> u`, and `v` is accepting. No other edges exist. Its language is

- (A) `(aa)* + b(bb)*`
- (B) `(aa + b)(bb)*`
- (C) `(aa)*b(bb)*`
- (D) `a* + b*`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** The two branches never interact. From `p`, accepting after an even number of `a`s: `(aa)*`. From `u`, accepting at `v` after an odd number of `b`s: `b(bb)*`. ε-edges contribute nothing to strings, so the language is the union.

**Concept tested:** ε-NFA → RE; union via ε-branches.
**Difficulty:** Level 3
**Common trap:** (C) concatenates the branches; (D) ignores parity.
</details>

### Q13 · NAT

Over `{a, b}`, the number of strings of length at most 4 in `a*(ba*ba*ba*)*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 10

**Solution:** The RE denotes strings whose number of `b`s is a multiple of 3 (each block adds exactly three `b`s with arbitrary `a`s). Count by length: `n = 0`: 1; `n = 1`: `a` (1); `n = 2`: `aa` (1); `n = 3`: `aaa`, `bbb` (2); `n = 4`: zero `b`s (1) or three `b`s (`C(4,3) = 4`), total 5. Sum `1 + 1 + 1 + 2 + 5 = 10`.

**Concept tested:** reading a counting RE; counting by cases.
**Difficulty:** Level 3
**Common trap:** thinking the `b`s must be consecutive; the `a*` inside the block allows gaps.
</details>

### Q14 · NAT

The length of the shortest string over `{a, b}` that is **not** in `(a + ba)*b*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 3

**Solution:** Inside `(a + ba)*` every `b` is followed by `a`. The tail `b*` absorbs trailing `b`s. All strings of length ≤ 2 are members (`bb` via the tail, `ba` via a piece, `ab` as `a` then tail). At length 3, `bba` fails: a member beginning with `b` either begins with the piece `ba` (second symbol `a`) or is entirely tail (all `b`).

**Concept tested:** shortest non-member by forced structure.
**Difficulty:** Level 3
**Common trap:** claiming 2 because `bb` "cannot come from `(a + ba)*`" — it comes from the tail.
</details>

---

## Level 4 — Tricky / trap-based

### Q15 · MSQ

Which REs denote `(a + b)*`?

- (A) `(a*b*)*`
- (B) `(a* + b*)*`
- (C) `(a + ba)*`
- (D) `(a + b)*ab(a + b)* + b*a*`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (D)

**Solution:** (A), (B): each single symbol is a piece, so any string is produced. (D): a string either contains `ab` (first term) or does not, and over `{a, b}` the strings avoiding `ab` are exactly `b*a*`. (C) cannot produce a string ending in `b`, e.g. `b`.

**Concept tested:** star-absorption identities; complement decomposition.
**Difficulty:** Level 4
**Common trap:** rejecting (D) because it "looks restrictive".
</details>

### Q16 · NAT

The number of binary strings of length 5 that contain **at least two** `0`s and **no** substring `00` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 7

**Solution:** Strings of length 5 with no `00`: Fibonacci count `F(7) = 13`. Remove those with fewer than two `0`s: no `0` (1 string) and exactly one `0` (5 strings; a single `0` never forms `00`). `13 − 6 = 7`. Direct check: two non-adjacent `0`s among 5 positions, `C(4,2) = 6` (`01011, 01101, 01110, 10101, 10110, 11010`), plus three non-adjacent `0`s, only `01010`.

**Concept tested:** combining "at least two 0s" with "no 00".
**Difficulty:** Level 4
**Common trap:** confusing "at least two 0s" with "contains 00" — here they are almost opposite.
</details>

### Q17 · MCQ

Let `r = (a + b)*a(a + b)*` and `s = b*a(a + b)*`. Which is true?

- (A) `L(r) = L(s)`
- (B) `L(s)` is a proper subset of `L(r)`
- (C) `L(r)` is a proper subset of `L(s)`
- (D) `L(r) ∩ L(s) = ∅`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** Both denote "contains at least one `a`". In `s`, let the literal `a` be the **first** `a` of the string; everything before it is `b*`. So every string of `r` is in `s`, and `s ⊆ r` trivially.

**Concept tested:** choosing the canonical occurrence (first/last) to prove equality.
**Difficulty:** Level 4
**Common trap:** (B) — assuming the more specific-looking RE denotes fewer strings.
</details>

### Q18 · MSQ

Which statements hold for **every** RE `r`?

- (A) `r∅ = ∅`
- (B) `∅* = ε`
- (C) `(r + ε)* = r*`
- (D) `r*r = r*`

<details><summary>Answer and solution</summary>

**Answer:** (A), (B), (C)

**Solution:** (D) fails for `r = a`: `ε ∈ L(a*)` but `ε ∉ L(a*a)`. It holds only when `ε ∈ L(r)`.

**Concept tested:** algebra of `∅`, `ε` and star.
**Difficulty:** Level 4
**Common trap:** treating `r*r` and `r*` as the same because they agree on every non-empty string of `a*`.
</details>

---

## Level 5 — Challenge

### Q19 · NAT

The number of strings of length 6 in `(aa + ab + b)*` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 43

**Solution:** The pieces `b`, `aa`, `ab` form a prefix code (a leading `b` must be the piece `b`; a leading `a` must be `aa` or `ab` according to the next symbol), so each string has one parse and strings correspond to tilings. `t(n) = t(n − 1) + 2t(n − 2)`, `t(0) = t(1) = 1`: `1, 1, 3, 5, 11, 21, 43`.

**Concept tested:** counting via unambiguous decomposition.
**Difficulty:** Level 5
**Common trap:** using the recurrence on an ambiguous RE; here it is valid only because of the prefix property.
</details>

### Q20 · MCQ

Binary strings are read as unsigned numbers (leading zeros allowed). Which RE denotes exactly the strings whose value is congruent to 1 modulo 3?

- (A) `(0 + 1(01*0)*1)* 1 (01*0)*`
- (B) `(0 + 1(01*0)*1)* 1`
- (C) `1(01*0)*(0 + 1(01*0)*1)*`
- (D) `(0 + 1(01*0)*1)*(01*0)*1`

<details><summary>Answer and solution</summary>

**Answer:** (A)

**Solution:** In the mod-3 DFA (`r → (2r + b) mod 3`), split any path from `r0` to `r1` at its **last** departure from `r0` (which is on `1`). Before it: an `r0 → r0` path, `(0 + 1(01*0)*1)*`. After it: `r1 → r1` loops that avoid `r0`, i.e. through `r2` only, `(01*0)*`. (B) misses `100` (value 4). (C) must start with `1`, so it misses `01` (value 1), and it contains `10` (value 2) because its trailing `r0`-loop pieces are read from `r1`, not from `r0`. (D) puts the `(01*0)*` loops before the final `1`, where the machine is in `r0`, not `r1`; it contains `0101` (value 5 ≡ 2) and misses `100`.

**Concept tested:** DFA → RE with a non-start accepting state; last-exit decomposition.
**Difficulty:** Level 5
**Common trap:** assuming the string must end with `1`.
</details>

### Q21 · NAT

For a language `L`, let `L^0 = {ε}` and `L^k = L^{k−1}L`. Over `{a}`, let `L = {ε, aa, aaa} ∪ { a^n | n ≥ 5 }`. The smallest `k ≥ 0` with `L^k = L^{k+1}` is ____.

<details><summary>Answer and solution</summary>

**Answer:** 2

**Solution:** Work with lengths. `L` has lengths `{0, 2, 3, 5, 6, 7, …}`, missing `1` and `4`. `L^0 = {ε} ≠ L^1`. `L^2`: sums of two lengths from `L`; `4 = 2 + 2` appears, `1` cannot. So `L^2` has every length except `1`, and `L^1 ≠ L^2`. `L^3`: still no way to make `1` (only `0` and numbers ≥ 2 are available), so `L^3 = L^2`. Smallest `k` is 2.

**Concept tested:** powers of a language; role of `ε ∈ L` (makes the powers increasing).
**Difficulty:** Level 5
**Common trap:** answering 1 by not noticing the missing length `4` in `L`.
</details>

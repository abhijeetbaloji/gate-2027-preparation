# Regular Expressions — Notes

Syllabus line: *Regular expressions and finite automata* (GATE CS 2027, Section 6).

This topic also hosts the foundations that every later TOC topic uses: alphabets, strings, languages and operations on languages. Read Sections 1–2 even if you already know regular expressions.

## What the PYQs actually test

From the mapped questions (`../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/01-REGULAR-EXPRESSIONS/questions.md`) and RE questions found in the text of the archived papers:

| Pattern | Seen in |
|---|---|
| Pick the RE for an English description (odd number of 1s, contains `00` and `11`, at least two 0s, divisible by 3) | 2021, 2020, 2016, 2009 |
| Pick the RE / ε-NFA for an automaton or token definition | 2024 (ε-NFA), 2023 (identifier token), 2008 (match NFAs), 2007 |
| Count strings of bounded length in or outside an RE language | 2024 (two papers) |
| Shortest string not in an RE | 2014 |
| Operations with `∅` and `{ε}` | 2013 |
| Powers `L^k` of a language | 2018 |

The common thread is **reading** an RE exactly (what it includes and what it misses), not writing long REs from scratch.

---

## 1. Alphabets, strings, languages

**Alphabet `Σ`**: a finite, non-empty set of symbols, e.g. `{0, 1}` or `{a, b}`.

**String (word) over `Σ`**: a finite sequence of symbols from `Σ`.

- `|w|` is the length. `|abba| = 4`.
- `ε` is the empty string, `|ε| = 0`. It is a string, not a symbol of `Σ`.
- `n_a(w)` or `#_a(w)` is the number of occurrences of `a` in `w`.
- Concatenation `xy` writes `x` then `y`. `εw = wε = w`. Concatenation is associative but not commutative.
- `w^k` is `w` concatenated `k` times; `w^0 = ε`.
- `w^R` is the reversal. `(xy)^R = y^R x^R`.
- Prefix of `w`: any `x` with `w = xy`. Suffix: any `y` with `w = xy`. Substring: any `y` with `w = xyz`. `ε` and `w` itself are prefixes, suffixes and substrings of `w`.

Counting facts used constantly:

| Quantity | Value | Why |
|---|---|---|
| Strings of length `n` over `|Σ| = k` | `k^n` | `k` choices per position |
| Strings of length `≤ n` | `(k^{n+1} − 1)/(k − 1)` for `k ≥ 2` | geometric sum |
| Prefixes of a string of length `n` | `n + 1` | one per cut point, including `ε` |
| Non-empty substrings of `w` with all symbols distinct | `n(n+1)/2` | choose start ≤ end; with repeated symbols there can be fewer *distinct* substrings |

**`Σ*`** is the set of all strings over `Σ`, including `ε`. **`Σ+ = Σ* − {ε}`**. `Σ*` is countably infinite (list strings by length, then alphabetically).

**Language over `Σ`**: any subset `L ⊆ Σ*`. Two special languages are always confused:

| | `∅` | `{ε}` |
|---|---|---|
| Number of strings | 0 | 1 |
| `L · ∅` | `∅` | — |
| `L · {ε}` | — | `L` |
| Star | `∅* = {ε}` | `{ε}* = {ε}` |

`∅` is the "zero" of concatenation; `{ε}` is the "one". Mixing them up is the single most common slip in these questions.

## 2. Operations on languages

For languages `L, M`:

- Union `L ∪ M`, intersection `L ∩ M`, complement `L̄ = Σ* − L`, difference `L − M = L ∩ M̄`.
- Concatenation `LM = { xy | x ∈ L, y ∈ M }`.
- Powers: `L^0 = {ε}`, `L^{k} = L^{k−1} L`.
- Kleene star `L* = L^0 ∪ L^1 ∪ L^2 ∪ …`. Always contains `ε`, even when `L = ∅`.
- Positive closure `L+ = L^1 ∪ L^2 ∪ … = LL*`. `L+ = L*` exactly when `ε ∈ L`.
- Reversal `L^R = { w^R | w ∈ L }`.

Why `∅* = {ε}`: the term `L^0 = {ε}` is in the union no matter what `L` is; every higher power `∅^k` for `k ≥ 1` is empty.

**Worked example (pattern seen in 2013).** Let `L1 = ∅`, `L2 = {a}`. Compute `L1 L2* ∪ L1*`.

- `L1 L2* = ∅ · {a}* = ∅` (concatenating with `∅` kills everything).
- `L1* = ∅* = {ε}`.
- Union: `{ε}`.

**Powers of a language and when they stabilise.** If `ε ∈ L` then `L^k ⊆ L^{k+1}` (append `ε`), so the powers grow. They may or may not stop growing.

- `L = {ε} ∪ {a^n | n ≥ 2}`: lengths in `L` are `{0, 2, 3, 4, …}`. A sum of two such numbers is `0` or `≥ 2`, so `L^2 = L`. The powers stabilise at `k = 1`.
- `L = {ε, aa, aaa}`: `L^k` contains lengths `0` and `2 … 3k` (all of them), so `L^k ≠ L^{k+1}` for every `k`. The powers never stabilise, although every `L^k` is finite.
- `L = {a^n | n ≥ 2}` (no `ε`): `L^k = { a^n | n ≥ 2k }`, strictly shrinking. Without `ε` the chain is not even increasing.

When a question defines "the smallest `k` with `L^k = L^{k+1}`", compute the set of **lengths** (for unary languages) or the set of strings at each power, and check `ε ∈ L` first.

## 3. Regular expressions: syntax and meaning

A regular expression (RE) over `Σ` is built by these rules; `L(r)` is the language it denotes.

| RE | Language |
|---|---|
| `∅` | `∅` |
| `ε` | `{ε}` |
| `a` (for `a ∈ Σ`) | `{a}` |
| `r + s` (also written `r | s`) | `L(r) ∪ L(s)` |
| `rs` | `L(r) L(s)` |
| `r*` | `L(r)*` |
| `(r)` | `L(r)` |

Derived notation: `r+ = rr*`, `r? = ε + r`, `Σ` or `(a+b)` for "any symbol".

**Precedence**: star binds tightest, then concatenation, then union. So

- `ab* + c` means `(a(b*)) + c` = `{a, ab, abb, …} ∪ {c}`.
- `ab + c` is `{ab, c}`, not `{ab, ac}`.
- `(ab)*` and `ab*` are different: `(ab)*` contains `abab`; `ab*` contains `abb`.

**Why REs matter**: REs describe exactly the regular languages (Kleene's theorem). Every RE can be turned into an ε-NFA (Section 9) and every finite automaton into an RE (Section 8). That equivalence is what lets lexical analysers specify tokens with REs and run them as DFAs.

## 4. Reading an RE precisely

Method that avoids almost every reading error:

1. **Parse with precedence.** Put explicit brackets around every star and every concatenation group.
2. **List the shortest members.** Write all strings of length 0, 1, 2 (and 3 if cheap). Most wrong options fail here.
3. **Find what is forced.** First symbol? Last symbol? A symbol that must appear? A parity?
4. **Find what is forbidden.** Is there a pattern no member can contain (e.g. `00`)?
5. **State the language in words, then test both directions**: every member satisfies the description, and every string satisfying the description is generated.

**Example.** `(0 + 1)*0(0 + 1)*0(0 + 1)*` (2009 pattern).

- The two literal `0`s must both appear, in that order, with anything between and around.
- So every member has at least two `0`s. Conversely any string with at least two `0`s: let the first two `0`s be the literal ones; the rest fits into the three `(0+1)*` slots.
- Language: *at least two 0s*. It is **not** "contains `00`": `010` is a member.

**Example.** `(1 + 01)*(ε + 0)`.

- Each block `1` or `01` ends in `1`, so between blocks no two `0`s meet. The optional final `0` follows a `1` (or stands alone).
- Language: binary strings with no substring `00`. Check: `ε, 0, 1, 01, 10, 11` are members; `00` is not.

## 5. A library of standard REs (and why each works)

Over `{0, 1}` unless stated.

| Language | RE | Reason |
|---|---|---|
| all strings | `(0+1)*` | |
| contains substring `w` | `(0+1)* w (0+1)*` | |
| ends with `w` | `(0+1)* w` | |
| starts with `w` | `w (0+1)*` | |
| at least `k` 1s | `(0+1)*1(0+1)*1…` (`k` literal 1s) | literal 1s are the first `k` |
| exactly `k` 1s | `0*10*1…0*` (`k` 1s, `k+1` blocks of `0*`) | |
| at most one 1 | `0* + 0*10*` | |
| even number of 1s | `(0*10*1)*0*` or `0*(10*10*)*` or `(0 + 10*1)*` | pair up the 1s |
| odd number of 1s | `0*1(0*10*1)*0*` or `0*(10*10*)*10*` | one unpaired 1 |
| length divisible by 3 | `((0+1)(0+1)(0+1))*` | |
| no `00` | `(1 + 01)*(ε + 0)` | every 0 is followed by 1 or ends the string |
| every 0 followed immediately by 1 | `(1 + 01)*` | |
| contains both `00` and `11` | `(0+1)*(00(0+1)*11 + 11(0+1)*00)(0+1)*` | either `00` occurs first or `11` does |
| at least one 0 and at least one 1 | `(0+1)*(01 + 10)(0+1)*` | a string with both symbols has some adjacent change |
| binary value divisible by 3 (ε allowed) | `(0 + 1(01*0)*1)*` | derived in Section 8 |

Why "contains both `00` and `11`" needs two orders: `0011` and `1100` are both members. Writing only `(0+1)*00(0+1)*11(0+1)*` misses `1100`.

Why `(0+1)*0011(0+1)* + (0+1)*1100(0+1)*` is wrong for that language: it forces `00` and `11` to be adjacent. `00 1 0 11`, i.e. `001011`, is a member of the language but has neither `0011` nor `1100`.

## 6. Algebraic identities

Write `r ≡ s` when `L(r) = L(s)`.

| Identity | Why it holds |
|---|---|
| `r + s ≡ s + r`, `(r + s) + t ≡ r + (s + t)` | union is commutative and associative |
| `r + r ≡ r` | union is idempotent |
| `r + ∅ ≡ r`, `r∅ ≡ ∅r ≡ ∅`, `rε ≡ εr ≡ r` | `∅` is the union identity and concatenation zero; `ε` is the concatenation identity |
| `r(s + t) ≡ rs + rt`, `(s + t)r ≡ sr + tr` | concatenation distributes over union |
| `∅* ≡ ε`, `ε* ≡ ε` | only `L^0` survives |
| `(r*)* ≡ r*`, `r*r* ≡ r*` | concatenating or starring stars adds nothing new |
| `(ε + r)* ≡ r*` | `ε` inside a star is redundant |
| `rr* ≡ r*r ≡ r+`, `r* ≡ ε + rr*` | unrolling the star once |
| `(r + s)* ≡ (r*s*)* ≡ (r* + s*)* ≡ (r*s)*r*` | each side can produce any sequence of `r`-pieces and `s`-pieces |
| `r(sr)* ≡ (rs)*r` | both are `r s r s … r` with one more `r` than `s` |

**Non-identities** (all appear as wrong options):

| Claim | Counterexample with `r = a`, `s = b` |
|---|---|
| `(r + s)* ≡ r* + s*` | `ab` is on the left only |
| `(rs)* ≡ r*s*` | `a` is on the right only; `abab` is on the left only |
| `r*r ≡ r*` | `ε` is on the right only (they agree only if `ε ∈ L(r)`) |
| `(r + s)* ≡ r*s*` | `ba` is on the left only |

**Proving two REs are not equal**: find one string in one and not the other. **Proving they are equal**: show each string of one has a decomposition in the other (or convert both to minimal DFAs and compare; Section 11).

## 7. Arden's theorem

**Statement.** Let `P` and `Q` be REs with `ε ∉ L(P)`. Then the equation `X = Q + XP` has the unique solution `X = QP*`. Symmetrically, `X = Q + PX` has the unique solution `X = P*Q`.

**Why `QP*` is a solution**: substitute: `Q + QP*P = Q(ε + P*P) = Q(ε + P+) = QP*`.

**Why it is the only one** (and why `ε ∉ L(P)` matters): unroll `X = Q + XP` `k` times:
`X = Q + QP + QP^2 + … + QP^k + XP^{k+1}`.
Take any string `w ∈ X` of length `n`. With `k = n`, every string in `XP^{n+1}` has length ≥ `n + 1` because each `P`-piece is non-empty. So `w` lies in `Q + QP + … + QP^n ⊆ QP*`. If `ε ∈ L(P)` the last term can contain short strings and other solutions exist (for `P = ε`, `X = Q + X` is solved by every `X ⊇ Q`).

Which form to use:

- Equations "language **reaching** state `q`" are written `X_q = (sum over p --a--> q of X_p a) + (ε if q is the start)`. The unknown is on the **left** of each term: use `X = Q + XP ⇒ X = QP*`.
- Equations "language **accepted from** state `q`" are written `Y_q = (sum over q --a--> p of a Y_p) + (ε if q is accepting)`. Unknown on the **right**: use `X = Q + PX ⇒ X = P*Q`.

Mixing the two forms (writing `P*Q` when the equation was `Q + XP`) gives the reversed language. For `X = b + Xa` the answer is `ba*`, not `a*b`.

## 8. Finite automaton → RE

### 8.1 State elimination

1. Make sure there is a single start state with no incoming edges and a single accept state with no outgoing edges; add new states with ε-edges if needed.
2. Label each edge with an RE; parallel edges `p → q` labelled `r1`, `r2` merge into `r1 + r2`.
3. Eliminate an intermediate state `q` with self-loop `S` (use `S = ε`'s effect, i.e. `S* = ε`, if no loop). For **every** pair of an incoming edge `p --R1--> q` and an outgoing edge `q --R2--> t`, add the edge `p --R1 S* R2--> t` (merged with any existing `p → t` edge).
4. When only start and accept remain, the label of the edge between them is the RE.

**Worked example: binary numbers divisible by 3.** Reading bit `b` sends remainder `r` to `(2r + b) mod 3`.

| state | on 0 | on 1 |
|---|---|---|
| `r0` (start, accept) | `r0` | `r1` |
| `r1` | `r2` | `r0` |
| `r2` | `r1` | `r2` |

Eliminate `r2`: incoming `r1 --0--> r2`, loop `1`, outgoing `r2 --0--> r1`. New loop on `r1`: `01*0`.

Eliminate `r1`: incoming `r0 --1--> r1`, loop `01*0`, outgoing `r1 --1--> r0`. New loop on `r0`: `1(01*0)*1`, merged with existing loop `0`.

Result: `(0 + 1(01*0)*1)*`. Because `r0` is both start and accept, the language is the star of the `r0` loop. (It includes `ε`, which a question may or may not count as "divisible by 3".)

**Changing the accept state changes the RE.** For remainder 1 (accept `r1`), a path from `r0` to `r1` is: any number of `r0 → r0` loops, then the last departure `r0 --1--> r1`, then `r1 → r1` loops that never return to `r0` (those go through `r2` only). So the RE is `(0 + 1(01*0)*1)* 1 (01*0)*`. Ending with `1` is not required: `100` (= 4) is a member.

### 8.2 State equations (Arden)

Same example as a "reaching" system:

`R0 = ε + R0·0 + R1·1`, `R1 = R0·1 + R2·0`, `R2 = R1·0 + R2·1`.

From the third, `R2 = R1 0 1*` (Arden, `P = 1`). Substitute: `R1 = R0 1 + R1 0 1* 0`, so `R1 = R0 1 (01*0)*`. Substitute: `R0 = ε + R0 (0 + 1(01*0)*1)`, so `R0 = (0 + 1(01*0)*1)*`. Same answer.

**Small check example.** DFA: `A` (start), `B` (accept); `A --0--> A`, `A --1--> B`, `B --0--> A`, `B --1--> B`.
`B = A1 + B1 ⇒ B = A11*`. `A = ε + A0 + B0 = ε + A(0 + 11*0) ⇒ A = (0 + 11*0)*`. So `L = (0 + 11*0)*11*`, which simplifies to `(0+1)*1`: the DFA accepts exactly the strings ending in `1` (being in `B` means the last symbol was `1`).

### 8.3 Checking a candidate RE against an automaton (the usual GATE task)

You rarely need to derive the RE. Faster:

1. Find short strings accepted and rejected by the automaton (length ≤ 3).
2. Strike every option that accepts a rejected string or rejects an accepted one.
3. If two options survive, find what distinguishes them (often a string with a repeated loop, or the empty string) and trace it.

## 9. RE → ε-NFA (Thompson construction)

Inductive construction, each piece has one start and one accept state:

- `a`: `s --a--> f`. `ε`: `s --ε--> f`. `∅`: `s`, `f` with no edge.
- `r + s`: new start with ε-edges to the starts of `N(r)` and `N(s)`; ε-edges from both accepts to a new accept.
- `rs`: ε-edge from accept of `N(r)` to start of `N(s)`.
- `r*`: new start and new accept; ε-edges new-start → start of `N(r)`, new-start → new-accept, accept of `N(r)` → start of `N(r)`, accept of `N(r)` → new-accept.

Why the star needs the bypass edge: `ε ∈ L(r*)` must be accepted even when `N(r)` itself rejects `ε`. Why it needs the back edge: repeating `r` any number of times.

**Reading an ε-NFA for a token** (2023 pattern, identifier `letter (letter | digit)*`): the machine must read exactly one `letter` before any loop, and the loop must allow `letter` and `digit` in any order and any number of times, including zero. Check each candidate machine for: (i) can it accept a lone `digit`? (it must not); (ii) can it accept `letter` alone? (it must); (iii) can it accept `letter digit letter`? (it must).

**ε-NFA with branches** (2024 pattern): if the start state has ε-edges into two separate loops, the language is the union of the two loop languages; ε-edges never contribute symbols. Example: start `--ε-->` a two-state `a`-cycle whose entry is accepting, and `--ε-->` a two-state `b`-cycle whose exit is accepting, accepts `(aa)* + b(bb)*`.

## 10. Counting strings in an RE language

Typical: "number of strings of length `n` (or `≤ n`) in / not in `L(r)`".

Methods, from fastest to safest:

1. **Direct combinatorics** when the RE is a simple pattern. "Third symbol from the end is `a`" over `{a, b}` at length `n ≥ 3`: `2^{n−1}`.
2. **Unambiguous decomposition.** If the RE is a star of pieces that can be parsed in only one way (a prefix code), count tilings. `(aa + ab + b)*` at length `n`: `t(n) = t(n−1) + 2t(n−2)`, `t(0) = t(1) = 1`, giving `1, 1, 3, 5, 11, 21, 43`. The parse is unique because a leading `b` must be the piece `b`, and a leading `a` must be `aa` or `ab` depending on the next symbol.
3. **Complement counting**: strings with no `ab` over `{a, b}` are exactly `b*a*`, so `n + 1` of length `n`.
4. **DFA path counting.** Build a small DFA and count paths of length `n` to accepting states with a table (one row per length). This never double-counts, which is its advantage over counting RE decompositions.

**Ambiguity trap.** For an ambiguous RE (e.g. `(a + b)*a(a + b)*`), counting decompositions over-counts: `aa` has two decompositions but is one string. Count strings, not parses: use complement or a DFA.

**Union of two REs** (2024 pattern): use inclusion–exclusion `|A ∪ B| = |A| + |B| − |A ∩ B|` per length, and identify the overlap explicitly.
Example: over `{0, 1}`, strings of length `≤ 3` outside `0*1* + 1*0*`. Per length `n ≥ 1`, `0*1*` has `n + 1` strings, `1*0*` has `n + 1`, and the overlap is `0^n, 1^n` (2 strings); at `n = 0` both contain only `ε`. Union sizes `1, 2, 4, 6`; totals `1, 2, 4, 8`. Outside: `0, 0, 0, 2` (`010`, `101`). Answer 2.

## 11. Deciding RE equivalence

Equivalence of REs is decidable: convert both to DFAs, minimise, compare (or test emptiness of the symmetric difference). In an exam:

- To refute: one string.
- To confirm: argue both directions in words, or note a known identity from Section 6.
- Beware of options that are equal "except for `ε`" or "except for strings of length 1". Always test `ε` and single symbols.

## 12. Shortest string not in an RE

Enumerate by length. For each length, ask which strings the RE cannot produce, using its forced structure.

Example: `(a + ba)*b*` over `{a, b}`.

- The `(a + ba)*` part can only start with `a` or `ba`. Every `b` in it is followed by `a`.
- The `b*` tail can absorb trailing `b`s.
- Length 0–2: all of `ε, a, b, aa, ab, ba, bb` are members (`bb` from the tail).
- Length 3: `bba` is not a member. A member that starts with `b` either starts the `(a+ba)*` part with `ba` (second symbol `a`) or is entirely in the tail (all `b`). `bba` is neither.
- Answer: length 3.

---

## GATE problem-solving approach

1. **Translate to a property** (forced symbols, forbidden patterns, parity, position).
2. **Test boundary strings** in every option: `ε`, single symbols, the shortest member, a string that just violates the property.
3. **Use complements** for "not containing" and for counting.
4. **For automaton-to-RE options**, trace 3–5 short strings rather than deriving.
5. **For counting**, choose a method that counts each string once.

## Common traps (summary)

- `∅*` is `{ε}`, not `∅`; `L∅ = ∅`, not `L`.
- Precedence: `ab + c` is `{ab, c}`.
- `(r + s)*` is not `r* + s*`; `(rs)*` is not `r*s*`.
- "Contains `00` and `11`" must allow either order and need not have them adjacent.
- "Even number of 1s" includes zero 1s, hence includes `ε` and `000`.
- Divisibility REs: decide whether `ε` counts; leading zeros are usually allowed.
- Counting with an ambiguous RE double-counts.
- In Arden's lemma the side on which `X` appears decides `QP*` versus `P*Q`.

## Edge cases

- `ε` versus `∅` in options: `L(ε) = {ε}` has one string; `L(∅)` has none.
- A star of a language containing only `ε`: `{ε}* = {ε}`.
- REs over a one-letter alphabet describe sets of lengths; every unary regular language is a finite set of lengths plus finitely many arithmetic progressions.

## Connections

- **Finite automata** (02): every RE ↔ ε-NFA ↔ DFA. Minimal DFA counts are often the fastest way to compare REs.
- **Regular languages** (05): closure properties let you build REs for intersections/complements by going through DFAs.
- **Regular grammars** (03): right-linear grammars are another equivalent description.
- **Compiler design**: lexical analysis specifies tokens with REs and runs the minimal DFA.
- **Undecidability** (09): RE equivalence, emptiness and membership are all decidable.

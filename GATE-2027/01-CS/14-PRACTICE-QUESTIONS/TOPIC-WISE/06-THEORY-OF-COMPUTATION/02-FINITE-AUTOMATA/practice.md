# Finite Automata — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question says otherwise, a DFA is complete: from every state there is exactly one transition on every alphabet symbol. An NFA accepts a string when at least one computation reads the whole string and ends in an accept state. The empty string is `ε`.

## Level 1 — Conceptual

## Q1 — MCQ

Consider the DFA over `{0, 1}` with start state `q0`, only accept state `q2`, and transitions

- `δ(q0, 0) = q1`, `δ(q0, 1) = q0`
- `δ(q1, 0) = q2`, `δ(q1, 1) = q0`
- `δ(q2, 0) = q2`, `δ(q2, 1) = q2`

The language of this DFA is

A. all strings that contain the substring `00`  
B. all strings that end with `00`  
C. all strings with an even number of `0`s  
D. all strings in which every `0` is immediately followed by another `0`

---

## Q2 — MCQ

An NFA accepts an input string `w` when

A. every computation on `w` ends in an accept state  
B. at least one computation reads all of `w` and ends in an accept state  
C. more than half of the computations on `w` end in an accept state  
D. the transition on each symbol is forced to be unique

---

## Q3 — NAT

The number of states in the minimal DFA for the binary language of strings that end with `01` is ____.

---

## Q4 — MCQ

In an `ε`-NFA, an `ε`-transition

A. reads a tape symbol called `ε`  
B. changes state without reading an input symbol  
C. may leave only the start state  
D. makes every branch of the automaton deterministic

---

## Q5 — MCQ

Which one of the following statements is true?

A. Some DFA accepts `{a^n b^n | n ≥ 0}`  
B. For every NFA there is a DFA that accepts the same language  
C. If an NFA has `n` states, every equivalent DFA has at least `n` states  
D. Deleting an unreachable state can change the language of a DFA

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

An `ε`-NFA has states `q0, q1, q2, q3` and `ε`-transitions `q0 → q1`, `q0 → q2`, and `q1 → q3` only. The `ε`-closure of `q0` is

A. `{q0}`  
B. `{q0, q1, q2}`  
C. `{q0, q1, q2, q3}`  
D. `{q1, q3}`

---

## Q7 — NAT

Consider the NFA with states `{p, q}`, start state `p`, accept state `q`, and transitions

- `δ(p, 0) = {p}`, `δ(p, 1) = {p, q}`
- `δ(q, 0) = {q}`, `δ(q, 1) = ∅`

The subset construction produces a DFA. The number of reachable states in that DFA, including the start state, is ____.

---

## Q8 — MCQ

The NFA of Q7 accepts

A. all binary strings that contain at least one `1`  
B. all binary strings that end with `1`  
C. all binary strings that contain the substring `10`  
D. all binary strings with an even number of `1`s

---

## Q9 — NAT

The number of states in the minimal DFA for

`{ w ∈ {a, b}* | the number of a's is even and the number of b's is even }`

is ____.

---

## Q10 — MSQ

Let `L` be the binary language of strings that end with `01`. Which of the following strings are in `L`? Select all that apply.

A. `01`  
B. `101`  
C. `011`  
D. `1001`

---

## Q11 — MCQ

With respect to the language of strings that end with `01`, which pair of strings is distinguishable?

A. `1` and `11`  
B. `0` and `10`  
C. `01` and `001`  
D. `ε` and `0`

---

## Level 3 — Multi-Step

## Q12 — NAT

Consider the NFA with states `{A, B, C}`, start state `A`, only accept state `C`, alphabet `{a, b}`, and transitions

- `δ(A, a) = {A, B}`, `δ(A, b) = {A}`
- `δ(B, a) = ∅`, `δ(B, b) = {C}`
- `δ(C, a) = {C}`, `δ(C, b) = {C}`

The number of reachable states in the subset-construction DFA is ____.

---

## Q13 — NAT

The number of states in the minimal DFA for `{ w ∈ {a, b}* | w contains the substring ab }` is ____.

---

## Q14 — MCQ

The NFA of Q12 accepts exactly the strings that contain the substring `ab`. Which statement about that NFA is true?

A. Subset construction can leave two reachable accepting subsets that minimization merges  
B. Subset construction drops a dead state that every equivalent minimal DFA must put back  
C. No accepting subset is reachable from the start subset  
D. This language has an NFA and no DFA

---

## Q15 — MSQ

Which of the following statements are true? Select all that apply.

A. Subset construction always produces a minimal DFA  
B. The minimal complete DFA of a regular language is unique up to renaming of states  
C. Every language accepted by an `ε`-NFA is regular  
D. If an NFA has `n` states, some DFA with at most `2^n` states accepts the same language

---

## Q16 — NAT

The following DFA over `{0, 1}` has start state `q0` and accept states `{q0, q2}`.

- `δ(q0, 0) = q1`, `δ(q0, 1) = q2`
- `δ(q1, 0) = q2`, `δ(q1, 1) = q3`
- `δ(q2, 0) = q3`, `δ(q2, 1) = q0`
- `δ(q3, 0) = q0`, `δ(q3, 1) = q1`

The number of states in the minimal equivalent DFA is ____.

---

## Level 4 — Tricky / Trap-Based

## Q17 — NAT

The number of states in the minimal complete DFA for the binary language of strings with exactly two `1`s is ____.

---

## Q18 — MCQ

An NFA over the alphabet `{a}` has start state `s`. On the symbol `a`, `s` has two transitions: one to an accept state `f` and one to a non-accept state `g`. There are no other transitions. On the input `a`, the NFA

A. rejects, because a rejecting computation exists  
B. accepts, because an accepting computation exists  
C. accepts only if every computation accepts  
D. is illegal, because an NFA cannot have two transitions on the same symbol

---

## Q19 — MSQ

Which of the following statements are true? Select all that apply.

A. In a complete DFA, a state from which no accept state is reachable is distinguishable from a state from which an accept state is reachable  
B. In every subset construction, the empty set of states is reachable  
C. An NFA may have both an accepting computation and a rejecting computation on the same string; the string is still accepted  
D. Unreachable states do not appear in a minimal DFA

---

## Level 5 — Challenge

## Q20 — NAT

The number of strings of length 6 over `{a, b}` that contain the substring `ab` is ____.

---

## Q21 — NAT

The number of states in the minimal DFA for

`{ w ∈ {a, b}* | the third symbol of w is a }`

is ____. Strings of length less than 3 are rejected.

---

## Q22 — NAT

The number of states in the minimal DFA for

`{ w ∈ {a, b}* | the third symbol from the end of w is a }`

is ____. Strings of length less than 3 are rejected.

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | NAT | 3 |
| 4 | MCQ | B |
| 5 | MCQ | B |
| 6 | MCQ | C |
| 7 | NAT | 2 |
| 8 | MCQ | A |
| 9 | NAT | 4 |
| 10 | MSQ | A, B, D |
| 11 | MCQ | D |
| 12 | NAT | 4 |
| 13 | NAT | 3 |
| 14 | MCQ | A |
| 15 | MSQ | B, C, D |
| 16 | NAT | 2 |
| 17 | NAT | 4 |
| 18 | MCQ | B |
| 19 | MSQ | A, C, D |
| 20 | NAT | 57 |
| 21 | NAT | 5 |
| 22 | NAT | 8 |

## Detailed Solutions

### Q1

Answer: A

From `q0`, `1`s do nothing. The first `0` enters `q1`. A second consecutive `0` enters `q2`. Every later symbol stays in `q2`, which is accepting. If the `0` in `q1` is followed by `1`, the machine returns to `q0` and must find a later `00`.

So the accepted strings are exactly those that contain `00` somewhere. The string `001` is accepted and does not end with `00`, so (B) is false. Parity of the number of `0`s is not the state, and a string such as `1001` is accepted even though its first `0` is followed by `1`.

### Q2

Answer: B

Acceptance for an NFA is existential. One accepting run is enough, and other runs on the same string may die or end in a non-accept state. Option (D) is the deterministic restriction, not the definition of acceptance.

### Q3

Answer: 3

The minimal states remember the longest suffix of the input that is still a prefix of `01`.

- `s` : the suffix is empty or ends with `1`
- `t` : the suffix is `0`
- `u` : the suffix is `01` (the only accept state)

The transitions are `s —0→ t`, `s —1→ s`, `t —0→ t`, `t —1→ u`, `u —0→ t`, `u —1→ s`.

Three states are necessary. The strings `ε`, `0`, and `01` are pairwise distinguishable:

- `01 ∈ L` and `ε, 0 ∉ L`, so `z = ε` separates `01` from the other two.
- `ε · 1 = 1 ∉ L` and `0 · 1 = 01 ∈ L`, so `z = 1` separates `ε` from `0`.

A DFA needs at least one state per distinguishable string, so the 3-state machine is minimal.

### Q4

Answer: B

The symbol `ε` in an `ε`-transition is not an input letter. The transition changes state and leaves the input head where it is. It may occur anywhere, and it is one of the features that makes the machine nondeterministic.

### Q5

Answer: B

Every NFA, including every `ε`-NFA, has an equivalent DFA obtained by the subset construction after `ε`-closure. NFAs and DFAs accept exactly the regular languages.

(A) is false because `{a^n b^n | n ≥ 0}` is not regular. (C) is false because an equivalent DFA may have fewer states than a given NFA; the NFA of Q7 is an example once it is minimized, and even a one-state DFA can accept the same language as a larger NFA for `Σ*`. (D) is false because an unreachable state lies on no computation that starts at the start state.

### Q6

Answer: C

The `ε`-closure of a state is the state itself together with everything reachable from it by zero or more `ε`-transitions.

From `q0` the `ε`-moves reach `q1` and `q2`, and from `q1` they reach `q3`. Thus

`ε-closure(q0) = {q0, q1, q2, q3}`.

Option (B) stops before the `ε`-transition out of `q1`.

### Q7

Answer: 2

Start with `{p}`.

- `{p} —0→ {p}`
- `{p} —1→ {p, q}`
- `{p, q} —0→ {p} ∪ {q} = {p, q}`
- `{p, q} —1→ {p, q} ∪ ∅ = {p, q}`

The empty set is not reached. Exactly two subsets are reachable: `{p}` and `{p, q}`.

### Q8

Answer: A

The reachable DFA of Q7 has non-accept state `{p}` and accept state `{p, q}`, and `{p, q}` is a sink. The first `1` moves from `{p}` to `{p, q}`, and every later symbol stays there. Strings with no `1` stay in `{p}`. The language is all binary strings that contain at least one `1`.

It is not “ends with `1`”: the string `10` is accepted. It is not “contains `10`”: the string `1` is accepted. It is not a parity condition: `1` and `11` are both accepted.

### Q9

Answer: 4

The state can be the pair `(parity of a's, parity of b's)`. All four pairs are reachable, and only `(even, even)` is accepting. They are pairwise distinguishable because a suitable string of `a`s and `b`s sends exactly one state of a pair to `(even, even)` and the other elsewhere. For example, `ε` separates the accept state from the other three, `a` separates `(odd, even)` from `(odd, odd)`, and `b` separates `(even, odd)` from `(odd, odd)`.

Hence the minimal DFA has 4 states. No dead state appears: every state can still reach the accept state.

### Q10

Answer: A, B, D

Check the last two symbols.

- `01` ends with `01`.
- `101` ends with `01`.
- `011` ends with `11`.
- `1001` ends with `01`.

So (A), (B), and (D) are in the language.

### Q11

Answer: D

Two strings are distinguishable when some continuation puts exactly one of them into the language.

- `1` and `11` both end with `1`. For every `z`, `1z` and `11z` end with the same two symbols whenever `|z| ≥ 2`, and the short cases `z = ε`, `z = 0`, and `z = 1` also agree. They are equivalent.
- `0` and `10` both end with `0`, so they are equivalent by the same suffix argument.
- `01` and `001` both end with `01`, so they are equivalent.
- `ε · 1 = 1` does not end with `01`, while `0 · 1 = 01` does. Thus `ε` and `0` are distinguishable.

### Q12

Answer: 4

Compute subsets from `{A}`.

- `{A} —a→ {A, B}`, `{A} —b→ {A}`
- `{A, B} —a→ {A, B}`, `{A, B} —b→ {A, C}`
- `{A, C} —a→ {A, B, C}`, `{A, C} —b→ {A, C}`
- `{A, B, C} —a→ {A, B, C}`, `{A, B, C} —b→ {A, C}`

The reachable subsets are `{A}`, `{A, B}`, `{A, C}`, and `{A, B, C}`. There are 4. The empty set is not among them.

The accepted strings are exactly those that contain `ab`. A computation accepts only by entering `C`, and the only entry is `B —b→ C` after a transition `A —a→ B`. That is an occurrence of `ab`. Before that `a`, the run can stay in `A` on every symbol, and after entering `C` every continuation stays in `C`. So the substring can sit anywhere.

### Q13

Answer: 3

A 3-state DFA remembers the progress toward seeing `ab`.

- `s0`: no pending `a` (start state)
- `s1`: the input so far ends with `a`, and `ab` has not yet occurred
- `s2`: `ab` has occurred (accept sink)

Transitions: `s0 —a→ s1`, `s0 —b→ s0`, `s1 —a→ s1`, `s1 —b→ s2`, and `s2` stays in `s2` on both letters.

The three states are distinguishable, so this is minimal.

- `s2` accepts `ε` as a continuation; `s0` and `s1` do not.
- From `s1`, the continuation `b` is accepted. From `s0`, `b` is not.

Fewer than three states cannot remember “nothing yet”, “just saw `a`”, and “already saw `ab`”.

### Q14

Answer: A

Q12 reaches four subsets. The accepting ones are `{A, C}` and `{A, B, C}`.

- both accept
- both go to `{A, B, C}` on `a`
- both go to `{A, C}` on `b`

They have the same accepting continuations, so minimization merges them into the sink `s2` of Q13. The other two subsets remain distinct: `{A, B}` on `b` enters an accept subset, while `{A}` on `b` does not. That leaves 3 states.

(B) is the wrong direction: minimization removes a redundant accept state; it does not add a dead state. All four subsets really are reachable, and the language is regular.

### Q15

Answer: B, C, D

(A) is false: Q12 and Q13 are a counterexample. Subset construction can leave equivalent states unmerged.

(B) is true for the complete minimal DFA. Its states are the Myhill–Nerode classes, so any two minimal complete DFAs are identical up to the names of those classes.

(C) is true: take `ε`-closures and then apply subset construction.

(D) is true: the powerset of an `n`-state NFA has `2^n` states, and the reachable part is no larger.

### Q16

Answer: 2

Track the parity of the number of `0`s read.

- `q0 —0→ q1` flips parity, and `q0 —1→ q2` preserves it.
- `q1 —0→ q2` flips back to even, and `q1 —1→ q3` stays odd.
- `q2 —0→ q3` flips to odd, and `q2 —1→ q0` stays even.
- `q3 —0→ q0` flips to even, and `q3 —1→ q1` stays odd.

The accept states are exactly `q0` and `q2`, the even-parity states. Thus the DFA accepts the strings with an even number of `0`s. The symbol `1` never changes the parity.

Initial partition: accept block `{q0, q2}` and non-accept block `{q1, q3}`.

- `q0` and `q2` both go to the non-accept block on `0` and to the accept block on `1`.
- `q1` and `q3` both go to the accept block on `0` and to the non-accept block on `1`.

The partition is stable, so there are 2 equivalence classes. All four states are reachable, but reachability does not prevent merging. The minimal DFA has the usual two parity states.

### Q17

Answer: 4

Use four states for “zero `1`s”, “one `1`”, “two `1`s”, and “three or more `1`s”.

- `p0 —1→ p1`, `p0 —0→ p0`
- `p1 —1→ p2`, `p1 —0→ p1`
- `p2 —1→ pd`, `p2 —0→ p2`, and `p2` is the only accept state
- `pd` is a rejecting sink on both symbols

The strings `ε`, `1`, `11`, and `111` are pairwise distinguishable, so at least four states are required.

- `11` is in the language and the other three are not.
- `ε · 11 = 11` is in, while `1 · 11 = 111` is not.
- `ε · 11` is in, while `111 · 11` is not.
- `1 · 1 = 11` is in, while `111 · 1` is not.
- `11` is in and `111` is not.
- `ε · 111` is not a needed extra pair: the pairs above already separate `ε` from `111` by `z = 11`, and `1` from `111` by `z = 1`.

The rejecting sink is reachable, for example by `111`, and it cannot be merged with `p0` or `p1`: from either of those, two or one further `1`s still reach the accept state. A complete DFA with only the three states `p0, p1, p2` has nowhere legal to send `p2` on `1`. The minimal complete DFA therefore has 4 states, not 3.

### Q18

Answer: B

The computation `s —a→ f` reads the whole input and ends in an accept state. The other computation ends in `g` and rejects. Existence of one accepting computation is enough, so the NFA accepts `a`. Two transitions on the same symbol are exactly what an NFA is allowed to have; a DFA is not.

### Q19

Answer: A, C, D

(A) is true. If state `p` can reach an accept state by some string `z`, and `d` cannot reach any accept state, then `z` distinguishes `p` from `d`.

(B) is false. In Q7 the empty set is a subset of the state set, but no reachable subset moves to it.

(C) is true. This is the same existential rule as Q18.

(D) is true. An unreachable state is not the target of any string from the start state, so it is not a Myhill–Nerode class of the language. Minimization deletes it. Adding an extra unused copy of a sink and then minimizing removes that copy.

### Q20

Answer: 57

A string over `{a, b}` fails to contain `ab` exactly when every `b` occurs before every `a`, that is, when the string belongs to `b*a*`. If an `a` occurred before a later `b`, those two positions would form the substring `ab`.

There are `2^6 = 64` strings of length 6, and `b*a*` contributes one string for each number of leading `b`s from 0 through 6, hence 7 strings. The number that contain `ab` is `64 − 7 = 57`.

### Q21

Answer: 5

Five states suffice.

- `u0`: nothing read (start)
- `u1`: exactly one symbol read
- `u2`: exactly two symbols read
- `yes`: the third symbol was `a` (accept sink)
- `no`: the third symbol was `b` (reject sink)

From `u0` every symbol enters `u1`, from `u1` every symbol enters `u2`, from `u2` the symbol `a` enters `yes` and `b` enters `no`, and both sinks stay where they are.

These states are necessary because the following strings are pairwise distinguishable.

| String | State it reaches | A continuation that separates it from the next candidate |
|---|---|---|
| `ε` | `u0` | `aa` produces `aa`, still too short to accept |
| `a` | `u1` | `aa` produces `aaa`, which is accepted |
| `aa` | `u2` | `a` produces `aaa`, accepted, whereas `a · a = aa` is not |
| `aaa` | `yes` | `ε` is accepted |
| `bbb` | `no` | `a` stays rejected, whereas `aa · a` is accepted |

Checking the remaining pairs the same way: `ε` is separated from `aa` by `a`, from `aaa` by `ε`, and from `bbb` by `aaa`; `a` is separated from `aaa` by `ε` and from `bbb` by `aa`; `aa` is separated from `bbb` by `a`. No two of the five strings are equivalent, and the machine has only these five states, so it is minimal.

Merging `u0` with `u1`, or either of them with `u2`, loses the count of symbols still needed before position 3. The two sinks cannot merge because one accepts and the other rejects.

### Q22

Answer: 8

Eight states suffice, and eight are necessary.

**Upper bound.** Let each state be a binary string of length 3. Start in `bbb`. On symbol `c`, move from `xyz` to `yzc`. Accept exactly the states whose first symbol is `a`.

After reading a string `w` of length at least 3, the state is the suffix of `w` of length 3, because each step forgets the oldest remembered symbol:

`bbb —c1→ bbc1 —c2→ bc1c2 —c3→ c1c2c3`.

For `|w| ≥ 3`, membership depends only on that suffix: the third symbol from the end is its first symbol. Strings of length less than 3 end in a state whose first symbol is still the padding symbol `b`, so they are rejected, which is correct. Every length-3 state is reached by reading that string. This is an 8-state DFA for the language.

**Lower bound.** The eight strings of length 3 are pairwise distinguishable. If `x` and `y` differ in position `i`, append a string `z` of length `i − 1`. In `xz` and `yz`, the third symbol from the end is the old symbol in position `i`. Exactly one of `xz` and `yz` is accepted.

Therefore there are at least eight Myhill–Nerode classes. The 8-state DFA is minimal. Remembering only the last two symbols would give four states and could not answer a question about the symbol three places from the end.

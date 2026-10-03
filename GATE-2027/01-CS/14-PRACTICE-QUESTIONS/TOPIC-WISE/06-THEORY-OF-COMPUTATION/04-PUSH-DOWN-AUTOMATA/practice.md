# Push-Down Automata — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Transition notation: `δ(q, a, X) = (p, γ)` means “in state `q`, read input `a` (or read nothing if `a = ε`), pop stack symbol `X`, move to `p`, and push the string `γ`”. The leftmost symbol of `γ` becomes the new top. Pushing `ε` only pops. The stack is never empty at the start: it contains the bottom symbol `Z`. A string is accepted only if some computation reads the entire input and then meets the stated acceptance condition.

## Level 1 — Conceptual

## Q1 — MCQ

Which language is accepted by some push-down automaton and by no finite automaton?

A. `a*b*`  
B. `{a^n b^{n+1} | n ≥ 0}`  
C. `(ab)*`  
D. all strings of even length over `{a, b}`

---

## Q2 — MCQ

A PDA accepts by final state when

A. the stack is empty, and the state is ignored  
B. the whole input has been read and the state is an accept state; the stack may still contain symbols  
C. every computation ends in an accept state  
D. the machine stops as soon as it enters an accept state, even if input remains

---

## Q3 — MCQ

Acceptance by empty stack

A. ignores the stack and uses the accept states  
B. requires the whole input to be read and the stack to be empty; accept states are irrelevant  
C. is defined only for deterministic PDAs  
D. accepts only regular languages

---

## Level 2 — Standard GATE Style

## Q4 — MSQ

The PDA below accepts by final state. The only accept state is `qf`. The start state is `q0`.

- `δ(q0, a, Z) = (q0, AZ)`
- `δ(q0, a, A) = (q0, AA)`
- `δ(q0, b, A) = (q1, ε)`
- `δ(q1, b, A) = (q1, ε)`
- `δ(q1, ε, Z) = (qf, Z)`

Which strings are accepted? Select all that apply.

A. `ab`  
B. `aabb`  
C. `aab`  
D. `ε`

---

## Q5 — NAT

On the accepting computation of the PDA in Q4 on input `aaabbb`, the maximum number of symbols on the stack, counting `Z`, is ____.

---

## Q6 — MCQ

Which statement is true?

A. For every PDA, acceptance by final state and acceptance by empty stack define the same language of that machine  
B. Those two modes may define different languages of one machine, but every language accepted by an NPDA in one mode is accepted by some NPDA in the other mode  
C. The two modes define the same language of a machine only when the machine is deterministic  
D. Both modes accept only regular languages

---

## Q7 — MCQ

Which language is accepted by some deterministic PDA?

A. `{a^n b^n c^n | n ≥ 0}`  
B. `{w c w^R | w ∈ {a, b}*}`  
C. `{ww | w ∈ {a, b}*}`  
D. `{a^n b^n c^n d^n | n ≥ 0}`

---

## Level 3 — Multi-Step

## Q8 — MCQ

The PDA below accepts by final state. The accept states are `q0` and `q1`. There is no `ε`-transition.

- `δ(q0, a, Z) = (q0, AZ)`
- `δ(q0, a, A) = (q0, AA)`
- `δ(q0, b, A) = (q1, ε)`
- `δ(q1, b, A) = (q1, ε)`

Its language is

A. `{a^n b^n | n ≥ 0}`  
B. `{a^n b^m | n ≥ m ≥ 0}`  
C. `{a^n b^m | m ≥ n ≥ 0}`  
D. `{a^n b^m | n, m ≥ 0}`

---

## Q9 — MSQ

Which statements are true? Select all that apply.

A. Every language accepted by a PDA is context-free  
B. Every context-free language is accepted by some PDA  
C. Every language accepted by a PDA is regular  
D. `{a^n b^n | n ≥ 0}` is accepted by some deterministic PDA

---

## Q10 — NAT

The number of strings of length 4 in the language of the PDA in Q8 is ____.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

A nondeterministic PDA for even-length palindromes guesses where the middle of the input is. On `abba`, one guess switches from pushing to popping too early and rejects, while another guess switches in the true middle and accepts. The string `abba` is

A. rejected, because a rejecting computation exists  
B. accepted, because an accepting computation exists  
C. outside every context-free language  
D. accepted only if the PDA is deterministic

---

## Q12 — MSQ

Which statements are true? Select all that apply.

A. The intersection of a context-free language and a regular language is context-free  
B. The intersection of two deterministic context-free languages is always deterministic context-free  
C. Every language accepted by a deterministic PDA by empty stack is prefix-free: no string in the language is a proper prefix of another  
D. `{a^n b^n | n ≥ 0} ∪ {a^n c^n | n ≥ 0}` is deterministic context-free

---

## Level 5 — Challenge

## Q13 — MCQ

The PDA below accepts by final state `qf`. The start state is `q0`, and the bottom symbol is `Z`.

- `δ(q0, a, Z) = (q0, XZ)`, `δ(q0, a, X) = (q0, XX)`
- `δ(q0, b, Z) = (q1, XZ)`, `δ(q0, b, X) = (q1, XX)`
- `δ(q0, c, X) = (q2, ε)`, `δ(q0, ε, Z) = (qf, Z)`
- `δ(q1, b, X) = (q1, XX)`, `δ(q1, c, X) = (q2, ε)`
- `δ(q2, c, X) = (q2, ε)`, `δ(q2, ε, Z) = (qf, Z)`

The language is `{a^i b^j c^k | ? }`, where the missing condition is

A. `i = j = k`  
B. `i + j = k`  
C. `i = j + k`  
D. `j = k`

---

## Q14 — MCQ

Which language is **not** context-free?

A. `{a^n b^n | n ≥ 0}`  
B. `{w w^R | w ∈ {a, b}*}`  
C. `{w c w^R | w ∈ {a, b}*}`  
D. `{a^n b^n c^n | n ≥ 0}`

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | MCQ | B |
| 4 | MSQ | A, B |
| 5 | NAT | 4 |
| 6 | MCQ | B |
| 7 | MCQ | B |
| 8 | MCQ | B |
| 9 | MSQ | A, B, D |
| 10 | NAT | 3 |
| 11 | MCQ | B |
| 12 | MSQ | A, C, D |
| 13 | MCQ | B |
| 14 | MCQ | D |

## Detailed Solutions

### Q1

Answer: B

A finite automaton can accept `a*b*`, `(ab)*`, and the even-length strings. It cannot accept `{a^n b^{n+1} | n ≥ 0}`: the strings `a^n` are pairwise distinguishable by the continuation `b^{n+1}`.

A PDA accepts that language by pushing one `A` for each `a`, popping one `A` for each of the first `n` `b`s, and then reading one extra `b` with `Z` on top before accepting. One stack is enough because there is a single unbounded count to match.

### Q2

Answer: B

Final-state acceptance looks at the state after the input has been consumed. Symbols may remain on the stack. It does not require every nondeterministic branch to accept, and it does not accept a proper prefix merely because an accept state occurred in the middle of the input.

### Q3

Answer: B

Empty-stack acceptance looks only at the stack after the input has been consumed. The set of accept states is not part of the condition. Nondeterministic PDAs may use either mode. The languages obtained are exactly the context-free languages, not only the regular languages.

### Q4

Answer: A, B

Invariant: in `q0` the stack is `A^n Z` after `n` leading `a`s, with `A` on top. The first `b` enters `q1` and pops one `A`. Each later `b` pops one `A`. The `ε`-move to `qf` is available only when `Z` is on top, so the number of `b`s must equal the number of `a`s, and that number must be at least 1 because the first `b` requires an `A`.

- `ab`: push `A`, pop `A`, move from `Z` to `qf`. Accepted.
- `aabb`: push twice, pop twice, then move to `qf`. Accepted.
- `aab`: two pushes and one pop leave `AZ`. No move to `qf`, and the input is finished in `q1`. Rejected.
- `ε`: the machine is still in `q0` with stack `Z`, and `q0` is not accept. There is no `ε`-move from `q0`. Rejected.

The language of this machine is `{a^n b^n | n ≥ 1}`.

### Q5

Answer: 4

Start with stack `Z`, height 1.

- first `a` replaces `Z` by `AZ`, height 2
- second `a` replaces `A` by `AA`, height 3
- third `a` replaces `A` by `AA`, height 4, stack `AAAZ`

Each `b` then pops one `A`. The height never exceeds 4. The final `ε`-move does not push an extra symbol; it replaces `Z` by `Z`.

### Q6

Answer: B

The machine of Q4, read by empty stack instead of final state, does not accept `ab`: after the input is consumed the stack still holds `Z`. Popping `Z` as well would accept by empty stack, but that is a different transition. So the two modes can disagree on one machine.

For nondeterministic PDAs the families coincide. From a final-state machine one can build an empty-stack machine that, from an accept state, clears the stack by `ε`-moves, and the construction can be arranged so that this clearing is not confused with an earlier empty stack. The opposite conversion adds a new bottom symbol and a new accept state entered only when the old bottom is popped. Determinism can break these conversions; the claim in (C) is not true in general, and (D) is false because `{a^n b^n | n ≥ 1}` is not regular.

### Q7

Answer: B

(B) has a deterministic PDA. Push every symbol of `w` until the centre marker `c` is read. After `c`, pop and match the input against the stack. The marker tells the machine exactly when to switch from pushing to popping, so no guess is required. Accept by final state when the input ends with only `Z` left.

(A) and (D) are not context-free, so no PDA accepts them. (C), the copy language `{ww}`, is not context-free either: one stack can compare a string with its reverse by the stack's last-in-first-out order, but comparing a string with a later copy in the same order is a different dependency. The pumping lemma for context-free languages separates `{ww}` from the context-free languages; the full quantifier argument is in the pumping-lemma set. The point here is the contrast with (B): the centre marker is what makes the deterministic stack strategy possible.

### Q8

Answer: B

The machine pushes one `A` per `a` while it stays in `q0`. On the first `b` it enters `q1` and pops, and further `b`s keep popping. There is no transition on `a` after a `b`, and no transition on `b` when `Z` is on top.

It accepts if the input ends in `q0` or in `q1`.

- Ending in `q0` means the input is `a^n`, including `ε`, so `n ≥ m = 0`.
- Ending in `q1` means the input is `a^n b^m` with `m ≥ 1` and at least one `A` was available for every `b`. An attempt to pop `Z` has no transition, so `m ≤ n`.

Thus the language is `{a^n b^m | n ≥ m ≥ 0}`.

It is larger than `{a^n b^n}` because `aaab` is accepted with `A`s left on the stack. It does not contain `abb`, where `m > n`. It does not contain every `a^n b^m`, for the same reason.

### Q9

Answer: A, B, D

Nondeterministic PDAs accept exactly the context-free languages, in either acceptance mode. So (A) and (B) are true, and (C) is false: Q4 accepts a non-regular language.

(D) is true. Modify Q4 by making `q0` an accept state and deleting the need for a special empty case: push on `a`, pop on `b`, and accept in the popping state only by an `ε`-move that fires when `Z` is uncovered. More explicitly, a deterministic machine is:

- `q0` is accept, for `ε`
- `δ(q0, a, Z) = (p, AZ)`, and `p` is not accept
- `δ(p, a, A) = (p, AA)`
- `δ(p, b, A) = (r, ε)`, `δ(r, b, A) = (r, ε)`
- `δ(r, ε, Z) = (qf, Z)`, with `qf` accept

There is no choice between an `ε`-move and a symbol move on the same state and stack top: the `ε`-move exists only on `Z`, and the `b`-move exists only on `A`. The machine accepts exactly when the `b`s uncover `Z`.

### Q10

Answer: 3

By Q8 the length-4 strings are `a^n b^m` with `n + m = 4` and `n ≥ m`. The pairs `(n, m)` are `(4, 0)`, `(3, 1)`, and `(2, 2)`. The strings are `aaaa`, `aaab`, and `aabb`. There are 3. The strings `abbb` and `bbbb` have more `b`s than `a`s and are rejected.

### Q11

Answer: B

PDA acceptance is existential, just as NFA acceptance is existential. The successful guess — push `a`, push `b`, then pop `b`, then pop `a` — reads `abba` and can accept. The early guess fails, and that failure does not cancel the successful computation.

The language of even-length palindromes is context-free. The machine just described is nondeterministic because at a state that can both push the next input symbol and start popping, both moves are available. Determinism is a restriction on the transition relation; it is not required for acceptance.

### Q12

Answer: A, C, D

(A) is true. Run the PDA and the DFA in parallel. The stack operations are those of the PDA, and the state is a pair `(pda state, dfa state)`. Accept when the PDA's acceptance condition holds and the DFA is in an accept state. The result is a PDA, so the intersection is context-free. It need not be regular.

(B) is false. Both `{a^n b^n c^m | n, m ≥ 0}` and `{a^n b^m c^m | n, m ≥ 0}` are deterministic context-free: the first matches `a`s with `b`s and then reads any number of `c`s, and the second reads any number of `a`s and then matches `b`s with `c`s. Their intersection is `{a^n b^n c^n | n ≥ 0}`, which is not context-free and therefore not deterministic context-free.

(C) is true. Suppose a deterministic PDA accepts `x` by empty stack, and `x` is a proper prefix of `xy` with `y` nonempty. When `x` has been read the stack is empty, so there is no stack symbol on which a next move could be defined. The deterministic computation cannot continue into `y` and later accept `xy`. Hence no accepted string is a proper prefix of another accepted string.

(D) is true. One deterministic strategy pushes on `a` and lets the first symbol after the `a`s select the check:

- `qs` is accept, so `ε` is accepted. `δ(qs, a, Z) = (p, AZ)`.
- `δ(p, a, A) = (p, AA)`.
- On `b`, pop `A`s in a state `rb`. When `Z` is uncovered, an `ε`-move on stack top `Z` enters an accept state. There is no `b`-transition on `Z`, so this `ε`-move does not compete with a symbol move on the same stack top.
- On `c` instead of `b`, use a separate copy of the same popping behaviour.

A string `a^n` ends in `p`, which is not accept. A string with the wrong number of `b`s or `c`s either gets stuck or finishes outside the accept state. The first symbol after the `a`s makes the choice, so the machine never guesses.

### Q13

Answer: B

Each `a` or `b` increases the number of `X` symbols by one: the first such symbol replaces `Z` by `XZ`, and each later one replaces `X` by `XX`. The state records the phase. The machine must see `a`s, then `b`s, then `c`s; an `a` after a `b`, or a `b` after a `c`, has no transition.

Each `c` pops one `X`. The move to `qf` is an `ε`-move that requires `Z` on top, so it is available only when every `X` has been popped. A branch that takes `δ(q0, ε, Z)` before the input is finished enters `qf` and then has no transition for the remaining input, so that branch dies. The branch that reads the input first still exists. Nondeterminism is used only for that end-of-input check; the count itself is deterministic.

Therefore the accepted strings are exactly `{a^i b^j c^k | i + j = k}`, including `ε` by the direct `ε`-move from `q0` on `Z`.

Checks: `abcc` pushes twice and pops twice, then enters `qf`. `abc` pushes twice and pops once, so an `X` remains and `qf` is not entered. `acc` pushes once; the second `c` sees `Z` in `q2` and has no symbol transition. `bcc` pushes twice and pops twice.

Option (A) rejects the legal string `bcc` (`i = 0`, `j = k = 2`). Option (C) is the opposite count. Option (D) fails on `ac`: that string is accepted, it satisfies `i + j = k`, and it does not satisfy `j = k`.

### Q14

Answer: D

(A) is context-free: `S → aSb | ε`, and Q9 gives a deterministic PDA.

(B) is context-free. The grammar `S → aSa | bSb | ε` generates every even-length palindrome. A PDA pushes the first half and pops the second half, guessing the middle. That guess makes the natural machine nondeterministic; the language is still context-free because the grammar is context-free.

(C) is context-free, and Q7 gives a deterministic PDA. The corresponding grammar is `S → aSa | bSb | c`.

(D) is not context-free. If it were, the pumping lemma for context-free languages would apply. Let `p` be a pumping length and take `s = a^p b^p c^p`. Write `s = uvwxy` with `|vwx| ≤ p` and `|vx| ≥ 1`. The window `vwx` has length at most `p`, so it cannot contain both an `a` and a `c`: those regions are separated by `p` `b`s. Pumping to `uv^2 wx^2 y` changes the count of at least one symbol and leaves at least one of the three counts unchanged. The three exponents are no longer equal, and the pumped string is outside the language. This contradiction shows that no PDA accepts (D).

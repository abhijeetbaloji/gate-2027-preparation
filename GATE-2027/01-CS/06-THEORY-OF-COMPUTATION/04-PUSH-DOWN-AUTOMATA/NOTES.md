# Push-Down Automata — Notes

Syllabus line: *Context-free grammars and push-down automata*.

The mapping file for this folder has **no construction stem** (2009 is compiler matching; 2008 is first-order logic). A 2025 “accepted by a DPDA” question is stored under undecidability. Depth here follows the existing practice file and the CFL questions that need a stack.

## 1. Definition

A (nondeterministic) PDA is

`P = (Q, Σ, Γ, δ, q0, Z, F)`

- `Γ` — stack alphabet; `Z ∈ Γ` is the start stack symbol (bottom)
- `δ(q, a, X) ⊆ Q × Γ*`, where `a ∈ Σ ∪ {ε}` and `X ∈ Γ`

A move `δ(q, a, X) ∋ (p, γ)` means: in state `q`, read `a` (or read nothing if `a = ε`), **pop** `X`, go to `p`, **push** the string `γ`. The leftmost symbol of `γ` is the new top. `γ = ε` means “pop only”.

A **configuration** is `(state, unread input, stack string with top on the left)`.

---

## 2. Two acceptance modes

**By final state.** After the whole input is read, the state is in `F`. The stack may be nonempty.

**By empty stack.** After the whole input is read, the stack is empty. `F` is ignored.

For a *single* machine the two languages may differ. Example: push `A` on `a`, pop `A` on `b`, ε-move to `qf` on seeing `Z` after the `b`s. By final state this accepts `{a^n b^n | n ≥ 1}`. By empty stack, `Z` is still there unless you also pop it — a different transition.

For **NPDAs as a family**, the two modes define the same class: the CFLs. Conversions:

- Final-state → empty-stack: from an accept state, ε-pop the stack (use a fresh bottom marker so you do not empty too early).
- Empty-stack → final-state: pop the old bottom into a new accept state.

Those conversions can destroy determinism.

---

## 3. NPDA = CFG

**Grammar → PDA (empty stack, one state is enough in outline).** Expand a leftmost variable on the stack by ε-moves; match a terminal on the stack against the input. Accept by empty stack.

**PDA → grammar.** Variables `[p X q]` meaning “from `p` to `q`, pop `X` and its descendants”. The construction is in every standard text; GATE asks you to *use* the equivalence, not to write the full table.

So: every language of a CFG has an NPDA, and conversely. Determinism is a restriction on the machine, not on the grammar class.

---

## 4. Deterministic PDA

A PDA is **deterministic** when, for each `(q, X)`,

- at most one move is possible on each letter `a`, and
- an ε-move and a letter-move are never both enabled.

**What DPDAs accept**

- Every regular language (ignore the stack, or keep `Z` and run a DFA in the state).
- `{a^n b^n}`, `{a^n b^m | n ≥ m}`, `{ w c w^R }`, `{a^i b^j c^{i+j}}`.
- **Not** every CFL. `{ww^R}` (no centre marker) needs a guess of the middle. `{a^n b^n} ∪ {a^n b^{2n}}` is a standard DCFL-union that is CFL but not DCFL.

So the 2025 stem “which is accepted by a DPDA?” has the safe correct option **any regular language**. “Any CFL” and “any NPDA language” are the same overclaim. “Any decidable language” is far larger (`{a^n b^n c^n}` is decidable and not CFL).

**Empty-stack languages of a DPDA are prefix-free.** When the stack first empties, no further move is defined, so a proper extension cannot be accepted. Final-state DPDAs do not have this restriction (`a*` is a DCFL and is not prefix-free).

---

## 5. Worked machines

**`{a^n b^n | n ≥ 1}` trace (final state `qf`).**

```
δ(q0, a, Z) = (q0, AZ)     δ(q0, a, A) = (q0, AA)
δ(q0, b, A) = (q1, ε)      δ(q1, b, A) = (q1, ε)
δ(q1, ε, Z) = (qf, Z)
```

On `aabb`: `(q0, aabb, Z) → (q0, abb, AZ) → (q0, bb, AAZ) → (q1, b, AZ) → (q1, ε, Z) → (qf, ε, Z)`. Accepted. On `aab` the machine ends in `q1` with `AZ`; the ε-move is not enabled. On `ε` it stays in `q0` with `Z` (`q0` is not accepting). The ε-move on `(q1, Z)` does not compete with a letter-move on `Z`, so this table is deterministic. An ε-move on `(q0, Z)` *would* compete with the `a`-move and would make the machine an NPDA.

**`{a^n b^n | n ≥ 0}` (DPDA, final state).** Same pops, but make the start state accepting so `ε` is in.

**`{a^n b^m | n ≥ m ≥ 0}`.** Same pushes and pops, but accept in the pushing state (pure `a^n`) *and* in the popping state (leftover `A`s allowed). Reject if a `b` sees `Z` too soon.

**`{a^i b^j c^{i+j}}`.** Push on every `a` and every `b`; pop on every `c`; accept when `Z` is uncovered after the `c`s. One count, two phases of pushing. Nested, not crossed.

**Even palindromes `{ww^R}`.** Push the first half; **guess** the middle (ε-switch); pop and match. Nondeterministic. With a centre letter `c`, the switch is forced: DPDA.

---

## 6. What one stack cannot do

- `{a^n b^n c^n}`: after matching `a`s with `b`s the stack is empty; the `c`s have nothing to compare, and keeping the `a`s would prevent matching the `b`s.
- `{a^n b^m c^n d^m}`: crossed dependencies. Nested `{a^n b^m c^m d^n}` is fine (outer `a`/`d`, inner `b`/`c`).
- `{ww}`: the stack’s LIFO matches a *reverse*, not a copy in the same order.

CFL ∩ regular is CFL: run the PDA and a DFA in parallel (state = pair, stack = PDA stack). DCFL is not closed under union or intersection (`{a^n b^n c^m} ∩ {a^n b^m c^m} = {a^n b^n c^n}`).

## Connections

- CFG (03): the other description of the same family.
- CFL (06): closure and the “one stack / nested pairs” test.
- FA (02): a PDA that never touches its stack is an NFA.
- Undecidability (09): equivalence of two PDAs is undecidable; equivalence of two DFAs is decidable.

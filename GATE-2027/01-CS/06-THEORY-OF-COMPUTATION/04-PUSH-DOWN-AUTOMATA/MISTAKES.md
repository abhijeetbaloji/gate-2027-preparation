# Push-Down Automata — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| One rejecting NPDA branch rejects the string | Acceptance is existential |
| Final-state acceptance requires an empty stack | Stack may hold leftover symbols |
| Empty-stack acceptance uses `F` | `F` is irrelevant in that mode |
| The two modes of one machine coincide | They need not; the families coincide for NPDAs |
| Every CFL has a DPDA | `{ ww^R }` is the standard counter-example |
| `{ ww }` is CFL because `{ ww^R }` is | Same-order copy is not LIFO |
| `{ a^n b^n c^n }` has a PDA with a “two-track stack” | One stack, one unbounded count |
| Every PDA language is regular | `{ a^n b^n }` |
| Empty-stack DPDA can accept `{ a^n b^n \| n ≥ 0 }` | That language is not prefix-free (`ε` prefixes `ab`) |
| Product of two PDAs is a PDA | Only PDA × DFA stays a PDA |

## 2. Trace mistakes

- Writing stack height without the top symbol, then firing a move that does not exist on that top.
- Taking an `ε`-move to an accept state **before** the input is finished and calling that acceptance.
- Forgetting that `Z` is present at height 1, so “maximum stack symbols including `Z`” is one more than the number of `A`’s.
- Treating a DPDA `ε`-move on `Z` as competing with a `b`-move on `A` (different tops: legal) vs competing with a `b`-move on `Z` (same top: illegal in a DPDA).

## 3. Construction mistakes

- Pushing on `a` and popping on `b` with the pushing state non-accepting, then claiming `ε` is accepted.
- Allowing extra `b`’s on `Z` accidentally when the language is `{ a^n b^n }`.
- Building a “DPDA” for `{ ww^R }` that has both a push-move and a pop-move on the same state, letter, and top.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2025 CS2 Q.24 (undecidability mapping) | “Any CFL” or “any NPDA language” as the DPDA family |
| 2009 Q.17 | Matching PDA to code generation or optimisation |
| 2008 Q.30 | Existential quantifier not bound to the FSA `x`; swapped `fsa`/`pda` |

## 5. Examination-time mistakes

- Naming the language after tracing only the matching strings, never `aab` or `abb`.
- Using CFL closure (union) to conclude DCFL (union of DCFLs need not be DCFL).

## 6. How to check yourself

1. Did I write full IDs `(state, remaining input, stack)`?
2. Is the machine deterministic on every `(q, a, X)` including `a = ε`?
3. Which acceptance mode is declared?
4. How many independent counts does the language need?
5. If the stem is a match or a FOL sentence, am I building a machine I was not asked for?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |

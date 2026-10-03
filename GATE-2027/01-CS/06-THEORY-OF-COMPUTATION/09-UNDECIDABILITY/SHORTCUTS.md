# Undecidability — Shortcuts

## 1. Underline the model
- The same English property changes status when the model changes (`L = Σ*` for a DFA vs a CFG vs a TM).

## 2. Syntax vs semantics
- Count states, read the transition table, simulate a **fixed** number of steps: decidable.
- Ask about `L(M)` for a TM: Rice, unless the property is trivial.

## 3. CFG: empty is easy, equal is hard
- Generating variables decide emptiness. Universality / equivalence / ambiguity do not become decidable because membership is.

## 4. Reduction direction
- To show `B` undecidable, reduce a known-undecidable `A` *to* `B` (`A ≤ B`).
- Trap: `B ≤ A` with `A` undecidable says nothing about `B`.

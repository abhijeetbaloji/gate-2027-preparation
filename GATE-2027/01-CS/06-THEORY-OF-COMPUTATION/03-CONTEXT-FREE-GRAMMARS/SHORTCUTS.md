# Context-Free Grammars — Shortcuts

## 1. Count vectors
- **Solves:** “which statement about `#a, #b` is true for every `w ∈ L(G)`?”
- **Why:** each production adds a fixed vector; the generated monoid is the set of sums.
- **Trap:** a relation that holds for the shortest strings may fail after a recursive production.

## 2. CNF length
- **Solves:** 2024-style NAT.
- **Why:** `n−1` binary + `n` terminals.
- **Trap:** using `|V|` or `2n` or `n`.

## 3. Absorb a wrapper
- **Solves:** `S → aSb | X` when `X` already generates a regular “middle”.
- **Why:** extra `a^i … b^i` can be eaten by `X`’s own `a*` / `b*`.
- **Trap:** claiming the wrap makes the language non-regular.

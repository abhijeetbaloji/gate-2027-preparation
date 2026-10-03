# Context-Free Grammars — Notes

Syllabus line: *Context-free grammars and push-down automata*.

Parser tables (LL(1), LALR) are Compiler Design. Several such stems are stored in this mapping file; they are listed as noise in [PYQ.md](PYQ.md). This folder owns the grammar as a generator of a language.

## What the PYQs actually test

| Pattern | Seen in |
|---|---|
| Language of `G` / letter-count invariants | 2026, 2025, 2024 (Q.52), 2023, 2016 |
| CNF derivation length | 2024 (Q.59): `2n − 1` steps for `|w| = n` |
| Ambiguity / number of derivations | 2026 (also filed under undecidability) |
| Linked “balanced `a`/`b`” CFG | 2007 (extract damaged) |

---

## 1. Definition

A context-free grammar is `G = (V, Σ, P, S)`:

- `V` — variables (nonterminals)
- `Σ` — terminals, `V ∩ Σ = ∅`
- `P` — productions `A → α` with `A ∈ V` and `α ∈ (V ∪ Σ)*`
- `S ∈ V` — start symbol

**Context-free** means a variable is replaced *regardless of its neighbours*. A context-sensitive production `a B c → a α c` is not allowed.

A **sentential form** is any string in `(V ∪ Σ)*` reachable from `S`. A **sentence** is a sentential form with no variables. `L(G)` is the set of sentences.

---

## 2. Derivations and parse trees

- **Leftmost:** at every step expand the leftmost variable.
- **Rightmost:** expand the rightmost variable.
- A **parse tree** has the start symbol at the root, variables as internal nodes, terminals (or `ε`) as leaves; the children of `A` are a right-hand side of `A`.

For a given grammar, these three are equivalent descriptions of “how `w` was generated”:

- a parse tree of `w`
- a leftmost derivation of `w`
- a rightmost derivation of `w`

Different trees ↔ different leftmost derivations. That is the definition of ambiguity.

**Worked leftmost vs not.** `S → AB`, `A → aA | a`, `B → bB | b`. Leftmost of `aab`: `S ⇒ AB ⇒ aAB ⇒ aaB ⇒ aab`. Expanding `B` while `A` is still present is not leftmost.

---

## 3. Reading a grammar by invariants

GATE 2023–2026 is this skill.

**Each production adds a vector of letter counts.** If every production preserves a linear relation, every generated string satisfies it. Conversely, check that every string with the relation (and the right shape) is generated.

**Standard family**

| Grammar | Language | Why |
|---|---|---|
| `S → aSb \| ε` | `{a^n b^n \| n ≥ 0}` | each wrap adds one `a` and one `b` |
| `S → aSbb \| ε` | `{a^n b^{2n}}` | one `a`, two `b`s |
| `S → aSb \| aS \| Sb \| ε` | `{a^i b^j}` | independent extra `a`s / `b`s |
| `S → aSbS \| ε` | Dyck / balanced: equal counts and every prefix has `#a ≥ #b` | first-return decomposition |
| `S → SS \| a \| b` | `{a,b}+` | ambiguous |
| `S → aaB \| Abb`, `A → a \| aA`, `B → b \| bB` | `{a^2 b^n \| n ≥ 1} ∪ {a^n b^2 \| n ≥ 1}` | 2025 |

**2023.** `S → aSb | X`, `X → aX | Xb | a | b`. `X` generates every nonempty string of `a*b*` (at least one letter). Wrapping `a^i _ b^i` around such a string still gives `a* (a+b) b*`. The language is regular. The trap is claiming “the wrap makes it `{a^n w b^n}`, hence not regular”.

**2024 `S → aS | aSbS | c`.** Let `A, B, C` be the counts.

- `c` contributes `(0,0,1)`
- `aS` contributes one `a` plus whatever `S` contributes
- `aSbS` contributes one `a`, one `b`, plus two recursive `S`

By induction `C = B + 1` always (one `c` is the unique “root” leaf if you view `aSbS` as combining two trees, and `aS` does not add a `c`). `A ≥ B` can fail to be strict: `acbc` has `A = B = 1`, `C = 2`. So `C = B + 1` is the reliable identity.

**2026-style (mapping extract).**

```
S → aba A B A bba
A → aa B B A b | b B abaa
B → a B b | ab
```

Confirm the first `A`-production against the PDF (`aaBBAb` in the extract).

- `B` generates `{ a^k b^k | k ≥ 1 }`: difference `Δ = n_a − n_b` is `0`.
- Base `A → bBabaa`: terminals contribute three `a`s and two `b`s plus a balanced `B`, so `Δ = 1` and `n_a = 3+k ≤ 2(2+k) = 2 n_b`.
- Recursive `A → aaBBAb`: terminals contribute two `a`s and one `b` plus two balanced `B`s plus one `A`. Each recursive use adds `1` to `Δ`. If the inner `A` satisfies `n_a ≤ 2 n_b`, the new pair still does (the extra `b` and the two `B`s supply enough `b`s).
- `S` wraps two `A`s and one `B` in balanced terminals (`aba`/`bba` together have three `a`s and three `b`s). So every sentence has `n_a > n_b` and `n_a ≤ 2 n_b`.

Do not expand `L(G)`. Lift `Δ` and the factor-2 bound through each production.

**2016-style two grammars.**

`G1`: `S → aS | B`, `B → b | bB` is `{ a^m b^n | m ≥ 0, n ≥ 1 }` (`and`, `n` strictly positive).

`G2`: `S → aA | bB`, `A → aA | B | ε`, `B → bB | ε` is `a+ b* ∪ b+ = { a^m b^n | m > 0 or n > 0 }`. `ε` is out. Options swap `and`/`or` and `≥`/`>`.

**2007-style equal-count grammar** (distinct from Dyck):

`S → aB | bA`, `B → b | bS | aBB`, `A → a | aS | bAA` generates every string with `#a = #b`, including `ba`. `S → aSbS | ε` does **not** generate `ba`.

**Regular grammars are CFGs.** Right-linear `A → aB | a | ε` (and left-linear) generate exactly the regular languages and are unambiguous if they come from a DFA. `S → aSb | ε` is a linear CFG but **not** a regular grammar.

**CNF step count (2024).** In Chomsky normal form a production is `A → BC` or `A → a` (and possibly `S → ε`, unused for `|w| ≥ 1`). A string of length `n ≥ 1` has `n` leaves. Each binary production increases the number of leaves of the tree by 1 (two children replace one variable-as-pending). Starting from 1 (the start symbol), you need `n − 1` binary steps to get `n` pending leaves, then `n` terminal steps. Total **`2n − 1`**. The number of variables in `V` is a red herring. For `w = a^{30}b^{30}c^{30}`, `n = 90`, steps = 179.

---

## 4. Ambiguity

`G` is **ambiguous** if some `w ∈ L(G)` has two different parse trees (two leftmost derivations).

Ambiguity is a property of the *grammar*, not of the language. `{a,b}+` has the unambiguous grammar of a DFA and the ambiguous grammar `S → SS | a | b`.

A language is **inherently ambiguous** if every CFG for it is ambiguous. The standard example is `{ a^i b^j c^k | i = j or j = k }`. (Whether a *given* CFG is ambiguous is undecidable — that fact lives in [../09-UNDECIDABILITY](../09-UNDECIDABILITY).)

**Counting leftmost derivations of `a^n` in `S → SS | a`.** These are Catalan numbers: `d(1) = 1`, `d(n) = Σ_i d(i) d(n−i)`. `d(4) = 5`.

---

## 5. Useless symbols, ε-productions, unit productions

A variable is **generating** if it derives some terminal string (including `ε`). A variable is **reachable** if it appears in some sentential form from `S`. **Useful** = generating and reachable.

**Order:** delete non-generating first (and every production that mentions them), *then* delete variables that are no longer reachable. The opposite order can leave a newly stranded variable.

Eliminating ε-productions, unit productions, and useless symbols **does not change** `L(G)` (except that `S → ε` is kept iff `ε ∈ L`).

---

## 6. Normal forms

**Chomsky (CNF).** `A → BC` or `A → a`. If `ε ∈ L`, allow only `S → ε` and keep `S` off every right-hand side.

**Why CNF is used.** Parse-tree fanout is 2, so height and step counts are controlled; CYK membership is a DP on spans; the `2n−1` count above.

**Greibach (GNF).** `A → a α` with `α` a (possibly empty) string of variables. Every step consumes one terminal, so a derivation of `w` has exactly `|w|` steps. Useful as the bridge to a PDA that reads on every move.

---

## 7. GATE approach

1. Generate the shortest strings and check every option.
2. Write the count change of each production; guess an invariant; prove both directions.
3. For “is `L` regular?”, try to absorb wrappers into a regular expression (`a* (a+b) b*`).
4. For CNF lengths, do not look at `|V|`.
5. Two leftmost derivations of one string ⇒ ambiguous grammar, not “not context-free”.

## Connections

- PDA (04): leftmost derivations ↔ NPDA moves.
- CFL (06): the languages these grammars define.
- Compilers: an unambiguous CFG is a prerequisite for deterministic parsing; the parsing algorithms themselves are a different subject.

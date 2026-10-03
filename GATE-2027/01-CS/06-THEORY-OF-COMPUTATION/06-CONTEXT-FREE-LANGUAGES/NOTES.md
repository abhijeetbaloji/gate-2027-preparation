# Context-Free Languages — Notes

Syllabus line: *Context-free grammars and push-down automata. Regular and context-free languages, pumping lemma.* (GATE CS 2027, Section 6).

A language is context-free when some CFG generates it, equivalently when some NPDA accepts it. Grammars: `03-CONTEXT-FREE-GRAMMARS`. Machines: `04-PUSH-DOWN-AUTOMATA`. Non-membership proofs that need pumping: `07-PUMPING-LEMMA`.

## What the PYQs actually test

From the mapped questions (`../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/06-CONTEXT-FREE-LANGUAGES/questions.md`):

| Pattern | Seen in |
|---|---|
| Two similar `{a^m b^? c^{m+n}}` languages: one CFL, one not | 2025 CS1 Q.45 |
| Closure with mixed regular / CFL operands; which combination is **not** necessarily CFL | 2021 Q.1 (extract garbled) |
| Algebra of complements / De Morgan identities with one regular and one CFL | 2021 Q.12 (extract destroyed — PDF required) |
| Closure of two CFLs and a regular: union yes, complement no, CFL−regular yes, CFL∩CFL no | 2017 Q.4 (extract damaged: bar on complement dropped) |
| `P` regular, `Q` CFL, `Q ⊆ P`: which of `P∩Q`, `P−Q`, `Σ*−P`, `Σ*−Q` is always regular | 2011 Q.24 |

The common job is **counting how many independent agreements a stack (or a CFG) can enforce**, then applying the closure table.

---

## 1. Definition and the Chomsky slot

A language `L ⊆ Σ*` is **context-free (CFL)** if `L = L(G)` for some CFG `G`, iff `L` is accepted by some NPDA.

```
finite ⊂ regular ⊂ DCFL ⊂ CFL ⊂ CSL ⊂ recursive ⊂ RE
```

Each inclusion is proper. Witnesses used in this folder:

- regular but infinite: `a*`
- DCFL not regular: `{ a^n b^n }`
- CFL not DCFL: `{ ww^R }`
- not CFL: `{ a^n b^n c^n }`, `{ ww }`, `{ a^n b^m c^n d^m }`

Deterministic CFL (DCFL) = languages of DPDAs (final-state acceptance). Regular ⊂ DCFL is proper, DCFL ⊂ CFL is proper. Details in `04`.

## 2. Nested vs crossed dependencies

A CFG / one stack can match **nested** or **sequential** pairs. It cannot match **crossed** pairs.

| Language | Shape | CFL? | Why |
|---|---|---|---|
| `{ a^n b^n c^m d^m }` | sequential pairs | yes | `S → XY`, `X → aXb \| ε`, `Y → cYd \| ε` |
| `{ a^n b^m c^m d^n }` | nested pairs | yes | `S → aSd \| T`, `T → bTc \| ε` |
| `{ a^n b^n c^m }` | one pair plus a regular tail | yes | `S → TC`, `T → aTb \| ε`, `C → cC \| ε` |
| `{ a^n b^m c^n }` | `a` with `c`, free `b` | yes | `S → aSc \| T`, `T → bT \| ε` |
| `{ a^n b^m c^n d^m }` | crossed pairs | **no** | a window of length `p` in `a^p b^p c^p d^p` cannot repair both equalities; one stack stores LIFO, so `a` paired with `c` fights `b` paired with `d` |
| `{ a^n b^n c^n }` | two agreements on one count | **no** | three blocks |
| `{ ww \| w ∈ {a,b}* }` | copy in the same order | **no** | stack would have to compare `w` with `w`, not with `w^R` |
| `{ ww^R }` | copy reversed | yes | `S → aSa \| bSb \| ε` |
| `{ w c w^R }` | marked reverse copy | yes (DCFL) | centre marker |

**Worked grammar: sequential pairs.** `X` matches `a` with `b` and empties the obligation before `Y` matches `c` with `d`. One stack, two phases.

**Worked grammar: nested pairs.** The outer `a … d` is pushed first and popped last; the inner `b … c` uses the stack in between.

**Why the crossed language fails (pointer).** The pumping argument belongs in `07-PUMPING-LEMMA`. The one-stack picture is enough to *guess* “not CFL”: after reading `a^n b^m` the stack holds some encoding of `(n, m)`, and popping on `c^n` destroys the information needed for `d^m`.

`{ ww }` intersected with the regular language `a* b* a* b*` is `{ a^n b^m a^n b^m }`, the same crossed shape. So `{ ww }` is not CFL.

Unary copy `{ a^n a^n } = { a^{2n} }` **is** regular. The alphabet size matters.

## 3. Closure properties of CFL

| Operation | Closed? | Construction / counter-example |
|---|---|---|
| union | yes | new start `S → S1 \| S2` (disjoint variables) |
| concatenation | yes | `S → S1 S2` |
| Kleene star | yes | `S → S1 S \| ε` |
| reversal | yes | reverse every right-hand side |
| homomorphism / substitution | yes | replace each terminal by a CFG for its image |
| intersection with a **regular** language | yes | PDA × DFA (product); the stack is the PDA’s stack |
| intersection of two CFLs | **no** | `{ a^n b^n c^m } ∩ { a^n b^m c^m } = { a^n b^n c^n }` |
| complement | **no** | if it were, De Morgan plus union would give intersection |
| difference of two CFLs | **no** | `L1 − L2 = L1 ∩ complement(L2)` |
| CFL − **regular** | **yes** | `L − R = L ∩ complement(R)`, and `complement(R)` is regular, then product |
| regular − CFL | **no** | take the regular language `Σ*`; this is complement of a CFL |

Homomorphism images of CFLs are CFLs; **inverse** homomorphism also preserves CFL (useful, rarely asked).

**CFL ∩ regular is CFL but not always regular.** `{ a^n b^n } ∩ a* b* = { a^n b^n }`.

## 4. Both a language and its complement can be CFL without the language being regular

A common false slogan is “if `L` and `complement(L)` are CFL then `L` is regular”. It is false for CFL. It is also false if you replace CFL by DCFL: DCFL is closed under complement, so every DCFL has a DCFL complement, and `{a^n b^n}` is DCFL but not regular. The slogan that *is* true is the regular one: `L` is regular if and only if `complement(L)` is regular.

Over `{a, b}`, `L = { a^n b^n | n ≥ 0 }` is CFL and not regular. Its complement is the union of

- the regular language of strings not in `a* b*`, namely `(a+b)* ba (a+b)*`, and
- `{ a^i b^j | i ≠ j }`, which has the CFG

```
S → T | U
T → aTb | A        A → aA | a      (more a’s than b’s)
U → aUb | B        B → bB | b      (more b’s than a’s)
```

Union of CFLs is CFL, so `complement(L)` is CFL. This is the standard counter-example.

(The complement of `{ a^n b^n c^n }` is also CFL — strings outside `a*b*c*`, plus `a*b*c*` with a broken equality — while `{ a^n b^n c^n }` itself is not CFL. That pair shows CFL is not closed under complement without going through De Morgan.)

## 5. DCFL closures (the deterministic slice)

| Operation | DCFL closed? |
|---|---|
| complement | yes |
| intersection with regular | yes |
| union | **no** |
| intersection | **no** |
| concatenation, star | **no** |

`{ a^n b^n } ∪ { a^n c^n }` **is** DCFL: the letter after the `a`s selects which match to run. `{ a^n b^n } ∪ { a^n b^{2n} }` is CFL and **not** DCFL (both arms continue with `b`). `{ a^n b^n c^* } ∪ { a^* b^n c^n }` is the three-block union that is CFL and not DCFL.

Empty-stack DCFL (DPDA by empty stack) is a proper subclass and is prefix-free; see `04`.

## 6. Identifying CFL vs not CFL on GATE stems

**One comparison plus a regular free part:** CFL. `{ a^n b^n c^m }`, `{ a^n b^m c^n }`, `{ a^i b^j c^{i+j} }`.

**Two comparisons that nest or run in sequence:** CFL. `{ a^n b^n c^m d^m }`, `{ a^n b^m c^m d^n }`.

**Two comparisons that share a count or cross:** not CFL. `{ a^n b^n c^n }`, `{ a^n b^m c^n d^m }`, `{ ww }`.

**Worked example (2025 pattern, relabelled in NOTES so the method is visible).**

Let `Σ = {a, b, c}` and `m, n ≥ 1`.

`L2 = { a^m b^n c^{m+n} }`.

Grammar:

```
S → a S c | T
T → b T c | b c
```

At least one `aSc` (so `m ≥ 1`) and `T` contributes at least `bc` (so `n ≥ 1`). PDA: push on `a` and on `b`, pop on `c`, accept when the stack returns to the bottom and at least one `a` and one `b` occurred. One stack, one equality ` #c = #a + #b `. **CFL.**

`L1 = { a^m b^m c^{m+n} | m, n ≥ 1 } = { a^m b^m c^m } · c+`.

This asks for `#a = #b` **and** `#c ≥ #a + 1`. After a PDA has matched `a`’s against `b`’s the stack is empty, so it cannot still enforce a lower bound that depends on `m`. Pushing two stack symbols per `a` and popping one per `b` leaves `m` symbols, which can then constrain `#c`, **but** the same machine then accepts strings with `#b ≠ #a` unless a second check is added — which a single stack cannot do. CFG attempt `S → aSc | T` produces `a^i T c^i`; `T` would still have to generate `b^i c^{n}` with `n ≥ 1`, i.e. `T` would have to know `i`. That is a third copy of the same count.

Pumping pointer (full quantifiers in `07`): take `w = a^p b^p c^{2p}` with `p` a pumping length. A window of length `≤ p` sits in at most two adjacent blocks, so pumping down changes `#a` or `#b` without the other, or reduces `#c` to at most `p`, which violates `#c ≥ #a + 1` when `#a = #b = p`. Hence `L1` is not CFL.

Concatenation with a regular language does **not** automatically preserve non-CFL-ness, so “`{a^n b^n c^n}` is not CFL, therefore `{a^n b^n c^n} · c+` is not CFL” is not a proof by itself. The pumping (or the two-agreement) argument is.

## 7. Mixed regular / CFL operands

Let `R` be regular and `C` a CFL.

| Expression | Always CFL? | Reason |
|---|---|---|
| `R ∪ C`, `R C`, `C R`, `C*` | yes | regular languages are CFLs; CFL closed under union, concat, star |
| `R ∩ C` | yes | product |
| `C − R` | yes | `C ∩ complement(R)` |
| `R − C` | **no** | `Σ* − C` is the case `R = Σ*` |
| `C1 ∩ C2` | **no** | three-block intersection |
| `complement(C)` | **no** | same |

**2011 pattern.** `P` regular, `Q` CFL, `Q ⊆ P`.

- `P ∩ Q = Q`, which need not be regular (`Q = { p^n q^n } ⊆ p* q* = P`).
- `P − Q` need not be regular (same example: `p* q* − { p^n q^n }`).
- `Σ* − P` is the complement of a regular language, hence **always regular**.
- `Σ* − Q` is the complement of a CFL, not always regular (not even always CFL).

The subset hypothesis is a trap: it makes `P ∩ Q` look like it might become regular, and it does not.

**2017 pattern (what the intact stem asks).** `L1, L2` any CFLs, `R` any regular.

- `L1 ∪ L2` is CFL.
- `complement(L1)` is not necessarily CFL. The mapping extract dropped the complement bar and printed “`L1` is context-free”, which is a tautology; use the PDF.
- `L1 − R` is CFL.
- `L1 ∩ L2` is not necessarily CFL.

**2021 Q.1 pattern.** `L1` regular, `L2` CFL. Union, concatenation, and `L1 ∩ L2` are CFL. `L1 − L2` is not necessarily CFL. The extract is OCR-garbled; the PDF is the source.

**2021 Q.12 pattern.** The mapping extract is destroyed (no options). The kind of question GATE asks in that slot is “simplify each option with set identities, then apply the table”: e.g. `complement(complement(L1) ∪ complement(L2)) = L1 ∩ L2`, which is CFL when `L1` is regular; `L1 ∪ (L2 ∪ complement(L2)) = Σ*`; `(L1 ∩ L2) ∪ (complement(L1) ∩ L2) = L2`; while `L1 ∩ complement(L2)` need not be CFL. Confirm the actual options on the PDF; do not memorise a reconstructed option list as if it were the extract.

## 8. GATE problem-solving approach

1. Count independent unbounded equalities. One (possibly with a regular free block, or nested/sequential pairs) → CFL. Two on the same exponent, or crossed pairs, or an unmarked copy → not CFL.
2. Write a two-line CFG when the answer is “CFL”, or name the PDA strategy (push on the first block, pop on the matching block).
3. For closure, rewrite the expression (`L − R = L ∩ complement(R)`, `R − L = R ∩ complement(L)`) **before** applying the table. Complement binds to the nearest language.
4. “Always” means “for every pair of languages of those types”. One counter-example kills “always”. “Not necessarily” is the matching positive claim.
5. If both `L` and `complement(L)` are CFL, do not conclude that `L` is regular.
6. Destroyed extracts: open the PDF named in the mapping. Do not invent the missing bars and options.

## Common traps (summary)

- `{ a^n b^n c^m }` is CFL; `{ a^n b^n c^n }` is not. The free index is the whole difference.
- `{ a^n b^m c^n d^m }` vs `{ a^n b^m c^m d^n }`: only the second is CFL.
- `{ ww }` vs `{ ww^R }`.
- CFL − regular **is** CFL; regular − CFL **need not** be.
- Intersection with regular **is** CFL; intersection of two CFLs **need not** be.
- `Q ⊆ P` with `P` regular does not make `Q` regular.
- Concatenating a non-CFL with a regular language is not an automatic non-CFL proof.
- DCFL closed under complement does not make CFL closed under complement.

## Edge cases

- `∅` and `{ε}` are regular, hence CFL.
- Every regular language is a CFL; a question that asks for “CFL but not regular” must exclude `a* b*` and friends.
- Finite languages are regular. `{ a^n b^n c^n | n ≤ 1000 }` is regular.
- Over a unary alphabet, CFL = regular (Parikh / pumping). `{ a^{n^2} }` is not CFL.

## Connections

- **CFG** (`03`): existence of a grammar is the definition used on paper.
- **PDA** (`04`): existence of an NPDA is the other definition; DPDA = DCFL.
- **Regular languages** (`05`): the inner class; DFA product is how `CFL ∩ regular` is proved.
- **Pumping lemma** (`07`): the proof tool for the “not CFL” cells of the table.
- **Undecidability** (`09`): emptiness of a CFG is decidable; whether `L(G1) = L(G2)`, whether `L(G) = Σ*`, whether `L(G1) ∩ L(G2) = ∅` are not.

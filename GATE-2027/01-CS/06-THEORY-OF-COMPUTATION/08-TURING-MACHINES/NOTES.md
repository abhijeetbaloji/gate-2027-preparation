# Turing Machines — Notes

Syllabus line: *Turing machines and undecidability*.

This folder owns the machine and the two language classes it defines (decidable / RE). The decision problems *about* machines and grammars are in [../09-UNDECIDABILITY](../09-UNDECIDABILITY). Complexity (P/NP) is not a TOC syllabus line.

## What the PYQs actually test

| Pattern | Seen in |
|---|---|
| What “`M` decides `L`” means | 2026 |
| Which machine class accepts which language | 2011 (`0^p 1^q` regular; `0^p 1^p` CFL; `0^p 1^p 0^p` not CFL; TM accepts all three) |
| `{a^p \| p prime}` | 2008 (not regular, not CFL, TM-acceptable) |

2011 Q.18 in this mapping file is a probability stem (noise).

---

## 1. The machine

A TM has a finite control, a tape that is infinite in at least one direction, and a head.

A move, from state `q` scanning `a`, writes a symbol, moves L or R, and changes state. The input starts on the tape, head on the leftmost input cell, blanks `⊔` elsewhere.

**Configuration:** (state, full tape contents, head position). Enough to resume the computation.

**Resources.** States, tape alphabet, and accept/reject states are finite. The **tape** is the unbounded resource. That is why a TM can accept `{a^n b^n c^n}` (count, then compare) and `{a^p | p prime}` (check that the length is prime).

---

## 2. Decides vs recognizes

Three outcomes on an input: accept, reject, or loop forever.

**`M` recognizes (accepts) `L`** when

- every `w ∈ L` makes `M` halt and accept, and
- every `w ∉ L` is *not* accepted ( `M` may reject or loop).

`L` is **recursively enumerable (RE, Turing-recognizable)**.

**`M` decides `L`** when

- `M` **halts on every input**, and
- `M` accepts exactly the strings in `L` and **rejects** every string outside `L`.

`L` is **decidable (recursive)**.

**2026.** “`M` decides `L ⊆ {0,1}*`” is equivalent to: `M` accepts every string in `L` **and** rejects every string in `{0,1}* − L`. Not equivalent to “halts on all strings” (it could decide the wrong language). Not equivalent to “accepts all of `L`” (it could loop outside `L`). Not equivalent to “rejects the complement” alone.

A recognizer that happens to halt on every yes-instance is still only a recognizer unless it also halts on the no-instances.

---

## 3. Closure of the two classes

|  | Decidable | RE |
|---|---|---|
| complement | **yes** (swap accept/reject; still halts) | **no** (`A_TM` is RE, its complement is not) |
| union, intersection | yes | yes (dovetail two recognizers; for intersection wait until both have accepted) |
| concatenation, star | yes | yes |

**Both `L` and `L̄` RE ⇔ `L` decidable.** Dovetail a recognizer for `L` with one for `L̄`. Exactly one accepts; halt with that answer.

---

## 4. Variants that do not add languages

- **Multi-tape TMs** accept exactly the RE languages. One tape can store all tapes, marked heads, and simulate a step by a sweep. (Time changes; the language class does not.)
- **Nondeterministic TMs** accept exactly the RE languages. A deterministic TM dovetails all branches by depth. (For *decidable* languages the same is true: an NTM decider can be simulated with a halt on every input, though the simulation is more delicate. GATE’s usual fact: NTM = TM as language acceptors.)

---

## 5. Standard languages

**`A_TM = { ⟨M, w⟩ | M accepts w }`.**

- RE: simulate `M` on `w`; accept if that simulation accepts.
- Not decidable: if a decider `H` existed, build `D` that on `⟨M⟩` runs `H` on `⟨M, ⟨M⟩⟩` and flips the answer. Then `D` accepts `⟨D⟩` iff it does not.

**`HALT = { ⟨M, w⟩ | M halts on w }`.** RE (simulate and accept if the simulation ever stops). Not decidable (reduce `A_TM` to it: make `M'` loop instead of reject).

**`E_TM = { ⟨M⟩ | L(M) = ∅ }`.** Not even RE. Its complement (non-emptiness) is RE: dovetail over all strings and step counts. If emptiness were also RE, non-emptiness would be decidable.

**`{a^p | p prime}`.** Decidable: on `a^n`, test whether `n` is prime (try divisors up to `√n`). Not regular (unary pumping / gaps between primes). Not CFL (CFL pumping on a unary language gives an arithmetic progression).

**2011.** `L1 = {0^p 1^q}` regular (`0*1*`). `L2 = {0^p 1^p}` CFL. `L3 = {0^p 1^p 0^p}` not CFL (two agreements). A TM decides all three. A PDA accepts `L1` and `L2`, not `L3`. “All three are CFL” is the false statement.

---

## 6. Hierarchy

```
regular ⊂ CFL ⊂ decidable ⊂ RE ⊂ all languages
```

- Every regular language is decidable: run the DFA for `|w|` steps.
- Every CFL is decidable: CYK (or a bounded search for a leftmost derivation in GNF / CNF).
- `{a^n b^n c^n}` shows decidable ⊈ CFL.
- `A_TM` shows RE ⊈ decidable.
- `complement(A_TM)` is not RE.

## 7. GATE approach

1. Decide whether the stem is about *halting on every input* (decidable) or *accepting the yes-instances* (RE).
2. A language given by a finite check on `|w|` or a CFG is decidable.
3. “TM accepts all three” is almost always true of the standard counting languages; “PDA accepts all three” is not.
4. Trace questions: write the tape, head, state after each move. Count moves until the accept state is *entered*.

## Connections

- [Undecidability](../09-UNDECIDABILITY/NOTES.md): reductions, Rice, the table by model.
- [Context-free languages](../06-CONTEXT-FREE-LANGUAGES/NOTES.md): every CFL is decidable — “`L(G)` is an undecidable language” is false for a CFG `G`.
- [Context-free grammars](../03-CONTEXT-FREE-GRAMMARS/NOTES.md): CNF and the `2n−1` derivation count used by CYK.
- [Push-down automata](../04-PUSH-DOWN-AUTOMATA/NOTES.md): a TM can decide languages (such as `{a^n b^n c^n}`) that no PDA accepts.

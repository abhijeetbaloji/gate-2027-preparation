# Undecidability — Notes

Syllabus line: *Turing machines and undecidability*.

Name the **model** first. A fact proved for Turing machines is not a fact about DFAs or CFGs.

## What the PYQs actually test

The mapping is thick and noisy. Recognizable stems ask a decidability table, a reduction / Rice application, or a bounded-step TM property. Compiler, NP-complete, and architecture blocks are listed in [PYQ.md](PYQ.md).

Recurring jobs:

- DFA / RE problems are decidable; CFG emptiness and membership are decidable; CFG equivalence, universality, ambiguity are not; TM language properties are not.
- “Runs more than a fixed `k` steps on every / some input” **is** decidable (2022, 2021).
- Rice applies to properties of `L(M)`, not to “`M` has five states”.
- Every language in NP is decidable (2015). That one sentence is the only complexity fact this folder needs.

---

## 1. The three kinds of problem

A decision problem is a language of encodings.

| Class | Meaning | Example |
|---|---|---|
| decidable | some TM **halts** on every instance with the correct yes/no | DFA emptiness |
| RE but not decidable | a recognizer exists; no decider | `A_TM`, TM non-emptiness, CFG non-equivalence |
| not RE | no recognizer | TM emptiness, CFG equivalence, `complement(A_TM)` |

`L` decidable ⇔ `L` and `L̄` both RE.

---

## 2. Reductions

A **many-one reduction** `A ≤ B` is a computable `f` with `x ∈ A ⇔ f(x) ∈ B`.

Valid inference: if `A ≤ B` and `A` is undecidable, then `B` is undecidable. (A decider for `B` would decide `A` by first computing `f`.)

**Direction trap.** `A ≤ B` and `B` undecidable does **not** make `A` undecidable. Every decidable `A` reduces to `A_TM` (map yes-instances to a fixed yes of `A_TM` and no-instances to a fixed no).

**Worked: `A_TM ≤` TM-non-emptiness.** From `⟨M, w⟩` build `M'` that **ignores its input**, simulates `M` on `w`, and accepts (on every input) iff that simulation accepts. Then `L(M') ≠ ∅` iff `M` accepts `w`. The map `⟨M, w⟩ ↦ ⟨M'⟩` is computable.

---

## 3. Rice’s theorem

Any **nontrivial semantic** property of RE languages is undecidable.

- **Semantic:** the answer depends only on `L(M)`, not on how `M` is written. Two machines with the same language get the same answer.
- **Nontrivial:** at least one RE language has the property and at least one does not.

So “is `L(M)` empty / finite / regular / `Σ*` / infinite / a CFL?” are all undecidable.

**Not Rice:** “Does `M` have at most 10 states?” — read the encoding. Two equivalent machines can have different sizes, so this is not a property of `L(M)`.

---

## 4. The table by model

### Regular / DFA / NFA / RE

All of the following are decidable.

| Problem | Why |
|---|---|
| membership | run the DFA for `\|w\|` steps |
| emptiness | is an accept state reachable from the start? |
| finiteness | is there a cycle on a path from start to an accept state? |
| equivalence | minimize both, or test emptiness of the symmetric difference |
| universality (`L = Σ*`) | emptiness of the complement |
| infiniteness | the cycle test above |

NFA / RE problems reduce to DFA problems (determinize / convert).

### Context-free / CFG / PDA

| Problem | Status | Why |
|---|---|---|
| membership | decidable | CNF + CYK |
| emptiness | decidable | generating variables; is `S` generating? |
| finiteness | decidable | after deleting useless symbols, look for a productive cycle |
| “at most `k` strings”, `k` fixed | decidable | decide finite; if finite, enumerate up to the derivation bound |
| equivalence `L(G1) = L(G2)` | **undecidable** | reduce from universality: `L(G) = Σ*` iff `L(G) = L(G_all)` |
| universality `L(G) = Σ*` | **undecidable** | standard |
| ambiguity of `G` | **undecidable** | standard |
| `L(G)` regular | **undecidable** | |
| `L(G1) ∩ L(G2) = ∅` | **undecidable** | |
| `L(G) = L(R)` for a regular `R` | **undecidable** | special case of equivalence / regularity |

Non-equivalence of two CFGs **is** RE: enumerate strings and decide membership of each in both grammars; accept when a witness appears. Equivalence, the complement, is therefore not RE.

### Turing machines

| Problem | Status |
|---|---|
| membership `w ∈ L(M)` | RE, not decidable (`A_TM`) |
| “does `M` halt on `w`” | RE, not decidable |
| non-emptiness `L(M) ≠ ∅` | RE, not decidable |
| emptiness `L(M) = ∅` | not RE |
| `L(M) = L(M')`, `L(M)` regular, `L(M) = Σ*`, `L(M)` finite | undecidable (Rice); typically not RE |
| `M` has ≤ 10 states | **decidable** (syntax) |
| `M` runs more than a **fixed** `k` steps on **every** input | **decidable** |
| `M` runs more than a **fixed** `k` steps on **some** input | **decidable** |

**Why a fixed-`k` step property is decidable.** A computation of `k` steps sees at most `k` cells. Only the prefix of the input of length ≤ `k` matters; longer inputs look like their length-`k` prefix plus unread symbols that the machine has not reached. There are finitely many tapes / states / head positions to simulate for `k+1` steps. Check them all. This is 2021 (both “all inputs” and “some input”) and 2022 (more than 1073 steps on every string).

**Unrestricted grammar membership** is `A_TM` in other clothes: undecidable (2018).

**NFA vs DPDA, same language (2018 IV).** The stem is “given an NFA `N`, does there *exist* a DPDA `P` with `L(N) = L(P)`?” Every regular language has a DPDA (run the DFA and ignore the stack), so the answer is yes for every `N`. The problem is decidable because it is constantly true. That is different from “given both an NFA and a *particular* DPDA, are they equivalent?”

---

## 5. “Is this grammar’s language undecidable?”

A CFG generates a CFL. Every CFL is a decidable *set of strings*. So “`L(G)` is an undecidable language” is false for a CFG `G` (2026). What *is* undecidable is a *problem about* `G` (ambiguity, equivalence, universality).

---

## 6. NP, in one paragraph

`NP` is a class of *decidable* languages: a nondeterministic TM that halts in polynomial time is, in particular, a decider. So “there exists a language in NP that is not Turing decidable” is false, and “if `L ∈ NP` then `L` is decidable” is true (2015). `P = NP` is open and is not a TOC syllabus question. 2SAT / NP-complete stems stored in this mapping file are complexity noise.

---

## 7. GATE approach

1. **Underline the model** (DFA, CFG, TM) and the **property** (empty, equal, regular, `Σ*`, finite, “has 5 states”, “> k steps”).
2. If the property is syntactic (size of `M`, a bound on steps that sees a finite window), it is decidable.
3. If it is a property of `L(M)` for a TM and is nontrivial, Rice: undecidable.
4. If two CFGs are being compared for equality / universe / intersection-empty, undecidable. If one CFG is tested for empty / finite / membership, decidable.
5. Reductions: write `x ∈ A iff f(x) ∈ B` in one line. Check the direction before concluding.

## Connections

- [Turing machines](../08-TURING-MACHINES/NOTES.md): decides vs recognizes; `A_TM`.
- [Context-free grammars](../03-CONTEXT-FREE-GRAMMARS/NOTES.md): emptiness = generating variables; ambiguity is a grammar property whose *decision problem* is here.
- [Push-down automata](../04-PUSH-DOWN-AUTOMATA/NOTES.md): two PDAs equivalent is undecidable; every regular language has a DPDA.
- [Regular languages](../05-REGULAR-LANGUAGES/NOTES.md): every question about a DFA language is decidable; “does this TM accept a regular language?” is not.

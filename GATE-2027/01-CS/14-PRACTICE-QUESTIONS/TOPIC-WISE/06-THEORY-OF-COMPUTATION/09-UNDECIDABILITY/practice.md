# Undecidability — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Each question names the model. A property proved for Turing machines is not being claimed for DFAs or context-free grammars, and the converse is not being claimed either. “Decidable” means recursive. “Recursively enumerable but not decidable” means a recognizer exists and no decider exists. Rice's theorem is used only in the form: a nontrivial property of the language recognized by a Turing machine is undecidable. Nontrivial means that at least one recursively enumerable language has the property and at least one does not.

## Level 1 — Conceptual

## Q1 — MCQ

Given a DFA `D` and a string `w`, the question “Does `D` accept `w`?” is

A. decidable  
B. undecidable  
C. not recursively enumerable  
D. meaningless, because a DFA has no accept states

---

## Q2 — MCQ

Emptiness for a DFA `D`, that is “Is `L(D) = ∅`?”, is decidable because

A. one checks whether any accept state is reachable from the start state  
B. one must test infinitely many strings, and no algorithm does that  
C. emptiness is undecidable for every machine model  
D. a DFA cannot be simulated on the empty string

---

## Q3 — MCQ

Whether two regular expressions denote the same language is

A. decidable  
B. undecidable  
C. recursively enumerable but not decidable  
D. not recursively enumerable

---

## Q4 — MCQ

Whether a Turing machine `M` accepts a given string `w` is

A. decidable, by simulating `M` for exactly `|w|` steps  
B. undecidable  
C. decidable, because `M` has finitely many states  
D. always “yes”

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Whether a context-free grammar generates at least one string is

A. decidable, by computing which variables derive a terminal string  
B. undecidable, because grammars can have recursive productions  
C. decidable only when the grammar is regular  
D. the same problem as Turing-machine emptiness

---

## Q6 — MCQ

Whether two context-free grammars generate the same language is

A. decidable, by converting both grammars to minimal DFAs  
B. undecidable  
C. decidable, because membership for each grammar is decidable  
D. decidable, because emptiness for one grammar is decidable

---

## Q7 — MCQ

Given a context-free grammar `G` and a string `w`, whether `w ∈ L(G)` is

A. decidable  
B. undecidable  
C. recursively enumerable but not decidable  
D. not recursively enumerable

---

## Q8 — NAT

Consider these four decision problems.

1. Emptiness of a DFA
2. Finiteness of a DFA: does `L(D)` contain only finitely many strings?
3. Equivalence of two DFAs
4. Emptiness of a Turing machine: does `L(M) = ∅`?

The number of these problems that are decidable is ____.

---

## Q9 — MCQ

Whether a DFA `D` satisfies `L(D) = Σ*` is

A. decidable, by testing emptiness of the complement  
B. undecidable, by the same argument used for context-free grammars  
C. decidable only if `D` has one state  
D. not recursively enumerable

---

## Level 3 — Multi-Step

## Q10 — MCQ

Whether a context-free grammar `G` satisfies `L(G) = Σ*` is

A. decidable, because membership is decidable  
B. undecidable  
C. decidable, because finiteness of `L(G)` is decidable  
D. the same problem as emptiness of `G`, and emptiness is decidable

---

## Q11 — MCQ

Which problem is decidable?

A. Given a CFG `G`, is `L(G)` finite?  
B. Given a Turing machine `M`, is `L(M)` finite?  
C. Given a Turing machine `M`, is `L(M)` regular?  
D. Given two CFGs `G1` and `G2`, is `L(G1) = L(G2)`?

---

## Q12 — MSQ

Which of the following problems are undecidable by Rice's theorem? Select all that apply.

A. Given a Turing machine `M`, is `L(M)` empty?  
B. Given a Turing machine `M`, is `L(M)` finite?  
C. Given a Turing machine `M`, is `L(M)` regular?  
D. Given a Turing machine `M`, does `M` have exactly five states?

---

## Q13 — MCQ

Whether a context-free grammar is ambiguous is

A. decidable, by counting leftmost derivations of every string up to a fixed length  
B. undecidable  
C. decidable, because every context-free language has an unambiguous grammar  
D. decidable exactly when the grammar is in Chomsky normal form

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

Which statement is true?

A. Every undecidable language fails to be recursively enumerable  
B. `A_TM = {⟨M, w⟩ | M accepts w}` is recursively enumerable but not decidable  
C. `A_TM` is decidable but not recursively enumerable  
D. If a language is not decidable, it has no recognizer

---

## Q15 — MCQ

The emptiness problem `{⟨M⟩ | M is a Turing machine and L(M) = ∅}` is

A. decidable  
B. recursively enumerable but not decidable  
C. not recursively enumerable, while its complement, non-emptiness, is recursively enumerable  
D. regular

---

## Q16 — MSQ

Which problems are recursively enumerable but not decidable? Select all that apply.

A. `A_TM`, membership for Turing machines  
B. Non-equivalence of two context-free grammars: `L(G1) ≠ L(G2)`  
C. Emptiness of a Turing machine  
D. Non-emptiness of a Turing machine

---

## Level 5 — Challenge

## Q17 — MCQ

Fix an alphabet `Σ` and a context-free grammar `G_all` with `L(G_all) = Σ*`. Universality for context-free grammars, “Does `L(G) = Σ*`?”, is undecidable. Which conclusion follows?

A. Equivalence of two CFGs is undecidable, because `L(G) = Σ*` if and only if `L(G) = L(G_all)`, so a decider for equivalence would decide universality  
B. Equivalence of two CFGs is decidable, because universality does not mention a second grammar  
C. Equivalence of two CFGs is decidable, because membership of a string in a CFG is decidable  
D. Universality of a DFA is undecidable by the same reduction

---

## Q18 — MSQ

Which problems are decidable? Select all that apply.

A. Given a Turing machine `M`, does `M` have at most 10 states?  
B. Given a Turing machine `M`, does `L(M)` contain at most 10 strings?  
C. Given a DFA `D`, does `L(D)` contain at most 10 strings?  
D. Given a CFG `G`, does `L(G)` contain at most 10 strings?

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | MCQ | A |
| 4 | MCQ | B |
| 5 | MCQ | A |
| 6 | MCQ | B |
| 7 | MCQ | A |
| 8 | NAT | 3 |
| 9 | MCQ | A |
| 10 | MCQ | B |
| 11 | MCQ | A |
| 12 | MSQ | A, B, C |
| 13 | MCQ | B |
| 14 | MCQ | B |
| 15 | MCQ | C |
| 16 | MSQ | A, B, D |
| 17 | MCQ | A |
| 18 | MSQ | A, C, D |

## Detailed Solutions

### Q1

Answer: A

Simulate `D` on `w`. After exactly `|w|` transitions the DFA is in one state. Accept the instance if that state is an accept state, and reject it otherwise. The procedure always halts. A DFA does have accept states; the computation is not a search over an infinite tape.

### Q2

Answer: A

Treat the DFA as a directed graph, with an edge `p → q` whenever some symbol takes `p` to `q`. The language is nonempty exactly when a breadth-first search from the start state reaches an accept state. The graph is finite, so the search halts. Emptiness is not undecidable for every model: it is decidable for DFAs and for context-free grammars, and undecidable for Turing machines.

### Q3

Answer: A

Convert each regular expression to an NFA, then to a DFA, then to the unique minimal complete DFA. Two regular expressions are equivalent exactly when those minimal DFAs are identical up to renaming of states. Alternatively, build a DFA for the symmetric difference and test emptiness as in Q2. Either algorithm halts on every pair of expressions.

The same problem for context-free grammars is undecidable. The model is the whole difference.

### Q4

Answer: B

Simulating `M` for `|w|` steps is not enough: a Turing machine may accept `w` only after more than `|w|` steps. Finitely many states do not make the acceptance question decidable, because the tape is unbounded. The language `A_TM` is the standard undecidable acceptance problem. It is still recursively enumerable, by simulation that is allowed to loop when `M` loops.

### Q5

Answer: A

Compute the generating variables. Terminals are generating. A variable is generating when some production has a right-hand side whose every symbol is already generating. Repeat until the set stops growing. The grammar generates a string exactly when the start symbol is generating. Each pass inspects a finite grammar, so the algorithm halts.

Recursive productions do not make this undecidable: a variable that can only produce longer sentential forms containing itself is simply never marked generating. Turing-machine emptiness is a different, undecidable problem.

### Q6

Answer: B

There is no “minimal DFA” construction that preserves an arbitrary context-free language, because not every context-free language is regular. Decidable membership does not decide equivalence: two grammars can agree on every string one happens to test and differ on a string one has not tested yet. Emptiness of `L(G1)` does not compare `G1` with `G2`.

Equivalence is undecidable. Q17 gives the reduction from the undecidable universality problem: a decider for equivalence could test `L(G) = L(G_all)` for a fixed grammar of `Σ*`.

### Q7

Answer: A

Membership for a CFG is decidable. One complete algorithm is to convert `G` to Chomsky normal form, which is effective and preserves the language apart from an explicitly checked empty word, and then run the Cocke–Younger–Kasami dynamic program on `w`. The program fills a finite table of size `O(|w|^2)` and always halts. Its answer is yes exactly when `w ∈ L(G)`.

So this problem is not an example of “recursively enumerable but not decidable”. That boundary matters for Turing machines, whose membership problem has a recognizer and no decider.

### Q8

Answer: 3

The first three problems are decidable, and the fourth is not. The count is 3.

Emptiness of a DFA is Q2. Finiteness of a DFA is decidable by searching the finite transition graph for a cycle that lies on some path from the start state to an accept state. Such a cycle can be pumped, so the language is infinite exactly then. If no such cycle exists, every accepted string has length less than the number of states. Equivalence of two DFAs is decidable by minimizing both, or by testing emptiness of the symmetric difference, as in Q3.

Emptiness of a Turing machine is not decidable. It is not even recursively enumerable. Q15 shows that its complement, non-emptiness, is recognizable and undecidable, so emptiness itself cannot be recognizable.

### Q9

Answer: A

`L(D) = Σ*` if and only if the complement is empty. The complement of a DFA language is obtained by swapping accept and non-accept states, and Q2 decides emptiness. Equivalently, the minimal DFA accepts `Σ*` exactly when every state is accepting.

Universality of a context-free grammar does not become decidable by this construction. A CFG need not have a DFA. Option (B) copies a theorem across models.

### Q10

Answer: B

Universality for CFGs is a standard undecidable problem: no algorithm takes an arbitrary CFG and decides whether it generates every string. Q17 uses that fact.

Membership does not decide it. One can check any particular string, but a “no” answer for universality is the existence of some missing string, and a “yes” answer quantifies over every string. Finiteness does not decide it either. The empty language is not `Σ*`, and `Σ*` is not empty, so universality is not the emptiness problem.

### Q11

Answer: A

(A) is decidable. Remove useless symbols. In the remaining grammar, the language is infinite exactly when some variable `A` derives, in one or more steps, a sentential form that contains `A` again and produces at least one extra terminal somewhere in that cycle. Both the existence of such a derivation and the usefulness of the variables are finite graph searches on the grammar. If no such cycle exists, every derivation has a bounded length and the language is finite.

(B) is undecidable by Rice's theorem. “`L(M)` is finite” is a property of the recognized language. The empty language is finite and recursively enumerable. `Σ*` is recursively enumerable and not finite. The property is nontrivial, so no algorithm decides it from `M`.

(C) is undecidable by the same theorem. “`L(M)` is regular” is nontrivial: `∅` is regular, while `A_TM` is recursively enumerable and not regular, because a regular language would be decidable.

(D) is undecidable by Q6.

### Q12

Answer: A, B, C

Rice's theorem applies to (A), (B), and (C) because each question depends only on `L(M)` and each property is nontrivial.

- Emptiness: `∅` has it, and `Σ*` does not.
- Finiteness: `∅` has it, and `Σ*` does not.
- Regularity: `∅` has it, and `A_TM` does not.

(D) is decidable and is not an application of Rice's theorem. Read the finite list of states in the encoding of `M` and count it. The property is about the machine, not about the language: two machines can recognize the same language and have different numbers of states. A language property must give the same answer for every machine that recognizes a given language. “Exactly five states” does not.

### Q13

Answer: B

Ambiguity of a CFG is undecidable. There is no algorithm that inspects an arbitrary grammar and decides whether some string has two distinct leftmost derivations.

Checking all strings up to a fixed length can certify ambiguity when a short ambiguous string exists, but it cannot certify unambiguity: the shortest ambiguous string may be longer than the bound. Chomsky normal form does not remove this quantifier over strings. Also, not every context-free language has an unambiguous grammar. The language `{a^i b^j c^k | i = j or j = k}` is a standard inherently ambiguous context-free language, so the hope in (C) is false for grammars of that language and does not yield a decision procedure anyway.

### Q14

Answer: B

(B) is the correct boundary. A recognizer for `A_TM` simulates `M` on `w` and accepts if the simulation accepts. The diagonal argument shows there is no decider: a supposed decider `H` would build a machine `D` that accepts `⟨D⟩` exactly when `H` says it does not.

(A) and (D) are the same mistake. Undecidable does not mean “not recursively enumerable”. `A_TM` is the counterexample. (C) swaps the two classes: a decidable language is always recursively enumerable, because a decider is a recognizer.

### Q15

Answer: C

Non-emptiness is recursively enumerable. Dovetail over all strings `x` and all step counts `t`. Simulate `M` on `x` for `t` steps. If any simulation accepts, accept the instance `⟨M⟩`. If `L(M)` contains some string, that string is accepted after finitely many steps, and the dovetailing eventually tries that pair `(x, t)`.

Non-emptiness is not decidable. Q16 of the Turing-machine set, repeated here in one line, reduces `A_TM` to it: `M'` ignores its input and accepts everything exactly when `M` accepts `w`. Then `L(M')` is nonempty exactly on the yes-instances of `A_TM`.

Emptiness is the complement of non-emptiness. If emptiness were recursively enumerable as well, both a set and its complement would be recursively enumerable, and non-emptiness would be decidable. It is not. Therefore emptiness is not recursively enumerable. It is certainly not decidable and not regular.

### Q16

Answer: A, B, D

(A) is `A_TM`: recognizable by simulation, not decidable by diagonalization.

(B) is recognizable. Enumerate every string `x`. For each `x`, decide membership of `x` in `G1` and in `G2` by the algorithm of Q7. If some `x` belongs to exactly one of the two languages, accept. If the languages differ, a shortest witness appears after finitely many trials. If they are equal, the search runs forever, which is allowed for a recognizer.

(B) is not decidable. Its complement is CFG equivalence, which Q17 shows is undecidable. A set is decidable exactly when it and its complement are, so non-equivalence is not decidable either. This is the trap: non-equivalence is undecidable and still recursively enumerable, because CFG membership is decidable and supplies the witness search. Turing-machine non-equivalence does not have that easy witness search, because Turing-machine membership is only recognizable.

(C) is not recursively enumerable, by Q15.

(D) is non-emptiness: the dovetailing recognizer of Q15, and the reduction from `A_TM` shows it is not decidable.

### Q17

Answer: A

The map `G ↦ (G, G_all)` is computable, and `L(G) = Σ*` if and only if `L(G) = L(G_all)`. This is a many-one reduction from universality to equivalence. A decider for equivalence would decide universality. Universality is undecidable, so equivalence is undecidable. That is (A).

(B) ignores that `G_all` is a perfectly legal second grammar. (C) confuses membership, which is decidable, with a universal quantification over all strings. (D) is false. Q9 decides universality for a DFA by complementing and testing emptiness. The reduction does not transfer to DFAs, because a DFA's complement is a DFA, whereas the complement of a context-free language need not be context-free.

The reduction also explains a finer point from Q16. Non-equivalence remains recursively enumerable by the witness search. Equivalence, the complement, is therefore not recursively enumerable: if it were, equivalence would be decidable.

### Q18

Answer: A, C, D

(A) is decidable by reading the encoding. Count the states. This is a syntactic question. Rice's theorem does not apply, and it does not say that every question about a Turing machine is undecidable.

(B) is undecidable by Rice's theorem. The property “`|L| ≤ 10`” depends only on the language. It is nontrivial: `∅` has it, and `Σ*` does not. Both of those languages are recursively enumerable.

(C) is decidable. Use Q8(B). If an accepting cycle is reachable, the language is infinite and the answer is no. Otherwise every accepted string has length less than the number of states. Enumerate the finitely many walks from the start state to an accept state and count the distinct labels. Compare the count with 10.

(D) is decidable. Q11(A) decides whether `L(G)` is infinite. If it is, the answer is no. If it is finite, the useful part of the grammar has no productive cycle, so there is a finite bound on the length of a derivation and on the length of a generated string. Enumerate every derivation up to that bound, collect the terminal strings, and compare the size of the set with 10. The search is finite.

The contrast between (B) and (D) is the model. “At most ten strings” is decidable for a DFA and for a CFG, and undecidable for a Turing machine.

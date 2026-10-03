# Turing Machines — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

A language is decidable (recursive) when some Turing machine halts on every input, accepting exactly the strings in the language and rejecting every other string. A language is recursively enumerable when some Turing machine accepts exactly the strings in the language; on other strings that machine may reject or loop. These questions are about what is computable, not about time or space bounds.

## Level 1 — Conceptual

## Q1 — MCQ

Which resource of a Turing machine is unbounded?

A. the number of states  
B. the tape  
C. the input alphabet  
D. the number of accept states

---

## Q2 — MCQ

A configuration of a Turing machine records

A. only the current state  
B. the current state, the tape contents, and the head position  
C. only the symbols to the left of the head  
D. the number of states in the finite control

---

## Q3 — MCQ

A Turing machine `M` decides a language `L` when

A. `M` accepts every string in `L` and is allowed to loop on strings outside `L`  
B. `M` halts on every input, accepts exactly the strings in `L`, and rejects every string outside `L`  
C. `M` rejects every input  
D. `M` has no rejecting state, so every halting computation accepts

---

## Q4 — MCQ

A Turing machine that recognizes `L` 

A. must halt and reject every string outside `L`  
B. must accept every string in `L`, and on a string outside `L` it may halt and reject or loop  
C. must loop on every string in `L`  
D. is necessarily a decider for `L`

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Compared with ordinary one-tape Turing machines, multi-tape Turing machines

A. accept a strictly larger class of languages  
B. accept exactly the same class of languages  
C. accept only the regular languages  
D. cannot be simulated if they have more than two tapes

---

## Q6 — MCQ

Nondeterministic Turing machines, as language acceptors,

A. accept some languages that no deterministic Turing machine accepts  
B. accept exactly the recursively enumerable languages, the same class deterministic Turing machines accept  
C. accept only decidable languages  
D. are illegal models because a Turing machine must have a unique move

---

## Q7 — MCQ

The acceptance language `A_TM = {⟨M, w⟩ | M is a Turing machine and M accepts w}` is

A. decidable  
B. recursively enumerable but not decidable  
C. not recursively enumerable  
D. regular

---

## Q8 — NAT

The Turing machine below has start state `q0`, accept state `q_acc`, and reject state `q_rej`. The blank is `⊔`. The head starts on the leftmost input cell. A move is one application of `δ`.

- `δ(q0, a) = (q1, a, R)`, `δ(q0, b) = (q_rej, b, R)`, `δ(q0, ⊔) = (q_rej, ⊔, R)`
- `δ(q1, a) = (q1, a, R)`, `δ(q1, b) = (q_rej, b, R)`, `δ(q1, ⊔) = (q_acc, ⊔, L)`

On input `aa`, the number of moves made before the machine enters `q_acc` is ____.

---

## Level 3 — Multi-Step

## Q9 — MCQ

If both `L` and its complement are recursively enumerable, then

A. `L` is decidable  
B. `L` is not recursively enumerable  
C. the complement of `L` is not recursively enumerable  
D. `L` must be finite

---

## Q10 — MSQ

Which statements are true? Select all that apply.

A. Decidable languages are closed under complement  
B. Recursively enumerable languages are closed under complement  
C. Recursively enumerable languages are closed under union  
D. Recursively enumerable languages are closed under intersection

---

## Q11 — MCQ

Which condition is equivalent to “`L` is decidable”?

A. `L` is recursively enumerable  
B. both `L` and its complement are recursively enumerable  
C. `L` is infinite  
D. `L` is accepted by some nondeterministic Turing machine

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

A Turing machine `M` accepts exactly the strings of a language `L`, and `M` halts on every string in `L`. On strings outside `L`, `M` may loop. Then `L` is

A. necessarily decidable  
B. recursively enumerable, and not necessarily decidable  
C. not recursively enumerable  
D. regular

---

## Q13 — MCQ

Which statement is false?

A. Every decidable language is recursively enumerable  
B. Every recursively enumerable language is decidable  
C. Every regular language is decidable  
D. Every context-free language is decidable

---

## Q14 — MSQ

Which languages are recursively enumerable but not decidable? Select all that apply.

A. `{⟨M, w⟩ | the Turing machine M accepts w}`  
B. `{⟨D, w⟩ | the DFA D accepts w}`  
C. `{⟨M, w⟩ | the Turing machine M halts on w}`  
D. `{⟨M⟩ | M is a Turing machine and L(M) = ∅}`

---

## Level 5 — Challenge

## Q15 — MCQ

A many-one reduction from `A` to `B` is a computable function `f` such that `x ∈ A` if and only if `f(x) ∈ B`. Which inference is valid?

A. If `A` reduces to `B` and `A` is undecidable, then `B` is undecidable  
B. If `A` reduces to `B` and `B` is undecidable, then `A` is undecidable  
C. If `A` reduces to `B` and `A` is decidable, then `B` is decidable  
D. If `A` reduces to `B` and `B` is recursively enumerable, then `A` is not recursively enumerable

---

## Q16 — MCQ

Given `⟨M, w⟩`, define `M'` to ignore its own input, simulate `M` on `w`, and accept if that simulation accepts. If `M` rejects `w` or loops on `w`, then `M'` never accepts. Which conclusion does this construction justify?

A. Non-emptiness `{⟨N⟩ | L(N) ≠ ∅}` is undecidable, because `L(M') ≠ ∅` exactly when `M` accepts `w`  
B. Non-emptiness is decidable, because `M'` is built by a computable translation  
C. `A_TM` is not recursively enumerable  
D. `M'` accepts its input only when the input equals `w`

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | B |
| 3 | MCQ | B |
| 4 | MCQ | B |
| 5 | MCQ | B |
| 6 | MCQ | B |
| 7 | MCQ | B |
| 8 | NAT | 3 |
| 9 | MCQ | A |
| 10 | MSQ | A, C, D |
| 11 | MCQ | B |
| 12 | MCQ | B |
| 13 | MCQ | B |
| 14 | MSQ | A, C |
| 15 | MCQ | A |
| 16 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

The finite control has finitely many states, the input alphabet is finite, and there are finitely many accept states. The tape is infinite in at least one direction, so the machine can use as many cells as the computation demands. An unbounded tape is what lets a Turing machine go beyond a finite automaton or a push-down automaton.

### Q2

Answer: B

To resume a computation one must know the state, every symbol currently written on the tape, and which cell the head is scanning. The left part of the tape alone does not determine the next move. The number of states is part of the machine, not part of a configuration.

### Q3

Answer: B

A decider has two halting outcomes, accept and reject, and it must reach one of them on every input. Accepting the members of `L` is not enough if some non-member makes the machine loop. That weaker behaviour is recognition, which is option (A).

### Q4

Answer: B

Recognition requires a correct “yes” answer: every string in `L` must lead to acceptance. Strings outside `L` must not be accepted. The machine may reject them, or it may run forever. A recognizer is a decider only in the special case where it also halts on the no-instances.

### Q5

Answer: B

A multi-tape machine can be simulated by a one-tape machine. One standard encoding stores all tapes on a single tape, marks each head position, and sweeps the tape once per simulated step to find those marks and apply the multi-tape transition. Every language accepted by a multi-tape machine is therefore accepted by a one-tape machine. The other inclusion is immediate, because a one-tape machine is a multi-tape machine that happens to use one tape. The class of accepted languages does not grow. This says nothing about the number of steps the simulation uses.

### Q6

Answer: B

A nondeterministic Turing machine accepts when at least one branch accepts. Its language is still recursively enumerable: a deterministic machine can dovetail the finitely many branches to depth 1, then depth 2, and so on, and accept if any branch accepts. Conversely every deterministic machine is a nondeterministic machine with one choice. Nondeterminism does not add languages and does not restrict the machine to the decidable languages. `A_TM` is accepted by a nondeterministic, in fact deterministic, recognizer and is not decidable.

### Q7

Answer: B

`A_TM` is recursively enumerable. On input `⟨M, w⟩`, simulate `M` on `w`. If the simulation accepts, accept. If it rejects, reject. If it loops, the simulator loops. The accepted language is exactly `A_TM`.

`A_TM` is not decidable. Suppose a decider `H` exists. Build `D` which, on input `⟨M⟩`, runs `H` on `⟨M, ⟨M⟩⟩` and reverses the answer: if `H` accepts, `D` rejects; if `H` rejects, `D` accepts. Then `D` accepts `⟨D⟩` exactly when `H` says that `D` does not accept `⟨D⟩`. That is a contradiction. Hence no decider exists.

The language is not regular, because it is not even decidable.

### Q8

Answer: 3

The input tape begins as `a a`, with the head on the first `a`.

1. `δ(q0, a) = (q1, a, R)`. The head moves to the second `a`, and the state is `q1`.
2. `δ(q1, a) = (q1, a, R)`. The head moves onto the blank after the input, and the state is `q1`.
3. `δ(q1, ⊔) = (q_acc, ⊔, L)`. The machine enters `q_acc`.

Exactly three moves occur before acceptance. The machine recognizes `a+`: from `q0` it requires a first `a`, then `q1` scans further `a`s and accepts only when the blank is reached without a `b`.

### Q9

Answer: A

Let `R` recognize `L` and let `S` recognize the complement. On an arbitrary input `x`, simulate one step of `R`, then one step of `S`, then the next step of `R`, and so on. Exactly one of the two machines accepts `x`, because `x` is in exactly one of the two languages. When that acceptance appears, halt: accept if it was `R`, and reject if it was `S`. The combined machine always halts and decides `L`.

Finiteness is not required. Recursively enumerable languages need not be closed under complement, so (C) is not forced by the hypothesis; the hypothesis is precisely that this particular complement is recursively enumerable.

### Q10

Answer: A, C, D

(A) is true. Swap the accept and reject outcomes of a decider. The resulting machine still halts on every input, and it decides the complement.

(B) is false. `A_TM` is recursively enumerable and its complement is not. If the complement were recursively enumerable, Q9 would make `A_TM` decidable.

(C) is true. On input `x`, dovetail a recognizer for `L1` with a recognizer for `L2`, and accept if either accepts. 

(D) is true. Run the two recognizers one step at a time and accept only when both have accepted. If `x` is in the intersection, both accept after finitely many steps. If it is outside, at least one never accepts, so the intersection machine does not accept it.

### Q11

Answer: B

By Q9, if both `L` and its complement are recursively enumerable, then `L` is decidable. Conversely, a decider for `L` is a recognizer for `L`, and swapping its accept and reject outcomes recognizes the complement. So (B) is equivalent to decidability.

(A) and (D) are equivalent to each other and strictly weaker: both say that `L` is recursively enumerable. `A_TM` satisfies them and is not decidable. (C) is independent of decidability. The empty language is decidable and finite; `a*` is decidable and infinite.

### Q12

Answer: B

The stated machine accepts exactly `L`, so `L` is recursively enumerable. Halting on the yes-instances is already part of acceptance. Decidability also demands a halt on every no-instance. `A_TM` itself has a recognizer that halts and accepts on the yes-instances and loops on some no-instances. Thus (A) does not follow. The language need not fail to be recursively enumerable, and it need not be regular.

### Q13

Answer: B

(A) is true: a decider is a recognizer. (B) is false: `A_TM` is recursively enumerable and not decidable. This is the recursive-versus-RE trap.

(C) is true. Simulate the DFA on the input and accept or reject according to the state it reaches. The simulation halts after `|w|` steps.

(D) is true. Membership for a context-free grammar is decidable, for example by converting to Chomsky normal form and using the Cocke–Younger–Kasami dynamic program, which halts on every input. A context-free language is therefore a decidable set.

### Q14

Answer: A, C

(A) is `A_TM`, which Q7 shows is recursively enumerable and not decidable.

(B) is decidable. Simulate the DFA on `w`. It is recursively enumerable as well, but the question asks for languages that are not decidable, so (B) is not selected.

(C) is the halting language. It is recursively enumerable: simulate `M` on `w`, and accept if the simulation ever halts, whether the halting state is accept or reject. It is not decidable. If it were, `A_TM` would be decidable by the following reduction. From `⟨M, w⟩` build `M'`, which simulates `M` on `w`, halts if `M` accepts, and loops if `M` rejects. Then `M'` halts on `w` exactly when `M` accepts `w`. A halting decider would decide acceptance.

(D) is the emptiness problem for Turing machines. It is not recursively enumerable. Its complement, non-emptiness, is recursively enumerable by dovetailing over all strings and all numbers of steps. Q16 shows that non-emptiness is undecidable. If emptiness were also recursively enumerable, Q9 would make non-emptiness decidable. So (D) is not recursively enumerable at all.

### Q15

Answer: A

A reduction from `A` to `B` means `A` is no harder than `B`, up to a computable translation.

(A) is valid. If `B` had a decider, then on input `x` one could compute `f(x)` and run that decider. The answer would decide `A`. So an undecidable `A` forces `B` to be undecidable.

(B) reverses the direction. A decidable language can reduce to an undecidable one. Map every input to a fixed no-instance of `A_TM`, if the source language is empty, or more generally decide the source language first and map yes-instances and no-instances to two fixed strings, one inside `A_TM` and one outside it. The target is undecidable and the source need not be.

(C) has the same reversed direction. Deciding `A` does not decide `B`.

(D) has the wrong closure. If `B` is recursively enumerable and `f` is computable, a recognizer for `A` computes `f(x)` and runs the recognizer for `B`. Thus `A` is recursively enumerable as well.

### Q16

Answer: A

The map `⟨M, w⟩ ↦ ⟨M'⟩` is computable from the encoding of `M` and `w`. By construction, every input is accepted by `M'` if `M` accepts `w`, and no input is accepted by `M'` otherwise. Therefore

`L(M') ≠ ∅` if and only if `M` accepts `w`.

If a decider for non-emptiness existed, applying it to `M'` would decide `A_TM`. Q7 says `A_TM` is undecidable, so non-emptiness is undecidable. That is (A).

The translation being computable is what makes this a reduction; it does not decide non-emptiness, so (B) is false. (C) is false because `A_TM` is recursively enumerable. (D) is false because `M'` ignores its own input. It does not compare that input with `w`.

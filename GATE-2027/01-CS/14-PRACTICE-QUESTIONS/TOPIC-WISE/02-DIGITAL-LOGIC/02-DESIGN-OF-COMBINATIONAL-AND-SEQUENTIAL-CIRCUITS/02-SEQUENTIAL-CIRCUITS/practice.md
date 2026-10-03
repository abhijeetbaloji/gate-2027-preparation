# Sequential Circuits — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The characteristic equation of a D flip-flop is

A. \(Q^+ = D\)

B. \(Q^+ = D'\)

C. \(Q^+ = D \oplus Q\)

D. \(Q^+ = D + Q\)

---

## Q2 — MSQ

Select all that apply.

A. For a T flip-flop, \(Q^+ = T \oplus Q\).

B. For a JK flip-flop, \(Q^+ = JQ' + K'Q\).

C. Driving a JK flip-flop with \(J = 1\) and \(K = 1\) complements \(Q\).

D. For an SR latch, \(S = 1\) and \(R = 1\) is the hold condition.

---

## Q3 — NAT

The minimum number of flip-flops in a synchronous counter that must visit 10 distinct states is ______.

---

## Q4 — MCQ

A JK flip-flop must go from \(Q = 0\) to \(Q^+ = 1\). A valid excitation is

A. \(J = 1,\ K = X\)

B. \(J = 0,\ K = 1\)

C. \(J = X,\ K = 0\)

D. \(J = 0,\ K = X\)

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

A 2-bit binary up counter is built from T flip-flops \(Q_1\) (MSB) and \(Q_0\) (LSB). The inputs are

A. \(T_0 = 1\), \(T_1 = Q_0\)

B. \(T_0 = Q_0\), \(T_1 = 1\)

C. \(T_0 = 1\), \(T_1 = 1\)

D. \(T_0 = Q_1\), \(T_1 = Q_0\)

---

## Q6 — NAT

A 3-bit Johnson counter shifts left on each clock. The bit shifted into the LSB is the complement of the old MSB. Started at \(000\), the number of distinct states visited before the start state repeats is ______.

---

## Q7 — MSQ

Select all that apply. Consider three different 4-bit synchronous counters, each started on its main cycle: a binary up counter, a one-hot ring counter, and a Johnson counter.

A. The binary counter visits 16 states.

B. The ring counter visits 4 states.

C. The Johnson counter visits 8 states.

D. The ring counter visits 8 states.

---

## Q8 — MCQ

A T flip-flop is built from a D flip-flop and combinational logic. The \(D\) input must be

A. \(T \oplus Q\)

B. \(T \odot Q\)

C. \(TQ\)

D. \(T + Q\)

---

## Q9 — NAT

A synchronous circuit has flip-flop clock-to-\(Q\) delay 8 ns, setup time 3 ns, and worst-case next-state logic delay 12 ns. Hold time is satisfied by a separate check and does not add to the period. The minimum clock period, in nanoseconds, is ______.

---

## Q10 — MCQ

A D flip-flop is wired as \(D = X \oplus Q\), with \(Q\) initially 0. The input \(X\) on five successive clocks is \(0, 1, 0, 1, 1\). After the fifth clock, \(Q\) is

A. 0

B. 1

C. still 0, because \(D\) is gated by the old \(Q\)

D. equal to \(X\) with no dependence on the previous \(Q\)

---

## Level 3 — Multi-Step

## Q11 — MCQ

A JK flip-flop has \(J = X\), \(K = X'\) and starts at \(Q = 0\). The input \(X\) on four successive clocks is \(1, 1, 0, 1\). After the fourth clock, \(Q\) is

A. 0

B. 1

C. undefined, because \(J = X\) and \(K = X'\) is a forbidden input

D. 0, and the third clock already forced it to stay 0

---

## Q12 — NAT

A 3-bit binary up counter uses T flip-flops with \(T_0 = 1\), \(T_1 = Q_0\) and \(T_2 = Q_1 Q_0\). The present state \(Q_2 Q_1 Q_0\) is \(011\). After six clocks, the state interpreted as an unsigned integer is ______.

---

## Q13 — MSQ

Select all that apply.

A. A JK flip-flop realizes a D flip-flop when \(J = D\) and \(K = D'\).

B. An SR latch with \(S = R = 0\) holds \(Q\).

C. A T flip-flop with \(T = 1\) toggles on every triggering edge.

D. For every transition of a D flip-flop, the excitation table leaves \(D\) as a don't care.

---

## Q14 — MCQ

A Moore machine has five states. The minimum number of flip-flops needed for a binary encoding of those states is

A. 2

B. 3

C. 4

D. 5

---

## Level 4 — Tricky / Trap-Based

## Q15 — MSQ

Select all that apply.

A. \(J = 1, K = 1\) makes a JK flip-flop toggle.

B. \(S = 1, R = 1\) is an allowed hold input of a NOR SR latch.

C. Tying \(J\) and \(K\) together and driving that net with 1 produces a toggle.

D. Substituting \(J = K = 1\) into \(Q^+ = JQ' + K'Q\) gives \(Q^+ = Q'\).

---

## Q16 — NAT

For a flip-flop, the minimum clock-to-\(Q\) delay is 1 ns and the hold time is 2 ns. The contamination delay of the next-state logic is 0 ns. The hold slack, defined as \(t_{ccq}(\min) + t_{cd} - t_{hold}\), in nanoseconds, is ______.

---

## Q17 — MCQ

Both T inputs of a 2-bit counter are tied to 1. From \(Q_1 Q_0 = 00\), the number of distinct states on the resulting cycle is

A. 1

B. 2

C. 4

D. 8

---

## Level 5 — Challenge

## Q18 — NAT

A 4-bit ring counter rotates toward the LSB: the new MSB is the old LSB, and the other bits move one place toward the LSB. The start state is \(1000\). After six clocks, the state interpreted as an unsigned integer is ______.

---

## Q19 — MCQ

Two D flip-flops obey \(D_1 = Q_0\) and \(D_0 = Q_1'\). From \(Q_1 Q_0 = 00\), the cycle is

A. \(00 \to 01 \to 11 \to 10 \to 00\), of length 4

B. \(00 \to 01 \to 00\), of length 2

C. the single state \(00\), which is stable

D. \(00 \to 10 \to 11 \to 01 \to 00\), of length 4

---

## Q20 — MSQ

Select all that apply. A 3-bit synchronous binary up counter emits its state as the output.

A. If the output is the state vector, the machine is a Moore machine.

B. Three flip-flops are necessary and sufficient.

C. The clock takes state \(101\) to state \(110\).

D. In the T-flip-flop realization, \(T_0 = 0\).

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 4 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | NAT | 6 |
| 7 | MSQ | A, B, C |
| 8 | MCQ | A |
| 9 | NAT | 23 |
| 10 | MCQ | B |
| 11 | MCQ | B |
| 12 | NAT | 1 |
| 13 | MSQ | A, B, C |
| 14 | MCQ | B |
| 15 | MSQ | A, C, D |
| 16 | NAT | -1 |
| 17 | MCQ | B |
| 18 | NAT | 2 |
| 19 | MCQ | A |
| 20 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: **A**

By definition the next state of a D flip-flop is the value sampled on \(D\). Option (C) is the T characteristic equation with \(T\) renamed. Option (D) holds the old 1 forever once \(Q\) has become 1. Option (B) stores the complement of the data input.

### Q2

Answer: **A, B, C**

\(Q^+ = T \oplus Q\) is the T equation, and \(Q^+ = JQ' + K'Q\) is the JK equation. Setting \(J = K = 1\) in the JK equation gives \(Q^+ = Q' + 0 \cdot Q = Q'\), a toggle.

The hold input of an SR latch is \(S = R = 0\). The input \(S = R = 1\) is forbidden for the usual NOR or NAND SR latch: the two outputs are driven to the same level, and releasing the inputs can race. Option (D) copies the JK toggle input onto an SR latch.

### Q3

Answer: **4**

With \(n\) flip-flops there are at most \(2^n\) states. Since \(2^3 = 8 < 10\) and \(2^4 = 16 \ge 10\), the minimum is 4. Three flip-flops can build a mod-8 counter, not a mod-10 counter. The extra six codes of a 4-bit encoding are unused; they do not reduce the flip-flop count.

### Q4

Answer: **A**

From the JK excitation table, the transition \(0 \to 1\) requires \(J = 1\). The value of \(K\) is not observed, because the \(K'Q\) term is multiplied by the present 0. So \(K = X\).

Option (D) is the excitation for \(0 \to 0\). Option (B) forces a reset and cannot leave a 0-state as 1. Option (C) is the excitation for \(1 \to 1\), where \(J\) is the don't care. Using the \(1 \to 1\) row on a present-0 state is the usual table-reading slip.

### Q5

Answer: **A**

The LSB of a binary up counter toggles on every clock, so \(T_0 = 1\). The MSB toggles only when the LSB is 1, which is the carry into that bit, so \(T_1 = Q_0\). The states run \(00 \to 01 \to 10 \to 11 \to 00\).

Option (B) swaps the two inputs: the LSB would toggle only when it is already 1, and the counter leaves the binary cycle. Option (C) toggles both bits every clock, producing the cycle \(00 \leftrightarrow 11\) and skipping \(01\) and \(10\). Option (D) uses \(Q_1\) as the LSB toggle and is the excitation of a different machine.

### Q6

Answer: **6**

Write the state as \(Q_2 Q_1 Q_0\). The next state is \(Q_1 Q_0 Q_2'\).

\[
000 \to 001 \to 011 \to 111 \to 110 \to 100 \to 000.
\]

Exactly six distinct states appear. A 3-bit Johnson counter has \(2n = 6\) states on this cycle, not \(2^3 = 8\). The two missing codes are \(010\) and \(101\). Answering 8 treats the counter as a binary counter. Answering 3 treats it as a ring counter.

### Q7

Answer: **A, B, C**

A 4-bit binary counter uses all \(2^4 = 16\) codes. A one-hot ring counter circulates a single 1, so a 4-bit ring has 4 states on its main cycle, for example \(1000 \to 0100 \to 0010 \to 0001 \to 1000\). A Johnson counter feeds back the complement and therefore has \(2n = 8\) states. Option (D) assigns the Johnson length to the ring. The ring does not visit the two-hot or zero states unless it is designed to recover into them.

### Q8

Answer: **A**

The D flip-flop stores whatever is placed on \(D\). To obtain T behaviour one must place the desired next state on \(D\), and that next state is \(T \oplus Q\). XNOR would toggle when \(T = 0\) and hold when \(T = 1\), which is the opposite control polarity. AND and OR do not complement \(Q\) when \(T = 1\) and \(Q = 1\): both give 1, so the flip-flop would stick at 1.

### Q9

Answer: **23**

The period must satisfy

\[
T \ge t_{pcq} + t_{logic} + t_{setup} = 8 + 12 + 3 = 23\ \text{ns}.
\]

Hold time is a lower-bound constraint on the contamination path. When that constraint is already satisfied, it does not increase the clock period. Adding the hold time to 23, or replacing setup by hold, answers a different timing inequality.

### Q10

Answer: **B**

The next state is \(Q^+ = X \oplus Q\). From \(Q = 0\):

| Clock | \(X\) | old \(Q\) | new \(Q\) |
|---|---|---|---|
| 1 | 0 | 0 | 0 |
| 2 | 1 | 0 | 1 |
| 3 | 0 | 1 | 1 |
| 4 | 1 | 1 | 0 |
| 5 | 1 | 0 | 1 |

The fifth clock leaves \(Q = 1\). The third row shows why (C) fails: a 0 on \(X\) does not clear \(Q\) when \(Q\) is already 1, because \(0 \oplus 1 = 1\). Option (D) would be the wiring \(D = X\). Here the old \(Q\) is part of the excitation, which is why clock 4 turns a 1 into a 0 even though \(X = 1\).

### Q11

Answer: **B**

Substitute \(J = X\) and \(K = X'\) into the JK equation:

\[
Q^+ = XQ' + (X')'Q = XQ' + XQ = X.
\]

The circuit copies \(X\) into \(Q\). It is the standard conversion from JK to D, not a forbidden input. The successive values of \(Q\) are \(1, 1, 0, 1\). After the fourth clock, \(Q = 1\).

The inputs that actually occur are \((J, K) = (1, 0)\) or \((0, 1)\). The pair \(J = K = 1\) is never applied, and even if it were, it would be a toggle on a JK flip-flop rather than an illegal code. Option (D) is right about the state after the third clock and wrong about the fourth, which loads the new \(X = 1\).

### Q12

Answer: **1**

Those T equations are the binary up counter: the LSB always toggles, and each higher bit toggles when every bit below it is 1. From unsigned state 3, six clocks add 6. Modulo 8,

\[
(3 + 6) \bmod 8 = 1,
\]

which is the state \(001\). Answering 9 forgets the wrap past \(111\). Answering 6 reports the number of clocks instead of the resulting state.

### Q13

Answer: **A, B, C**

With \(J = D\) and \(K = D'\), the calculation in Q11 shows \(Q^+ = D\). With \(S = R = 0\), neither cross-coupled gate is told to force an output, so the latch holds. With \(T = 1\), \(Q^+ = 1 \oplus Q = Q'\), so every triggering edge toggles the flip-flop.

A D flip-flop has no excitation don't care. The only value that produces a prescribed \(Q^+\) is \(D = Q^+\). Don't cares appear in the JK and SR excitation tables because those devices have more than one input combination for some transitions. Importing an \(X\) into the D column leaves the next state unspecified.

### Q14

Answer: **B**

Five states need a code space of size at least 5. Two flip-flops provide only 4 codes, which is short by one state. Three flip-flops provide 8 codes, which is enough. Four or five flip-flops also work but are not minimum. One-hot encoding would use five flip-flops; the question allows any binary encoding, so the information-theoretic minimum applies.

### Q15

Answer: **A, C, D**

The JK input \(11\) is the toggle, not a forbidden state. The characteristic equation makes this unavoidable: \(JQ' + K'Q\) becomes \(Q'\) when \(J = K = 1\). Tying \(J\) and \(K\) to the constant 1 is one way to build that toggle. Tying them to a common variable \(T\), not necessarily the constant 1, is the conversion from JK to T.

Option (B) is the SR confusion. For a NOR SR latch, \(S = R = 1\) forces both latch outputs to 0. That combination is excluded from the characteristic equation \(Q^+ = S + R'Q\), which is valid only for \(SR = 0\). Hold is \(S = R = 0\). The fact that JK uses 11 safely does not make SR use 11 safely; the cross-coupled gates are not the same input logic.

### Q16

Answer: **-1**

Hold slack is \(1 + 0 - 2 = -1\) ns. A negative slack means the old \(Q\) can change at the next flip-flop's input before the hold window has closed. The fast clock-to-\(Q\) path is the dangerous one for hold; a large clock-to-\(Q\) delay, which hurts the setup period, helps hold. Setup and hold pull the design in opposite directions. Making the clock slower does not repair this hold violation, because both the launching and the capturing edge move together. The fix is extra contamination delay in the logic, or a flip-flop with a smaller hold time.

### Q17

Answer: **B**

\(T_1 = T_0 = 1\) complements both bits on every clock. The run is

\[
00 \to 11 \to 00.
\]

The cycle contains two states. It is not the binary up counter, whose LSB toggle is 1 but whose MSB toggle is \(Q_0\), not the constant 1. States \(01\) and \(10\) are unreachable from \(00\) under this input. Answering 4 assumes every 2-bit register with constant T inputs is a mod-4 counter.

### Q18

Answer: **2**

A 4-bit rotate toward the LSB has period 4. Six clocks are the same as \(6 \bmod 4 = 2\) rotates:

\[
1000 \to 0100 \to 0010.
\]

The unsigned value of \(0010\) is 2. Two further clocks would reach \(0001\) and then \(1000\). Answering 8 interprets \(1000\) as the final state after a Johnson shift rather than a ring rotate. Answering 6 counts clocks.

### Q19

Answer: **A**

Apply \(Q_1^+ = Q_0\) and \(Q_0^+ = Q_1'\) from \(00\):

\[
00 \to 01,\qquad 01 \to 11,\qquad 11 \to 10,\qquad 10 \to 00.
\]

The cycle length is 4, and \(00\) is not stable: its next state is \(01\) because \(Q_0^+ = (Q_1)' = 1\). Option (D) is the same four states in the other order. That order would be produced by \(Q_1^+ = Q_0'\) and \(Q_0^+ = Q_1\), which is not the given excitation. Checking the first next state is enough to reject it: from \(00\) the given equations produce \(01\), not \(10\).

### Q20

Answer: **A, B, C**

A Moore output is a function of state alone. Emitting the state vector is the simplest case. Eight states need three flip-flops, and three flip-flops are exactly enough for a binary coding of those eight states. From \(101_2 = 5\), one up-count produces \(110_2 = 6\).

In the T realization the LSB toggles on every clock, so \(T_0 = 1\), not 0. Setting \(T_0 = 0\) would freeze the LSB and the counter would be unable to leave the even states. The higher toggle equations \(T_1 = Q_0\) and \(T_2 = Q_1 Q_0\) do not change the fact that \(T_0\) is the constant 1.

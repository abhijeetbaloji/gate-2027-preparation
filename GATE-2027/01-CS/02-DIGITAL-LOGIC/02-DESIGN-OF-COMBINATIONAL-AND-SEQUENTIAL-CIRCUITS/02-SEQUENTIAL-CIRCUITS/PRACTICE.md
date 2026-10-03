# Sequential Circuits — Practice

Original questions on excitation, state counting, Johnson and binary counters, and timing. They are not previous-year questions.

## Level 1 — Conceptual

### Q1 — MCQ

The characteristic equation of a JK flip-flop is

A. \(Q^+ = JQ' + K'Q\)

B. \(Q^+ = JQ' + KQ\)

C. \(Q^+ = J + K'Q\), with \(JK=1\) forbidden

D. \(Q^+ = J \oplus K\)

**Answer.** A

**Concept.** JK equation, including toggle.

**Difficulty.** Level 1

**Solution.** \(J=0, K=0\) must hold, which A does and B does not: B gives \(Q^+=0\) when \(J=K=0\) and \(Q=1\). \(J=K=1\) must complement \(Q\). A gives \(Q'\). C describes an SR equation and forbids the toggle input that JK allows.

---

### Q2 — NAT

A synchronous counter must visit 12 distinct states. The minimum number of flip-flops is ______.

**Answer.** 4

**Concept.** \(\lceil \log_2 N \rceil\).

**Difficulty.** Level 1

**Solution.** \(2^3 = 8 < 12\) and \(2^4 = 16 \ge 12\). Three flip-flops are not enough.

---

## Level 2 — Standard GATE

### Q3 — NAT

A 5-bit Johnson counter is started on its main cycle. The number of distinct states on that cycle is ______.

**Answer.** 10

**Concept.** Johnson length \(2n\).

**Difficulty.** Level 2

**Solution.** Complement feedback around 5 flip-flops fills the register with 1s in 5 clocks and clears it in 5 clocks. The main cycle has \(2\cdot 5 = 10\) states, not 32 and not 5.

---

### Q4 — MCQ

A 3-bit synchronous binary up counter uses T flip-flops. The inputs are

A. \(T_0 = 1\), \(T_1 = Q_0\), \(T_2 = Q_1 Q_0\)

B. \(T_0 = 1\), \(T_1 = 1\), \(T_2 = 1\)

C. \(T_0 = Q_0\), \(T_1 = Q_1\), \(T_2 = Q_2\)

D. \(T_0 = Q_1 Q_2\), \(T_1 = Q_2\), \(T_2 = 1\)

**Answer.** A

**Concept.** Toggle when all lower bits are 1.

**Difficulty.** Level 2

**Solution.** Bit 0 toggles every clock. Bit 1 toggles when \(Q_0=1\). Bit 2 toggles when \(Q_1 Q_0=1\). Option B toggles every bit every clock: from 000 the next state is 111, then 000. That is not binary counting.

---

## Level 3 — Multi-step

### Q5 — NAT

The output sequence \(0,1,2,0,1,3\) repeats. The two printed 0s have different futures, and so do the two printed 1s. The minimum number of flip-flops is ______.

**Answer.** 3

**Concept.** States, not output symbols.

**Difficulty.** Level 3

**Solution.** Walk the cycle. Call the steps \(s_0 \to s_1 \to s_2 \to s_3 \to s_4 \to s_5 \to s_0\) with outputs \(0,1,2,0,1,3\).

- \(s_0\) (output 0) is followed by output 1, then 2.
- \(s_3\) (output 0) is followed by output 1, then 3.

The successors differ, so \(s_0 \neq s_3\). The same argument separates the two 1s. The six steps are six states. \(2^2 = 4 < 6 \le 8\), so 3 flip-flops.

**Trap.** Counting \(\{0,1,2,3\}\) and answering 2.

---

### Q6 — NAT

Clock-to-\(Q\) delay is 5 ns, setup time is 2 ns, and the worst-case next-state delay is 9 ns. Hold time is satisfied separately. The minimum clock period, in nanoseconds, is ______.

**Answer.** 16

**Concept.** \(T \ge t_{cq} + t_{pd} + t_{su}\).

**Difficulty.** Level 3

**Solution.** \(5+9+2 = 16\). Hold time is not a term in this sum.

---

## Level 4 — Trap

### Q7 — MSQ

Select all that apply.

A. \(J=1, K=1\) toggles a JK flip-flop.

B. \(S=1, R=1\) is the hold input of a NOR SR latch.

C. \(Q^+ = JQ' + K'Q\) equals \(Q'\) when \(J=K=1\).

D. For a D flip-flop, every transition leaves \(D\) as a don’t-care.

**Answer.** A, C

**Concept.** Toggle is legal for JK and forbidden as an SR pair; D is determined.

**Difficulty.** Level 4

**Solution.** Substitute \(J=K=1\): \(Q^+ = Q' + 0\cdot Q = Q'\). NOR SR hold is \(S=R=0\). \(S=R=1\) forces both latch outputs to 0 and is not a hold. D excitation equals the required next bit on every row; there is no X in that column.

---

## Level 5 — Challenge

### Q8 — NAT

Two D flip-flops obey \(D_1 = Q_0\) and \(D_0 = Q_1'\). The start state \(Q_1 Q_0\) is \(01\). After three clocks, the state interpreted as an unsigned integer is ______.

**Answer.** 0

**Concept.** Next-state trace on a 4-cycle.

**Difficulty.** Level 5

**Solution.** From the equations, \(00 \to 01 \to 11 \to 10 \to 00\). Starting at \(01\): after one clock \(11\), after two clocks \(10\), after three clocks \(00\). Unsigned value 0.

**Trap.** Treating \(D_0 = Q_1'\) as sampled after \(Q_1\) has already updated on the same edge. Both D inputs are computed from the state before the edge.

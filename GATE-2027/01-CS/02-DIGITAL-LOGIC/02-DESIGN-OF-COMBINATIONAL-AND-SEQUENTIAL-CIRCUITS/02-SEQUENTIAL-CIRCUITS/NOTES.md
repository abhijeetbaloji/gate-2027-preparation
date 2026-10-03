# Sequential Circuits

A sequential circuit has memory. The outputs and the next memory state depend on the inputs and on what was stored. Combinational logic computes the next-state bits; flip-flops store them on a clock edge. The mapped stems (see `PYQ.md`) are characteristic equations, counters (binary, Johnson, saturating, ripple), “how many flip-flops does this sequence need,” and “how many distinct states does this clocked circuit visit.” Rows about pipelines, caches, semaphores, and TCP are in the same file and are not this topic.

---

## 1. Latch versus flip-flop

A **latch** is level-sensitive. While its enable is active, the output follows the input. A **flip-flop** is edge-triggered. It samples its inputs on a rising or falling clock edge and then holds, even if the inputs change before the next edge.

**Why the difference matters.** A ripple counter chains the clock of the next flip-flop to the output of the previous one. That only makes sense with edge-triggered flip-flops. A latch in that path would be transparent for a whole level and the chain could race through several bits in one enable pulse.

**SR latch, NOR gates.** Cross-coupled NOR gates. \(S=1, R=0\) sets \(Q=1\). \(S=0, R=1\) resets \(Q=0\). \(S=R=0\) holds. \(S=R=1\) forces both NOR outputs to 0; when the inputs then fall, the latch can settle either way. That input is forbidden, not a hold. The NAND SR latch has the opposite active level: \(S=R=0\) is the forbidden pair, and \(S=R=1\) holds.

---

## 2. Characteristic equations

\(Q\) is the state before the triggering edge. \(Q^+\) is the state after it.

| Flip-flop | Equation | What it means |
|-----------|----------|----------------|
| D | \(Q^+ = D\) | Copies the input |
| T | \(Q^+ = T \oplus Q\) | \(T=1\) toggles, \(T=0\) holds |
| JK | \(Q^+ = JQ' + K'Q\) | Set, reset, hold, or toggle |
| SR | \(Q^+ = S + R'Q\), provided \(SR=0\) | Set, reset, or hold. \(S=R=1\) is not this equation’s domain |

**Why the JK equation is right.** Check the four input pairs.

| \(J\) | \(K\) | \(Q^+ = JQ' + K'Q\) | Name |
|------:|------:|---------------------|------|
| 0 | 0 | \(Q\) | hold |
| 0 | 1 | \(0\) | reset |
| 1 | 0 | \(1\) | set |
| 1 | 1 | \(Q'\) | toggle |

\(J=K=1\) is legal on a JK flip-flop. It is the usual way to build a toggle. Substituting into the equation gives \(Q^+ = Q'\). An SR latch does not have this row.

**Conversions that questions use.**

- JK behaves as D when \(J = D\) and \(K = D'\). Then \(Q^+ = DQ' + D Q = D\).
- D behaves as T when \(D = T \oplus Q\).
- T behaves as D when \(T = D \oplus Q\), the same wire seen from the other side.

---

## 3. Excitation tables

The characteristic equation predicts \(Q^+\) from the input. The excitation table runs backwards: given \(Q\) and the \(Q^+\) you want, which input is allowed.

| Present \(Q\) | Next \(Q^+\) | \(D\) | \(T\) | \(J\) | \(K\) | \(S\) | \(R\) |
|--------------:|-------------:|------:|------:|------:|------:|------:|------:|
| 0 | 0 | 0 | 0 | 0 | X | 0 | X |
| 0 | 1 | 1 | 1 | 1 | X | 1 | 0 |
| 1 | 0 | 0 | 1 | X | 1 | 0 | 1 |
| 1 | 1 | 1 | 0 | X | 0 | X | 0 |

**Why the X appears.** For a JK, the transition \(0 \to 1\) happens both for \(J=1, K=0\) (set) and for \(J=1, K=1\) (toggle). So \(K\) is don’t-care. Using the strict value instead of X is still correct, and it may cost a larger gate. Using a 0 where the table requires a 1 is a wrong next state.

**D has no X.** \(D\) must equal the desired next state. A claim that “\(D\) is don’t-care for every transition” is false.

**Worked excitation.** Present \(Q=0\), desired \(Q^+=1\). A legal JK input is \(J=1, K=X\). \(J=0\) cannot leave 0.

---

## 4. How many flip-flops

With binary encoding, \(k\) flip-flops provide \(2^k\) states. A design that must visit \(N\) distinct states needs

\[
k = \lceil \log_2 N \rceil.
\]

**Distinct states are not distinct output numbers.** The cycle \((0,0,1,1,2,2,3,3)\) prints four numbers and has eight steps. The first 0 is followed by 0; the second 0 is followed by 1. Those are different states. \(N=8\), so \(k=3\). The cycle \(0,1,0,2,0,3\) has three different visits to output 0, plus 1, 2, and 3: six states, still three flip-flops. Two flip-flops supply only four states, so they are not enough.

This is the 2015 and 2016 counting pattern. Count states in the cycle, then take the log. Do not count the size of the output alphabet.

A Moore machine with five states needs \(\lceil \log_2 5 \rceil = 3\) flip-flops in a binary encoding. One-hot encoding would use 5. The minimum is the binary figure unless the stem fixes the code.

---

## 5. Synchronous binary counters

All flip-flops share one clock. The combinational network holds the \(T\) or \(D\) inputs.

For a T-flip-flop binary **up** counter, bit 0 toggles every clock, bit 1 toggles when bit 0 is 1, bit 2 toggles when bits 1 and 0 are both 1:

\[
T_0 = 1, \qquad T_1 = Q_0, \qquad T_2 = Q_1 Q_0, \qquad T_i = Q_{i-1} Q_{i-2} \cdots Q_0.
\]

**Why.** Bit \(i\) flips exactly when the lower bits roll from all 1s to all 0s, which is when every lower \(T\) will toggle and every lower \(Q\) is currently 1.

**Example.** State \(Q_2 Q_1 Q_0 = 011\). Then \(T_0=1\), \(T_1=1\), \(T_2=1\cdot 1=1\). All three toggle, so the next state is \(100\). Six clocks later the unsigned value is \((3+6) \bmod 8 = 1\).

**Both \(T\) inputs tied to 1.** Every bit toggles every clock. From \(00\) the cycle is \(00 \to 11 \to 00\). Two distinct states, not four. A binary up counter needs \(T_1 = Q_0\), not \(T_1 = 1\).

**Down counter.** Bit 0 still toggles every time. Bit \(i\) toggles when all lower bits are 0.

---

## 6. Ring, Johnson, ripple, saturating

### Ring counter

A 1 circulates around \(n\) flip-flops. From \(1000\), a rotate toward the LSB gives \(0100, 0010, 0001\), then back. An \(n\)-bit ring visits \(n\) states on its main cycle, not \(2n\) and not \(2^n\). It is a one-hot code. Self-correcting is a separate design; the plain ring can have other cycles if it starts with two 1s.

### Johnson counter

An \(n\)-bit shift register with the **complement** of the last bit fed back. It visits \(2n\) states on the main cycle, not \(2^n\).

One standard wiring, MSB on the left, shift toward the LSB, new MSB \(= Q_0'\):

\[
0000 \to 1000 \to 1100 \to 1110 \to 1111 \to 0111 \to 0011 \to 0001 \to 0000.
\]

As integers: \(0, 8, 12, 14, 15, 7, 3, 1\). A 4-bit Johnson counter does not count \(0,1,3,7,15,\ldots\) (that is a different shift of 1s without the return half) and does not count the even numbers. The 2015 stem’s options include this sequence. The initial state in that stem is \(0000\); a different initial state on the same cycle is a rotation of this list. An initial state off the cycle (for example \(0101\)) can sit on a different, shorter cycle. The stem’s initial value is part of the question.

A 3-bit Johnson counter from \(000\) visits \(2\cdot 3 = 6\) states before returning.

### Ripple counter

The output of one flip-flop clocks the next. For a binary ripple counter the LSB is clocked by the external clock and toggles at half the clock frequency if it is a T flip-flop with \(T=1\), or a JK with \(J=K=1\). Each next bit toggles half as often. The MSB of an \(n\)-bit counter completes one cycle every \(2^n\) clocks.

If the waveform at the last flip-flop of a 4-bit ripple counter has period \(64\,\mu s\), that waveform’s frequency is \(1/64\,\mu s = 15.625\,\text{kHz}\), and the clock frequency is \(16\) times larger, \(250\,\text{kHz}\). The mapped 2025 stem says “frequency of the ripple counter.” That phrase does not by itself say whether the clock or the MSB is wanted. Compute the relationship, then match the noun in the paper. Do not assume a memorised number.

### Saturating counter

A saturating up counter stops at its maximum code instead of wrapping to 0. A saturating down counter stops at 0. A 2-bit saturating up counter: \(00 \to 01 \to 10 \to 11 \to 11\). The next-state table is what gets converted into \(T\) or \(D\) inputs. At the saturated state the excitation must be “hold,” not “toggle.” The 2026 and 2017 stems are this table, including an up/down input.

---

## 7. Tracing a small synchronous circuit

On each clock:

1. Read \(Q\) now. The flip-flop ignores input changes until the edge.
2. Evaluate \(D\), \(T\), or \(J,K\) from the combinational equations, using that \(Q\).
3. Apply the characteristic equation to get \(Q^+\).
4. That \(Q^+\) is the input to the next evaluation.

**Example.** \(D = X \oplus Q\), \(Q\) starts at 0, and \(X\) on five clocks is \(0,1,0,1,1\).

| Clock | \(X\) | \(Q\) before | \(D\) | \(Q\) after |
|------:|------:|-------------:|------:|------------:|
| 1 | 0 | 0 | 0 | 0 |
| 2 | 1 | 0 | 1 | 1 |
| 3 | 0 | 1 | 1 | 1 |
| 4 | 1 | 1 | 0 | 0 |
| 5 | 1 | 0 | 1 | 1 |

After the fifth clock, \(Q=1\). This is a T flip-flop controlled by \(X\): it toggles only when \(X=1\).

**Two flip-flops.** \(D_1 = Q_0\), \(D_0 = Q_1'\), start \(Q_1 Q_0 = 00\).

| Now | \(D_1 = Q_0\) | \(D_0 = Q_1'\) | Next |
|-----|---------------|----------------|------|
| 00 | 0 | 1 | 01 |
| 01 | 1 | 1 | 11 |
| 11 | 1 | 0 | 10 |
| 10 | 0 | 0 | 00 |

Cycle \(00 \to 01 \to 11 \to 10\), length 4. The other starting states are on the same cycle.

**JK with \(J=X\), \(K=X'\).** This is the D conversion: \(Q^+ = X\). It is not a forbidden SR input. From \(Q=0\) and \(X = 1,1,0,1\), the state after each clock is \(1,1,0,1\). After four clocks, \(Q=1\).

---

## 8. Timing

Let \(t_{cq}\) be the clock-to-\(Q\) delay, \(t_{pd}\) the worst-case delay of the next-state logic, \(t_{su}\) the setup time, \(t_{hold}\) the hold time, and \(t_{cd}\) the contamination delay (minimum delay) of the next-state logic.

\[
T_{clk} \ge t_{cq} + t_{pd} + t_{su}
\]

**Why.** After the edge, \(Q\) becomes valid only after \(t_{cq}\). The next-state gates need \(t_{pd}\) more. The result must be stable at the flip-flop input for \(t_{su}\) before the next edge. Hold time is a separate inequality and does not get added into this minimum period.

\[
t_{cq}(\min) + t_{cd} \ge t_{hold}
\]

**Why.** The new data must not race through a very fast path and change the input while the flip-flop is still required to hold the previous sample. Hold slack is \(t_{cq}(\min) + t_{cd} - t_{hold}\). A negative slack means the hold constraint fails, independent of how slow you make the clock.

**Example.** \(t_{cq}=8\,\text{ns}\), \(t_{su}=3\,\text{ns}\), \(t_{pd}=12\,\text{ns}\). Minimum period \(8+12+3=23\,\text{ns}\). If \(t_{cq}(\min)=1\), \(t_{cd}=0\), \(t_{hold}=2\), the hold slack is \(1+0-2 = -1\,\text{ns}\): hold is violated.

---

## 9. Moore and Mealy

A **Moore** output is a function of the state only. A **Mealy** output is a function of the state and the current input, so it can change in the middle of a clock period when the input changes.

A synchronous counter whose output is the state vector is Moore. An edge detector that outputs 1 only while the input is 1 and the state says “previous bit was 0” is Mealy.

The 2021 string-rewriting stem (“replace the first 1 in a string of 0s and 1s”) is a small FSM: the state remembers whether that first 1 has already been seen. Write the state diagram before writing equations. The number of states is the number of memories the sentence requires, not the length of the string.

---

## 10. Solving procedure

1. Decide latch or edge-triggered flip-flop. Forbidden \(S=R=1\) applies to the NOR latch, not to JK.
2. If the stem gives a next-state table, fill the excitation table for the named flip-flop. Simplify \(J, K\) or \(T\) with a K-map. Don’t-cares in the excitation are real don’t-cares.
3. If the stem gives a sequence of output numbers, split repeated numbers into different states whenever their successors differ. Then \(k=\lceil \log_2 N \rceil\).
4. If the stem gives gates between flip-flops, make a table: present state, input, next state. Walk the stated number of clocks. Count distinct rows in the cycle actually reached from the given initial state.
5. Ring: \(n\) states on the one-hot cycle. Johnson: \(2n\). Binary: \(2^n\). Saturating: \(2^n\) codes but the ends hold.
6. Ripple frequency: MSB period \(= 2^n\) clock periods. Read which frequency the question names.
7. Period and hold are different inequalities. Do not add hold time to the clock period.

---

## 11. Traps

| Trap | Correction |
|------|------------|
| \(S=R=1\) called hold | Forbidden on a NOR SR latch. Hold is \(S=R=0\) |
| \(J=K=1\) called forbidden | Legal toggle on JK |
| \(Q^+ = JQ' + KQ\) | The reset term is \(K'Q\), not \(KQ\) |
| Repeated outputs counted once | States differ when successors differ |
| Johnson length \(2^n\) | Length \(2n\) |
| Ring length \(2n\) | Length \(n\) on the one-hot cycle |
| Both \(T\) pins tied to 1 | Not a binary counter |
| Hold time added to the period | Hold is a minimum-delay check |
| MSB frequency called the clock | MSB runs at \(f/2^n\) |
| Mux feedback called a flip-flop | A mux loop is a latch: transparent while selected |

---

## 12. Connections

- **Algebra and K-maps.** \(J\), \(K\), \(T\), and \(D\) are Boolean functions of state and input. Excitation don’t-cares are the X cells on that map.
- **Combinational blocks.** A counter feeding a decoder walks the decoder outputs. A mux in a next-state equation is still the Shannon formula.
- **Fixed-point counters.** A binary up counter’s state is an unsigned integer. Saturating behaviour is an arithmetic clamp, implemented by a different next-state equation at the ends.
- **Computer organisation.** Setup and hold are the same constraints as in a pipeline register. The pipeline questions stored in this mapping folder are not sequential-design questions; the timing identities are.

# TCP Congestion Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

These questions use TCP Reno with the following rules. The congestion window `cwnd` and the threshold `ssthresh` are counted in MSS. While `cwnd < ssthresh`, slow start doubles `cwnd` once per RTT. While `cwnd ≥ ssthresh`, congestion avoidance adds 1 MSS per RTT. On a timeout, `ssthresh` becomes half of `cwnd` (an integer here) and `cwnd` becomes 1 MSS. On three duplicate acknowledgements, Reno sets `ssthresh` to half of `cwnd` and, once fast recovery finishes, continues in congestion avoidance with `cwnd` equal to that new threshold. It does not reset `cwnd` to 1 on three duplicate acknowledgements.

## Level 1 — Conceptual

## Q1 — MCQ

During slow start, while the congestion window is below the threshold, TCP Reno

A. doubles the congestion window once per RTT
B. adds 1 MSS per RTT
C. holds the window constant until a timeout
D. cuts the window in half on every acknowledgement

---

## Q2 — MSQ

Select all that apply. Congestion avoidance in this Reno model is additive increase. A later loss causes multiplicative decrease. Which statements match that description?

A. The window grows by 1 MSS per RTT while it is at or above the threshold.
B. A timeout sets the threshold to half the current window.
C. The window doubles on every RTT for the entire connection, including after the threshold.
D. Multiplicative decrease on a timeout is the cut of the threshold to half, followed by a return of the window to 1 MSS.

---

## Q3 — MCQ

The slow-start threshold is the boundary at which Reno

A. stops doubling and starts adding 1 MSS per RTT
B. closes the connection
C. switches from bytes to packets
D. disables acknowledgements

---

## Q4 — NAT

`ssthresh` is 16 MSS and `cwnd` starts at 1 MSS. There is no loss. Enter the number of RTTs required until `cwnd` first becomes 16.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

A timeout occurs while `cwnd` is 16 MSS. Immediately after Reno applies the timeout rule,

A. `ssthresh` is 8 and `cwnd` is 1
B. `ssthresh` is 16 and `cwnd` is 16
C. `ssthresh` is 8 and `cwnd` is 8
D. `ssthresh` is 1 and `cwnd` is 16

---

## Q6 — MCQ

Three duplicate acknowledgements tell Reno that

A. a segment was likely lost and fast retransmit should resend it without waiting for a timeout
B. the receiver window is zero
C. slow start must begin again from 1 MSS in this Reno model
D. the connection must be reset

---

## Q7 — MSQ

Select all that apply. Under the Reno rules in the introduction, which statements are true?

A. A timeout sets `cwnd` to 1 MSS.
B. Three duplicate acknowledgements set `cwnd` to 1 MSS.
C. Three duplicate acknowledgements set `ssthresh` to half of `cwnd`.
D. After fast recovery, congestion avoidance continues from the new threshold rather than from 1 MSS.

---

## Q8 — NAT

`ssthresh` is 16 MSS and `cwnd` starts at 1 MSS. There is no loss. In each RTT the sender transmits a number of segments equal to the `cwnd` at the start of that RTT, then the window grows. Enter the number of segments transmitted during the first 6 RTTs.

---

## Q9 — MCQ

`ssthresh` is 16 MSS and `cwnd` starts at 1. There is no loss. At the start of the 6th RTT the window is 17 MSS. The connection is then in

A. congestion avoidance
B. slow start, and the next step doubles 17 to 34
C. fast recovery
D. timeout recovery, with the window forced to 1

---

## Level 3 — Multi-Step

## Q10 — MCQ

After a timeout at `cwnd` = 16, so that `ssthresh` is 8 and `cwnd` is 1, the window grows with no further loss. The sequence of window sizes at the ends of successive RTTs begins 2, 4, 8, 9. The value 9 means the connection has

A. left slow start, because the window reached the threshold and the next growth is additive
B. stayed in slow start, so the step after 8 must be 16
C. suffered another timeout
D. switched the unit from MSS to bytes

---

## Q11 — NAT

A timeout occurs when `cwnd` is 16 MSS, so `ssthresh` becomes 8 and `cwnd` becomes 1. No further loss occurs. Enter the number of additional RTTs until `cwnd` first equals 16 again.

---

## Q12 — MSQ

Select all that apply. Fast recovery in this Reno description means

A. three duplicate acknowledgements do not return `cwnd` to 1
B. `ssthresh` becomes half the window that was in use when the loss was detected
C. the sender waits for a timeout before retransmitting
D. after recovery, the window grows by 1 MSS per RTT from the new threshold

---

## Q13 — MCQ

`cwnd` is 20 MSS and three duplicate acknowledgements arrive. No timeout occurs. Immediately after Reno finishes fast recovery, `cwnd` is

A. 10 MSS
B. 1 MSS
C. 20 MSS
D. 40 MSS

---

## Level 4 — Tricky / Trap-Based

## Q14 — NAT

Use the same event: `cwnd` is 20 MSS and three duplicate acknowledgements arrive. Reno sets the window, after fast recovery, to the new threshold. Enter that window in MSS. Do not apply the timeout rule.

---

## Q15 — MCQ

Fast retransmit is triggered by

A. three duplicate acknowledgements
B. the first duplicate acknowledgement
C. a zero advertised window
D. the window reaching `ssthresh` with no loss

---

## Q16 — MSQ

Select all that apply. Which claims misstate the Reno rules given above?

A. During congestion avoidance the window doubles every RTT.
B. During slow start the window grows by only 1 MSS per RTT.
C. A timeout sets `ssthresh` to the current `cwnd` and leaves `cwnd` unchanged.
D. Three duplicate acknowledgements, in this Reno model, do not set `cwnd` to 1.

---

## Level 5 — Challenge

## Q17 — MCQ

`ssthresh` starts at 8 MSS and `cwnd` starts at 1 MSS. There is no loss. Consider the RTT in which the sender transmits 8 MSS. At the start of that RTT, `cwnd` is 8, which is not strictly below the threshold, so the growth rule adds 1. At the end of that RTT, `cwnd` is

A. 9
B. 16
C. 8
D. 10

---

## Q18 — MSQ

Select all that apply. `cwnd` is 12 MSS and the connection is in congestion avoidance. A timeout occurs. Then two RTTs pass with no loss. Then three duplicate acknowledgements occur, and fast recovery finishes. Which statements are true?

A. Immediately after the timeout, `cwnd` is 1 MSS.
B. Immediately after the timeout, `ssthresh` is 6 MSS.
C. After the three duplicate acknowledgements, Reno sets `cwnd` to 1 MSS.
D. After fast recovery finishes, `cwnd` is 2 MSS.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | NAT | 4 |
| 5 | MCQ | A |
| 6 | MCQ | A |
| 7 | MSQ | A, C, D |
| 8 | NAT | 48 |
| 9 | MCQ | A |
| 10 | MCQ | A |
| 11 | NAT | 11 |
| 12 | MSQ | A, B, D |
| 13 | MCQ | A |
| 14 | NAT | 10 |
| 15 | MCQ | A |
| 16 | MSQ | A, B, C |
| 17 | MCQ | A |
| 18 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: A

Slow start is the exponential phase: one doubling per RTT while `cwnd < ssthresh`. Adding 1 MSS is congestion avoidance. The window is not frozen, and a single acknowledgement does not halve it. The halving events are loss events, not ordinary acknowledgements.

### Q2

Answer: A, B, D

Additive increase is +1 MSS per RTT at or above the threshold. A timeout halves the threshold and restarts the window at 1, which is the multiplicative cut followed by slow start. C keeps doubling after the threshold and erases the difference between the two phases.

### Q3

Answer: A

The threshold is only a change of growth law. It does not close the connection, change the sequence-number unit, or turn acknowledgements off.

### Q4

Answer: 4

The window at the end of each RTT, starting from 1, with the threshold at 16:

\[
2,\ 4,\ 8,\ 16
\]

The fourth RTT is the one that doubles 8 to 16. Three RTTs would leave the window at 8. Five RTTs would already be in congestion avoidance, at 17.

### Q5

Answer: A

Half of 16 is 8, and a timeout sets the window itself to 1, not to the new threshold. B leaves both values untouched. C is the three-duplicate-ACK outcome, not the timeout outcome. D halves the wrong variable.

### Q6

Answer: A

Three duplicate acknowledgements are the fast-retransmit signal: a later byte has arrived, so the missing segment should be sent now. They are not a zero window. In this Reno model they do not restart slow start from 1, and they do not reset the connection.

### Q7

Answer: A, C, D

Timeout and three duplicate acknowledgements both halve the threshold. Only the timeout sets `cwnd` to 1. After fast recovery, Reno continues from the halved window. B is the Tahoe behaviour, and it contradicts the Reno rule stated for these questions.

### Q8

Answer: 48

Windows at the start of the six RTTs:

\[
1,\ 2,\ 4,\ 8,\ 16,\ 17
\]

The fifth RTT starts at 16. Because \(16 \ge 16\), the window then grows by 1, so the sixth RTT starts at 17.

\[
1+2+4+8+16+17 = 48
\]

Doubling through the sixth RTT would send \(1+2+4+8+16+32 = 63\) and would ignore the threshold. Stopping at the end of slow start sends \(1+2+4+8 = 15\), which is only four RTTs.

### Q9

Answer: A

The window became 16 by doubling, met the threshold, and the next RTT added 1 to make 17. That additive step is congestion avoidance. It is not another doubling, not fast recovery, and not a timeout.

### Q10

Answer: A

Growth from 1 with threshold 8:

- \(1 < 8\), so the first RTT ends at 2
- \(2 < 8\), so the next ends at 4
- \(4 < 8\), so the next ends at 8
- \(8 \ge 8\), so the next ends at 9

The step from 8 to 9 is the first additive step. Doubling 8 to 16 would require the strict test `cwnd < ssthresh` to be true at 8, and \(8 < 8\) is false under the rule used here. Nothing in the question says another timeout occurred.

### Q11

Answer: 11

After the timeout the window is 1 and the threshold is 8. Ends of successive RTTs:

\[
2,\ 4,\ 8,\ 9,\ 10,\ 11,\ 12,\ 13,\ 14,\ 15,\ 16
\]

That is 3 RTTs to reach 8, then 8 more RTTs to climb from 8 to 16 by adding 1 each time. \(3 + 8 = 11\). A common miss is to double from 8 to 16 in one extra RTT and answer 4. Another is to count the starting window as an RTT and answer 12.

### Q12

Answer: A, B, D

Fast recovery keeps the window at the halved threshold instead of at 1, and the following growth is additive. The retransmission itself is the fast retransmit and does not wait for a timeout, so C is false.

### Q13

Answer: A

\[
\lfloor 20 / 2 \rfloor = 10
\]

Reno’s post-recovery window is 10 MSS. B applies the timeout action to a three-duplicate-ACK event. C ignores the loss. D doubles the window in the wrong direction.

### Q14

Answer: 10

The new threshold is half of 20, and the recovered window equals that threshold. The timeout answer 1 is the trap. The question says not to apply the timeout rule.

### Q15

Answer: A

The usual trigger is the third duplicate acknowledgement, which is enough evidence to retransmit before the retransmission timer fires. The first duplicate can be a reordering and is not the trigger. A zero window is flow control. Reaching the threshold is the change from slow start to congestion avoidance, not a loss signal.

### Q16

Answer: A, B, C

A, B, and C each swap the two phases or skip the reset to 1 after a timeout. D correctly states the Reno rule for three duplicate acknowledgements, so it is not a misstatement. The question asks for the claims that are wrong, and D is the one that is right.

### Q17

Answer: A

The RTT that sends 8 MSS starts with `cwnd = 8`. The test `8 < 8` fails, so congestion avoidance adds 1 and the window ends at 9. B doubles as if slow start were still in force. C leaves the window unchanged, which neither phase does. D would be the window two additive RTTs later, or half of 20, neither of which is this step.

### Q18

Answer: A, B, D

The timeout at 12 sets `ssthresh = 6` and `cwnd = 1`. The next two lossless RTTs see \(1 < 6\) and then \(2 < 6\), so the window goes \(1 \to 2 \to 4\). Three duplicate acknowledgements at window 4 set the threshold to 2 and finish recovery at `cwnd = 2`, not at 1. C is the timeout rule applied to the wrong event.

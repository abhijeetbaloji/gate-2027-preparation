# Medium Access Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Pure ALOHA does not divide time into slots and does not sense the carrier. If a frame takes time \(T\) to transmit, the vulnerable period in which another transmission can collide with it is

A. \(T/2\)
B. \(T\)
C. \(2T\)
D. \(4T\)

---

## Q2 — MSQ

Select all that apply. Which statements about random access are correct?

A. Pure ALOHA may begin a transmission even when another station is already transmitting.
B. Slotted ALOHA allows a station to start a frame only at a slot boundary.
C. Carrier sensing means a station listens before it transmits.
D. In pure ALOHA the maximum throughput of the channel is 1, because collisions are impossible.

---

## Q3 — NAT

A frame takes 40 ms to transmit. Enter the vulnerable period of pure ALOHA for this frame, in milliseconds.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Slotted ALOHA has throughput \(S = G e^{-G}\), where \(G\) is the offered load in frames per frame time. \(S\) is maximum when

A. \(G = 1\), and the maximum is \(1/e\)
B. \(G = 0.5\), and the maximum is \(1/(2e)\)
C. \(G = 2\), and the maximum is \(2/e\)
D. \(G = 1\), and the maximum is \(1\)

---

## Q5 — MCQ

In 1-persistent CSMA, a station that finds the medium busy

A. waits until the medium goes idle and then transmits immediately
B. waits a random time and then senses again, without watching for the idle moment
C. transmits immediately even though the medium is busy
D. drops the frame and never retries

---

## Q6 — MSQ

Select all that apply. Which descriptions match the named rule?

A. Non-persistent CSMA: if the medium is busy, wait a random time and sense again.
B. \(p\)-persistent CSMA: if the medium is idle, transmit with probability \(p\) and otherwise defer.
C. 1-persistent CSMA: if the medium is busy, discard the frame.
D. ALOHA: sense the carrier and transmit only when the medium is idle.

---

## Level 3 — Multi-Step

## Q7 — MCQ

CSMA/CD detects a collision while the sender is still transmitting. For one-way propagation \(T_p\), the frame transmission time must be at least

A. \(T_p\)
B. \(2T_p\)
C. \(T_p/2\)
D. \(4T_p\)

---

## Q8 — NAT

Use the efficiency formula \(\eta = 1/(1+5a)\) with \(a = T_p/T_t\). Here \(T_p = 20\) µs, \(T_t = 200\) µs, and the bandwidth is 6 Mbps. Enter the throughput in Mbps as an integer.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

A student says pure ALOHA and slotted ALOHA have the same vulnerable period \(T\). For a frame of duration \(T\), which statement is correct?

A. Both vulnerable periods are \(T\).
B. Pure ALOHA’s vulnerable period is \(2T\), and slotted ALOHA’s is \(T\).
C. Pure ALOHA’s vulnerable period is \(T\), and slotted ALOHA’s is \(2T\).
D. Both vulnerable periods are \(2T\).

---

## Q10 — MSQ

Select all that apply. Which statements about persistence and collisions are true?

A. 1-persistent CSMA can collide when two stations were waiting and both transmit the moment the medium becomes idle.
B. Non-persistent CSMA reduces that particular collision by backing off a random time instead of transmitting at the idle instant.
C. Carrier sensing removes every collision, so CSMA never needs retransmission.
D. Slotted ALOHA still has collisions; the slot boundary only shortens the vulnerable period relative to pure ALOHA.

---

## Level 5 — Challenge

## Q11 — NAT

One-way propagation is 16 µs. A CSMA/CD sender must still be transmitting when a collision indication from the far end can return. Enter the minimum frame transmission time in microseconds.

---

## Q12 — MCQ

Pure ALOHA throughput is \(S = G e^{-2G}\). Slotted ALOHA throughput is \(S = G e^{-G}\). At the load that maximises each protocol, the two maximum throughputs compare as

A. pure \(1/(2e)\), slotted \(1/e\), so slotted is twice pure
B. both equal \(1/e\)
C. pure \(1/e\), slotted \(1/(2e)\)
D. both equal \(1/2\)

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MSQ | A, B, C |
| 3 | NAT | 80 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B |
| 7 | MCQ | B |
| 8 | NAT | 4 |
| 9 | MCQ | B |
| 10 | MSQ | A, B, D |
| 11 | NAT | 32 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: C

A frame that starts up to \(T\) before this frame overlaps its beginning, and a frame that starts up to \(T\) after this frame’s start overlaps its end. The vulnerable window is \(2T\). Slotted ALOHA cuts this to one slot, which is why \(T\) and \(T/2\) are the traps. \(4T\) has no role in the basic vulnerable-period argument.

### Q2

Answer: A, B, C

Pure ALOHA does not listen, so it can transmit into an ongoing frame. Slotted ALOHA restricts the start time to a boundary. Carrier sensing is the “listen first” step in CSMA. D is false: ALOHA’s throughput is far below 1 because collisions are the central event, and the pure-ALOHA maximum is \(1/(2e)\).

### Q3

Answer: 80

\[
2 \times 40 = 80 \text{ ms}
\]

Entering 40 uses the slotted vulnerable period on a pure-ALOHA question.

### Q4

Answer: A

\[
\frac{dS}{dG} = e^{-G}(1 - G) = 0 \Rightarrow G = 1, \quad S = \frac{1}{e}
\]

B is the pure-ALOHA operating point, where \(S = G e^{-2G}\) peaks at \(G = 1/2\) with value \(1/(2e)\). C evaluates \(2/e\), which is not \(S(2)\). D claims a perfect channel at \(G = 1\); \(e^{-1}\) is about 0.368, not 1.

### Q5

Answer: A

“1-persistent” means that once the medium is idle, the station transmits with probability 1. While the medium is busy it keeps sensing. B is non-persistent. C is ALOHA, which does not wait for idle. D is not the persistence rule.

### Q6

Answer: A, B

Non-persistent backs off and senses later. \(p\)-persistent tosses a coin with probability \(p\) when it finds the medium idle. 1-persistent does not discard a frame just because the medium was busy; it waits for idle, so C is false. ALOHA does not sense the carrier, so D describes CSMA rather than ALOHA.

### Q7

Answer: B

The collision news from the far end takes \(T_p\) to reach the sender’s signal and another \(T_p\) to come back. The sender is sure to notice the collision while it is still on the air only if the frame lasts at least \(2T_p\). \(T_p\) is only one way. \(4T_p\) doubles the round trip again without a reason in this model.

### Q8

Answer: 4

\[
a = \frac{20}{200} = 0.1, \quad 5a = 0.5, \quad \eta = \frac{1}{1.5} = \frac{2}{3}
\]

\[
\frac{2}{3} \times 6 = 4 \text{ Mbps}
\]

Using \(a = 20/200\) but then computing \(1/(1+a)\) gives \(6/1.1\), which is not the formula in the stem. Using \(2T_p\) inside \(a\) doubles \(a\) and is a different model.

### Q9

Answer: B

Pure ALOHA can be hit by a frame that started during the previous frame time or during this one, so the window is \(2T\). Slotting removes the “previous frame time” half, leaving \(T\). A, C, and D each swap or share those windows.

### Q10

Answer: A, B, D

Two stations that both persisted through a busy period transmit together when the medium clears, so 1-persistence has a characteristic collision. Non-persistence avoids that instant by a random wait. Carrier sensing does not stop two stations from picking the same idle moment, and a collision can also occur inside the propagation window, so C is false. Slotted ALOHA still collides when two stations pick the same slot; it only shortens vulnerability from \(2T\) to \(T\).

### Q11

Answer: 32

\[
2 \times 16 = 32 \text{ µs}
\]

The far-end collision indication is a round trip away. A 16 µs frame would finish before that indication returned, so the sender could complete a short frame and miss the collision.

### Q12

Answer: A

Pure ALOHA peaks at \(G = 1/2\):

\[
S = \frac{1}{2} e^{-1} = \frac{1}{2e}
\]

Slotted ALOHA peaks at \(G = 1\):

\[
S = e^{-1} = \frac{1}{e}
\]

So the slotted maximum is twice the pure maximum. B and C swap or equate the two peaks. D uses \(1/2\), which is neither \(1/e\) nor \(1/(2e)\).

# Ethernet — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A standard Ethernet MAC address is

A. 32 bits
B. 48 bits
C. 64 bits
D. 128 bits

---

## Q2 — MSQ

Select all that apply. Which fields are part of the Ethernet frame that is protected and counted toward the 64-byte minimum (destination address through FCS)?

A. Destination MAC address
B. Source MAC address
C. Frame check sequence
D. Preamble and start-of-frame delimiter

---

## Q3 — NAT

A shared coaxial segment is 500 m long. Propagation speed is \(2 \times 10^8\) m/s and the bandwidth is 100 Mbps. A sender must still be transmitting when a collision signal from the far end returns. Enter the minimum frame length this constraint requires, in bits.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The classic minimum Ethernet frame, from destination address through FCS, is 64 bytes. The header fields before the data, together with the 4-byte FCS, occupy 18 bytes. The minimum data field, using padding if the payload is shorter, is

A. 46 bytes
B. 64 bytes
C. 18 bytes
D. 1500 bytes

---

## Q5 — MCQ

After a collision, classic Ethernet chooses a random backoff using binary exponential backoff. After \(n\) collisions, with \(n \le 10\), the station draws a wait uniformly from

A. \(0, 1, \ldots, 2^n - 1\) slot times
B. \(1, 2, \ldots, 2^n\) slot times
C. exactly \(2^n\) slot times, with no random choice
D. \(0, 1, \ldots, 10\) slot times, regardless of \(n\)

---

## Q6 — MSQ

Select all that apply. Classic shared-medium Ethernet CSMA/CD includes

A. sensing the carrier before transmitting
B. detecting a collision while transmitting
C. sending a jam signal so that other stations reliably notice the collision
D. reserving the medium with a virtual circuit before every frame

---

## Level 3 — Multi-Step

## Q7 — MCQ

Classic Ethernet on a shared medium is 1-persistent CSMA/CD. If a station finds the medium busy, it

A. transmits anyway
B. waits until the medium is idle and then transmits
C. waits a random time without monitoring the medium, then senses from scratch
D. drops the frame

---

## Q8 — NAT

A station has just seen its 4th consecutive collision, and \(k = \min(4, 10) = 4\). Enter the number of possible backoff choices.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

A student adds the 7-byte preamble and the 1-byte start-of-frame delimiter and says the minimum frame used for the collision slot is 72 bytes. For the classic 512-bit minimum that corresponds to the slot time, the length counted from the destination address through the FCS is

A. 64 bytes
B. 72 bytes
C. 46 bytes
D. 1518 bytes

---

## Q10 — MSQ

Select all that apply. Which statements are true?

A. The FCS is an error-detection field, not a next-hop address.
B. A full-duplex switched Ethernet link runs CSMA/CD on that link because full duplex still shares a coaxial bus.
C. Classic half-duplex shared Ethernet uses CSMA/CD.
D. The destination address in a standard Ethernet frame is 48 bits.

---

## Level 5 — Challenge

## Q11 — NAT

A 500-bit frame is transmitted at 100 Mbps. Enter the transmission time in microseconds.

---

## Q12 — MCQ

After 6 consecutive collisions, \(k = \min(6, 10) = 6\). The maximum backoff delay, in slot times, is

A. 63
B. 64
C. 32
D. 6

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, C |
| 3 | NAT | 500 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B, C |
| 7 | MCQ | B |
| 8 | NAT | 16 |
| 9 | MCQ | A |
| 10 | MSQ | A, C, D |
| 11 | NAT | 5 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

A standard MAC address is 48 bits, written as six octets. 32 bits is the size of an IPv4 address. 64 and 128 bits are not the Ethernet MAC length.

### Q2

Answer: A, B, C

The 64-byte minimum runs from the destination MAC through the FCS and includes the source MAC. The preamble and start-of-frame delimiter are sent on the wire ahead of that frame and are not part of the 64-byte count. Including them is the 72-byte trap.

### Q3

Answer: 500

One-way delay:

\[
\frac{500}{2 \times 10^8} = 2.5 \times 10^{-6} \text{ s}
\]

The sender must cover a round trip:

\[
100 \times 10^6 \times 2 \times 2.5 \times 10^{-6} = 500 \text{ bits}
\]

Using only one-way propagation gives 250 bits. Forgetting to convert 500 m, or using \(2 \times 10^8\) km/s, moves the result by orders of magnitude. This number is the constraint of this short segment; the classic 512-bit minimum is a separate standard floor and is not what this calculation asks for.

### Q4

Answer: A

\[
64 - 18 = 46
\]

The 18 bytes are destination (6), source (6), length or type (2), and FCS (4). A payload shorter than 46 bytes is padded so the frame still reaches 64 bytes. B is the whole minimum frame. C is the non-data overhead. D is the maximum payload, 1500 bytes, not the minimum.

### Q5

Answer: A

After \(n\) collisions the draw is uniform on \(\{0, 1, \ldots, 2^n - 1\}\) while \(n \le 10\). There are \(2^n\) choices, and the largest wait is \(2^n - 1\) slots, not \(2^n\). B starts at 1 and ends at \(2^n\), which shifts the range. C removes the randomness. D freezes the range at the attempt limit.

### Q6

Answer: A, B, C

CSMA/CD senses the carrier, detects collisions, and uses a jam so every station sees a collision that is long enough to notice. A virtual-circuit reservation before each frame is not part of Ethernet’s medium access, so D is false.

### Q7

Answer: B

1-persistent means the station transmits with probability 1 when it finds the medium idle. If the medium is busy, it keeps watching and sends when the medium clears. A is transmission without sensing. C is non-persistent. D drops the frame, which this rule does not do.

### Q8

Answer: 16

\[
2^4 = 16
\]

The choices are the slot counts 0 through 15. The trap is to answer 15, which is the maximum wait, or 4, which is the collision count. The question asks for the number of choices.

### Q9

Answer: A

The classic slot is 512 bit-times, which is 64 bytes, measured from the destination address through the FCS. The preamble and start-of-frame delimiter add 8 bytes on the wire and are outside that 64-byte minimum, so 72 counts bytes the slot definition does not count. 46 is only the minimum data field. 1518 is the maximum frame from destination through FCS, not the minimum.

### Q10

Answer: A, C, D

The FCS is the frame check sequence used for error detection. Classic shared Ethernet is half duplex and uses CSMA/CD. The destination MAC is 48 bits. B is false: a full-duplex link between a host and a switch is not a shared coaxial bus, and CSMA/CD is not used on that full-duplex link. There is no contention with the switch on a separate transmit pair.

### Q11

Answer: 5

\[
\frac{500}{100 \times 10^6} = 5 \times 10^{-6} \text{ s} = 5 \text{ µs}
\]

This is the transmission time of the 500-bit minimum computed for the 500 m segment at 100 Mbps. Answering 500 repeats the length in bits. Answering 2.5 uses the one-way propagation of that segment instead of the transmission time.

### Q12

Answer: A

\[
2^6 - 1 = 63
\]

The station may wait 0, 1, …, or 63 slot times, so the maximum is 63. B is the number of choices, \(2^6 = 64\), not the maximum wait. C is the maximum after 5 collisions. D is the collision count itself.

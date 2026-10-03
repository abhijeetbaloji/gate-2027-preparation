# TCP Flow Control — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Sequence numbers count bytes. An acknowledgement number is the next byte the receiver expects. The sender’s usable window is the minimum of the congestion window and the receiver’s advertised window.

## Level 1 — Conceptual

## Q1 — MCQ

The receiver’s advertised window exists so that

A. the sender does not transmit more data than the receiver can buffer
B. the sender doubles its rate on every round trip
C. lost segments are detected by a timeout only
D. the three-way handshake can be skipped

---

## Q2 — MSQ

Select all that apply. Which statements about TCP flow control are correct?

A. The amount the sender may have in flight is limited by the advertised window.
B. It is also limited by the congestion window; the usable window is the smaller of the two.
C. The acknowledgement number names the last byte the application has printed.
D. Sequence numbers advance by the number of data bytes, not by one per segment regardless of length.

---

## Q3 — MCQ

A receiver has collected every byte up to and including byte 4999. The acknowledgement number it sends is

A. 4999
B. 5000
C. 4998
D. 1

---

## Q4 — NAT

The receive buffer is 32,000 bytes. Of those, 12,500 bytes are occupied by data the application has not yet taken. Enter the advertised window in bytes.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

A segment carries 1460 bytes of data and the first byte has sequence number 4001. The sequence number of the following byte, the one not in this segment, is

A. 5461
B. 5460
C. 4001
D. 1460

---

## Q6 — MCQ

The receiver advertises a window of 0. The sender stops. So that the sender can notice when space appears again, TCP uses

A. a persist timer that sends window probes
B. an immediate abort of the connection
C. a switch from bytes to packets in the sequence space
D. a new three-way handshake for every later segment

---

## Q7 — MSQ

Select all that apply. Silly-window behaviour and the usual defences include which of the following?

A. A receiver that advertises a tiny amount of free space can cause tiny segments.
B. Clark’s receiver-side rule waits until a worthwhile amount of space is free before advertising it.
C. Nagle’s algorithm can hold back a small send while data is still unacknowledged.
D. The congestion window is required to stay at 1 MSS for the whole connection.

---

## Q8 — NAT

The latest acknowledgement number is 7000, so byte 7000 is the next byte the receiver wants. The sender has transmitted bytes up to and including sequence number 8999. Enter the number of unacknowledged bytes.

---

## Level 3 — Multi-Step

## Q9 — MCQ

The congestion window is 9,000 bytes and the advertised window is 2,000 bytes. The sender may have at most

A. 2,000 bytes in flight
B. 9,000 bytes in flight
C. 11,000 bytes in flight
D. 7,000 bytes in flight

---

## Q10 — NAT

The congestion window is 8,000 bytes and the advertised window is 3,000 bytes. Enter the usable send window in bytes.

---

## Q11 — MSQ

Select all that apply. A sliding window on a TCP byte stream means

A. bytes below the acknowledgement number are done and need not be kept for retransmission
B. bytes from the acknowledgement number onward, up to the usable window, may be sent or are already in flight
C. the window is counted in segments, and a 1,000-byte segment always consumes one sequence number
D. an acknowledgement of a prefix lets the window slide forward by the number of bytes acknowledged

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

The last acknowledgement number received is 5000. The highest sequence number sent is 6499. The number of unacknowledged bytes is

A. 1499
B. 1500
C. 1501
D. 6499

---

## Q13 — MCQ

The receive buffer has only 1 byte free, and the maximum segment size is 1000 bytes. A sensible receiver-side defence against the silly-window problem is to

A. advertise a window of 1 immediately
B. withhold a window update until the free space is at least the minimum of one MSS and half the buffer
C. set the advertised window equal to the congestion window
D. advertise a window of 0 for the rest of the connection, with no probes

---

## Q14 — MSQ

Select all that apply. Which statements are true?

A. Nagle’s rule concerns the sender coalescing small writes while an acknowledgement is outstanding.
B. A tiny advertised window is a receiver-side cause of tiny segments.
C. Nagle’s rule sets the slow-start threshold to half the congestion window.
D. If the sender honours an advertisement of 1 byte, it can emit a 1-byte segment.

---

## Level 5 — Challenge

## Q15 — NAT

The maximum segment size is 1,000 bytes. The advertised window is 4,500 bytes and the congestion window is 8,000 bytes. Enter the maximum number of full-sized segments the sender may have in flight. A leftover partial segment does not count.

---

## Q16 — MCQ

The receive buffer is 10,000 bytes and starts empty. A burst of 4,000 bytes arrives and is not yet read, so the advertised window becomes 6,000 bytes. The application then reads 1,500 bytes and nothing else arrives. The new advertised window is

A. 7,500 bytes
B. 6,000 bytes
C. 8,500 bytes
D. 10,000 bytes

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | NAT | 19500 |
| 5 | MCQ | A |
| 6 | MCQ | A |
| 7 | MSQ | A, B, C |
| 8 | NAT | 2000 |
| 9 | MCQ | A |
| 10 | NAT | 3000 |
| 11 | MSQ | A, B, D |
| 12 | MCQ | B |
| 13 | MCQ | B |
| 14 | MSQ | A, B, D |
| 15 | NAT | 4 |
| 16 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

Flow control is the receiver protecting its buffer. Doubling every round trip is slow start, a congestion-control rule. Timeouts detect loss; they are not what the window is for. The handshake is independent of the advertised window.

### Q2

Answer: A, B, D

Both windows apply, and the sender is bound by the smaller one. Sequence numbers move by the byte count in the segment. The acknowledgement number is the next byte expected in order, not a description of what the application has printed, so C is false. Data can be acknowledged and still be sitting in the receive buffer.

### Q3

Answer: B

Bytes through 4999 are in order, so the next expected byte is 5000. Acknowledging 4999 would name the last received byte and would be an off-by-one. 4998 drops an extra byte. 1 would restart the stream.

### Q4

Answer: 19500

\[
32000 - 12500 = 19500
\]

The advertisement is free space, not the occupied space and not the whole buffer. Advertising 32000 would invite the sender to overwrite data the application has not consumed.

### Q5

Answer: A

The segment occupies sequence numbers 4001 through \(4001 + 1460 - 1 = 5460\). The next byte is

\[
4001 + 1460 = 5461
\]

B is the last byte inside the segment. C is the first byte. D is the length, not a sequence number.

### Q6

Answer: A

A zero window is legal and temporary. The persist timer sends probes so a lost window-update cannot leave the sender silent forever. The connection is not aborted, the sequence space stays in bytes, and a new handshake is not required for each later segment.

### Q7

Answer: A, B, C

Tiny advertisements produce tiny segments. Clark’s rule is the receiver waiting until it can advertise a useful window, typically at least one MSS or half the buffer. Nagle’s rule is the sender holding a small new segment while older data is unacknowledged. The congestion window is not frozen at 1 MSS, so D is false.

### Q8

Answer: 2000

Unacknowledged sequence numbers run from 7000 through 8999 inclusive.

\[
8999 - 7000 + 1 = 2000
\]

Subtracting without the +1 gives 1999. Treating 7000 as the last acknowledged byte, and then computing \(8999 - 7000\), also drops a byte. The acknowledgement number itself is not a count of bytes already received unless the stream started at 0 and nothing about the start was stated; the safe count is the inclusive range.

### Q9

Answer: A

\[
\min(9000, 2000) = 2000
\]

The receiver cannot buffer the extra 7,000 bytes, so the congestion window does not raise the usable window. Adding the two windows, or subtracting them, does not match the rule.

### Q10

Answer: 3000

\[
\min(8000, 3000) = 3000
\]

The congestion window would have allowed 8,000 bytes. Flow control cuts that to the advertised 3,000.

### Q11

Answer: A, B, D

The acknowledgement moves the left edge. Bytes inside the usable window are the ones in flight or still allowed. When those bytes are acknowledged, the right edge moves with the left edge according to the current window. A segment of 1,000 bytes consumes 1,000 sequence numbers, not one, so C is false.

### Q12

Answer: B

Acknowledgement 5000 means bytes before 5000 are done. Bytes 5000 through 6499 are not.

\[
6499 - 5000 + 1 = 1500
\]

A is \(6499 - 5000\), the off-by-one that treats the range as half-open at the wrong end. C counts one byte past 6499. D is the highest sequence number, not the number of unacknowledged bytes.

### Q13

Answer: B

Advertising the single free byte is the silly window this defence avoids. Clark’s rule waits until free space is at least \(\min(\text{MSS}, \text{buffer}/2)\). With an MSS of 1,000 bytes, one free byte is not advertised. The advertised window is not taken from the congestion window, and a permanent zero window with no probes would stall the connection after the application later reads data.

### Q14

Answer: A, B, D

Nagle coalesces small sender writes; it is not the rule that halves the congestion window on loss. A 1-byte advertisement is a receiver-side silly window, and a sender that follows it can send a 1-byte segment. The two mechanisms sit on opposite ends of the connection and are easy to swap.

### Q15

Answer: 4

\[
\min(4500, 8000) = 4500, \quad \lfloor 4500 / 1000 \rfloor = 4
\]

Four full segments use 4,000 bytes. The remaining 500 bytes are not a fifth full segment. Using the congestion window instead of the minimum would allow 8 full segments and would overflow the receiver.

### Q16

Answer: A

After the burst, occupied space is 4,000 and the window is \(10{,}000 - 4{,}000 = 6{,}000\). Reading 1,500 leaves

\[
4000 - 1500 = 2500
\]

bytes occupied.

\[
10000 - 2500 = 7500
\]

B leaves the advertisement at 6,000 and ignores the read. C, 8,500, equals \(10{,}000 - 1{,}500\), which treats the buffer as if the only data that ever arrived were the bytes just read. D treats the buffer as empty. The occupancy is 2,500 bytes, so the window is 7,500.

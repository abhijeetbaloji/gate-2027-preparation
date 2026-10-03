# IPv4 Fragmentation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question says otherwise, the IPv4 header is 20 bytes and has no options. A fragment’s offset field is stored in 8-byte units. Every fragment carries its own 20-byte header. Reassembly is done only at the destination.

## Level 1 — Conceptual

## Q1 — MCQ

The fragment offset field in the IPv4 header counts

A. 8-byte blocks of original payload
B. single bytes of original payload
C. whole fragments, starting at 1
D. the MTU of the next link, in bytes

---

## Q2 — MSQ

Select all that apply. Which statements about IPv4 fragmentation are correct?

A. Every fragment of one datagram carries the same identification value.
B. The more-fragments flag is 0 only on the last fragment.
C. A router that must fragment a datagram with the do-not-fragment bit set forwards it in pieces anyway.
D. Each fragment has its own IPv4 header.

---

## Q3 — MCQ

An IPv4 datagram is fragmented by a router. The pieces are reassembled

A. by the next router, before it forwards anything
B. only at the destination host
C. by every router, which then may fragment them again from the rebuilt datagram
D. by the data-link layer of the source

---

## Q4 — NAT

A datagram is 2020 bytes, including the 20-byte header. It must cross a link whose MTU is 620 bytes, including the header. Enter the number of fragments.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

A 4000-byte datagram, including a 20-byte header, is fragmented to fit an MTU of 1500 bytes. How much header is on the wire for the fragments, taken together?

A. 60 bytes, because each of the three fragments has a 20-byte header
B. 20 bytes, because only the first fragment carries a header
C. 40 bytes, because the last fragment reuses the first header
D. 1500 bytes, because the header is padded to the MTU

---

## Q6 — MCQ

A datagram is 2020 bytes including a 20-byte header, and the MTU is 620 bytes including the header. The offset field of the second fragment is

A. 75
B. 600
C. 620
D. 1

---

## Q7 — MSQ

Select all that apply. For a datagram of 5000 bytes including a 20-byte header, fragmented for an MTU of 1500 bytes, which statements are true?

A. The largest payload that can be put in a non-final fragment is 1480 bytes.
B. There are 4 fragments.
C. The offset fields are 0, 185, 370, and 555.
D. The last fragment’s total length is 1500 bytes.

---

## Q8 — NAT

A datagram is 2020 bytes including a 20-byte header. The MTU is 620 bytes including the header. Enter the total length, in bytes, of the last fragment, header included.

---

## Level 3 — Multi-Step

## Q9 — MCQ

A router must forward a datagram larger than the next-hop MTU, and the do-not-fragment bit is set. The router

A. fragments the datagram and clears the flag
B. drops the datagram and does not send the oversized packet on that link
C. forwards the datagram unchanged, because the flag is only a hint
D. strips the IPv4 header and sends the payload as one fragment with offset 0

---

## Q10 — NAT

A datagram is 3000 bytes including a 20-byte header. The MTU is 1000 bytes including the header. Enter the offset field of the second fragment.

---

## Q11 — MSQ

Select all that apply. A datagram of 3000 bytes including a 20-byte header is fragmented for MTU 1000. Which statements are true?

A. A non-final fragment can carry 980 bytes of payload, since \(1000 - 20 = 980\).
B. A non-final fragment carries 976 bytes of payload.
C. The third fragment has offset field 244.
D. The last fragment has total length 72 bytes.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

For the 3000-byte datagram and MTU 1000 from the previous question, the offset field of the last fragment is

A. 366
B. 375
C. 976
D. 2980

---

## Q13 — MCQ

Which statement about fragment headers is correct?

A. Only the first fragment includes an IPv4 header. Later fragments are bare payload.
B. Every fragment includes an IPv4 header, so header bytes are repeated once per fragment.
C. The header is split: the first 10 bytes go in the first fragment and the rest go in the last.
D. Intermediate fragments use a 8-byte header because the offset unit is 8.

---

## Q14 — MSQ

Select all that apply. Which statements are true of IPv4?

A. An intermediate router reassembles fragments before forwarding them.
B. An intermediate router may fragment a fragment again if the next MTU is smaller.
C. The offset of a piece cut from an already fragmented datagram is measured from the start of the original payload, not from the start of the parent fragment.
D. The more-fragments bit on the last piece of a parent fragment is 0 even when the parent fragment itself had more fragments coming after it.

---

## Level 5 — Challenge

## Q15 — NAT

A datagram of 4000 bytes, including a 20-byte header, is fragmented for an MTU of 1500 bytes. Those fragments later cross a link with MTU 820 bytes, and fragments are not reassembled at the router. Enter the number of fragments that arrive at the destination.

---

## Q16 — MCQ

In that two-MTU trip (first 1500, then 820), the fragments that reach the destination have total lengths

A. 820, 700, 820, 700, 820, and 240 bytes, and only the last has MF = 0
B. 1500, 1500, and 1040 bytes, because the second router reassembles and does not fragment further
C. 820, 680, 820, 680, 820, and 220 bytes, with headers omitted from the lengths
D. six fragments, and every fragment that finishes one of the MTU-1500 pieces has MF = 0

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | NAT | 4 |
| 5 | MCQ | A |
| 6 | MCQ | A |
| 7 | MSQ | A, B, C |
| 8 | NAT | 220 |
| 9 | MCQ | B |
| 10 | NAT | 122 |
| 11 | MSQ | B, C, D |
| 12 | MCQ | A |
| 13 | MCQ | B |
| 14 | MSQ | B, C |
| 15 | NAT | 6 |
| 16 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

The offset is in units of 8 bytes so that a 13-bit field can name a position inside a long datagram. It does not count bytes, fragments, or the MTU. Forgetting the unit of 8 is the error that later questions are built to catch.

### Q2

Answer: A, B, D

The identification ties the pieces together. MF is 1 on every fragment except the last. Each piece is a datagram and needs a header. If DF is set, the router must not fragment; it drops the datagram. C says the opposite.

### Q3

Answer: B

IPv4 reassembly is an end-host job. The next router does not rebuild the datagram, which is why a later, smaller MTU fragments the pieces again. C describes a design IPv4 does not use. The source data-link layer is not the reassembly point.

### Q4

Answer: 4

Payload is \(2020 - 20 = 2000\) bytes. The MTU leaves \(620 - 20 = 600\) bytes, and 600 is divisible by 8, so the maximum non-final payload is 600.

\[
\lceil 2000 / 600 \rceil = 4
\]

The payloads are 600, 600, 600, and 200.

### Q5

Answer: A

Payload \(4000 - 20 = 3980\). Maximum piece \(1500 - 20 = 1480\), which is divisible by 8.

\[
\lceil 3980 / 1480 \rceil = 3
\]

Three headers are \(3 \times 20 = 60\) bytes. B is the trap that the header appears once. The payloads are 1480, 1480, and 1020, so the fragment lengths are 1500, 1500, and 1040.

### Q6

Answer: A

The first fragment carries 600 bytes of payload, so the second starts at byte 600 of the original payload.

\[
600 / 8 = 75
\]

B writes the byte offset into the field. C writes the MTU. D counts fragments instead of 8-byte blocks.

### Q7

Answer: A, B, C

Payload is \(5000 - 20 = 4980\). Maximum non-final payload is 1480.

\[
1480 \times 3 = 4440, \quad 4980 - 4440 = 540
\]

So there are 4 fragments, with payloads 1480, 1480, 1480, and 540. Offsets:

\[
0,\ 1480/8 = 185,\ 2960/8 = 370,\ 4440/8 = 555
\]

The last fragment’s total length is \(540 + 20 = 560\), not 1500. D is false.

### Q8

Answer: 220

Three fragments take \(600 \times 3 = 1800\) bytes of the 2000-byte payload. The last payload is 200 bytes, plus a 20-byte header:

\[
200 + 20 = 220
\]

Answering 200 drops the header that every fragment carries.

### Q9

Answer: B

DF means the router is not allowed to fragment. The datagram is dropped rather than sent oversized. A ignores the flag. C treats the flag as advice. D is not a fragmentation format.

### Q10

Answer: 122

The MTU allows \(1000 - 20 = 980\) bytes, but 980 is not a multiple of 8.

\[
\lfloor 980 / 8 \rfloor \times 8 = 976
\]

The second fragment starts after 976 bytes:

\[
976 / 8 = 122
\]

Using 980 produces \(980/8 = 122.5\), which cannot be stored in the offset field. Using 1000 produces 125. The legal offset is 122.

### Q11

Answer: B, C, D

Non-final payload is 976, not 980, so A is the alignment trap and B is the correction. Payload is \(3000 - 20 = 2980\).

\[
976 \times 3 = 2928, \quad 2980 - 2928 = 52
\]

Offsets are 0, 122, 244, and 366. The third fragment’s offset is 244. The last total length is \(52 + 20 = 72\).

### Q12

Answer: A

The last fragment starts after three 976-byte pieces:

\[
2928 / 8 = 366
\]

B comes from stepping by 1000 bytes: \(3000/8 = 375\). C is the payload of an earlier fragment, in bytes, written into the offset field. D is the original payload length, also in bytes.

### Q13

Answer: B

Fragmentation copies a header onto every piece and adjusts length, offset, MF, and the header checksum. A is a common shortcut that undercounts bytes on the wire. The header is not split across fragments, and it is not shortened to 8 bytes. The 8-byte unit is only the unit of the offset field.

### Q14

Answer: B, C

IPv4 routers do not reassemble before forwarding, so A is false. A router can cut a fragment into smaller fragments. Offsets stay relative to the original datagram, otherwise the destination could not place the bytes. D is the MF trap: if the parent still had MF = 1, the last child of that parent must also have MF = 1. Only a child that ends the original datagram gets MF = 0.

### Q15

Answer: 6

First MTU 1500: payload \(3980\), pieces 1480, 1480, and 1020. That is 3 fragments, of total lengths 1500, 1500, and 1040.

Second MTU 820: maximum payload \(\lfloor 800/8 \rfloor \times 8 = 800\).

- 1480 becomes 800 + 680
- 1480 becomes 800 + 680
- 1020 becomes 800 + 220

Each parent splits into 2, so the destination sees 6 fragments. Reassembling at the second router would have left 3, which IPv4 does not do.

### Q16

Answer: A

The six total lengths, each including a 20-byte header, are

\[
820,\ 700,\ 820,\ 700,\ 820,\ 240
\]

because the payloads are 800, 680, 800, 680, 800, and 220. Offsets from the original payload are 0, 100, 185, 285, 370, and 470. The first five fragments all have MF = 1. The fragment of 240 bytes ends the original datagram and is the only one with MF = 0.

B stops after the first router and assumes reassembly. C reports payloads without headers (680 and 220 instead of 700 and 240). D clears MF at the end of each MTU-1500 parent. Those parents were not the end of the datagram, so their second children keep MF = 1.

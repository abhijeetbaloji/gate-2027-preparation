# Packet Switching — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In datagram packet switching, packets of one flow

A. must all follow the path chosen for the first packet
B. are forwarded independently, so later packets may take a different path
C. cannot leave the source until a circuit-setup message returns
D. are stored and reassembled at every router before any packet continues

---

## Q2 — MSQ

Select all that apply. Which statements describe datagram packet switching?

A. Each packet carries a header used to choose the next hop.
B. Bandwidth is reserved at the peak rate for the whole session before the first data packet.
C. Delay can vary from packet to packet because packets share queues.
D. Capacity unused by one flow can be used by another flow.

---

## Q3 — NAT

Each packet has a 40-byte header and a 960-byte payload. Enter the header overhead as a percentage of the full packet length.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Store-and-forward packet switching at a router means the router

A. starts sending the packet on the next link only after the whole packet has arrived
B. forwards each bit as soon as that bit arrives
C. never queues more than one packet
D. reserves the outgoing link for the flow before the packet arrives

---

## Q5 — MCQ

On a path of \(h\) equal links, \(k\) equal packets are sent with store-and-forward. Propagation is zero and there is no other traffic. Why is the total time \((h + k - 1)\) packet transmission times, rather than \(h \times k\)?

A. Only the first packet crosses every link; the others are delivered locally.
B. Packets pipeline: after the first packet, each new packet adds one transmission time, not a full trip.
C. Routers cut through and never wait for a whole packet.
D. The formula counts headers only and ignores payloads.

---

## Q6 — MSQ

Select all that apply. Why does packet switching suit bursty sources better than a peak-rate circuit reservation?

A. An idle source does not hold a reserved slice it is not using.
B. Many bursty sources can share a link if their bursts do not always overlap.
C. A packet source must still reserve its peak rate before it may send.
D. No per-flow setup is required before the first datagram.

---

## Level 3 — Multi-Step

## Q7 — MCQ

A message is split into 4 packets. There are 4 links. Every packet takes 2 seconds to transmit on a link. Propagation, processing, and queueing from other traffic are zero. Store-and-forward is used. The time until the last packet arrives is

A. 14 seconds
B. 16 seconds
C. 32 seconds
D. 8 seconds

---

## Q8 — NAT

Five packets cross three links. Each packet takes 2 ms to transmit on a link, and each link has a 3 ms propagation delay. Processing delay is zero and there is no competing traffic. Store-and-forward is used. Enter the time, in milliseconds, until the last packet arrives.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

All links are identical. There are \(h\) hops (links), \(k\) packets, packet transmission time \(T\), and propagation time \(P\) on each link. Processing delay is zero, there is no competing traffic, and forwarding is store-and-forward. The time until the last packet arrives is

A. \((h + k - 1)T + hP\)
B. \(hkT + hkP\)
C. \(kT + P\)
D. \((h + k)T + (h + k)P\)

---

## Q10 — MSQ

Select all that apply. Which statements are true?

A. Datagrams of one flow can arrive out of order if they follow different paths.
B. Basic datagram switching reserves the peak bandwidth of a flow before the first packet.
C. Each packet needs a header so the next hop can be chosen.
D. Pure store-and-forward sends the first bit of a packet onward before the last bit of that packet has arrived.

---

## Level 5 — Challenge

## Q11 — NAT

15,000 bits of data are sent. Each packet carries 1,000 bits of data and a 200-bit header. There are 3 links, each of rate 1,200 bits/s. Propagation and processing are zero, and there is no other traffic. Store-and-forward is used. Enter the time in seconds until the last bit arrives.

---

## Q12 — MCQ

Using the packet size from the previous situation (1,200 bits, of which 200 are header, and 15 such packets), the packets cross a single link of 12,000 bits/s. The time to send all 15 packets on that one link is

A. 1.5 seconds
B. 1.25 seconds
C. 15 seconds
D. 18 seconds

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C, D |
| 3 | NAT | 4 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 23 |
| 9 | MCQ | A |
| 10 | MSQ | A, C |
| 11 | NAT | 17 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

A datagram carries its own destination and is routed when it arrives, so two packets of one flow need not share a path. A and C describe a virtual circuit or a reserved circuit. D is stronger than store-and-forward: a router stores one packet, not the whole message, and it does not reassemble the transport stream.

### Q2

Answer: A, C, D

Headers make independent forwarding possible. Queues are shared, so delay varies, and an idle flow does not own the link. B is circuit switching, not the datagram model.

### Q3

Answer: 4

The packet is \(40 + 960 = 1000\) bytes.

\[
\frac{40}{1000} \times 100 = 4
\]

The percentage of the payload would be \(40/960\), which is not what the question asks. The percentage of the packet is 4.

### Q4

Answer: A

Store-and-forward waits for the last bit of the packet, checks it, and then transmits it on the next link. B is cut-through. C is not required by store-and-forward. D is a reservation, which datagram forwarding does not make.

### Q5

Answer: B

The first packet takes \(h\) transmission times to reach the destination. Each following packet is one transmission time behind the previous one on the pipeline, so the extra \(k - 1\) packets add \(k - 1\) transmission times. The product \(h \times k\) would restart the whole path for every packet with no overlap. C denies the store-and-forward assumption. D is unrelated to the hop count.

### Q6

Answer: A, B, D

Bursty users leave gaps. Packet switching can fill those gaps with other users’ packets, and a datagram can leave without a setup handshake. C is what a peak-rate circuit would demand, so it is not a reason packet switching fits bursts.

### Q7

Answer: A

\[
(h + k - 1)T = (4 + 4 - 1) \times 2 = 14 \text{ s}
\]

B uses \((h + k)T = 16\). C uses \(h \times k \times T = 32\), which refuses the pipeline. D uses only \(kT = 8\), which ignores the extra hops after the first link.

### Q8

Answer: 23

\[
(h + k - 1)T + hP = (3 + 5 - 1) \times 2 + 3 \times 3 = 14 + 9 = 23 \text{ ms}
\]

Propagation is paid once per hop along the path, not once per packet per hop. Multiplying \(P\) by \(k\) as well produces \(14 + 45 = 59\), which is too large.

### Q9

Answer: A

The pipelined store-and-forward time is \((h + k - 1)T\), and the \(h\) propagation delays sit on the path of the packets. B multiplies both terms by \(hk\) and erases the pipeline. C keeps a single propagation and pretends later hops add no transmission. D adds one extra \(T\) and one extra \(P\).

### Q10

Answer: A, C

Independent routes can reorder a flow. Every datagram needs a forwarding header. B describes reservation, which this service does not require. D describes cut-through; pure store-and-forward waits for the whole packet.

### Q11

Answer: 17

The number of packets is \(15{,}000 / 1{,}000 = 15\). Each packet is \(1{,}200\) bits, and the link rate is \(1{,}200\) bits/s, so \(T = 1\) second. With \(h = 3\) and zero propagation,

\[
(3 + 15 - 1) \times 1 = 17 \text{ s}
\]

Forgetting the header and treating \(T\) as \(1{,}000/1{,}200\) seconds changes the problem. Using \(3 \times 15 = 45\) ignores pipelining.

### Q12

Answer: A

Fifteen packets are \(15 \times 1{,}200 = 18{,}000\) bits.

\[
\frac{18{,}000}{12{,}000} = 1.5 \text{ s}
\]

On one link the same result is \((1 + 15 - 1) \times (1{,}200/12{,}000) = 1.5\). B sends only the 15,000 data bits and drops the headers: \(15{,}000/12{,}000 = 1.25\). C and D treat the packet count or the bit count as if it were already in seconds.

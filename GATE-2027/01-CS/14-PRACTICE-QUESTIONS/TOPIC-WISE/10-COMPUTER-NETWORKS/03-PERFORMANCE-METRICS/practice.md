# Performance Metrics — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

The four usual pieces of nodal delay for a packet are processing delay, queueing delay, transmission delay, and

A. propagation delay
B. congestion-window delay
C. checksum delay only
D. setup delay of a virtual circuit

---

## Q2 — MSQ

Select all that apply. Which statements about delay are correct?

A. Transmission delay grows when the packet gets longer, for a fixed link rate.
B. Propagation delay grows when the link gets longer, for a fixed propagation speed.
C. Queueing delay grows when other packets are already waiting on that output link.
D. Propagation delay is computed as packet length divided by bandwidth.

---

## Q3 — MCQ

A link’s bandwidth is 10 Mbps. During one measurement the useful bits delivered to the application are 4 Mbps. In this measurement, 10 Mbps is the bandwidth and 4 Mbps is the

A. propagation speed
B. throughput
C. round-trip time
D. bandwidth-delay product

---

## Q4 — NAT

A packet is 4,000 bits long and the link bandwidth is 2 Mbps. Enter the transmission delay in milliseconds.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

A link is 500 km long and the propagation speed is \(2 \times 10^8\) m/s. The propagation delay is

A. 2.5 ms
B. 25 ms
C. 0.25 ms
D. 250 ms

---

## Q6 — MCQ

For a path with one-way propagation delay \(T_p\) and negligible transmission and processing delays, the round-trip time is

A. \(T_p\)
B. \(2T_p\)
C. \(T_p / 2\)
D. \(T_p^2\)

---

## Q7 — MSQ

Select all that apply. The bandwidth-delay product \(R \times \text{RTT}\) is

A. a count of how many bits can be in flight on the path during one round trip, if the sender fills the pipe
B. the packet length divided by the bandwidth
C. the window, in bits, that a stop-and-wait sender must reach before the link can stay busy for the whole RTT
D. measured in bits when \(R\) is in bits per second and RTT is in seconds

---

## Q8 — NAT

A path has bandwidth 20 Mbps and RTT 50 ms. Define the bandwidth-delay product as bandwidth times RTT. Enter that product in bits.

---

## Level 3 — Multi-Step

## Q9 — MCQ

At one router the delays for a packet are processing 2 ms, queueing 5 ms, transmission 3 ms, and propagation 10 ms. The total nodal delay is

A. 20 ms
B. 15 ms
C. 18 ms
D. 10 ms

---

## Q10 — NAT

Stop-and-wait is used. The frame is 2,500 bytes, the bandwidth is 2 Mbps, and the RTT is 40 ms. Acknowledgement transmission time is negligible, and no frame is lost. Enter the throughput in kbps.

---

## Q11 — MSQ

Select all that apply. A sender uses a sliding window on a path whose bandwidth-delay product is \(B\) bits. Which statements are correct?

A. If the window is smaller than \(B\), the sender must go idle waiting for acknowledgements and the path is not kept full.
B. If the window is at least \(B\), the window is large enough to keep the pipe full, ignoring protocol overhead.
C. Increasing the window without bound always increases throughput, even after the window already exceeds \(B\) and the link is the bottleneck.
D. Throughput cannot exceed the bottleneck bandwidth.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

Stop-and-wait sends a 1,000-bit frame on a 1 Mbps link. One-way propagation is 4 ms, and the acknowledgement transmission time is negligible. A student uses utilisation \(T_{tx}/(T_{tx}+T_p)\) with \(T_p = 4\) ms. What is wrong, and what is the utilisation?

A. Nothing is wrong; utilisation is \(1/5\).
B. The wait is one RTT, not one one-way delay. Transmission is 1 ms and RTT is 8 ms, so utilisation is \(1/9\).
C. Propagation should be ignored, so utilisation is 1.
D. Transmission delay is 4 ms, so utilisation is \(1/2\).

---

## Q13 — MCQ

Bandwidth is 10 Mbps and one-way propagation is 20 ms, so the RTT is 40 ms. Using the definition bandwidth \(\times\) RTT, the bandwidth-delay product is

A. 400,000 bits
B. 200,000 bits
C. 400,000 bytes
D. 50,000 bits

---

## Q14 — MSQ

Select all that apply. A student computes nodal delay. Which corrections are valid?

A. Transmission delay is packet length divided by link bandwidth, not divided by propagation speed.
B. Propagation delay is distance divided by propagation speed, not divided by bandwidth.
C. Queueing delay can be larger than transmission delay when the output queue holds several earlier packets.
D. Processing delay must equal propagation delay on every link.

---

## Level 5 — Challenge

## Q15 — NAT

The bandwidth is 10 Mbps, the RTT is 100 ms, and each packet is 1,000 bytes. Define the bandwidth-delay product as bandwidth times RTT. Enter the minimum window, in packets, that covers this product. Assume the window is an integer number of these packets.

---

## Q16 — MCQ

A 4,000,000-byte file crosses a path of three links with bandwidths 8 Mbps, 2 Mbps, and 4 Mbps. There is no other traffic. Propagation, processing, and packetisation effects are ignored, and the throughput is limited by the bottleneck bandwidth. The transfer time is

A. 4 seconds
B. 8 seconds
C. 16 seconds
D. 32 seconds

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | MCQ | B |
| 4 | NAT | 2 |
| 5 | MCQ | A |
| 6 | MCQ | B |
| 7 | MSQ | A, D |
| 8 | NAT | 1000000 |
| 9 | MCQ | A |
| 10 | NAT | 400 |
| 11 | MSQ | A, B, D |
| 12 | MCQ | B |
| 13 | MCQ | A |
| 14 | MSQ | A, B, C |
| 15 | NAT | 125 |
| 16 | MCQ | C |

## Detailed Solutions

### Q1

Answer: A

The standard sum is processing, queueing, transmission, and propagation. Congestion window, checksum work, and circuit setup are not the fourth term of nodal delay.

### Q2

Answer: A, B, C

Transmission delay is \(L/R\). Propagation delay is distance over speed. Queueing delay depends on the packets already waiting. D swaps the formulas: packet length over bandwidth is transmission delay, not propagation delay.

### Q3

Answer: B

Bandwidth is the rate the link can carry. Throughput is the rate actually achieved by the transfer being measured. Propagation speed is in distance per time, RTT is a time, and the bandwidth-delay product is a volume of bits, so none of those is the 4 Mbps figure.

### Q4

Answer: 2

\[
\frac{4{,}000}{2 \times 10^6} = 0.002 \text{ s} = 2 \text{ ms}
\]

Using 4,000 bytes instead of 4,000 bits would inflate the delay by 8. The question states bits.

### Q5

Answer: A

\[
\frac{500 \times 10^3}{2 \times 10^8} = 0.0025 \text{ s} = 2.5 \text{ ms}
\]

B uses a speed of \(2 \times 10^7\) m/s. C drops a factor of 10 in the distance conversion. D treats the speed as \(2 \times 10^6\) m/s.

### Q6

Answer: B

A bit goes to the far end and the response comes back, so the round trip is twice the one-way propagation when the other delays are negligible. A is one way. C and D are not RTT definitions.

### Q7

Answer: A, D

\(R \times \text{RTT}\) is a volume of bits: the amount that leaves the sender during one round trip if it sends continuously. Units multiply to bits. B is a time, the transmission delay, not the product. C overstates the claim: a stop-and-wait window is one packet, and that product is the volume a large window would need in order to fill the RTT. Stop-and-wait fills the pipe only when one packet is already at least that large. So C is not a correct reading of the product.

### Q8

Answer: 1000000

\[
20 \times 10^6 \times 0.050 = 1{,}000{,}000 \text{ bits}
\]

Half of this, 500,000, is the product with the one-way delay of 25 ms. The question defines the product with the RTT.

### Q9

Answer: A

\[
2 + 5 + 3 + 10 = 20 \text{ ms}
\]

B drops processing. C drops processing or swaps a term and lands short. D keeps only propagation.

### Q10

Answer: 400

The frame is \(2{,}500 \times 8 = 20{,}000\) bits.

\[
T_{tx} = \frac{20{,}000}{2 \times 10^6} = 0.010 \text{ s} = 10 \text{ ms}
\]

The cycle is transmission plus RTT:

\[
10 + 40 = 50 \text{ ms}
\]

\[
\text{throughput} = \frac{20{,}000}{0.050} = 400{,}000 \text{ bps} = 400 \text{ kbps}
\]

Dividing by the 10 ms transmission alone just returns the link rate, 2 Mbps, and ignores the idle wait. Using 2,500 bits instead of 2,500 bytes produces a transmission time that is eight times too small.

### Q11

Answer: A, B, D

A window below the bandwidth-delay product leaves the sender idle for part of the RTT. A window of at least that product can keep sending until the first acknowledgement returns. Once the bottleneck is already full, a still larger window adds queueing rather than throughput, so C is false. D is the bottleneck cap.

### Q12

Answer: B

\[
T_{tx} = \frac{1{,}000}{10^6} = 1 \text{ ms}, \quad \text{RTT} = 2 \times 4 = 8 \text{ ms}
\]

\[
U = \frac{1}{1 + 8} = \frac{1}{9}
\]

The student put the one-way delay in the denominator and got \(1/(1+4) = 1/5\). Stop-and-wait cannot reuse the link until the acknowledgement returns. C ignores the wait. D assigns the propagation time to transmission.

### Q13

Answer: A

\[
10 \times 10^6 \times 0.040 = 400{,}000 \text{ bits}
\]

B uses the 20 ms one-way delay and gets 200,000 bits. C reports bits as if they were bytes. D uses 5 ms or divides by 8 and then slips a factor: \(400{,}000/8 = 50{,}000\) bytes, not bits. The product asked for is in bits and uses the RTT.

### Q14

Answer: A, B, C

A and B are the two formulas students swap. Queueing is the wait behind earlier packets and can dominate transmission, so C is true. Nothing forces processing delay to equal propagation delay, so D is false.

### Q15

Answer: 125

\[
10 \times 10^6 \times 0.100 = 1{,}000{,}000 \text{ bits}
\]

\[
\frac{1{,}000{,}000}{1{,}000 \times 8} = 125 \text{ packets}
\]

Using the one-way delay of 50 ms would give 62.5 packets and, after an integer step, the wrong window. Dividing by 1,000 without the factor of 8 counts bytes as bits and gives 1,000 packets.

### Q16

Answer: C

The bottleneck is 2 Mbps. The file is \(4{,}000{,}000 \times 8 = 32{,}000{,}000\) bits.

\[
\frac{32{,}000{,}000}{2 \times 10^6} = 16 \text{ s}
\]

A uses the fastest link, 8 Mbps, and gets 4 s. B uses 4 Mbps and gets 8 s. D uses 1 Mbps, which is not a link on the path. The question says to ignore store-and-forward packetisation, so the three transmission times are not added.

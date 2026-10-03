# Circuit Switching — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

During the data-transfer phase of circuit switching, the reserved path

A. stays allocated to the call even while the sender is idle
B. is chosen independently for every packet of the call
C. stores the entire message at each switch before any bit is forwarded
D. shares every link with all other users and keeps no reservation

---

## Q2 — MSQ

Select all that apply. Which are properties of circuit switching?

A. A setup phase runs before data transfer.
B. Once a circuit is reserved, any number of extra calls may use that same reserved bandwidth.
C. The message transmission delay is not multiplied by the hop count the way a store-and-forward packet pipeline is.
D. Time when the call is silent is time when the reserved capacity carries no data for that call.

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

After a circuit has been set up, how does its data-transfer delay compare with datagram packet switching?

A. Every packet still waits in an unpredictable queue because nothing was reserved.
B. The call has a dedicated path and a stable data rate, and a call can be blocked at setup if that rate is unavailable.
C. Propagation delay disappears because the path was reserved.
D. Every bit must carry a full destination-address header so each switch can route it.

---

## Q4 — NAT

Setup takes 80 ms. The message is 2,000,000 bits. The reserved rate is 4 Mbps. The propagation delays on the path sum to 20 ms. Processing and queueing delays are zero. Enter the total time, in milliseconds, from the start of setup until the last bit of the message arrives.

---

## Q5 — MCQ

A circuit reserves an entire 2 Mbps link, and the application generates 500 kbps on average. While the reservation is held, the unused part of that 2 Mbps is

A. automatically given to other calls, because a circuit always sublets idle capacity
B. unused by this call
C. turned into packet buffers for datagrams
D. added to the propagation delay of the path

---

## Level 3 — Multi-Step

## Q6 — MSQ

Select all that apply. In which situations does a reserved circuit waste capacity?

A. The source sends continuously at the reserved rate.
B. The source stays idle for long intervals while the reservation is held.
C. The source’s average rate is far below the peak rate it reserved.
D. The path propagation delay is zero.

---

## Q7 — NAT

A circuit crosses three links of 6 Mbps, 3 Mbps, and 12 Mbps. The reserved rate equals the bottleneck rate. A 750,000-byte file is sent. Ignore setup and propagation. Enter the transmission time in seconds.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

Setup takes 2 seconds. The message is 8,000 bits. There are four links, each of rate 1,000 bits/s. Propagation and processing delays are zero. Switches do not store the whole message before forwarding. The total time from the start of setup until the last bit arrives is

A. 10 seconds
B. 34 seconds
C. 8 seconds
D. 32 seconds

---

## Q9 — MSQ

Select all that apply. Which statements are true for circuit switching?

A. The correct delay formula multiplies the message transmission delay by the number of hops, as in store-and-forward of a packet.
B. The message transmission delay is incurred once, at the reserved rate, as the bits enter the pipe.
C. Each hop still contributes its propagation delay.
D. After setup, successive pieces of the call are routed independently and may follow different paths.

---

## Level 5 — Challenge

## Q10 — MCQ

A circuit crosses links of 8 Mbps, 2 Mbps, and 4 Mbps. Setup takes 100 ms. The three propagation delays are 10 ms, 15 ms, and 25 ms. The message is 500,000 bytes. Processing and queueing delays are zero. The total time until the last bit arrives is

A. 2150 ms
B. 2000 ms
C. 650 ms
D. 3650 ms

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, C, D |
| 3 | MCQ | B |
| 4 | NAT | 600 |
| 5 | MCQ | B |
| 6 | MSQ | B, C |
| 7 | NAT | 2 |
| 8 | MCQ | A |
| 9 | MSQ | B, C |
| 10 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

A circuit keeps the reserved resources for the life of the call, including silent periods. B describes datagram routing. C describes store-and-forward of a whole message. D describes statistical multiplexing without a reservation.

### Q2

Answer: A, C, D

Setup comes first. Once bandwidth is reserved, that slice is not an open pool for extra calls, so B is false. Bits flow through the pipe, so the source transmission delay is not repeated as a full store-and-forward delay at every hop. Idle time on a held circuit is wasted from that call’s point of view.

### Q3

Answer: B

Reservation removes the per-packet fight for bandwidth, so the data delay is predictable, but setup can fail if the rate cannot be reserved. A describes an unreserved packet network. Propagation does not vanish, so C is false. A circuit does not put a full destination address on every bit; the path was chosen at setup, so D is false.

### Q4

Answer: 600

Transmission time at 4 Mbps:

\[
\frac{2{,}000{,}000}{4 \times 10^6} = 0.5 \text{ s} = 500 \text{ ms}
\]

\[
80 + 500 + 20 = 600 \text{ ms}
\]

Do not multiply 500 ms by the number of hops. Propagation is already given as a path total of 20 ms.

### Q5

Answer: B

The call reserved 2 Mbps and uses 500 kbps on average, so 1.5 Mbps of the reservation sits idle. Circuit switching does not automatically donate that idle slice to other calls. It is not converted into datagram buffers or into propagation delay.

### Q6

Answer: B, C

Waste appears when reserved capacity is not filled: long silences, or an average rate well below the reserved peak. Continuous sending at the reserved rate fills the circuit, so A is not waste. A zero propagation delay says nothing about whether the reserved bandwidth is occupied, so D is not a waste case.

### Q7

Answer: 2

The reserved rate is \(\min(6, 3, 12) = 3\) Mbps. The file is \(750{,}000 \times 8 = 6{,}000{,}000\) bits.

\[
\frac{6{,}000{,}000}{3 \times 10^6} = 2 \text{ s}
\]

Using 6 Mbps or 12 Mbps as the sending rate ignores the bottleneck. Adding the three link times would be a store-and-forward calculation, which this circuit question excludes.

### Q8

Answer: A

Transmission time is \(8{,}000 / 1{,}000 = 8\) seconds at the reserved rate. With a 2-second setup and no propagation,

\[
2 + 8 = 10 \text{ s}
\]

B is the trap \(2 + 4 \times 8 = 34\), which multiplies transmission by the hop count. C forgets setup. D is \(4 \times 8\), the same hop multiplication with setup omitted.

### Q9

Answer: B, C

On a circuit the bits stream through, so the large transmission delay is paid once at the reserved rate, while every hop still adds propagation. A copies the packet store-and-forward formula into the wrong network. D describes datagrams: a plain circuit does not reroute each piece independently after setup.

### Q10

Answer: A

The bottleneck is 2 Mbps. Transmission time:

\[
\frac{500{,}000 \times 8}{2 \times 10^6} = 2 \text{ s} = 2000 \text{ ms}
\]

Propagation is \(10 + 15 + 25 = 50\) ms. Setup is 100 ms.

\[
2000 + 50 + 100 = 2150 \text{ ms}
\]

B drops setup and propagation. C treats 8 Mbps as the bottleneck: transmission would be 500 ms, and \(500 + 100 + 50 = 650\). D adds a separate full transmission delay on every link (\(0.5 + 2 + 1 = 3.5\) s) and then adds setup and propagation: \(3500 + 150 = 3650\). That sum is the store-and-forward mistake.

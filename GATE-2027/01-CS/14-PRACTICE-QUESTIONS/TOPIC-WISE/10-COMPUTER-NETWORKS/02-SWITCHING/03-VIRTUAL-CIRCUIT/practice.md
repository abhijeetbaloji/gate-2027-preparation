# Virtual Circuit Switching — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In virtual-circuit packet switching, after setup,

A. every data packet of the flow is forwarded independently and may use a new path
B. data packets of the flow follow the path chosen at setup
C. no packet is stored at any switch, because the circuit is physical
D. the source must put the full list of routers in every data packet

---

## Q2 — MSQ

Select all that apply. Which statements describe a virtual circuit?

A. A setup step creates forwarding state before data packets flow.
B. Each switch keeps a table that maps an incoming virtual-circuit identifier to an outgoing link and identifier.
C. Switches of a pure virtual circuit keep no per-flow state.
D. The virtual-circuit identifier on an incoming link can be rewritten on the outgoing link.

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

A virtual-circuit data packet is forwarded through the network. In the basic model, the packet

A. carries a circuit identifier that indexes the switch table, rather than being routed from scratch by a full destination lookup at every switch
B. carries no identifier of any kind
C. may leave on a different path from the previous packet of the same circuit whenever a link is busy
D. is delivered without any store-and-forward, because “circuit” means the bits are never queued

---

## Q4 — NAT

A flow’s path contains exactly three virtual-circuit switches between the source and the destination. Each of those switches rewrites the virtual-circuit identifier. The source’s choice of the first identifier is not counted as a rewrite. Enter the number of rewrites.

---

## Q5 — MCQ

A virtual circuit uses one path, and every link on that path forwards packets of the circuit in FIFO order. Packets of this circuit

A. can still be reordered by taking different paths
B. stay in order at the destination
C. must be reassembled into one message at every switch
D. do not need a circuit identifier because the path is FIFO

---

## Level 3 — Multi-Step

## Q6 — MSQ

Select all that apply. Which statements are true of virtual circuits as used in packet networks?

A. Setup can fail if the network will not accept another circuit.
B. All data packets of one circuit share the forwarding path installed at setup.
C. A virtual circuit is always a dedicated wire with no packet headers.
D. Teardown is how the switches drop the per-circuit table rows when the call ends.

---

## Q7 — NAT

A switch table says: a packet that arrives on port 1 with virtual-circuit identifier 17 leaves on port 3 with virtual-circuit identifier 44. A packet arrives on port 1 with identifier 17. Enter the identifier placed on the outgoing packet.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

Which statement about the virtual-circuit identifier (VCI) is correct?

A. The source picks one VCI and every link keeps that same number until the destination.
B. The VCI is meaningful on a particular link. The next switch can replace it with a different VCI on the next link.
C. The VCI is the destination IP address written in decimal.
D. Routers ignore the VCI and forward each packet by flooding.

---

## Q9 — MSQ

Select all that apply. Which statements are true when virtual circuits are compared with datagrams?

A. A datagram network can send the first data packet without a per-flow setup.
B. A virtual-circuit switch keeps no per-circuit state.
C. In the basic virtual-circuit model, data packets of one circuit are free to take different paths for load balancing.
D. Teardown releases the virtual-circuit table entries for that flow.

---

## Level 5 — Challenge

## Q10 — MCQ

Virtual-circuit setup takes 50 ms. Then 4 data packets cross 3 links. Each packet takes 10 ms to transmit on a link. Propagation and processing are zero, there is no competing traffic, and forwarding is store-and-forward. The time from the start of setup until the last data bit arrives is

A. 110 ms
B. 60 ms
C. 120 ms
D. 170 ms

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | NAT | 3 |
| 5 | MCQ | B |
| 6 | MSQ | A, B, D |
| 7 | NAT | 44 |
| 8 | MCQ | B |
| 9 | MSQ | A, D |
| 10 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

Setup installs one path, and the data packets follow it. A is datagram behaviour. C confuses a virtual circuit with a physical wire: the packets are still packets. D describes source routing, not a VCI lookup.

### Q2

Answer: A, B, D

Setup builds state, each switch stores a row, and the outgoing identifier can differ from the incoming one. C is the opposite of B and is false for a virtual circuit. Datagram switches do not keep per-flow rows; virtual-circuit switches do.

### Q3

Answer: A

The established circuit is a table lookup on the identifier, not a fresh global route computation for every packet. B would make the lookup impossible. C breaks the single-path rule of the basic model. D is wrong because a virtual circuit still moves packets, and those packets can be stored and forwarded.

### Q4

Answer: 3

Each of the three switches replaces the identifier as the packet leaves toward the next hop. The source’s initial choice is the value on the first link; it is not a rewrite by a switch. Counting the destination as a fourth rewrite, or counting only the source, both miss the statement of the question.

### Q5

Answer: B

One path plus FIFO links preserves order. A would require the multipath behaviour that this circuit does not have. Reassembly of the whole message at every switch is not part of virtual-circuit forwarding, so C is false. FIFO does not remove the need for an identifier: the switch still has to know which circuit a packet belongs to, so D is false.

### Q6

Answer: A, B, D

The network can refuse the circuit at setup. Accepted packets share the installed path. When the call ends, teardown deletes the rows. C is false: the circuit is virtual, packets still exist, and they carry a circuit identifier.

### Q7

Answer: 44

The row is a rewrite rule. Identifier 17 on port 1 is consumed locally and identifier 44 is written on port 3. Leaving 17 unchanged is the usual slip, and it would collide with whatever 17 means on the outgoing link.

### Q8

Answer: B

A VCI is a link-local label. The next switch is free to choose a different label on the next hop, which is why the table stores both values. A is the trap of treating the VCI like a global address. C confuses it with an IP address. D is flooding, not virtual-circuit forwarding.

### Q9

Answer: A, D

Datagrams need no per-flow setup. Virtual-circuit teardown exists to free the rows that setup created. B denies that state. C gives datagram freedom to a virtual circuit; the basic model keeps one path for the life of the circuit.

### Q10

Answer: A

The data phase has \(h = 3\), \(k = 4\), and \(T = 10\) ms:

\[
(3 + 4 - 1) \times 10 = 60 \text{ ms}
\]

Add setup:

\[
50 + 60 = 110 \text{ ms}
\]

B forgets setup. C uses \((h + k)T + 50 = 120\). D uses \(h \times k \times T + 50 = 170\), which drops the pipeline and then adds setup.

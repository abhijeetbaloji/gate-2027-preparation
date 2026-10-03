# Principles of Layering — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the TCP/IP stack, which layer provides process-to-process delivery by demultiplexing flows with port numbers?

A. Network layer
B. Transport layer
C. Data-link layer
D. Physical layer

---

## Q2 — MSQ

Select all that apply. Which functions belong to the data-link layer on a single hop?

A. Framing a packet between a header and a trailer
B. Choosing an end-to-end path across several interconnected networks
C. Detecting bit errors on the link it serves
D. Assigning a globally routable 32-bit logical address to a host

---

## Q3 — NAT

A packet travels from a source host through exactly four routers and then reaches the destination host. The network-layer header is inspected once at the source, once at each router, and once at the destination. Enter the number of inspections.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

An application message moves down the stack at the sending host. Ignoring the physical layer, the first header wrapped around the message, the second header, and the third header are respectively

A. transport, network, data-link
B. network, transport, data-link
C. data-link, network, transport
D. session, network, transport

---

## Q5 — MCQ

Which statement correctly distinguishes a service from a protocol?

A. A service is the set of rules two peer entities use to talk; a protocol is the interface a layer offers upward.
B. A service is the interface a layer offers to the layer above it; a protocol is the set of rules between peer entities of that layer.
C. A service exists only at the physical layer, and a protocol exists only at the application layer.
D. A service and a protocol are two names for the same header format.

---

## Q6 — MSQ

Select all that apply. Which statements about the TCP/IP model are correct?

A. Its application layer covers the roles that OSI splits among application, presentation, and session.
B. It defines a separate session layer between transport and application.
C. Its internet layer is responsible for host-to-host forwarding across interconnected networks.
D. Its link layer is concerned with moving a frame across one hop.

---

## Level 3 — Multi-Step

## Q7 — MCQ

A router forwards an IPv4 datagram and does not terminate the transport connection. Which information does it use to choose the next hop?

A. The transport port number, which names the next router
B. The destination address in the network-layer header
C. The application URL, which names the next hop
D. The data-link trailer, which stores the remaining route

---

## Q8 — NAT

An application sends 1000 bytes. The transport header is 20 bytes, the network header is 20 bytes, and the data-link layer adds a 14-byte header and a 4-byte trailer. Enter the number of bytes in the frame placed on one link.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

A path contains five links. A student says five transport headers are stacked on the segment because each router adds one. Which statement is correct?

A. The student is right: every router pushes a new transport header and the destination pops all five.
B. Exactly one transport header is added, at the source host. Routers forward the datagram and do not add transport headers.
C. A transport header is added only at the destination host.
D. A transport header is added only on links faster than 10 Mbps.

---

## Q10 — MSQ

Select all that apply. A datagram crosses three successive links. Which statements are true?

A. While the datagram is on one link, it carries one data-link header for that link, not a stack of the headers of later links.
B. The three data-link headers stay stacked together until the destination removes all of them.
C. Each router removes the incoming frame header and trailer and builds a new frame for the outgoing link.
D. The router deletes the network-layer header, so the next link carries only the transport segment.

---

## Level 5 — Challenge

## Q11 — NAT

Application data is 1000 bytes. The transport header is 20 bytes, the network header is 20 bytes, and every link uses a 14-byte data-link header plus a 4-byte trailer. The path has five links, and each link transmits a freshly built frame of this same size. Enter the total number of bytes transmitted, summed over all five links.

---

## Q12 — MCQ

Hop-by-hop retransmission is used on every link, and the transport layer also retransmits lost data end to end. Which reasoning matches the end-to-end argument?

A. Hop-by-hop retransmission makes an end-to-end loss check unnecessary.
B. An end-to-end check is still required, because loss or corruption can occur off the wire, including inside the end hosts.
C. Reliability belongs only in the physical coding of each wire and never in a higher layer.
D. The network layer must reserve a circuit before any reliability check is meaningful.

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, C |
| 3 | NAT | 6 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | MSQ | A, C, D |
| 7 | MCQ | B |
| 8 | NAT | 1058 |
| 9 | MCQ | B |
| 10 | MSQ | A, C |
| 11 | NAT | 5290 |
| 12 | MCQ | B |

## Detailed Solutions

### Q1

Answer: B

Port numbers let the transport layer deliver a segment to the correct process on a host. The network layer delivers a datagram to a host, the data-link layer delivers a frame across one hop, and the physical layer moves bits. A common slip is to assign ports to the network layer because IP addresses and ports appear together in a socket; the address selects the host and the port selects the process.

### Q2

Answer: A, C

Framing and hop error detection are data-link jobs. End-to-end path selection is a network-layer job, so B is out. A globally routable 32-bit address is an IP address, also a network-layer concern, so D is out. The data-link layer uses a local hardware address on the hop, which is not the same object as D.

### Q3

Answer: 6

The inspectors are the source host, four routers, and the destination host: \(1 + 4 + 1 = 6\). The trap is to count only the routers, or to count the five links instead of the six devices that look at the header.

### Q4

Answer: A

Encapsulation wraps from the inside out as the message moves down: the transport header is added first, then the network header, then the data-link header. Option B swaps the first two layers. Option C is the order in which the receiver peels headers. Option D inserts a session header that TCP/IP does not add as its own layer on this path.

### Q5

Answer: B

The service is the vertical contract (what the layer above may ask for). The protocol is the horizontal contract (how the two peers cooperate). Option A reverses the two words. Option C invents a layer restriction. Option D collapses the interface and the peer rules into a header format; the header is only one part of a protocol.

### Q6

Answer: A, C, D

TCP/IP has four familiar layers: application, transport, internet, and link. The application layer absorbs OSI session and presentation functions, so A is true and B is false. The internet layer routes between networks, and the link layer handles one hop.

### Q7

Answer: B

A router selects the next hop from the destination network address. It does not use the port number as a next-hop name, so A is wrong. It does not parse the application message to forward, so C is wrong. The frame trailer is removed and checked on input; it does not store the route, so D is wrong.

### Q8

Answer: 1058

\[
1000 + 20 + 20 + 14 + 4 = 1058
\]

Each of those five pieces is on the wire exactly once for this single link. Leaving out the 4-byte trailer produces 1054; leaving out both data-link fields produces 1040.

### Q9

Answer: B

The transport header is an end-to-end object. It is created by the source and read by the destination. Routers forward the network datagram and do not push another transport header, so five links do not mean five transport headers. Option C puts the header at the wrong host. Option D has no basis in the layering rule.

### Q10

Answer: A, C

Frame headers are hop-scoped. A router strips the incoming frame and emits a new frame on the outgoing link, so only one data-link header is attached at a time. B is the stacking trap. D is wrong because the network header continues on the next hop; the router may update fields such as the hop count, but it does not discard the network header as part of normal forwarding.

### Q11

Answer: 5290

One frame is \(1000 + 20 + 20 + 14 + 4 = 1058\) bytes, the same size computed in the single-link case. Five links each transmit that frame:

\[
5 \times 1058 = 5290
\]

The network and transport headers travel on every link, and a new data-link header and trailer of the same size are built on every link. Counting the data-link overhead once and the other headers five times is the usual miss, and it does not match this size model.

### Q12

Answer: B

The end-to-end argument says a function that must be correct for the application has to be checked where the application’s data finally lands. Hop checks do not see corruption or loss inside a host, a middlebox that the hop protocol does not cover, or a failure after the last hop check. So hop retransmission can be a useful optimisation and still leave the transport check in place. A overclaims what hop checks can see. C and D move reliability to the wrong place.

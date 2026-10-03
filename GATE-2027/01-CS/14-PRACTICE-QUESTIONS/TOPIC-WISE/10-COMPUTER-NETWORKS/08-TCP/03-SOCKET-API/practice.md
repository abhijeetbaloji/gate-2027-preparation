# Socket API — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A TCP server prepares to receive connections. The usual order of the calls that arm it is

A. `socket`, `bind`, `listen`, `accept`
B. `socket`, `connect`, `listen`, `bind`
C. `listen`, `accept`, `socket`, `bind`
D. `accept`, `bind`, `socket`, `listen`

---

## Q2 — MSQ

Select all that apply. Which calls belong on which side of a TCP connection?

A. The client calls `connect` to start the handshake.
B. The server calls `listen` to mark the socket as willing to accept connections.
C. The client must call `listen` before it can call `connect`.
D. The server calls `accept` to take one established connection out of the queue.

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

On a TCP server, a successful `accept`

A. returns a new connected socket for one client, and the listening socket stays open for further clients
B. destroys the listening socket, so no later client can connect
C. sends the client’s first application byte
D. chooses the client’s port number

---

## Q4 — NAT

A TCP server takes a connection by calling `socket`, then `bind`, then `listen`, then `accept`. Counting `socket` as call number 1, enter the position of `accept` in that sequence.

---

## Q5 — MCQ

`bind` on a server socket

A. assigns the local address and port that clients will connect to
B. performs the three-way handshake
C. blocks until a client sends data
D. chooses the congestion window

---

## Level 3 — Multi-Step

## Q6 — MSQ

Select all that apply. Which statements about TCP and UDP sockets are correct?

A. A TCP server uses `listen` and `accept`.
B. A UDP socket can send with `sendto` without a prior `connect`.
C. `listen` is required before every UDP datagram.
D. `connect` on a TCP socket starts the handshake.

---

## Q7 — NAT

A TCP connection is identified by the client’s IP address, the client’s port, the server’s IP address, and the server’s port. Enter the number of items in that tuple.

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

The server has already called `socket`, `bind`, and `listen`. The client calls `connect`. When does `connect` return successfully?

A. When the handshake completes, which can happen before the server application reaches `accept`, because the kernel queues the new connection
B. Only after the server application has called `accept` and has also read the first byte
C. As soon as the client calls `socket`, before any packet is sent
D. Only after the server calls `connect` as well

---

## Q9 — MSQ

Select all that apply. Which statements are true?

A. A TCP client may omit `bind` and let the kernel pick an ephemeral local port.
B. The backlog argument of `listen` limits the queue of pending connections; it is not the number of bytes in a segment.
C. `accept` on a blocking socket waits if the queue of established connections is empty.
D. A client must call `accept` to finish its own `connect`.

---

## Level 5 — Challenge

## Q10 — MCQ

A process calls `socket` and then `connect` toward a TCP server that is not running, and nothing is listening on the target port. The call that fails is

A. `connect`, because the handshake is refused or times out
B. `socket`, because a socket cannot be created unless the server is up
C. `bind` on the client, even though the client never called `bind`
D. `listen` on the client, even though the client never called `listen`

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | NAT | 4 |
| 5 | MCQ | A |
| 6 | MSQ | A, B, D |
| 7 | NAT | 4 |
| 8 | MCQ | A |
| 9 | MSQ | A, B, C |
| 10 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

The server creates a socket, binds it to a local address, marks it listening, and then accepts connections. `connect` is the client’s call and does not belong between `socket` and `listen`. The other orders use calls before the socket exists or accept before there is a listening socket.

### Q2

Answer: A, B, D

The client starts the handshake with `connect`. The server must `listen` and then `accept`. The client does not listen; C puts a server call on the client.

### Q3

Answer: A

`accept` allocates a separate connected socket for the client it dequeues. The original socket remains the listening socket. It does not carry application data by itself, and it does not choose the client’s port. The client chose that port, often as an ephemeral port.

### Q4

Answer: 4

The server sequence is `socket` (1), `bind` (2), `listen` (3), `accept` (4). The client’s `connect` is not one of these calls, and skipping `listen` would leave `accept` without a listening socket.

### Q5

Answer: A

`bind` attaches the local IP address and port. The handshake is `connect` on the client and the kernel’s response to a listening server. `bind` does not block for payload bytes, and it does not set the congestion window.

### Q6

Answer: A, B, D

TCP’s connection queue is why a TCP server listens and accepts. UDP is connectionless, so `sendto` can name the peer on each datagram without `connect`. `listen` is not part of ordinary UDP sending. TCP `connect` is what starts the three-way handshake.

### Q7

Answer: 4

The identity is the 4-tuple: source IP, source port, destination IP, destination port. Two connections from the same client host to the same server port are still distinct when the client ports differ. Counting only the two IP addresses, or only the two ports, undercounts the tuple.

### Q8

Answer: A

Once `listen` has been called, the kernel completes the handshake and places the connection on the accept queue. `connect` returns at the end of that handshake. The application might call `accept` a moment later and still find the connection waiting. B adds an application read that the handshake does not need. C returns before any packet. D makes the server call `connect`, which is not how a listening server picks up a client.

### Q9

Answer: A, B, C

The client can skip `bind`; the kernel selects the local port. The backlog is a queue length for connections, not a segment size. A blocking `accept` sleeps when that queue is empty. The client does not call `accept` to finish `connect`, so D is the call-side trap.

### Q10

Answer: A

`socket` only allocates a local endpoint and succeeds with no server present. The failure appears at `connect`, when the handshake cannot be completed. The client in this question never called `bind` or `listen`, so those calls cannot be the ones that fail.

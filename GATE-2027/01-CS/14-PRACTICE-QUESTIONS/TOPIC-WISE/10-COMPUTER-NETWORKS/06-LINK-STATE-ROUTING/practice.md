# Link State Routing — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Link-state routing gives every router a map of the topology and then runs

A. Dijkstra’s algorithm locally
B. a distance-vector exchange with neighbours only, and no map
C. flooding of user data packets to discover the path at send time
D. a circuit-setup handshake for every data packet

---

## Q2 — MSQ

Select all that apply. Which are parts of link-state routing?

A. Each router learns the full set of links and their costs.
B. Link-state packets are flooded so that every router can collect the same topology.
C. A sequence number helps a router tell a fresh link-state packet from an old one.
D. A router forwards using only a neighbour’s distance to the destination and never builds a topology map.

---

## Q3 — NAT

Router R floods a link-state packet with sequence number 8. A delayed copy of an older packet from R, with sequence number 5, arrives afterward. The router keeps the packet whose sequence number is the one you enter.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

On the network S—A 7, S—B 2, A—B 3, A—C 4, B—C 1, B—D 8, C—D 5, Dijkstra from S settles nodes in the order of increasing distance. After S, the next node settled is

A. B
B. A
C. C
D. D

---

## Q5 — MCQ

On the same network, the shortest-path cost from S to C is

A. 3
B. 2
C. 7
D. 8

---

## Q6 — MSQ

Select all that apply. Compared with distance-vector routing, link-state routing

A. computes routes from a topology map rather than from a neighbour’s vector alone
B. reacts to a changed link once the new link-state flood has been received, without a count-to-infinity loop of the distance-vector kind
C. sends each router’s entire distance vector only to neighbours and hides the topology
D. uses Dijkstra’s algorithm on the collected map

---

## Level 3 — Multi-Step

## Q7 — MCQ

On S—A 7, S—B 2, A—B 3, A—C 4, B—C 1, B—D 8, C—D 5, a shortest path from S to D is

A. S—B—C—D
B. S—B—D
C. S—A—C—D
D. S—A—B—D

---

## Q8 — NAT

On that same network, enter the shortest-path cost from S to D.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

On S—A 7, S—B 2, A—B 3, the shortest-path cost from S to A is

A. 5
B. 7
C. 2
D. 10

---

## Q10 — MSQ

Select all that apply. Which statements about Dijkstra on this network are true? All link costs are positive.

A. Once a node is settled with the current minimum distance, a later relaxation does not find a cheaper path to it.
B. The direct edge S—A of cost 7 is present and is still not the shortest path to A.
C. A correct run can settle D before B, because D’s tentative distance 8 looks final while B is still at 2.
D. The algorithm’s next settled node is always one with the smallest tentative distance among unsettled nodes.

---

## Level 5 — Challenge

## Q11 — NAT

On S—A 7, S—B 2, A—B 3, A—C 4, B—C 1, B—D 8, C—D 5, enter the shortest-path cost from S to A.

---

## Q12 — MCQ

After S is settled, the first relaxation sets A to 7 and B to 2. B is settled next. Which triple of tentative distances (A, C, D) is correct immediately after relaxing B’s edges, before any later node is settled?

A. (5, 3, 10)
B. (7, 3, 8)
C. (5, 1, 8)
D. (7, 1, 10)

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 8 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 8 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | NAT | 5 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

Link state collects the map and runs Dijkstra locally. B is distance vector. C floods data rather than routing information. D confuses routing with per-packet circuit setup.

### Q2

Answer: A, B, C

The flood of link-state packets, helped by sequence numbers, is how every router builds the same map. D is the distance-vector rule and is the method link state is designed not to rely on.

### Q3

Answer: 8

A larger sequence number marks the newer link-state information. The packet numbered 5 is older, even though it arrives later, so it is discarded. Keeping 5 would reinstall stale link costs. The sequence number is not a hop count and it is not added to 8.

### Q4

Answer: A

Dijkstra starts with S at distance 0. The first relaxation offers A at 7 and B at 2. The smallest unsettled distance is B. A, C, and D are still more expensive or still unknown at that moment, so none of them is second.

### Q5

Answer: A

S—B—C costs \(2+1 = 3\). There is no direct S—C edge. S—A—C costs \(7+4 = 11\). The shortest cost is 3. The values 2, 7, and 8 are real distances in this graph, but they are S to B, the direct S to A, and S to D, not S to C.

### Q6

Answer: A, B, D

Link state uses the map and Dijkstra. It does not form the two-neighbour count-to-infinity loop, because a router is not adopting a neighbour’s vague distance; it recomputes from the links it has heard. C describes distance-vector advertisements, not link state.

### Q7

Answer: A

S—B—C—D costs \(2+1+5 = 8\). S—B—D costs \(2+8 = 10\). S—A—C—D costs \(7+4+5 = 16\). S—A—B—D costs \(7+3+8 = 18\). The unique cheapest of these is S—B—C—D. The direct-looking path S—B—D is the trap.

### Q8

Answer: 8

\[
2 + 1 + 5 = 8
\]

The path is S—B—C—D. The next best simple candidate, S—B—D, costs 10.

### Q9

Answer: A

S—B—A costs \(2+3 = 5\), which beats the direct edge S—A of cost 7. Answering 7 is the direct-edge trap. Answering 2 stops at B. Answering 10 adds an unused edge.

### Q10

Answer: A, B, D

With positive costs, the first time a node is chosen as the minimum unsettled distance, that distance is final. The direct edge to A costs 7 and loses to the path of cost 5, so the edge can exist without being the shortest path. C is false: B’s distance 2 is smaller than D’s tentative 8, so B is settled first. D is the selection rule of Dijkstra.

### Q11

Answer: 5

The path S—B—A has cost \(2+3 = 5\). The direct edge costs 7. No other simple path is cheaper: S—B—C—A costs \(2+1+4 = 7\). The shortest-path cost is 5.

### Q12

Answer: A

Settling B at distance 2 relaxes three edges:

- A: \(\min(7, 2+3) = 5\)
- C: \(2+1 = 3\)
- D: \(2+8 = 10\)

So the tentative triple is (5, 3, 10). B leaves A at the old direct cost 7. C uses the edge B—C as if its cost were the whole distance from S, forgetting the 2 already spent to reach B. D mixes the improved A, the raw edge B—C, and the raw edge B—D.

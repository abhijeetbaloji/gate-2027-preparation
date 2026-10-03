# Distance Vector Routing — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In distance-vector routing, a router sends its distance estimates

A. only to its neighbours
B. by flooding them to every router in the network
C. only to the destination named in the vector
D. only when a link-state Dijkstra computation asks for them

---

## Q2 — MSQ

Select all that apply. Which statements describe distance-vector routing?

A. A router’s new distance to a destination can be computed as the minimum, over neighbours, of (link cost to the neighbour + that neighbour’s advertised distance).
B. Every router must already know the full map of every link before it can compute anything.
C. A router learns remote destinations from what its neighbours advertise.
D. The algorithm is a distributed form of the Bellman-Ford update.

---

## Q3 — NAT

Router A is directly connected to neighbour N by a link of cost 2. N advertises distance 4 to destination E. No other neighbour offers A a route to E. Enter A’s distance to E from this advertisement.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

The undirected link costs are A—B 2, A—C 5, B—C 1, B—D 4, C—D 1, C—E 6, D—E 2. After distance-vector routing has converged, A’s next hop toward E is

A. B
B. C
C. D
D. E

---

## Q5 — MCQ

Count-to-infinity is a distance-vector problem in which

A. a failed link makes two neighbours keep advertising a route to each other, and the distance climbs on each exchange
B. Dijkstra’s algorithm loops because a link cost is positive
C. a router floods a link-state packet forever
D. the hop count is reset to 0 after every successful delivery

---

## Q6 — MSQ

Select all that apply. Which statements about this behaviour are correct?

A. Good news, such as a new shorter link, tends to settle in a small number of exchanges.
B. Bad news, such as a link failure that leaves routers pointing at each other, can cause the count-to-infinity climb.
C. Split horizon means a router does not advertise a route back out the neighbour from which it learned that route.
D. Split horizon requires every router to flood the full topology.

---

## Level 3 — Multi-Step

## Q7 — MCQ

Use the link costs A—B 2, A—C 5, B—C 1, B—D 4, C—D 1, C—E 6, D—E 2. After convergence, A’s distance to D is

A. 4
B. 5
C. 6
D. 7

---

## Q8 — NAT

Use the same link costs: A—B 2, A—C 5, B—C 1, B—D 4, C—D 1, C—E 6, D—E 2. After convergence, enter A’s distance to E.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Use A—B 2, A—C 5, B—C 1. After convergence, A’s distance to C is

A. 3, via B
B. 5, because a direct link is always preferred to an indirect path
C. 2, the cost of A—B alone
D. 1, the cost of B—C alone

---

## Q10 — MSQ

Select all that apply. After the only path to a destination has failed, which claims are true of basic distance-vector updates with no poison reverse and no hop-count cap?

A. A router may accept a neighbour’s route even though that neighbour’s route still points back at it.
B. The reported distance can increase by the link cost on every exchange for a long time.
C. The failure is installed everywhere in a single exchange, with no further growth in the metric.
D. The slow growth is the count-to-infinity behaviour.

---

## Level 5 — Challenge

## Q11 — NAT

A and B are joined by a link of cost 1. Before a failure, B—C also has cost 1, A reaches C only through B, and B reaches C on the direct link. So A’s distance to C is 2 and B’s distance to C is 1. Then B—C fails. Neither node has any other neighbour. In each synchronous round, both recompute using only the distance the other advertised in the previous round. A down link is not used. Enter B’s distance to C after exactly 3 rounds.

---

## Q12 — MCQ

Start from the converged network A—B 2, A—C 5, B—C 1, B—D 4, C—D 1, C—E 6, D—E 2, and then change only C—E from 6 to 1. After the distance vectors converge again, A’s distance to E is

A. 4
B. 6
C. 8
D. 3

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, C, D |
| 3 | NAT | 6 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B, C |
| 7 | MCQ | A |
| 8 | NAT | 6 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | NAT | 5 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

A distance vector is an advertisement to neighbours. Flooding the full topology is link-state behaviour. The vector is not sent only to the destination, and Dijkstra is not the distance-vector update.

### Q2

Answer: A, C, D

The Bellman-Ford step is exactly that minimum over neighbours. Routers do not start with a global map; they learn remote distances from advertisements. B describes link state, not distance vector.

### Q3

Answer: 6

\[
2 + 4 = 6
\]

The link cost and the neighbour’s advertised distance are added. Using only 4 ignores the cost to reach N. Using only 2 ignores how far E is beyond N.

### Q4

Answer: A

Converged distances from B include E at cost 4, by B—C—D—E (\(1+1+2\)). A’s candidate through B is \(2+4 = 6\). Through C it is \(5+3 = 8\), because C’s best distance to E is C—D—E \(= 3\), which beats the direct C—E cost 6. The better next hop is B. D and E are not neighbours of A, so they cannot be next hops.

### Q5

Answer: A

Count-to-infinity is the mutual advertisement of a stale route after a failure: each neighbour treats the other as the way to the destination, and the metric grows. B and C belong to other algorithms. D is not the failure mode.

### Q6

Answer: A, B, C

A shorter path is adopted as soon as the advertisement arrives, so good news moves quickly. A loop of advertisements makes bad news move as a slow climb. Split horizon stops a router from telling a neighbour a route that it learned from that neighbour. It does not turn distance vector into flooding, so D is false.

### Q7

Answer: A

B’s distance to D is \(\min(4, 1+1) = 2\), using B—C—D rather than the direct B—D edge. A through B costs \(2+2 = 4\). A through C costs \(5+1 = 6\). The minimum is 4. The direct-looking sums 5, 6, and 7 are the worse candidates.

### Q8

Answer: 6

B’s distance to E is 4, as in the path B—C—D—E. A through B costs \(2+4 = 6\). A—C—D—E costs \(5+1+2 = 8\). A—B—D—E costs \(2+4+2 = 8\). The converged distance is 6.

### Q9

Answer: A

A—B—C costs \(2+1 = 3\), which beats the direct edge of cost 5. Distance vector keeps the minimum, so a direct link is not automatically the chosen route. C forgets B—C. D forgets A—B. B is the trap this question is built around.

### Q10

Answer: A, B, D

Without split horizon or poisoned reverse, a neighbour’s stale finite distance is a legal Bellman-Ford input, even when that route came from this router. Each exchange then adds another link cost, which is the count-to-infinity climb. C claims the opposite, a one-round global correction, which basic distance vector does not provide.

### Q11

Answer: 5

Both nodes use link cost 1 and the other node’s previous distance.

- Start: A \(= 2\), B \(= 1\).
- Round 1: A \(= 1+1 = 2\), B \(= 1+2 = 3\).
- Round 2: A \(= 1+3 = 4\), B \(= 1+2 = 3\).
- Round 3: A \(= 1+3 = 4\), B \(= 1+4 = 5\).

B’s distance after three rounds is 5. Stopping after round 1 gives the trap value 3. A’s distance after round 3 is 4, which is the other easy number to report by mistake.

### Q12

Answer: A

With C—E equal to 1, C’s distance to E is 1. B’s distance to E becomes \(\min(1+1, 4, 1+1+2) = 2\) through C. A through B costs \(2+2 = 4\). A through C costs \(5+1 = 6\). The old distance 6 is no longer best, and 8 was a worse path even before the change. 3 would be A—B—C without the last hop. The new distance is 4.

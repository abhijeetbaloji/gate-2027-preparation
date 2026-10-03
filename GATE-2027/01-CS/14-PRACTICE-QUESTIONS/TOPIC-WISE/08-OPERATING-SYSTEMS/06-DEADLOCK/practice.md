# Deadlock — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MSQ

**Select all that apply.**

Deadlock among processes that use serially reusable resources requires which conditions together?

A. Mutual exclusion
B. Hold and wait
C. No preemption
D. Circular wait

---

## Q2 — MCQ

A deadlock is

A. a set of processes each waiting for an event that only another process in the set can cause
B. the same event as starvation of a single runnable process
C. a cycle of length zero in an empty graph
D. a situation that occurs only when a process waits for itself and for nobody else

---

## Q3 — MCQ

Circular wait can be prevented by

A. imposing a total order on resource types and requiring every process to request types in increasing order
B. letting every process request resource types in any order it chooses
C. adding an edge from every process to every other process in the resource-allocation graph
D. refusing to grant a resource unless the grant closes a cycle

---

## Q4 — MCQ

A state is safe when

A. there is an order of the processes in which each can obtain its declared maximum and release its resources, even in the worst case of those claims
B. the system is already deadlocked
C. every possible continuation deadlocks
D. the available vector is the zero vector and every claim is positive

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Each of R1, R2, and R3 has one instance. P1 holds R1 and requests R2. P2 holds R2 and requests R3. P3 holds R3 and requests R1. Which statement is correct?

A. The system is deadlocked; with one instance per type, a cycle is decisive
B. The system is safe because three processes can always share three resources
C. A cycle matters only when some type has two or more instances
D. P1 can still obtain R2 without waiting

---

## Q6 — NAT

Three processes and three resource types:

|  | Allocation (A B C) | Max (A B C) |
|---|---|---|
| P0 | 1 0 2 | 3 2 2 |
| P1 | 0 1 0 | 1 3 1 |
| P2 | 2 1 1 | 2 2 3 |

Available = (1, 2, 2). Need = Max − Allocation. How many processes can be first in some safe sequence?

---

## Q7 — MCQ

One practical way to recover from a deadlock is to

A. abort one process in the deadlocked set and reclaim the resources it holds
B. add another request edge so the cycle becomes a clique
C. raise every process's Max claim
D. mark the state safe without releasing resources

---

## Q8 — MCQ

Five processes each have a maximum claim of 3 instances of one resource type. The smallest number of instances that guarantees deadlock is impossible is

A. 5
B. 10
C. 11
D. 15

---

## Q9 — MSQ

**Select all that apply.**

A. In a wait-for graph, an edge \(P_i \rightarrow P_j\) means \(P_i\) is waiting for a resource that \(P_j\) holds
B. The wait-for graph is the usual deadlock-detection tool when every resource type has a single instance
C. In that single-instance setting, a cycle is necessary and sufficient for deadlock
D. The same graph, unchanged, is the banker's algorithm for multi-instance claims

---

## Level 3 — Multi-Step

## Q10 — NAT

Use the Allocation, Max, and Available data of Q6. Need = Max − Allocation. How many distinct safe sequences are there?

---

## Q11 — MCQ

Start again from Q6, with Available = (1, 2, 2). P0 requests (1, 0, 0). The request is within P0's Need and within Available. If it is granted tentatively, the resulting state is safe. The system should

A. grant the request now
B. refuse it, because a safe state must be left unchanged
C. grant it only after P0's Need has been increased
D. refuse it, because P0 cannot be first before the request

---

## Q12 — MSQ

**Select all that apply.**

Resource type R has 3 instances. Process P holds 1 and requests 1 more. Process Q holds 1 and requests 1 more. One instance is free. No other processes use R.

A. The free instance can be given to either waiting process
B. The system is deadlocked
C. After the process that receives the free instance finishes and releases what it holds, the other process can obtain an instance
D. A drawing that puts request and assignment edges around R is enough, by itself, to declare deadlock when R has several instances

---

## Q13 — MCQ

The wait-for graph on single-instance resources has edges P1 → P2, P2 → P3, P3 → P1, and P4 → P2. No other edges exist. How many of these four processes can never run to completion?

A. 1
B. 2
C. 3
D. 4

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

A resource-allocation graph contains a cycle. At least one resource type in the graph has several instances. Which conclusion is justified?

A. The system is certainly deadlocked
B. The system might be deadlocked, but a cycle alone does not prove it when a type has multiple instances
C. A cycle proves that the state is safe
D. The banker's algorithm reports safety only when the graph has a cycle

---

## Q15 — NAT

Process P has Max = (4, 2) and Allocation = (1, 2). Need = Max − Allocation. The first component of P's Need vector is ____.

---

## Q16 — MSQ

**Select all that apply.**

A. Requiring a process to receive every resource it will need before it starts denies hold and wait
B. That all-at-once policy can leave resources idle that a running process does not yet need
C. Allowing the system to take a resource back denies the no-preemption condition
D. Mutual exclusion can be dropped for every resource, including a printer in the middle of a page, with no effect on the output

---

## Level 5 — Challenge

## Q17 — NAT

Four processes and two resource types. Available = (2, 1).

|  | Allocation (A B) | Max (A B) |
|---|---|---|
| P0 | 1 0 | 3 2 |
| P1 | 1 1 | 2 2 |
| P2 | 0 1 | 1 3 |
| P3 | 2 0 | 4 1 |

Need = Max − Allocation. How many distinct safe sequences does this state have?

---

## Q18 — MCQ

One resource type has 6 instances. Five processes have

| Process | Allocation | Max |
|---|---|---|
| P0 | 2 | 3 |
| P1 | 0 | 2 |
| P2 | 1 | 3 |
| P3 | 1 | 2 |
| P4 | 0 | 2 |

Available = 2. How many of these processes can stand first in some safe sequence?

A. 1
B. 2
C. 4
D. 5

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MSQ | A, B, C, D |
| 2 | MCQ | A |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | NAT | 2 |
| 7 | MCQ | A |
| 8 | MCQ | C |
| 9 | MSQ | A, B, C |
| 10 | NAT | 3 |
| 11 | MCQ | A |
| 12 | MSQ | A, C |
| 13 | MCQ | D |
| 14 | MCQ | B |
| 15 | NAT | 3 |
| 16 | MSQ | A, B, C |
| 17 | NAT | 8 |
| 18 | MCQ | D |

## Detailed Solutions

### Q1

Answer: A, B, C, D

The four Coffman conditions are mutual exclusion, hold and wait, no preemption, and circular wait. Deadlock of this kind arises when all four hold. Requiring every resource to be preemptible removes the no-preemption condition, so it is not a deadlock requirement.

### Q2

Answer: A

Each member of a deadlocked set is waiting for an event that can be produced only by another member, so none of them proceeds. Starvation is a process that remains ready, or that can in principle run, but is passed over repeatedly. A deadlock set has at least two processes in the usual resource cycle (a process can also wait for itself, but the definition is the closed set of waiters).

### Q3

Answer: A

If every process requests resource types in one global increasing order, a cycle in the request order cannot form. Allowing arbitrary order leaves circular wait possible. Adding edges or granting a request that closes a cycle creates the condition instead of preventing it.

### Q4

Answer: A

Safety means there exists at least one order in which the processes can finish if each one still asks for the rest of its declared maximum. A deadlocked state is unsafe. The zero available vector with positive remaining claims is not safe.

### Q5

Answer: A

With one instance of each type, deadlock exists exactly when the resource-allocation graph (or the wait-for graph) has a cycle. Here

\[
P1 \rightarrow R2 \rightarrow P2 \rightarrow R3 \rightarrow P3 \rightarrow R1 \rightarrow P1.
\]

P1 is waiting for the instance P2 holds, and the cycle continues around to R1, which P1 holds. Nobody in the cycle can run.

### Q6

Answer: 2

\[
\begin{align*}
Need(P0) &= (3,2,2) - (1,0,2) = (2,2,0) \\
Need(P1) &= (1,3,1) - (0,1,0) = (1,2,1) \\
Need(P2) &= (2,2,3) - (2,1,1) = (0,1,2)
\end{align*}
\]

Available Work = (1, 2, 2).

- P0 needs (2, 2, 0): the A component 2 is greater than 1, so P0 cannot be first.
- P1 needs (1, 2, 1) ≤ (1, 2, 2). Finish P1. Work becomes \((1,2,2)+(0,1,0) = (1,3,2)\). Then P2 needs (0, 1, 2) ≤ (1, 3, 2). Work becomes \((1,3,2)+(2,1,1) = (3,4,3)\). Then P0 finishes. Sequence: P1, P2, P0.
- P2 needs (0, 1, 2) ≤ (1, 2, 2). Finish P2. Work becomes \((1,2,2)+(2,1,1) = (3,3,3)\). Both remaining needs fit. Sequences: P2, P0, P1 and P2, P1, P0.

P1 and P2 can be first. That is 2 processes. P0 cannot.

### Q7

Answer: A

Aborting one process in the set releases its allocation, which can break the wait. Adding edges, increasing claims, or relabeling the state does not free a resource.

### Q8

Answer: C

A deadlock configuration for this claim bound has every process holding \(3 - 1 = 2\) instances and still needing one more, with nothing left free. Those processes hold \(5 \times 2 = 10\) instances. One additional instance means some process can reach its maximum and finish:

\[
1 + \sum_i (\textit{Max}_i - 1) = 1 + 5 \times 2 = 11.
\]

With 11 instances, deadlock is impossible. With 10 it is possible, so 10 does not guarantee freedom. 5 is only one per process, and 15 is larger than the minimum guarantee.

### Q9

Answer: A, B, C

The wait-for edge points from the waiter to the holder. Collapsing single-instance resources into those edges yields a graph in which a cycle is necessary and sufficient for deadlock. The banker's algorithm instead compares remaining Need vectors with an Available vector; it is not that graph.

### Q10

Answer: 3

From the work in Q6, the safe sequences are exactly

- P1, P2, P0
- P2, P0, P1
- P2, P1, P0

P0 cannot start, and after P1 the only process that fits the new Work (1, 3, 2) is P2 (P0 still needs 2 of A). After P2, both orders of the other two work. There are 3 safe sequences.

### Q11

Answer: A

Request (1, 0, 0) ≤ Need(P0) = (2, 2, 0) and ≤ Available (1, 2, 2). Tentative state:

- Available becomes (0, 2, 2)
- P0 Allocation becomes (2, 0, 2), Need becomes (1, 2, 0)

P2 needs (0, 1, 2) ≤ (0, 2, 2). Work becomes \((0,2,2)+(2,1,1) = (2,3,3)\). P0 needs (1, 2, 0) ≤ (2, 3, 3). Work becomes \((2,3,3)+(2,0,2) = (4,3,5)\). P1 then fits. The tentative state is safe (sequences P2, P0, P1 and P2, P1, P0), so the request is granted. P0 being unable to run first before the request does not forbid a later grant that leaves a safe state. The grant must not increase Need; it decreases Need.

### Q12

Answer: A, C

Two instances are held and one is free. Either P or Q can take the free instance, reach the extra instance it wants, finish, and release both of its instances. The other process then runs. The system is not deadlocked. With multiple instances of a type, a cycle in a resource-allocation drawing is not sufficient evidence of deadlock; the free instance is a concrete witness that someone can proceed.

### Q13

Answer: D

P1, P2, and P3 form a cycle, so each waits for another member of the cycle. P4 waits for P2. P2 never releases the resource P4 wants, because P2 is inside the cycle. All four processes stay blocked. Being outside the cycle does not save P4.

### Q14

Answer: B

For multi-instance types, a cycle is necessary for deadlock in the resource-allocation graph and is not sufficient. The system may still have a free instance, or an order in which some process finishes and breaks the apparent cycle. A cycle does not mean the state is safe. The banker's algorithm is a separate claim-versus-available test.

### Q15

Answer: 3

\[
Need = (4, 2) - (1, 2) = (3, 0).
\]

The first component is 3. Subtracting Allocation from Max in the other order would produce negative numbers and is not the Need matrix.

### Q16

Answer: A, B, C

Taking every resource before execution means a process never holds one resource while waiting for another, so hold and wait does not occur. Resources that sit unused until the process's whole claim is assembled can reduce utilization. Preemption directly denies "no preemption." A printer that is taken away in the middle of a page mixes two jobs on the paper; mutual exclusion stays necessary for that resource.

### Q17

Answer: 8

\[
\begin{align*}
Need(P0) &= (2, 2) \\
Need(P1) &= (1, 1) \\
Need(P2) &= (1, 2) \\
Need(P3) &= (2, 1)
\end{align*}
\]

Work starts at (2, 1).

- P0 needs (2, 2): B is short, so P0 cannot start.
- P2 needs (1, 2): B is short, so P2 cannot start.
- P1 needs (1, 1) ≤ (2, 1). After P1, Work = \((2,1)+(1,1) = (3,2)\).
- P3 needs (2, 1) ≤ (2, 1). After P3, Work = \((2,1)+(2,0) = (4,1)\).

After P1, Work is (3, 2). That vector covers P0's (2, 2), P2's (1, 2), and P3's (2, 1), and every later release makes Work still larger, so all \(3! = 6\) orders of the other three processes are safe.

Sequences that start with P1:

- P1, P0, P2, P3
- P1, P0, P3, P2
- P1, P2, P0, P3
- P1, P2, P3, P0
- P1, P3, P0, P2
- P1, P3, P2, P0

After P3, Work is (4, 1). P0 needs (2, 2), which does not fit yet, and P2 needs (1, 2), which does not fit yet. P1 needs (1, 1) and does fit. So every sequence that starts with P3 continues with P1, and then both orders of P0 and P2 work:

- P3, P1, P0, P2
- P3, P1, P2, P0

That is \(6 + 2 = 8\) safe sequences.

### Q18

Answer: D

Allocated instances: \(2+0+1+1+0 = 4\). Available \(6 - 4 = 2\), which matches the given Available.

\[
Need = (1, 2, 2, 1, 2).
\]

Every Need entry is at most 2, so each of the five processes can be the first to finish. After any one finishes, Available increases and the rest still fit. The state is safe, and the number that can stand first is 5.

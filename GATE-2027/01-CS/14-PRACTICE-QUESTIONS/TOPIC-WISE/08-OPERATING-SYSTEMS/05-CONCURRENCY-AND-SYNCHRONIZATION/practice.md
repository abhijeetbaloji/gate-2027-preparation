# Concurrency and Synchronization — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Mutual exclusion for a critical section means

A. at most one process executes that critical section at a time
B. processes enter in order of increasing pid
C. a process may be postponed forever in favor of newcomers
D. the critical section must run with interrupts disabled on every CPU

---

## Q2 — MSQ

**Select all that apply.**

Which of the following are synchronization tools for a critical section or a resource pool?

A. A binary semaphore
B. A mutex
C. A counting semaphore
D. An ordinary shared integer that is incremented with a non-atomic read-modify-write and is never tested by a lock

---

## Q3 — MCQ

A mutex, in its usual role, differs from a counting semaphore because

A. a mutex is an ownership lock for mutual exclusion, while a counting semaphore can represent a pool of several permits
B. any thread may raise a mutex value above 1 to let several threads into the same critical section
C. a semaphore operation is not allowed to block
D. mutexes exist only between processes, and semaphores exist only between threads

---

## Q4 — MCQ

A spinlock protects a short critical section. A thread that finds the lock held

A. burns CPU cycles while repeatedly testing the lock
B. always blocks in the kernel without consuming a CPU
C. increments a counting semaphore past its maximum
D. disables interrupts on every processor in the system by itself

---

## Q5 — MSQ

**Select all that apply.**

A shared structure is guarded by a mutex. Which statements are correct?

A. A thread acquires the mutex before using the structure
B. A thread that acquired the mutex releases it on the way out of the critical section
C. Two threads on two cores may hold that same mutex at the same time
D. Keeping the critical section short reduces the time other threads spend waiting

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

A binary semaphore `s` is initialized to 1. Process A has executed `wait(s)` and is inside the critical section. Process B now executes `wait(s)`. B

A. also enters the critical section
B. blocks until A executes `signal(s)`
C. sets `s` to 2 and continues
D. terminates the process that initialized `s`

---

## Q7 — NAT

A counting semaphore starts at 4. The operations below all complete; none of them block. `W` is `wait` and `S` is `signal`.

```text
W  W  S  W  W  W
```

The semaphore value after the last operation is ____.

---

## Q8 — NAT

A bounded buffer uses the usual semaphores: `empty` starts at 5, `full` starts at 0, and `mutex` starts at 1. Producers and consumers use the correct wait/signal order. The system completes three produce operations and then one consume operation. The value of `empty` after those four operations is ____.

---

## Q9 — MCQ

A test-and-set instruction used to build a lock

A. atomically writes 1 into the lock word and returns the previous value
B. is a non-atomic pair of an ordinary load and an ordinary store
C. always blocks the caller in the kernel
D. computes a deadlock-avoidance safe sequence

---

## Q10 — MSQ

**Select all that apply.**

Which producer actions can break a correct bounded buffer?

A. Signaling `full` before the item is inserted
B. Waiting on `mutex` before waiting on `empty`
C. Waiting on `empty`, then on `mutex`, inserting, signaling `mutex`, then signaling `full`
D. Releasing `mutex` before the buffer slot is updated

---

## Q11 — MCQ

A mutex is implemented by a binary semaphore initialized to 1. Thread A executes `wait` and enters. Thread B then executes `wait` and blocks. Before A signals, how many threads are inside the critical section?

A. 0
B. 1
C. 2
D. 4

---

## Level 3 — Multi-Step

## Q12 — NAT

Semaphore `s` starts at 2. `W` is wait and `S` is signal. If the value is 0, wait blocks and leaves the value at 0 while counting a waiter. Signal wakes one waiter when a waiter exists, and otherwise increments the value. The operation sequence is

```text
W  W  W  S  W  S  S
```

Every woken thread has passed its wait. At the end nobody is blocked. The final value of `s` is ____.

---

## Q13 — MCQ

In the readers-preference solution of the readers–writers problem, readers do not wait if another reader is already active. A steady stream of new readers can

A. postpone a waiting writer indefinitely
B. force every writer to run before the next reader
C. make readers run one at a time
D. remove the need for a mutex around the reader count

---

## Q14 — NAT

`empty` starts at 8 and `mutex` starts at 1. A producer executes `wait(empty)` and then `wait(mutex)` and is now inside the critical section. It has not signaled yet. The value of `mutex` at this moment is ____.

---

## Q15 — MCQ

A binary semaphore `S` is initialized to 1. Process P executes `wait(S)` twice in a row before any `signal(S)`.

A. P enters the critical section and leaves it normally
B. P's second `wait(S)` blocks forever
C. `S` becomes 3
D. two critical sections of P run concurrently

---

## Q16 — MSQ

**Select all that apply.**

A barrier is set for 4 threads. Three threads have arrived and are waiting. The fourth has not arrived.

A. Those three threads are blocked at the barrier
B. The barrier has already released the three threads into the next phase
C. The arrival of the fourth thread releases the group
D. Any one of the three may leave for the next phase while the others stay

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

A producer uses this order on a buffer that is already full (`empty = 0`, `mutex = 1`). The consumer needs `mutex` to remove an item and signal `empty`.

```text
wait(mutex);
wait(empty);
insert item
signal(full);
signal(mutex);
```

The producer runs first. What happens?

A. The producer acquires `mutex`, then blocks on `empty`, still holding `mutex`. The consumer cannot enter, and both sides wait
B. This is the correct order, and the producer inserts immediately
C. `wait(empty)` increments `empty` because the buffer is full
D. `signal(mutex)` runs before `wait(empty)` in this listing

---

## Q18 — MCQ

A semaphore meant to be an unlocked mutex is initialized to 0 by mistake. The first thread executes `wait`. That thread

A. enters the critical section immediately
B. blocks; 0 means no permit is available
C. sets the semaphore to 1 and continues
D. enters together with the next thread that waits

---

## Q19 — MSQ

**Select all that apply.**

A. A solution can provide mutual exclusion and still allow one process to starve
B. Disabling interrupts on the CPU that executes the entry code is enough to lock out every other CPU on a multiprocessor
C. A correct critical-section solution must not assume a particular relative speed among the processes
D. The classical two-process Peterson solution is built from shared variables under atomic reads and writes of a word

---

## Level 5 — Challenge

## Q20 — MSQ

**Select all that apply.**

Shared `x` starts at 0. Semaphore `m` starts at 1 and semaphore `r` starts at 0.

```text
Thread A          Thread B           Thread C
wait(m);          wait(r);           wait(r);
x = x + 5;        wait(m);           wait(m);
signal(m);        x = x + 3;         x = x * 2;
signal(r);        signal(m);         signal(m);
```

Scheduling continues until every thread that is not blocked has finished. Which values of `x` are possible in that state?

A. 8
B. 10
C. 16
D. 13

---

## Q21 — NAT

`empty` starts at 4 and `full` starts at 0. Each letter below is one completed produce (`P`) or consume (`C`) that uses the correct semaphore order. The sequence never blocks.

```text
P  P  C  P  P  C  C
```

The number of items in the buffer at the end is ____.

---

## Q22 — MCQ

Semaphores `sA` and `sB` start at 0.

```text
Thread A                 Thread B
a1;                      b1;
signal(sA);              signal(sB);
wait(sB);                wait(sA);
a2;                      b2;
```

Which ordering is guaranteed?

A. `a1` happens before `b2`, and `b1` happens before `a2`
B. `a2` happens before `b1`
C. `a1` happens before `b1` on every execution
D. There is no constraint between `{a1, b1}` and `{a2, b2}`

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | MSQ | A, B, D |
| 6 | MCQ | B |
| 7 | NAT | 0 |
| 8 | NAT | 3 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, D |
| 11 | MCQ | B |
| 12 | NAT | 1 |
| 13 | MCQ | A |
| 14 | NAT | 0 |
| 15 | MCQ | B |
| 16 | MSQ | A, C |
| 17 | MCQ | A |
| 18 | MCQ | B |
| 19 | MSQ | A, C, D |
| 20 | MSQ | A, B |
| 21 | NAT | 1 |
| 22 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

Mutual exclusion limits the critical section to one process at a time. Entry order by pid, starvation, and interrupt disabling are different properties. Starvation is the failure of bounded waiting, not the definition of mutual exclusion.

### Q2

Answer: A, B, C

Binary semaphores, mutexes, and counting semaphores are standard tools. A plain shared integer updated with a non-atomic increment does not provide exclusion or a permit count.

### Q3

Answer: A

A mutex is held by the thread that locked it and is released by that thread; its purpose is exclusion. A counting semaphore's value is a number of available permits, so it can guard a pool of size N. A mutex is not raised above 1 to admit several holders. Both tools can block, and both are used with threads and, in many systems, with processes.

### Q4

Answer: A

The waiter stays on the CPU and tests the lock word until the holder releases it. That is busy waiting. A blocking lock would park the thread. One CPU disabling its own interrupts does not stop another CPU from entering the same section.

### Q5

Answer: A, B, D

The lock is acquired on the way in and released on the way out. Exclusion means two threads do not hold it together, on one core or on many. A long critical section keeps waiters delayed, so the section should do only the shared update.

### Q6

Answer: B

The first `wait` changes `s` from 1 to 0. The second `wait` finds 0 and blocks. B enters only after A's `signal` releases a permit.

### Q7

Answer: 0

\[
4 \xrightarrow{W} 3 \xrightarrow{W} 2 \xrightarrow{S} 3 \xrightarrow{W} 2 \xrightarrow{W} 1 \xrightarrow{W} 0
\]

The value never hits 0 before a wait, so nobody blocks. The final value is 0.

### Q8

Answer: 3

Each completed produce does `wait(empty)` and each completed consume does `signal(empty)`.

\[
5 \xrightarrow{P} 4 \xrightarrow{P} 3 \xrightarrow{P} 2 \xrightarrow{C} 3
\]

`full` ends at \(0 + 3 - 1 = 2\). The question asks for `empty`, which is 3.

### Q9

Answer: A

Test-and-set reads the old bit and writes 1 in one indivisible step. The caller spins or parks according to the old value; the instruction itself is not a kernel block and it does not run the banker's algorithm. A separate load and store would race.

### Q10

Answer: A, B, D

Signaling `full` before the insert lets a consumer observe an empty slot. Waiting on `mutex` before `empty` can deadlock: a producer that finds the buffer full holds `mutex` while it waits for `empty`, and the consumer needs `mutex` to free a slot. Releasing `mutex` before the update publishes an unfinished slot. The order in C is the standard correct order.

### Q11

Answer: B

A's `wait` consumes the only permit. B's `wait` blocks. Exactly one thread, A, is inside the section.

### Q12

Answer: 1

Using the blocked-waiter form (value stays non-negative):

| Step | Action | Value | Waiters |
|---|---|---|---|
| start |  | 2 | 0 |
| 1 | W acquires | 1 | 0 |
| 2 | W acquires | 0 | 0 |
| 3 | W blocks | 0 | 1 |
| 4 | S wakes | 0 | 0 |
| 5 | W blocks | 0 | 1 |
| 6 | S wakes | 0 | 0 |
| 7 | S increments | 1 | 0 |

The negative-value convention reaches the same end: \(2,1,0,-1,0,-1,0,1\). After the last signal nobody is waiting and the value is 1.

### Q13

Answer: A

If readers keep arriving, the reader count stays positive and the writer never obtains the writer lock. That is writer starvation under reader preference. Readers are allowed to overlap, and the reader count is still protected when it is updated.

### Q14

Answer: 0

`wait(mutex)` consumes the permit that started at 1. While the producer is inside and has not signaled, `mutex` is 0. (`empty` has moved from 8 to 7; the question asks for `mutex`.)

### Q15

Answer: B

The first `wait` sets `S` to 0 and P enters. The second `wait` finds an empty semaphore and blocks. No other process signals `S`, so P stays blocked. P cannot run two critical sections concurrently with itself this way.

### Q16

Answer: A, C

A barrier opens when the last required thread arrives. Until then the threads that have arrived wait. One of them does not proceed alone.

### Q17

Answer: A

`wait(mutex)` succeeds and sets `mutex` to 0. `wait(empty)` then finds 0 and blocks. The consumer's `wait(mutex)` also blocks. The producer is waiting for the consumer to signal `empty`, and the consumer is waiting for `mutex`. This is the classic lock-order deadlock. The correct producer order waits for `empty` before taking `mutex`. `wait` does not increment `empty`.

### Q18

Answer: B

`wait` on 0 blocks. Initialization to 1 is what makes the first `wait` succeed for an unlocked mutex. Initialization to 0 starts the semaphore locked, with no permit.

### Q19

Answer: A, C, D

Mutual exclusion does not by itself guarantee bounded waiting; a process can be excluded forever. Interrupt disabling on one CPU leaves the other CPUs free to enter the section. Progress and exclusion arguments assume nothing about who runs faster. Peterson's two-process algorithm uses shared `flag` and `turn` variables and relies on atomic word reads and writes.

### Q20

Answer: A, B

`r` starts at 0, so B and C block on `wait(r)` until A signals. A adds 5 under `m` and signals `r` once. Exactly one of B or C consumes that permit. The other stays blocked.

- If B runs, \(x = 5 + 3 = 8\).
- If C runs, \(x = 5 \times 2 = 10\).

Both cannot run, so \(x\) does not become \((5+3)\times 2 = 16\) or \(5\times 2+3 = 13\).

### Q21

Answer: 1

Track the item count. Produce adds one when `empty > 0`. Consume removes one when `full > 0`.

| Op | Items | empty | full |
|---|---|---|---|
| start | 0 | 4 | 0 |
| P | 1 | 3 | 1 |
| P | 2 | 2 | 2 |
| C | 1 | 3 | 1 |
| P | 2 | 2 | 2 |
| P | 3 | 1 | 3 |
| C | 2 | 2 | 2 |
| C | 1 | 3 | 1 |

The buffer holds 1 item. Four produces and three consumes also give \(4 - 3 = 1\), and the running count shows the sequence never asked for an item that was not there or a free slot that was not there.

### Q22

Answer: A

`b2` is after `wait(sA)`, and `signal(sA)` is after `a1`, so `a1` happens before `b2`. Symmetrically, `b1` happens before `a2`. Nothing orders `a1` against `b1`: each side does its first statement before it waits. `a2` cannot be required to precede `b1`, because `a2` itself waits for `b1`'s signal.

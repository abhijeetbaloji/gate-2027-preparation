# Queues — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Circular-queue questions use this representation unless they say otherwise. The array has length `N`. `front` is the index of the next element to remove. `rear` is the index of the next free slot. The queue is empty when `front == rear` and full when `(rear + 1) % N == front`. An enqueue writes at `rear` and then sets `rear = (rear + 1) % N`. A dequeue reads the value at `front` and then sets `front = (front + 1) % N`. Both indices start at 0. This representation leaves one slot unused, so at most `N - 1` elements are stored.

A deque can insert or delete at either end.

## Level 1 — Conceptual

## Q1 — MCQ

An empty queue receives enqueue 1, enqueue 2, enqueue 3, dequeue, dequeue, enqueue 4. The value then at the front is

A. 1

B. 2

C. 3

D. 4

---

## Q2 — NAT

A circular queue uses an array of length 8 and the representation in the header. The maximum number of elements it can store is ____.

---

## Q3 — MCQ

Which structure returns values in first-in, first-out order?

A. stack

B. queue

C. binary max-heap

D. binary search tree

---

## Level 2 — Standard GATE Style

## Q4 — NAT

A circular queue has array length `N = 5`, with `front` and `rear` starting at 0. The operations are enqueue 10, enqueue 20, enqueue 30, dequeue, enqueue 40, enqueue 50. The value at the front after these operations is ____.

---

## Q5 — MCQ

An empty queue receives enqueue A, enqueue B, dequeue, enqueue C, enqueue D, dequeue, dequeue. The sequence of dequeued values is

A. A, B, C

B. A, C, D

C. B, C, D

D. A, B, D

---

## Q6 — NAT

A queue is implemented with two stacks, `inStack` and `outStack`. Enqueue pushes onto `inStack`. Dequeue pops from `outStack`; if `outStack` is empty, every element of `inStack` is first popped and pushed onto `outStack`, and then `outStack` is popped. Starting from two empty stacks, the operations are enqueue 1, enqueue 2, enqueue 3, dequeue, dequeue, enqueue 4, dequeue. The number of pop operations performed on either stack is ____.

---

## Q7 — MCQ

A non-circular queue uses an array of length 5. `front` starts at 0 and `rear` starts at `-1`. Enqueue increments `rear` and then writes at `rear`. Dequeue reads `front` and then increments `front`. After five enqueues and five dequeues, which statement is true?

A. `front` is 0 and `rear` is `-1`, so five further enqueues fit in the array.

B. `front` is 5 and `rear` is 4. No element is stored, but this non-circular implementation has `rear` at the last index, so it cannot enqueue again.

C. The five enqueued values are still stored as members of the queue.

D. `rear` has returned to `-1`.

---

## Level 3 — Multi-Step

## Q8 — NAT

A deque starts empty. The operations are insertRear 1, insertRear 2, insertFront 3, deleteRear, insertRear 4, deleteFront. The sum of the values still in the deque is ____.

---

## Q9 — MCQ

Under the circular-queue representation in the header, the queue is full when

A. `front == rear`

B. `(rear + 1) % N == front`

C. `rear == N`

D. `front == 0`

---

## Q10 — NAT

A circular queue has array length `N = 6`, with both indices starting at 0. It then performs four enqueues, two dequeues, and three enqueues, in that order. Every enqueue succeeds. The number of elements stored at the end is ____.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Under the header’s convention, a circular queue has `front = 2` and `rear = 2`. Which statement is correct?

A. It contains one element, stored at index 2.

B. It is empty.

C. It is full.

D. It contains two elements.

---

## Q12 — MSQ

Select all that apply. For the circular queue defined in the header, with array length `N`:

A. At most `N - 1` elements can be stored.

B. `front == rear` means the queue is full.

C. `(rear + 1) % N == front` means the queue is full.

D. `N` enqueues in a row, with no dequeue, all succeed.

---

## Level 5 — Challenge

## Q13 — NAT

A circular queue has array length `N = 7`, with both indices starting at 0. The operations, in order, are:

enqueue 1, enqueue 2, enqueue 3, enqueue 4, dequeue, dequeue, enqueue 5, enqueue 6, dequeue, enqueue 7, enqueue 8, dequeue, dequeue.

The sum of the values still stored after these operations is ____.

---

## Q14 — MCQ

A deque starts empty. The operations are insertRear 4, insertRear 1, insertFront 7, deleteRear, insertRear 9, deleteFront, deleteFront. The sequence of deleted values is

A. 1, 7, 4

B. 7, 4, 1

C. 4, 1, 7

D. 1, 4, 7

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (C) |
| 2 | NAT | 7 |
| 3 | MCQ | (B) |
| 4 | NAT | 20 |
| 5 | MCQ | (A) |
| 6 | NAT | 6 |
| 7 | MCQ | (B) |
| 8 | NAT | 5 |
| 9 | MCQ | (B) |
| 10 | NAT | 5 |
| 11 | MCQ | (B) |
| 12 | MSQ | (A), (C) |
| 13 | NAT | 21 |
| 14 | MCQ | (A) |

## Detailed Solutions

### Q1

Answer: (C)

The queue from front to rear is `1`, then `1 2`, then `1 2 3`. The two dequeues remove 1 and 2, leaving `3`. Enqueue 4 leaves `3 4`. The front value is 3.

### Q2

Answer: 7

One array slot stays unused so that `front == rear` can mean empty while `(rear + 1) % N == front` means full. For `N = 8`, the maximum number of stored elements is 7.

### Q3

Answer: (B)

A queue removes the element that has been present longest. A stack removes the most recently pushed element. A max-heap removes the largest key, and a binary search tree does not by itself define a first-in, first-out removal order.

### Q4

Answer: 20

`N = 5`, and both indices start at 0.

- Enqueue 10 writes index 0; `rear = 1`.
- Enqueue 20 writes index 1; `rear = 2`.
- Enqueue 30 writes index 2; `rear = 3`.
- Dequeue reads 10 and sets `front = 1`.
- Enqueue 40 writes index 3; `rear = 4`.
- Enqueue 50 writes index 4; `rear = 0`.

The stored elements are 20 at index 1, 30 at index 2, 40 at index 3, and 50 at index 4. The front value is 20. Also, `(rear + 1) % 5 = 1`, which equals `front`, so the queue is now full. That agrees with storing `N - 1 = 4` elements.

### Q5

Answer: (A)

Enqueue A and B, then dequeue A. Enqueue C and D. The queue from front to rear is now `B C D`. The next two dequeues return B and C. The full dequeued sequence is A, B, C.

### Q6

Answer: 6

Enqueue pushes 1, then 2, then 3 onto `inStack`, so its top is 3. No pop has happened yet.

The first dequeue finds `outStack` empty. It pops 3, 2, and 1 from `inStack` and pushes them onto `outStack`. Those are three pops. From bottom to top, `outStack` is then `3 2 1`. Popping 1 is the fourth pop and leaves top 2.

The second dequeue pops 2. That is the fifth pop.

Enqueue 4 pushes 4 onto `inStack` and does not pop.

The third dequeue finds 3 still on `outStack` and pops it. That is the sixth pop. The dequeued values are 1, 2, and 3, and the total number of pops is 6.

### Q7

Answer: (B)

The five enqueues set `rear` to 0, 1, 2, 3, and finally 4. The five dequeues set `front` to 1, 2, 3, 4, and finally 5. No enqueued value remains in the queue. However, `rear` is still 4, the last legal index. Another enqueue would increment `rear` to 5 and write outside the array, so this non-circular implementation cannot accept it. This is false overflow: the logical queue is empty, but the indices have moved to the right end and do not wrap. A circular queue reuses the slots freed on the left.

### Q8

Answer: 5

insertRear 1 leaves `1`. insertRear 2 leaves `1 2`, with 2 at the rear. insertFront 3 leaves `3 1 2`. deleteRear removes 2, leaving `3 1`. insertRear 4 leaves `3 1 4`. deleteFront removes 3, leaving `1 4`. The remaining sum is 5.

### Q9

Answer: (B)

By the stated convention, `front == rear` means empty, because `rear` is the next write position and the two indices meet when nothing is waiting. Full is the condition that would make the next enqueue land on `front`: `(rear + 1) % N == front`. The value of `front` alone does not say whether the queue is full.

### Q10

Answer: 5

Start with `front = rear = 0` and `N = 6`.

Four enqueues leave `rear = 4` and a count of 4. Two dequeues set `front = 2` and leave a count of 2. The next enqueue writes index 4 and sets `rear = 5`, count 3. The next writes index 5 and sets `rear = 0`, count 4. The next writes index 0 and sets `rear = 1`, count 5. The full test does not fail on any of these enqueues: after the last one, `(1 + 1) % 6 = 2`, which equals `front`, so the queue has just become full. The stored count is 5, which is `N - 1`.

### Q11

Answer: (B)

Here `rear` is the next free index, not the index of the last stored element. If `front` and `rear` are equal, the next read position and the next write position are the same, which is the empty state. It is not the full state: full requires `(rear + 1) % N == front`, and it is not a one-element queue. A different textbook convention lets both indices point at the single stored element. That is not the convention fixed in the header, so the snapshot is empty.

### Q12

Answer: (A), (C)

(A) and (C) restate the header. One unused slot distinguishes full from empty, so the capacity is `N - 1`, and the full test is `(rear + 1) % N == front`. (B) is the empty test, not the full test. (D) is false: the `N`th consecutive enqueue would make `rear` catch `front`, and the full test rejects it. After `N - 1` successful enqueues from empty, the queue is full.

### Q13

Answer: 21

`N = 7`, and both indices start at 0. There are eight enqueues and five dequeues, so three values remain. From front to rear, the contents change as follows.

- After enqueue 1, 2, 3, 4: `1 2 3 4`.
- Two dequeues leave `3 4`.
- Enqueue 5 and 6: `3 4 5 6`.
- One dequeue leaves `4 5 6`.
- Enqueue 7 and 8: `4 5 6 7 8`.
- Two dequeues leave `6 7 8`.

The removed values are 1, 2, 3, 4, and 5. The stored values are 6, 7, and 8, and their sum is 21.

The indices confirm the count. `rear` advances eight times from 0 and ends at 1. `front` advances five times and ends at 5. The stored count is `(1 - 5) mod 7 = 3`. Those three slots are indices 5, 6, and 0, written by the enqueues of 6, 7, and 8.

### Q14

Answer: (A)

The deque, written from front to rear, changes as follows.

- insertRear 4 leaves `4`.
- insertRear 1 leaves `4 1`.
- insertFront 7 leaves `7 4 1`.
- deleteRear removes 1 and leaves `7 4`.
- insertRear 9 leaves `7 4 9`.
- deleteFront removes 7 and leaves `4 9`.
- deleteFront removes 4 and leaves `9`.

The deleted sequence is 1, 7, 4. The value 9 is still stored and is not part of the deleted sequence.

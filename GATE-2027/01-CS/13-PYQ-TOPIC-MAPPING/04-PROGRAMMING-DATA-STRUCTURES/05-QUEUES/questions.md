# GATE PYQs

## 2026

### Q.50

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a stack 𝑆 and a queue 𝑄. Both of them are initially empty and have the
capacity to store ten elements each. The elements 1, 2, 3, 4, and 5 arrive one by one,
in that order. When an element arrives, it is assigned either to 𝑆 (pushed on 𝑆 ) or
to 𝑄 (enqueued to 𝑄). Once all the five elements are stored, the output is generated
in two steps. First, stack S is emptied by popping all elements. Then queue  𝑄 is
emptied by dequeueing all elements. The output obtained by following this process
is 4 3 1 2 5 .
Given the output, the objective is to predict whether an element was assigned to 𝑆
or 𝑄.
Which of the following options is/are possible valid assignment(s) of the
elements?
Note: In the options, the notation 𝑥𝑆 denotes that element 𝑥 was assigned to 𝑆 and
𝑦𝑄 denotes that element 𝑦 was assigned to 𝑄.

**Options:**

A. 1𝑆, 2𝑄, 3𝑆, 4𝑆, 5𝑄
B. 1𝑄, 2𝑄, 3𝑆, 4𝑆, 5𝑄
C. 1𝑄, 2𝑄, 3𝑄, 4𝑆, 5𝑆
D. 1𝑆, 2𝑆, 3𝑆, 4𝑄, 5𝑄

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2023

### Q.59

**Paper:** GATE 2023 CS

**Question:**

Consider a sequence a of elements a_{0} = 1, a_{1} = 5, a_{2} = 7, a_{3} = 8, a_{4} = 9, and
a_{5} = 2. The following operations are performed on a stack S and a queue Q, both
of which are initially empty.
I: push the elements of a from a_{0} to a_{5} in that order into S.
II: enqueue the elements of a from a_{0} to a_{5} in that order into Q.
III: pop an element from S.
IV: dequeue an element from Q.
V: pop an element from S.
VI: dequeue an element from Q.
VII: dequeue an element from Q and push the same element into S.
VIII: Repeat operation VII three times.
IX: pop an element from S.
X: pop an element from S.
The top element of S after executing the above operations is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.62

**Paper:** GATE 2022 CS

**Question:**

Consider the queues  Q_{1}  containing four elements and  Q_{2}  containing none (shown
as the Initial State in the figure). The only operations allowed on these two queues
are  Enqueue(Q,element) and  Dequeue(Q). The minimum number of
Enqueue operations on  Q_{1} required to place the elements of  Q_{1} in  Q_{2}  in reverse
order (shown as the Final State in the figure) without using any additional storage
is___________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.21

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following sequence of operations on an empty stack.
push(54); push(52); pop(); push(55); push(62); s = pop();
Consider the following sequence of operations on an empty queue.
enqueue(21); enqueue(24); dequeue(); enqueue(28); enqueue(32); q = dequeue();
The value of s + q is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.35

**Paper:** GATE 2020 CS

**Question:**

Consider the following five disk access requests of the form (request id, cylinder
number) that are present in the disk scheduler queue at a given time.
(P, 155), (Q. 85), (R, 110), (S, 30), (T, 115)
Assume the head is positioned at cylinder 100. The scheduler follows Shortest
Seek Time First scheduling to service the requests.
Which one of the following statements is FALSE?

**Options:**

A. T is serviced before P.
B. Q is serviced after S, but before T. () The head reverses its direction of movement between servicing of Q and P.
D. R is serviced before P.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2017

### Q.15

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 1 Wrong : -0.33
The Breadth First Search (BFS) algorithm has been implemented using the queue data structure.
Which one of the following is a possible order of visiting the nodes in the graph below?

**Options:**

A. MNOPQR
B. NQMPOR
C. QMNROP
D. POQNMR

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.10

**Paper:** GATE 2016 CS-1

**Question:**

A queue is implemented using an array such that ENQUEUE and DEQUEUE operations are
performed efficiently. Which one of the following statements is CORRECT (n refers to the
number of items in the queue)?

**Options:**

A. Both operations can be performed in O(1) time
B. At most one operation can be performed in O(1) time but the worst case time for the other operation will be Ω(n)
C. The worst case time complexity for both operations will be Ω(n)
D. Worst case time complexity for both operations will be Ω(log n) CS(Set A) 2/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2016 CS-1

**Question:**

Let Q denote a queue containing sixteen numbers and S be an empty stack. Head(Q) returns
the element at the head of the queue Q without removing it from Q. Similarly Top(S) returns
the element at the top of S without removing it from S. Consider the algorithm given below.
while Q is not Empty do
if S is Empty OR Top(S) ≤ Head(Q) then
x := Dequeue(Q);
Push(S, x);
else
x := Pop(S);
Enqueue(Q, x);
end
end
The maximum possible number of iterations of the while loop in the algorithm is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.48

**Paper:** GATE 2016 CS-1

**Question:**

Consider a disk queue with requests for I/O to blocks on cylinders 47, 38, 121, 191, 87, 11,
92, 10. The C-LOOK scheduling algorithm is used. The head is initially at cylinder number
63, moving towards larger cylinder numbers on its servicing pass. The cylinders are numbered
from 0 to 199. The total head movement (in number of cylinders) incurred while servicing
these requests is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2014

### Q.19

**Paper:** GATE 2014 CS SET-1

**Question:**

Suppose a disk has 201 cylinders, numbered from 0 to 200. At some time the disk arm is at cylinder
100, and there is a queue of disk access requests for cylinders 30, 85, 90, 100, 105, 110, 135 and
145. If Shortest-Seek Time First (SSTF) is being used for scheduling the disk access, the request for
cylinder 90 is serviced after servicing ____________ number of requests.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.41

**Paper:** GATE 2014 CS SET-2

**Question:**

Suppose a stack implementation supports an instruction REVERSE, which reverses the order of
elements on the stack, in addition to the PUSH and POP instructions. Which one of the following
statements is TRUE with respect to this modified stack?

**Options:**

A. A queue cannot be implemented using this stack.
B. A queue can be implemented where ENQUEUE takes a single instruction and DEQUEUE takes a sequence of two instructions.
C. A queue can be implemented where ENQUEUE takes a sequence of three instructions and DEQUEUE takes a single instruction.
D. A queue can be implemented where both ENQUEUE and DEQUEUE take a single instruction each.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.44

**Paper:** GATE 2013 CS Booklet A

**Question:**

Consider the following operation along with Enqueue and Dequeue operations on queues, where
k is a global parameter.
MultiDequeue(Q){
m = k
while (Q is not empty) and (m > 0) {
Dequeue(Q)
m = m – 1
}
}
What is the worst case time complexity of a sequence of n queue operations on an initially empty
queue?

**Options:**

A. Θ(n)
B. Θ(n + k)
C. Θ(nk)
D. Θ(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2013 CS Booklet B

**Question:**

Consider the following operation along with Enqueue and Dequeue operations on queues, where
k is a global parameter.
MultiDequeue(Q){
m = k
while (Q is not empty) and (m > 0) {
Dequeue(Q)
m = m – 1
}
}
What is the worst case time complexity of a sequence of n queue operations on an initially empty
queue?

**Options:**

A. Θ(n)
B. Θ(n + k)
C. Θ(nk)
D. Θ(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.40

**Paper:** GATE 2013 CS Booklet C

**Question:**

Consider the following operation along with Enqueue and Dequeue operations on queues, where
k is a global parameter.
MultiDequeue(Q){
m = k
while (Q is not empty) and (m > 0) {
Dequeue(Q)
m = m – 1
}
}
What is the worst case time complexity of a sequence of n queue operations on an initially empty
queue?

**Options:**

A. Θ(n)
B. Θ(n + k)
C. Θ(nk)
D. Θ(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2013 CS Booklet D

**Question:**

Consider the following operation along with Enqueue and Dequeue operations on queues, where
k is a global parameter.
MultiDequeue(Q){
m = k
while (Q is not empty) and (m > 0) {
Dequeue(Q)
m = m – 1
}
}
What is the worst case time complexity of a sequence of n queue operations on an initially empty
queue?

**Options:**

A. Θ(n)
B. Θ(n + k)
C. Θ(nk)
D. Θ(n^{2})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.35

**Paper:** GATE 2012 CS Booklet A

**Question:**

Suppose a circular queue of capacity (n −1) elements is implemented with an array of n elements.
Assume that the insertion and deletion operations are carried out using REAR and FRONT as array
index variables, respectively. Initially, REAR = FRONT = 0. The conditions to detect  queue full
and queue empty are

**Options:**

A. full: (REAR+1) mod n == FRONT
B. full: (REAR+1) mod n == FRONT empty: REAR == FRONT empty: (FRONT+1) mod n == REAR
C. full: REAR == FRONT
D. full: (FRONT+1) mod n == REAR empty: (REAR+1) mod n == FRONT empty: REAR == FRONT CS-A 8/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2008

### Q.19

**Paper:** GATE 2008 CS

**Question:**

The Breadth First Search algorithm has been implemented using the queue data structure. One
possible order of visiting the nodes of the following graph is

**Options:**

A. MNOPQR
B. NOMPOR
C. QMNPRO
D. QMNPOR

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

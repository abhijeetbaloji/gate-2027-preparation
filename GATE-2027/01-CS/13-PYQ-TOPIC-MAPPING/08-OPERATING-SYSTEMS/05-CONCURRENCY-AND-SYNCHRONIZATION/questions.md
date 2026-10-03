# GATE PYQs

## 2026

### Q.51

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider three processes P1, P2, and P3 running identical code, as shown in the
pseudocode below.  A and B are two binary semaphores initialized to  1 and  0,
respectively. X is a shared variable initialized to 0. Each line in the pseudocode is
executed atomically.
Pseudocode of P1, P2, and P3
Wait(A);
Print(*);
X = X+1;
If (X == 2)
{
Print($);
Signal(B);
}
Signal(A);
Wait(B);
Print(#);
Signal(B);
Assume that any of the three processes can start to execute first and context
switching can happen between these processes at any arbitrary time and in any
arbitrary order.
Which of the following patterns is/are possible to be generated as an outcome of the
execution of these three processes?

**Options:**

A. **$*###
B. **$#*##
C. **$##*#
D. ***$###

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2023

### Q.38

**Paper:** GATE 2023 CS

**Question:**

Consider the two functions incr and decr shown below.
incr(){  decr(){
wait(s);  wait(s);
X = X+1;  X = X-1;
signal(s);  signal(s);
}  }
There are 5 threads each invoking incr once, and 3 threads each invoking decr
once, on the same shared variable X. The initial value of X is 10.
Suppose there are two implementations of the semaphore s, as follows:
I-1: s is a binary semaphore initialized to 1.
I-2: s is a counting semaphore initialized to 2.
Let V1, V2 be the values of X at the end of execution of all the threads with
implementations I-1, I-2, respectively.
Which one of the following choices corresponds to the minimum possible values of
V1, V2, respectively?

**Options:**

A. 15, 7
B. 7, 7
C. 12, 7
D. 12, 8

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.19

**Paper:** GATE 2022 CS

**Question:**

Consider the following threads, T_{1}, T_{2}, and T_{3} executing on a single processor,
synchronized using three binary semaphore variables, S_{1}, S_{2}, and S_{3}, operated upon
using standard wait() and signal(). The threads can be context switched in
any order and at any time.
T_{1}  T_{2}  T_{3}
while(true){  while(true){  while(true){
wait(S_{3});  wait(S_{1});  wait(S_{2});
print(“C”);  print(“B”);  print(“A”);
signal(S_{2}); }  signal(S_{3}); }  signal(S_{1}); }
Which initialization of the semaphores would print the sequence BCABCABCA….?

**Options:**

A. S_{1}= 1; S_{2}= 1; S_{3}= 1
B. S_{1}= 1; S_{2}= 1; S_{3}= 0
C. S_{1}= 1; S_{2}= 0; S_{3}= 0
D. S_{1}= 0; S_{2}= 1; S_{3}= 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2022 CS

**Question:**

The following simple undirected graph is referred to as the Peterson graph.
Which of the following statements is/are TRUE?

**Options:**

A. The chromatic number of the graph is 3.
B. The graph has a Hamiltonian path.
C. The following graph is isomorphic to the Peterson graph.
D. The size of the largest independent set of the given graph is 3. (A subset of vertices of a graph form an independent set if no two vertices of the subset are adjacent.)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2020

### Q.34

**Paper:** GATE 2020 CS

**Question:**

Each of a set of n processes executes the following code using two semaphores
a and b initialized to 1 and 0, respectively. Assume that count is a shared
variable initialized to 0 and not used in CODE SECTION P.
CODE SECTION P
wait (a); count=count+1;
if (count==n) signal(b);
signal (a); wait(b); signal (b);
CODE SECTION Q
What does the code achieve?

**Options:**

A. It ensures that no process executes CODE SECTION Q before every process has finished CODE SECTION P.
B. It ensures that at most twoprocesses are in CODE SECTION Q at any time.
C. It ensures that all processes execute CODE SECTION P mutually exclusively.
D. It ensures that at most n-1 processes are in CODE SECTION P at any time.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.40

**Paper:** GATE 2018 CS

**Question:**

Consider the following solution to the producer-consumer synchronization problem. The
shared buffer size is 𝑁. Three semaphores empty,  full and mutex are defined with respective
initial values of 0, 𝑁 and 1. Semaphore empty denotes the number of available slots in the
buffer, for the consumer to read from. Semaphore full denotes the number of available slots
in the buffer, for the producer to write to. The placeholder variables, denoted by P, Q, R,
and S, in the code below can be assigned either  empty or  full. The valid semaphore
operations are: wait() and signal().
Producer:  Consumer:
do{  do{
wait(P);  wait(R);
wait(mutex);  wait(mutex);
//Add item to buffer  //Consume item from buffer
signal(mutex);  signal(mutex);
signal(Q);  signal(S);
}while(1);  }while(1);
Which one of the following assignments to P, Q, R and S will yield the correct solution?

**Options:**

A. P: full, Q: full, R: empty, S: empty
B. P: empty, Q: empty, R: full, S: full
C. P: full, Q: empty, R: empty, S: full
D. P: empty, Q: full, R: full, S: empty

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2016

### Q.48

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following two-process synchronization solution.
Process 0  Process 1
---------  ----------
Entry: loop while (turn == 1);  Entry: loop while (turn == 0);
(critical section)  (critical section)
Exit: turn = 1;  Exit: turn = 0;
The shared variable turn is initialized to zero. Which one of the following is TRUE?

**Options:**

A. This is a correct two-process synchronization solution.
B. This solution violates mutual exclusion requirement.
C. This solution violates progress requirement.
D. This solution violates bounded wait requirement.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2016 CS-2

**Question:**

Consider a non-negative counting semaphore S. The operation P(S) decrements S, and V (S)
increments S. During an execution, 20 P(S) operations and 12 V (S) operations are issued in
some order. The largest initial value of S for which at least one P(S) operation will remain
blocked is  .
CS(Set B)  15/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2014

### Q.23

**Paper:** GATE 2014 CS SET-3

**Question:**

In the following pairs of OSI protocol layer/sub-layer and its functionality, the INCORRECT pair
is

**Options:**

A. Network layer and Routing
B. Data Link Layer and Bit synchronization
C. Transport layer and End-to-end process communication
D. Medium Access Control sub-layer and Channel sharing CS03 (GATE 2014)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.34

**Paper:** GATE 2013 CS Booklet A

**Question:**

A shared variable x, initialized to zero, is operated on by four concurrent processes W, X, Y, Z as
follows. Each of the processes  W  and  X  reads  x from memory, increments by one, stores it to
memory, and then terminates. Each of the processes Y and Z reads x from memory, decrements by
two, stores it to memory, and then terminates. Each process before reading  x invokes the  P
operation (i.e., wait) on a counting semaphore S and invokes the V operation (i.e., signal) on the
semaphore S after storing x to memory. Semaphore S is initialized to two. What is the maximum
possible value of x after all processes complete execution?

**Options:**

A. –2
B. –1
C. 1
D. 2 CS-A 7/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2013 CS Booklet B

**Question:**

A shared variable x, initialized to zero, is operated on by four concurrent processes W, X, Y, Z as
follows. Each of the processes  W  and  X  reads  x from memory, increments by one, stores it to
memory, and then terminates. Each of the processes Y and Z reads x from memory, decrements by
two, stores it to memory, and then terminates. Each process before reading  x invokes the  P
operation (i.e., wait) on a counting semaphore S and invokes the V operation (i.e., signal) on the
semaphore S after storing x to memory. Semaphore S is initialized to two. What is the maximum
possible value of x after all processes complete execution?

**Options:**

A. –2
B. –1
C. 1
D. 2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2013 CS Booklet C

**Question:**

A shared variable x, initialized to zero, is operated on by four concurrent processes W, X, Y, Z as
follows. Each of the processes  W  and  X  reads  x from memory, increments by one, stores it to
memory, and then terminates. Each of the processes Y and Z reads x from memory, decrements by
two, stores it to memory, and then terminates. Each process before reading  x invokes the  P
operation (i.e., wait) on a counting semaphore S and invokes the V operation (i.e., signal) on the
semaphore S after storing x to memory. Semaphore S is initialized to two. What is the maximum
possible value of x after all processes complete execution?

**Options:**

A. –2
B. –1
C. 1
D. 2 CS- C 6/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2013 CS Booklet D

**Question:**

A shared variable x, initialized to zero, is operated on by four concurrent processes W, X, Y, Z as
follows. Each of the processes  W  and  X  reads  x from memory, increments by one, stores it to
memory, and then terminates. Each of the processes Y and Z reads x from memory, decrements by
two, stores it to memory, and then terminates. Each process before reading  x invokes the  P
operation (i.e., wait) on a counting semaphore S and invokes the V operation (i.e., signal) on the
semaphore S after storing x to memory. Semaphore S is initialized to two. What is the maximum
possible value of x after all processes complete execution?

**Options:**

A. –2
B. –1
C. 1
D. 2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2010

### Q.23

**Paper:** GATE 2010 CS

**Question:**

Consider thie methrals used by processes PI and I'2 for accessing cheir critical sections whenever
needed, as given below. The initial values of shared boolean variables 51 and S2 are randomly
assigned.
Method used by Pi Method used by P2
while (S1 == 52); while (S1 != S2):
Critical Section Critical Section
S1 = S2; S2 = not (S1);
Which one of the following statemonts descritus the properties achieved?

**Options:**

A. Mutual exclusion but not progross
B. Progress but not mutuat exclusion
C. Neither matual exelusion nos progruss
D. Borh mutual exclusion and progross

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2008

### Q.63

**Paper:** GATE 2008 CS

**Question:**

The Pand V operations on counting semaphores, where s is a counting semaphore, are defined as
follows:
P(s): S = S - 1;
ifs < 0 then wait;
V(s): s =s + 1; if s <= 0 then wakeup a process waiting on s;
Assume that Pb and Vo, the wait and signal operations on binary semaphores are provided. Two
binary semaphores b and yo are used to implement the semaphore operations P(s) and V(s) as
follows:
P(s) : Pb (xb);
s = s - 1;
if (s < 0) {
Vь (жb) ;
Рь(Уь) ;
else Vb(xb) ;
V (s) : Pb(xb) ;
S = S + 1;
if (s <= 0) Vb (Yb) :
Vь (хb) ;
The initial values of xb and yo are respectively

**Options:**

A. 0 and 0
B. 0 and 1
C. 1 and 0
D. 1 and 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

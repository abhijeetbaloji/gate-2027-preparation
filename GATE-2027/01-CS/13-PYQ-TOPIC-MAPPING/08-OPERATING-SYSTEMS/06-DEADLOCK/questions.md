# GATE PYQs

## 2026

### Q.29

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

With respect to deadlocks in an operating system, which of the following
statements is/are FALSE?

**Options:**

A. Banker’s algorithm is used to prevent deadlocks
B. Deadlock formation can be prevented by ensuring that the hold and wait condition is not allowed
C. An assignment edge in a resource allocation graph is marked from a process to a resource
D. A safe state guarantees that all processes can finish without formation of a deadlock

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a system consisting of  𝑘 instances of a resource  𝑅, being shared by
5 processes. Assume that each process requires a maximum of two instances of
resource 𝑅 and a process can request or release only one instance at a time. Further,
a process can request the second instance of the resource only after acquiring the
first instance.
The minimum value of 𝑘 for the system to be deadlock-free is ________. (answer
in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

## 2025

### Q.48

**Paper:** GATE 2025 CS-2

**Question:**

𝑃= {𝑃_{1}, 𝑃_{2}, 𝑃_{3}, 𝑃_{4}} consists of all active processes in an operating system.
𝑅= {𝑅_{1}, 𝑅_{2}, 𝑅_{3}, 𝑅_{4}} consists of single instances of distinct types of resources in the
system.
The resource allocation graph has the following assignment and claim edges.
Assignment edges:  𝑅_{1} →𝑃_{1},  𝑅_{2} →𝑃_{2},  𝑅_{3} →𝑃_{3},  𝑅_{4} →𝑃_{4} (the assignment edge
𝑅_{1} →𝑃_{1} means resource 𝑅_{1} is assigned to process 𝑃_{1} , and so on for others)
Claim edges:  𝑃_{1} →𝑅_{2},  𝑃_{2} →𝑅_{3},  𝑃_{3} →𝑅_{1},  𝑃_{2} →𝑅_{4},  𝑃_{4} →𝑅_{2} (the claim edge
𝑃_{1}  → 𝑅_{2}  means process 𝑃_{1}is waiting for resource  𝑅_{2} , and so on for others)
Which of the following statement(s) is/are CORRECT?

**Options:**

A. Aborting 𝑃_{1} makes the system deadlock free.
B. Aborting 𝑃_{3} makes the system deadlock free.
C. Aborting 𝑃_{2} makes the system deadlock free.
D. Aborting 𝑃_{1} and 𝑃_{4} makes the system deadlock free.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.27

**Paper:** GATE 2024 CS2

**Question:**

Which of the following statements about the Two Phase Locking (2PL) protocol
is/are TRUE?

**Options:**

A. 2PL permits only serializable schedules With 2PL, a transaction always locks the data item being read or written just
B. before every operation and always releases the lock just after the operation With 2PL, once a lock is released on any data item inside a transaction, no more
C. locks on any data item can be obtained inside that transaction
D. A deadlock is possible with 2PL

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2024 CS2

**Question:**

two semaphores:  s1 (initialized to 1) and  s2 (initialized to 0). The threads also
share a global variable  x (initialized to 0). The threads execute the code shown
below.
// code of T1  // code of T2
wait(s1);  wait(s1);
x = x+1;  x = x+1;
print(x);  print(x);
wait(s2);  signal(s2);
signal(s1);  signal(s1);
Which of the following outcomes is/are possible when threads T1 and T2 execute
concurrently?

**Options:**

A. T1 runs first and prints 1, T2 runs next and prints 2
B. T2 runs first and prints 1, T1 runs next and prints 2
C. T1 runs first and prints 1, T2 does not print anything (deadlock)
D. T2 runs first and prints 1, T1 does not print anything (deadlock) Let 𝐴 be an 𝑛× 𝑛 matrix over the set of all real numbers ℝ. Let 𝐵 be a matrix

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2022

### Q.26

**Paper:** GATE 2022 CS

**Question:**

Which of the following statements is/are TRUE with respect to deadlocks?

**Options:**

A. Circular wait is a necessary condition for the formation of deadlock.
B. In a system where each resource has more than one instance, a cycle in its wait-for graph indicates the presence of a deadlock.
C. If the current allocation of resources to processes leads the system to unsafe state, then deadlock will necessarily occur.
D. In the resource-allocation graph of a system, if every edge is an assignment edge, then the system is not in deadlock state.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.43

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider a computer system with multiple shared resource types, with one instance
per resource type. Each instance can be owned by only one process at a time.
Owning and freeing of resources are done by holding a global lock (L). The following
scheme is used to own a resource instance :
function OWNRESOURCE(Resource R)
Acquire lock L // a global lock
if R is available then
Acquire R
Release lock L
else
if R is owned by another process P then
Terminate P, after releasing all resources owned by P
Acquire R
Restart P
Release lock L
end if
end if
end function
Which of the following choice(s) about the above scheme is/are correct?

**Options:**

A. | The scheme ensures that deadlocks will not occur.
B. The scheme may lead to live-lock.
C. The scheme may lead to starvation.
D. | The scheme violates the mutual exclusion property. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2018

### Q.24

**Paper:** GATE 2018 CS

**Question:**

Consider a system with 3 processes that share 4 instances of the same resource type. Each
process can request a maximum of  𝐾 instances. Resource instances can be requested and
released only one at a time. The largest value of 𝐾 that will always avoid deadlock is ____.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

### Q.39

**Paper:** GATE 2018 CS

**Question:**

In a system, there are three types of resources: E, F and G. Four processes P_{0}, P_{1}, P_{2} and P_{3}
execute concurrently. At the outset, the processes have declared their maximum resource
requirements using a matrix named Max as given below. For example, Max[P_{2},F] is the
maximum number of instances of F that P_{2} would require. The number of instances of the
resources allocated to the various processes at any given state is given by a matrix named
Allocation.
Consider a state of the system with the Allocation matrix as shown below, and in which 3
instances of E and 3 instances of F are the only resources available.
Allocation  Max
E F G  E  F G
P_{0} 1 0  1  P_{0} 4  3  1
P_{1}  1 1  2  P_{1}  2  1  4
P_{2}  1 0  3  P_{2}  1  3  3
P_{3}  2 0  0  P_{3}  5  4  1
From the perspective of deadlock avoidance, which one of the following is true?

**Options:**

A. The system is in safe state.
B. The system is not in safe state, but would be safe if one more instance of E were available
C. The system is not in safe state, but would be safe if one more instance of F were available
D. The system is not in safe state, but would be safe if one more instance of G were available

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.33

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong: -0.66
A system shares 9 tape drives. The current allocation and maximum requirement of tape drives for
three processes are shown below:
Process Current Allocation Maximum Requirement
P1 3 7
P2 1 6
P3 3 5
Which of the following best describes current state of the system?

**Options:**

A. Safe, Deadlocked
B. Safe, Not Deadlocked
C. Not Safe, Deadlocked
D. Not Safe, Not Deadlocked

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.22

**Paper:** GATE 2016 CS-1

**Question:**

Which one of the following is NOT a part of the ACID properties of database transactions?

**Options:**

A. Atomicity
B. Consistency
C. Isolation
D. Deadlock-freedom CS(Set A) 7/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2016 CS-1

**Question:**

Consider the following proposed solution for the critical section problem. There are n
processes: P_{0} ... P_{n}−1. In the code, function pmax returns an integer not smaller than any
of its arguments. For all i, t[i] is initialized to zero.
Code for P_{i}:
do {
c[i]=1; t[i] = pmax(t[0],...,t[n-1])+1; c[i]=0;
for every j̸ = i in {0,...,n-1} {
while (c[j]);
while (t[j] != 0 && t[j]<=t[i]);
}
Critical Section;
t[i]=0;
Remainder Section;
} while (true);
Which one of the following is TRUE about the above solution?

**Options:**

A. At most one process can be in the critical section at any time
B. The bounded wait condition is satisfied
C. The progress condition is satisfied
D. It cannot cause a deadlock

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.51

**Paper:** GATE 2016 CS-1

**Question:**

Consider the following two phase locking protocol. Suppose a transaction T accesses (for
read or write operations), a certain set of objects {O_{1},..., O_{k}}. This is done in the following
manner:
Step 1. T acquires exclusive locks to O_{1}, ..., O_{k} in increasing order of their addresses.
Step 2. The required operations are performed.
Step 3. All locks are released.
This protocol will

**Options:**

A. guarantee serializability and deadlock-freedom
B. guarantee neither serializability nor deadlock-freedom
C. guarantee serializability but not deadlock-freedom
D. guarantee deadlock-freedom but not serializability CS(Set A) 16/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.30

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

A system has 6 identical resources and N processes competing for them. Each process can request
atmost 2 resources. Which one of the following values of N could lead to a deadlock?

**Options:**

A. 1
B. 2
C. 3
D. 4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Two processes X and Y need to access a critical section. Consider the following synchronization
construct used by both the processes
Process X Process Y
/* other code for process X */ /* other code for process Y */
while (true) while(true)
varP = true; varQ = true;
while (varl == true) while(varP == true)
/* Critical Section */ /* Critical Section */
varP = false; varQ = false;
/* other code for process X */ /* other code for process Y */
Here, varP and varQ are shared variables and both are initialized to false. Which one of the
following statements is true?

**Options:**

A. The proposed solution prevents deadlock but fails to guarantee mutual exclusion
B. The proposed solution guarantees mutual exclusion but fails to prevent deadlock
C. The proposed solution guarantees mutual exclusion and prevents deadlock
D. The proposed solution fails to prevent deadlock and fails to guarantee mutual exclusion B 3. 32 C 4. D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.45

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following policies for preventing deadlock in a system with mutually exclusive
resources.
I. Processes should acquire all their resources at the beginning of execution. If any resource is
not available, all resources acquired so far are released
II. The resources are numbered uniquely, and processes are allowed to request for resources
only in increasing resource numbers
III. The resources are numbered uniquely, and processes are allowed to request for resources
only in decreasing resource numbers
IV. The resources are numbered uniquely. A process is allowed to request only for a resource
with resource number larger than its currently held resources
Which of the above policies can be used for preventing deadlock?

**Options:**

A. Any one of I and III but not II or IV
B. Any one of I, II, and IV but not II
C. Any one of II and III but not I or IV
D. Any one of I, II, II, and IV 2 B 3. 4. VD

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.31

**Paper:** GATE 2014 CS SET-1

**Question:**

An operating system uses the  Banker’s algorithm for deadlock avoidance when managing the
allocation of three resource types X, Y, and Z to three processes P0, P1, and P2. The table given
below presents the current system state. Here, the Allocation matrix shows the current number of
resources of each type allocated to each process and the Max matrix shows the maximum number
of resources of each type required by each process during its execution.
Allocation  Max
CS01 (GATE 2014)  X  Y  Z  X  Y  Z
P0  0  0  1  8  4  3
P1  3  2  0  6  2  0
P2  2  1  1  3  3  3
There are 3 units of type X, 2 units of type Y and 2 units of type Z still available. The system is
currently in a safe state. Consider the following independent requests for additional resources in the
current state:
REQ1: P0 requests 0 units of  X, 0 units of  Y and 2 units of  Z
REQ2: P1 requests 2 units of  X, 0 units of  Y and 0 units of  Z
Which one of the following is TRUE?

**Options:**

A. Only REQ1 can be permitted.
B. Only REQ2 can be permitted.
C. Both REQ1 and REQ2 can be permitted.
D. Neither REQ1 nor REQ2 can be permitted.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2014 CS SET-2

**Question:**

Consider the procedure below for the Producer-Consumer problem which uses semaphores:
semaphore n = 0;
semaphore s = 1;
void producer()  void consumer()
{  {
while(true)  while(true)
{  {
produce();  semWait(s);
semWait(s);  semWait(n);
addToBuffer();  removeFromBuffer();
semSignal(s);  semSignal(s);
semSignal(n);  consume();
}  }
}  }
Which one of the following is TRUE?

**Options:**

A. The producer will be able to add an item to the buffer, but the consumer can never consume it.
B. The consumer will remove no more than one item from the buffer.
C. Deadlock occurs if the consumer succeeds in acquiring semaphore s when the buffer is empty.
D. The starting value for the semaphore n must be 1 and not 0 for deadlock-free operation.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.31

**Paper:** GATE 2014 CS SET-3

**Question:**

A system contains three programs and each requires three tape units for its operation. The
minimum number of tape units which the system must have such that deadlocks never arise
is _________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.16

**Paper:** GATE 2013 CS Booklet A

**Question:**

Three concurrent processes  X,  Y, and  Z execute three different code segments that access and
update certain shared variables. Process  X executes the  P  operation (i.e.,  wait) on semaphores
a, b and c; process Y executes the P operation on semaphores b, c and d; process Z executes the
P operation on semaphores  c,  d, and  a  before entering the respective code segments. After
completing the execution of its code segment, each process invokes the V operation (i.e., signal) on
its three semaphores. All semaphores are binary semaphores initialized to one. Which one of the
following represents a deadlock-free order of invoking the P operations by the processes?

**Options:**

A. X: P(a)P(b)P(c) Y: P(b)P(c)P(d) Z: P(c)P(d)P(a)
B. X: P(b)P(a)P(c) Y: P(b)P(c)P(d) Z: P(a)P(c)P(d)
C. X: P(b)P(a)P(c) Y: P(c)P(b)P(d) Z: P(a)P(c)P(d)
D. X: P(a)P(b)P(c) Y: P(c)P(b)P(d) Z: P(c)P(d)P(a)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.10

**Paper:** GATE 2013 CS Booklet B

**Question:**

Three concurrent processes  X,  Y, and  Z execute three different code segments that access and
update certain shared variables. Process  X executes the  P  operation (i.e.,  wait) on semaphores
a, b and c; process Y executes the P operation on semaphores b, c and d; process Z executes the
P operation on semaphores  c,  d, and  a  before entering the respective code segments. After
completing the execution of its code segment, each process invokes the V operation (i.e., signal) on
its three semaphores. All semaphores are binary semaphores initialized to one. Which one of the
following represents a deadlock-free order of invoking the P operations by the processes?

**Options:**

A. X: P(a)P(b)P(c) Y: P(b)P(c)P(d) Z: P(c)P(d)P(a)
B. X: P(b)P(a)P(c) Y: P(b)P(c)P(d) Z: P(a)P(c)P(d)
C. X: P(b)P(a)P(c) Y: P(c)P(b)P(d) Z: P(a)P(c)P(d)
D. X: P(a)P(b)P(c) Y: P(c)P(b)P(d) Z: P(c)P(d)P(a)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2013 CS Booklet C

**Question:**

Three concurrent processes  X,  Y, and  Z execute three different code segments that access and
update certain shared variables. Process  X executes the  P  operation (i.e.,  wait) on semaphores
a, b and c; process Y executes the P operation on semaphores b, c and d; process Z executes the
P operation on semaphores  c,  d, and  a  before entering the respective code segments. After
completing the execution of its code segment, each process invokes the V operation (i.e., signal) on
its three semaphores. All semaphores are binary semaphores initialized to one. Which one of the
following represents a deadlock-free order of invoking the P operations by the processes?

**Options:**

A. X: P(a)P(b)P(c) Y: P(b)P(c)P(d) Z: P(c)P(d)P(a)
B. X: P(b)P(a)P(c) Y: P(b)P(c)P(d) Z: P(a)P(c)P(d)
C. X: P(b)P(a)P(c) Y: P(c)P(b)P(d) Z: P(a)P(c)P(d)
D. X: P(a)P(b)P(c) Y: P(c)P(b)P(d) Z: P(c)P(d)P(a)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.4

**Paper:** GATE 2013 CS Booklet D

**Question:**

Three concurrent processes  X,  Y, and  Z execute three different code segments that access and
update certain shared variables. Process  X executes the  P  operation (i.e.,  wait) on semaphores
a, b and c; process Y executes the P operation on semaphores b, c and d; process Z executes the
P operation on semaphores  c,  d, and  a  before entering the respective code segments. After
completing the execution of its code segment, each process invokes the V operation (i.e., signal) on
its three semaphores. All semaphores are binary semaphores initialized to one. Which one of the
following represents a deadlock-free order of invoking the P operations by the processes?

**Options:**

A. X: P(a)P(b)P(c) Y: P(b)P(c)P(d) Z: P(c)P(d)P(a)
B. X: P(b)P(a)P(c) Y: P(b)P(c)P(d) Z: P(a)P(c)P(d)
C. X: P(b)P(a)P(c) Y: P(c)P(b)P(d) Z: P(a)P(c)P(d)
D. X: P(a)P(b)P(c) Y: P(c)P(b)P(d) Z: P(c)P(d)P(a)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2010

### Q.20

**Paper:** GATE 2010 CS

**Question:**

Which of the following concurrency contral prorocols ensure both conflict serializabilicy and
freedom from deadlock?
1. 2-phase locking
I. Tine-Stamp ordering

**Options:**

A. 1only
B. Il only
C. Both I and Il
D. Neither i nor Il

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2010 CS

**Question:**

A system has n resources Ra.Ru.s. and k processes Pa...Pt.. The implementation of the resource
request logic of each process P;, is as follows:
if (i$2==0; 1
if (i<n) request Ri i
if (i+2 < n) request Ri.zi
}
else (
1f (i<n) request R.i:
if (i-2<n) request kr...i
}
In which one of the following situations is a deadlock possible?

**Options:**

A. и = 40, k = 26
B. п = 2l.A = 12 (C.) " = 20, k = 10
D. n=41,k= 19

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.30

**Paper:** GATE 2009 CS

**Question:**

2009
Consider a system with 4 types of resources R1 (3 units), R2 (2 units), R3 (3 units), R4 (2 units). A
non-preemptive resource allocation policy is used. At any given instance, a request is not entertained if
it cannot be completely satisfied. Three processes P1, P2, P3 request the resources as follows if
executed independently.
Process P1: Process P2: Process P3:
t = O: requests 2 units of R2 t = 0: requests 2 units of R3 t = O: requests 1 unit of R4
t = 1: requests 1 unit of R3 t = 2: requests 1 unit of R4 t = 2: requests 2 units of R1
t = 3: requests 2 units of R1 t = 4: requests 1 unit of R1 t = 5: releases 2 units of R1
t = 5: releases 1 unit of R2 and t = 6: releases 1 unit of R3 t =7: requests 1 unit of R2
1 unit of R1 t = 8: Finishes t = 8: requests 1 unit of R3
t = 7: releases 1 unit of R3 t = 9: Finishes
t = 8: requests 2 units of R4
t = 10: Finishes
Which one of the following statements is TRUE if all three processes run concurrently starting at time
t=0?

**Options:**

A. All processes will finish without any deadlock.
B. Only P1 and P2 will be in deadlock.
C. Only P1 and P3 will be in deadlock.
D. All three processes will be in deadlock.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2009 CS

**Question:**

The enter_CS () and leave_CS () functions to implement critical section of a process are realized
using test-and-set instruction as follows :
void enter_CS(X)
while (test-and-set (X));
}
void leave_CS(X)
x=0;
}
In the above solution, X is a memory location associated with the CS and is initialized to 0. Now
consider the following statements :
I. The above solution to CS problem is deadlock-free.
II. The solution is starvation free.
III. The processes enter CS in FIFO order.
IV. More than one process can enter CS at the same time.
Which of the above statements are TRUE ?

**Options:**

A. Ionly
B. I and II
C. II and III
D. IV only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.65

**Paper:** GATE 2008 CS

**Question:**

Which of the following is NOT true of deadlock prevention and deadlock avoidance schemes?

**Options:**

A. In deadlock prevention, the request for resources is always granted if the resulting state is safe
B. In deadlock avoidance, the request for resources is always granted if the resulting state is safe
C. Deadlock avoidance is less restrictive than deadlock prevention
D. Deadlock avoidance requires knowledge of resource requirements a priori

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.57

**Paper:** GATE 2007 CS

**Question:**

A single processor system has three resource types X, Y, and Z, which are shared by
three processes. There are 5 units of each resource type. Consider the following
scenario, where the column alloc denotes the number of units of each resource type
allocated to each process, and the column request denotes the number of units of each
resource type requested by a process in order to complete execution. Which of these
processes will finish LAST?
alloc request
XYZ XYZ
PO 121 103
P1 201 012
P2 221 120

**Options:**

A. PO
B. PI
C. P2e of the above, since the system is in a deadlock.
D. None of the above, since the system is in a deadlock.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2007 CS

**Question:**

Two processes, P1 and P2, need to access a critical section of code. Consider the
following synchronization construct used by the processes:
/* P1 */ /* P2 */
while (true) | while (true) (
wantsl = true; wants2 = true;
while (wants2==true); while (wantsl==true);
/* Critical /* Critical
Section */ Section */
wants1=false; wants2=false;
}
/* Remainder section */ /* Remainder section */
Here, wants1 and wants2 are shared variables, which are initialized to false.
Which one of the following statements is TRUE about the above construct?

**Options:**

A. It does not ensure mutual exclusion.
B. It does not ensure bounded waiting.
C. It requires that processes enter the critical section in strict alternation.
D. It does not prevent deadlocks, but ensures mutual exclusion. CS - 14/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

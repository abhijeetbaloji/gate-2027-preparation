# GATE PYQs

## 2024

### Q.45

**Paper:** GATE 2024 CS2

**Question:**

The relation schema,  Person(pid,city), describes the city of residence for
every person uniquely identified by pid. The following relational algebra operators
are available: selection, projection, cross product, and rename.
To find the list of cities where at least 3 persons reside, using the above operators,
the minimum number of cross product operations that must be used is

**Options:**

A. 1
B. 2
C. 3
D. 4 Consider a multi-threaded program with two threads T1 and T2. The threads share

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2021

### Q.14

**Paper:** GATE 2021 CS Set-1

**Question:**

Which of the following standard C library functions will always invoke a system call
when executed from a single-threaded process in a UNIX/Linux operating system?

**Options:**

A. exit
B. malloc
C. I sleep
D. strlen GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following multi-threaded code segment (in a mix of C and pseudo-
code), invoked by two processes P1 and P2, and each of the processes spawns two
threads T1 and T2:
int x = 0; // global
Lock L1; // global
main() {
create a thread to execute foo(); // Thread T1
create a thread to execute foo(); // Thread T2
wait for the two threads to finish execution;
print (x) ;}
foo() {
int y = 0;
Acquire L1;
x = x + 1;
у = y + 1;
Release L1;
print (y) ;}
Which of the following statement(s) is/are correct?

**Options:**

A. Both P1 and P2 will print the value of x as 2.
B. At least one of P1 and P2 will print the value of x as 4.
C. At least one of the threads will print the value of y as 2.
D. Both T1 and 'T2, in both the processes, will print the value of y as 1. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2014

### Q.20

**Paper:** GATE 2014 CS SET-1

**Question:**

Which one of the following is FALSE?
CS01 (GATE 2014)

**Options:**

A. User level threads are not scheduled by the kernel.
B. When a user level thread is blocked, all other threads of its process are blocked.
C. Context switching between user level threads is faster than context switching between kernel level threads.
D. Kernel level threads cannot share the code segment.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

## 2011

### Q.16

**Paper:** GATE 2011 CS Booklet A

**Question:**

A thread is usually defined as a "light weight process" because an operating system (OS) maintains
smaller data structures for a thread than for a process. In relation to this, which of the following is TRUE?
(A) On per-thread basis, the OS maintains only CPU register state
CS-A 4/20
2011 CS

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2007

### Q.17

**Paper:** GATE 2007 CS

**Question:**

Consider the following statements about user level threads and kernel level threads.
Which one of the following statements is FALSE?

**Options:**

A. Context switch time is longer for kernel level threads than for user level threads.
B. User level threads do not need any hardware support.
C. Related kernel level threads can be scheduled on different processors in a multi-
D. Blocking one kernel level thread blocks all related threads. processor system.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

# GATE PYQs

## 2026

### Q.64

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider a CPU that has to execute two types of processes. The first type,
Actuators (A), requires a CPU burst of 6 seconds. The second type, Controllers (C),
requires a CPU burst of 8 seconds. A new process of type A arrives at time 𝑡 = 10,
20, 30, 40, and 50 (in seconds). Similarly, a new process of type C arrives at time 𝑡 =
11, 22, 33, 44, and 55 (in seconds). The CPU scheduling policy is First Come First
Serve (FCFS). The first process of type A starts running at  𝑡 = 10 seconds. The
average waiting time (in seconds) for the 10 processes is ___________. (rounded off
to one decimal place)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.23

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Which one of the following CPU scheduling algorithms cannot be preemptive?

**Options:**

A. Shortest Remaining Time First (SRTF) Scheduling
B. First Come First Serve (FCFS) Scheduling
C. Round Robin Scheduling
D. Priority Scheduling

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.38

**Paper:** GATE 2025 CS-1

**Question:**

A computer has two processors, 𝑀_{1} and 𝑀_{2}. Four processes 𝑃_{1}, 𝑃_{2}, 𝑃_{3}, 𝑃_{4} with CPU
bursts of 20, 16, 25, and 10 milliseconds, respectively, arrive at the same time and
these are the only processes in the system. The scheduler uses non-preemptive
priority scheduling, with priorities decided as follows:
•  𝑀_{1} uses priority of execution for the processes as, 𝑃_{1} > 𝑃_{3} > 𝑃_{2} > 𝑃_{4}, i.e.,
𝑃_{1} and 𝑃_{4} have highest and lowest priorities, respectively.
•  𝑀_{2} uses priority of execution for the processes as, 𝑃_{2} > 𝑃_{3} > 𝑃_{4} > 𝑃_{1}, i.e.,
𝑃_{2} and 𝑃_{1} have highest and lowest priorities, respectively.
A process 𝑃_{𝑖} is scheduled to a processor 𝑀_{𝑘}, if the processor is free and no other
process 𝑃_{𝑗} is waiting with higher priority.  At any given point of time, a process can
be allocated to any one of the free processors without violating the execution
priority rules. Ignore the context switch time. What will be the average waiting time
of the processes in milliseconds?

**Options:**

A. 9.00
B. 8.75
C. 6.50
D. 7.50

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.26

**Paper:** GATE 2025 CS-2

**Question:**

Processes 𝑃1, 𝑃2, 𝑃3, 𝑃4 arrive in that order at times 0, 1, 2, and 8 milliseconds
respectively, and have execution times of 10, 13, 6, and 9 milliseconds respectively.
Shortest Remaining Time First (SRTF) algorithm is used as the CPU scheduling
policy. Ignore context switching times.
Which ONE of the following correctly gives the average turnaround time of the four
processes in milliseconds?

**Options:**

A. 22
B. 15
C. 37
D. 19

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.37

**Paper:** GATE 2024 CS2

**Question:**

Consider a single processor system with four processes A, B, C, and D, represented
as given below, where for each process the first value is its arrival time, and the
second value is its CPU burst time.
A (0, 10), B (2, 6), C (4, 3), and D (6, 7).
Which one of the following options gives the average waiting times when
preemptive Shortest Remaining Time First (SRTF) and Non-Preemptive Shortest
Job First (NP-SJF) CPU scheduling algorithms are applied to the processes?

**Options:**

A. SRTF = 6, NP-SJF = 7
B. SRTF = 6, NP-SJF = 7.5
C. SRTF = 7, NP-SJF = 7.5
D. SRTF = 7, NP-SJF = 8.5 Which one of the following CIDR prefixes exactly represents the range of

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2024 CS2

**Question:**

Consider a disk with the following specifications: rotation speed of 6000 RPM,
average seek time of 5 milliseconds, 500 sectors/track, 512-byte sectors.
A file has content stored in 3000 sectors located randomly on the disk. Assuming
average rotational latency, the total time (in seconds, rounded off to 2 decimal
places) to read the entire file from the disk is _________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.27

**Paper:** GATE 2023 CS

**Question:**

Which one or more of the following CPU scheduling algorithms can potentially
cause starvation?

**Options:**

A. First-in First-Out
B. Round Robin
C. Priority Scheduling
D. Shortest Job First

**Type:** MSQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.42

**Paper:** GATE 2022 CS

**Question:**

Consider four processes P, Q, R, and S scheduled on a CPU as per round robin
algorithm with a time quantum of 4 units. The processes arrive in the order P, Q, R,
S, all at time t = 0. There is exactly one context switch from S to Q, exactly one
context switch from R to Q, and exactly two context switches from Q to R. There is
no context switch from S to P. Switching to a ready process after the termination of
another process is also considered a context switch. Which one of the following is
NOT possible as CPU burst time (in time units) of these processes?

**Options:**

A. P = 4, Q = 10, R = 6, S = 2
B. P = 2, Q = 9, R = 5, S = 1
C. P = 4, Q = 12, R = 5, S = 4
D. P = 3, Q = 7, R = 7, S = 3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.14

**Paper:** GATE 2021 CS Set-2

**Question:**

Which of the following statement (s) is/are correct in the context of CPU scheduling?

**Options:**

A. Turnaround time includes waiting time.
B. The goal is to only maximize CPU utilization and minimize throughput.
C. Round-robin policy can be used even when the CPU time required by each of the processes is not known apriori.
D. Implementing preemptive scheduling needs hardware support. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.12

**Paper:** GATE 2020 CS

**Question:**

Consider the following statements about process state transitions for a system
using preemptive scheduling.
I. A running process can move to ready state.
II. A ready process can move to running state.
III. A blocked process can move to running state.
IV. A blocked process can move to ready state.
Which of the above statements are TRUE?

**Options:**

A. 1, II, and Ill only
B. Il and IIl only
C. 1, Il, and IV only
D. 1, II, III, and IV

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

### Q.50

**Paper:** GATE 2020 CS

**Question:**

Consider the following setof processes,assumed tohave arrived at time 0.
Consider the CPU scheduling algorithms Shortest Job First (SJF) and Round
Robin (RR). For RR, assume that the processes are scheduled in the order
P,, P2, P3, P,.
Processes
Burst time (in ms)
If the time quantum for RR is 4 ms, then the absolute value of the difference
between the average turnaround times (in ms) of SJF and RR (round off to 2
decimal places) is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.41

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following four processes with arrival times (in milliseconds) and their length
of CPU bursts (in milliseconds) as shown below:
Process P2 P3 P4
Arrival time 1 4
CPU burst time 1 Z
These processes are run on a single processor using preemptive Shortest Remaining Time
First scheduling algorithm. If the average waiting time of the processes is 1 millisecond,
then the value of Z is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.53

**Paper:** GATE 2018 CS

**Question:**

Consider a storage disk with 4 platters (numbered as 0, 1, 2 and 3), 200 cylinders (numbered
as 0, 1, … , 199), and 256 sectors per track (numbered as 0, 1, … , 255). The following 6
disk requests of the form [sector number, cylinder number, platter number] are received by
the disk controller at the same time:
[120, 72, 2] , [180, 134, 1] , [60, 20, 0] , [212, 86, 3] , [56, 116, 2] , [118, 16, 1]
Currently the head is positioned at sector number 100 of cylinder 80, and is moving towards
higher cylinder numbers. The average power dissipation in moving the head over 100
cylinders is 20 milliwatts and for reversing the direction of the head movement once is 15
milliwatts. Power dissipation associated with rotational latency and switching of head
between different platters is negligible.
The total power consumption in milliwatts to satisfy all of the above disk requests using the
Shortest Seek Time First disk scheduling algorithm is _______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.51

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong: 0
Consider the set of processes with arrival time (in milliseconds), CPU burst time (in milliseconds),
and priority (0 is the highest priority) shown below. None of the processes have I/O burst time.
Process Arrival Time Burst Time Priority
0 11 2
5 28 0
P3 12 2 3
PA 2 10 1
9 16 4
The average waiting time (in milliseconds) of all the processes using preemptive priority
scheduling algorithm is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.20

**Paper:** GATE 2016 CS-1

**Question:**

Consider an arbitrary set of CPU-bound processes with unequal CPU burst lengths
submitted at the same time to a computer system. Which one of the following process
scheduling algorithms would minimize the average waiting time in the ready queue?

**Options:**

A. Shortest remaining time first
B. Round-robin with time quantum less than the shortest CPU burst
C. Uniform random
D. Highest priority first with priority proportional to CPU burst length

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following processes, with the arrival time and the length of the CPU burst given
in milliseconds. The scheduling algorithm used is preemptive shortest remaining-time first.
Process Arrival Time Burst Time
P_{1}  0  10
P_{2}  3  6
P_{3}  7  1
P_{4}  8  3
The average turn around time of these processes is  milliseconds.
CS(Set B)  14/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.54

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Ouestion Type : NAT
Consider a disk pack with a seek time of 4 milliseconds and rotational speed of 10000 rotations per
minute (RPM). It has 600 sectors per track and each sector can store 512 bytes of data. Consider a
file stored in the disk. The file contains 2000 sectors. Assume that every sector access necessitates a
seek, and the average rotational latency for accessing each sector is half of the time for one
complete rotation. The total time (in milliseconds) needed to read the entire file is
Correct Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.56

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

3.2

Suppose the following disk request sequence (track numbers) for a disk with 100 tracks is given:
45, 20, 90, 10, 50, 60, 80, 25, 70. Assume that the initial position of the R/W head is on track 50.
The additional distance that will be traversed by the R/W head when the Shortest Seek Time First
(SSTF) algorithm is used compared to the SCAN (Elevator) algorithm (assuming that SCAN
algorithm moves towards 100 when it starts execution) is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Consider a typical disk that rotates at 15000 rotations per minute (RPM) and has a transfer rate of
50x10° bytes/sec. If the average seek time of the disk is twice the average rotational delay and the
controller's transfer time is 10 times the disk transfer time, the average time (in milliseconds) to
read or write a 512-byte sector of the disk is
Correct Answer :
6.1 to 6.2

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.57

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

1575

For the processes listed in the following table, which of the following scheduling schemes will give
the lowest average turnaround time?
Process Arrival Time Processing Time
A 0
1
4
D 6

**Options:**

A. First Come First Serve
B. Non-preemptive Shortest Job First
C. Shortest Remaining Time
D. Round Robin with Quantum value two 4 K D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.32

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider the following set of processes that need to be scheduled on a single CPU. All the times are
given in milliseconds.
Process Name  Arrival Time  Execution Time
A  0  6
B  3  2
C  5  4
D  7  6
E  10  3
Using the shortest remaining time first scheduling algorithm, the average process turnaround time
(in msec) is ____________________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2014 CS SET-2

**Question:**

Three processes A, B and C each execute a loop of 100 iterations. In each iteration of the loop, a
process performs a single computation that requires t_{c} CPU milliseconds and then initiates a single
I/O operation that lasts for  t_{i}o milliseconds. It is assumed that the computer where the processes
execute has sufficient number of I/O devices and the OS of the computer assigns different I/O
devices to each process. Also, the scheduling overhead of the OS is negligible. The processes have
the following characteristics:
Process id  t_{c}  t_{io}
A  100 ms  500 ms
CS02 (GATE 2014)^{B}  350 ms  500 ms
C  200 ms  500 ms
The processes A, B, and C are started at times 0, 5 and 10 milliseconds respectively, in a pure time
sharing system (round robin scheduling) that uses a time slice of 50 milliseconds. The time in
milliseconds at which process C would complete its first I/O operation is ___________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2014 CS SET-3

**Question:**

An operating system uses  shortest remaining time first scheduling algorithm for pre-emptive
scheduling of processes. Consider the following set of processes with their arrival times and CPU
CS03 (GATE 2014)burst times (in milliseconds):
Process  Arrival Time  Burst Time
P1  0  12
P2  2  4
P3  3  6
P4  8  5
The average waiting time (in milliseconds) of the processes is _________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

## 2013

### Q.10

**Paper:** GATE 2013 CS Booklet A

**Question:**

A scheduling algorithm assigns priority proportional to the waiting time of a process. Every process
starts with priority zero (the lowest priority). The scheduler re-evaluates the process priorities every
T time units and decides the next process to schedule. Which one of the following is TRUE if the
processes have no I/O operations and all arrive at time zero?

**Options:**

A. This algorithm is equivalent to the first-come-first-serve algorithm.
B. This algorithm is equivalent to the round-robin algorithm.
C. This algorithm is equivalent to the shortest-job-first algorithm.
D. This algorithm is equivalent to the shortest-remaining-time-first algorithm.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.16

**Paper:** GATE 2013 CS Booklet B

**Question:**

A scheduling algorithm assigns priority proportional to the waiting time of a process. Every process
starts with priority zero (the lowest priority). The scheduler re-evaluates the process priorities every
T time units and decides the next process to schedule. Which one of the following is TRUE if the
processes have no I/O operations and all arrive at time zero?

**Options:**

A. This algorithm is equivalent to the first-come-first-serve algorithm.
B. This algorithm is equivalent to the round-robin algorithm.
C. This algorithm is equivalent to the shortest-job-first algorithm.
D. This algorithm is equivalent to the shortest-remaining-time-first algorithm.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.3

**Paper:** GATE 2013 CS Booklet C

**Question:**

A scheduling algorithm assigns priority proportional to the waiting time of a process. Every process
starts with priority zero (the lowest priority). The scheduler re-evaluates the process priorities every
T time units and decides the next process to schedule. Which one of the following is TRUE if the
processes have no I/O operations and all arrive at time zero?

**Options:**

A. This algorithm is equivalent to the first-come-first-serve algorithm.
B. This algorithm is equivalent to the round-robin algorithm.
C. This algorithm is equivalent to the shortest-job-first algorithm.
D. This algorithm is equivalent to the shortest-remaining-time-first algorithm.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.23

**Paper:** GATE 2013 CS Booklet D

**Question:**

A scheduling algorithm assigns priority proportional to the waiting time of a process. Every process
starts with priority zero (the lowest priority). The scheduler re-evaluates the process priorities every
T time units and decides the next process to schedule. Which one of the following is TRUE if the
processes have no I/O operations and all arrive at time zero?

**Options:**

A. This algorithm is equivalent to the first-come-first-serve algorithm.
B. This algorithm is equivalent to the round-robin algorithm.
C. This algorithm is equivalent to the shortest-job-first algorithm.
D. This algorithm is equivalent to the shortest-remaining-time-first algorithm.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.31

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the 3 processes, P1, P2 and P3 shown in the table.
Process  Arrival  Time Units
time  Required
P1  0  5
P2  1  7
P3  3  4
The completion order of the 3 processes under the policies FCFS and RR2 (round robin scheduling
with CPU quantum of 2 time units) are

**Options:**

A. FCFS: P1, P2, P3 RR2: P1, P2, P3
B. FCFS: P1, P3, P2 RR2: P1, P3, P2
C. FCFS: P1, P2, P3 RR2: P1, P3, P2
D. FCFS: P1, P3, P2 RR2: P1, P2, P3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.44

**Paper:** GATE 2011 CS Booklet A

**Question:**

An application loads 100 libraries at startup. Loading each library requires exactly one disk access.
The seek time of the disk to a random location is given as 10 ms. Rotational speed of disk is
6000 гpm. If all 100 libraries are loaded from random locations on the disk, how long does it take to
load all libraries? (The time to transfer data from the disk block once the head has been positioned
at the start of the block may be neglected.)

**Options:**

A. 0.50 s
B. 1.50 s
C. 1.25 s
D. 1.00 s CS-A 11/20

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2010

### Q.25

**Paper:** GATE 2010 CS

**Question:**

2010
Which of the following statements are true?
1. Shortest remaining time first scheduling inay cause starvation
II. Preemptive scheduling may cause starvation III. Round robin is belter than FCFS in terms of response time

**Options:**

A. pq+(1-p)(1-9)
B. (1-g)p
C. (1-P)4
D. p4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2010 CS, `12-PYQ/2010/question-paper.pdf`

---

## 2009

### Q.31

**Paper:** GATE 2009 CS

**Question:**

Consider a disk system with 100 cylinders. The requests to access the cylinders occur in following
sequence :
4, 34, 10, 7, 19, 73, 2, 15, 6, 20.
Assuming that the head is currently at cylinder 50, what is the time taken to satisfy all requests if it
takes 1 ms to move from one cylinder to adjacent one and shortest seek time first policy is used ?

**Options:**

A. 95 ms
B. 119 ms
C. 233 ms
D. 276 ms

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

### Q.32

**Paper:** GATE 2009 CS

**Question:**

In the following process state transition diagram for a uniprocessor system, assume that there are
always some processes in the ready state :
Start Ready Running D →(Terminated)
Blocked
Now consider the following statements :
I. If a process makes a transition D, it would result in another process making transition A
immediately.
II. A process P2 in blocked state can make transition E while another process P, is in running state.
III. The OS uses preemptive scheduling.
IV. The OS uses non-preemptive scheduling.
Which of the above statements are TRUE ?

**Options:**

A. I and II
B. I and III
C. II and III
D. II and IV 2009 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.32

**Paper:** GATE 2008 CS

**Question:**

For a magnetic disk with concentric circular tracks, the seek latency is not linearly proportional to
the seek distance due to

**Options:**

A. non-uniform distribution of requests
B. arm starting and stopping inertia
C. higher capacity of tracks on the periphery of the platter
D. use of unfair arm scheduling policies

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.16

**Paper:** GATE 2007 CS

**Question:**

Group 1 contains some CPU scheduling algorithms and Group 2 contains some
applications. Match entries in Group 1 to entries in Group 2.
Group 1 Group 2
P. Gang Scheduling 1. Guaranteed Scheduling
Q. Rate Monotonic Scheduling 2. Real-time Scheduling
R. Fair Share Scheduling 3. Thread Scheduling

**Options:**

A. P-3; Q-2; R-1
B. P-1; Q-2; R-3
C. P-2; Q-3; R-1
D. P-1; Q-3; R-2

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2007 CS

**Question:**

An operating system uses Shortest Remaining Time first (SRT) process scheduling
algorithm. Consider the arrival times and execution times for the following processes:
Process Execution Arrival
time time
PI 20 0
P2 25 15
P3 10 30
P4 15 45
What is the total waiting time for process P2?

**Options:**

A. 5
B. 15
C. 40
D. 55 CS - 13/24

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

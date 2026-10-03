# CPU and I/O Scheduling — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Time is in milliseconds. Context-switch time is 0. A running process keeps the CPU until it finishes or the stated policy preempts it.

For the CPU questions that use set S, the processes are

| Process | Arrival | Burst |
|---|---|---|
| P1 | 0 | 7 |
| P2 | 2 | 4 |
| P3 | 3 | 1 |
| P4 | 9 | 2 |

Tie rules for set S: at equal arrival time, the smaller index is ahead in FCFS. Non-preemptive SJF chooses the shortest burst among processes that have arrived, breaking ties by the smaller index. SRTF always runs a ready process of strictly smallest remaining time. If remaining times are equal, the process that is already running continues; if the CPU is idle, the smaller index runs.

For disk questions, cylinders are numbered 0 through 199. The head starts at cylinder 40. The queue, in arrival order, is 15, 25, 50, 85, 120, 160. The head is initially moving toward higher cylinder numbers. SCAN and C-SCAN travel all the way to an end cylinder, and that travel counts. The C-SCAN jump from cylinder 199 to cylinder 0 counts. LOOK and C-LOOK turn around at the furthest request in the current direction and do not visit an empty end cylinder. C-LOOK then jumps to the lowest remaining request, and that jump counts.

## Level 1 — Conceptual

## Q1 — MCQ

The convoy effect is associated with

A. FCFS, when a long CPU burst delays many short bursts that arrived behind it
B. round robin with a quantum of one instruction, which forces a convoy by definition
C. SRTF, which always runs the longest remaining job first
D. a disk SCAN that reverses direction at every request

---

## Q2 — MSQ

**Select all that apply.**

Which policies can preempt a running process because of a scheduling decision (not because the process blocks itself)?

A. SRTF
B. Round robin with a finite quantum
C. Preemptive priority
D. Non-preemptive SJF

---

## Q3 — MCQ

If the round-robin quantum is larger than every CPU burst in the workload, round robin behaves like

A. SRTF
B. FCFS
C. non-preemptive SJF
D. shortest remaining time among processes that have not arrived yet

---

## Q4 — MSQ

**Select all that apply.**

Assume every burst is finite. Which policies can still postpone some process forever because later arrivals keep being preferred?

A. Non-preemptive SJF
B. Preemptive static priority, when higher-priority processes keep arriving
C. Round robin with a fixed positive quantum
D. FCFS

---

## Q5 — MCQ

An I/O-bound process, compared with a CPU-bound process, typically has

A. short CPU bursts separated by I/O waits
B. one long CPU burst and no I/O
C. a higher priority number in every scheduler, by definition of I/O
D. a burst that round robin is not allowed to preempt

---

## Level 2 — Standard GATE Style

## Q6 — NAT

Schedule set S with FCFS. The sum of the four waiting times is ____.

---

## Q7 — MCQ

Under FCFS on set S, the waiting time of P3 is

A. 0
B. 5
C. 8
D. 9

---

## Q8 — NAT

Schedule set S with non-preemptive SJF. The sum of the four waiting times is ____.

---

## Q9 — MSQ

**Select all that apply.**

Under SRTF on set S,

A. P3's waiting time is 0
B. P1 completes at time 14
C. P4's waiting time is 0
D. P2 runs from time 2 to time 6 without a break

---

## Q10 — MSQ

**Select all that apply.**

Under non-preemptive SJF on set S,

A. P3 runs before P2
B. the sum of the waiting times is 13
C. P4 runs before P3
D. P1's waiting time is 0

---

## Q11 — MCQ

Under SRTF on set S, the sum of the four turnaround times is

A. 8
B. 16
C. 22
D. 30

---

## Level 3 — Multi-Step

## Q12 — NAT

Three processes use round robin with quantum 4.

| Process | Arrival | Burst |
|---|---|---|
| P1 | 0 | 8 |
| P2 | 3 | 5 |
| P3 | 6 | 2 |

A process that arrives during another process's quantum joins the tail of the ready queue and does not preempt. When a quantum expires at the same instant a new process arrives, the new arrival is queued first and the preempted process is queued after it. (In this workload those two events do not coincide.) The sum of the three waiting times is ____.

---

## Q13 — MSQ

**Select all that apply.**

Smaller priority number means higher priority. The scheduler is preemptive: a new arrival with a strictly better priority preempts at once. On equal priority the running process continues.

| Process | Arrival | Burst | Priority |
|---|---|---|---|
| P1 | 0 | 8 | 2 |
| P2 | 1 | 4 | 1 |
| P3 | 3 | 3 | 3 |
| P4 | 5 | 2 | 0 |

A. P4 runs from time 5 to time 7
B. P2's waiting time is 0
C. P3's waiting time is 11
D. P1 runs continuously from time 0 to time 8

---

## Q14 — NAT

Using the disk rules and request queue at the top of this file, the SCAN head movement (number of cylinders traversed) is ____.

---

## Q15 — MCQ

Using the disk rules and request queue at the top of this file, the C-SCAN head movement is

A. 265
B. 275
C. 343
D. 383

---

## Q16 — MCQ

Using the disk rules and request queue at the top of this file, the SSTF head movement is

A. 170
B. 190
C. 265
D. 343

---

## Level 4 — Tricky / Trap-Based

## Q17 — MCQ

Use the round-robin workload and queue rules of Q12. The response time of P2 (time from arrival until P2 first receives the CPU) is

A. 1
B. 7
C. 12
D. 5

---

## Q18 — MCQ

Use the round-robin workload and queue rules of Q12. P2 arrives at time 3 while P1 is still inside its quantum. The waiting time of P2 is

A. 0
B. 1
C. 7
D. 12

---

## Q19 — MCQ

Use the processes and priority numbers of Q13, but the scheduler is non-preemptive. Once a process starts a burst, it runs that burst to completion. When the CPU becomes free, the waiting process with the best priority is chosen. P2's waiting time is

A. 0
B. 3
C. 9
D. 13

---

## Level 5 — Challenge

## Q20 — NAT

Using the disk rules and request queue at the top of this file, the C-LOOK head movement is ____.

---

## Q21 — MSQ

**Select all that apply.**

For the disk rules and request queue at the top of this file,

A. LOOK traverses 265 cylinders
B. C-LOOK traverses 275 cylinders
C. SSTF traverses fewer cylinders than FCFS on this queue order
D. SCAN serves cylinder 15 before cylinder 160

---

## Q22 — MCQ

Using the disk rules and request queue at the top of this file, FCFS (service in the given queue order) traverses

A. 170 cylinders
B. 190 cylinders
C. 265 cylinders
D. 383 cylinders

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | MCQ | B |
| 4 | MSQ | A, B |
| 5 | MCQ | A |
| 6 | NAT | 16 |
| 7 | MCQ | C |
| 8 | NAT | 13 |
| 9 | MSQ | A, B, C |
| 10 | MSQ | A, B, D |
| 11 | MCQ | C |
| 12 | NAT | 17 |
| 13 | MSQ | A, B, C |
| 14 | NAT | 343 |
| 15 | MCQ | D |
| 16 | MCQ | B |
| 17 | MCQ | A |
| 18 | MCQ | C |
| 19 | MCQ | C |
| 20 | NAT | 275 |
| 21 | MSQ | A, B |
| 22 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

Under FCFS a long burst that starts first holds the CPU while short jobs wait behind it. That backup is the convoy effect. SRTF prefers the shortest remaining time, not the longest. A huge round-robin quantum resembles FCFS; a tiny quantum does not create this convoy. Disk SCAN is an I/O arm policy, not this CPU convoy.

### Q2

Answer: A, B, C

SRTF preempts when a new arrival has a shorter remaining time. Round robin preempts when the quantum expires. Preemptive priority preempts when a better priority arrives. Non-preemptive SJF and FCFS let the running burst finish. A process that blocks for I/O leaves the CPU under every policy, but that is the process's own wait, not a preemptive scheduling decision.

### Q3

Answer: B

If no burst is long enough to exhaust the quantum, the running process leaves only when its burst ends, and the ready queue stays in arrival order. That is FCFS. It is not SJF or SRTF, because the burst length is never consulted.

### Q4

Answer: A, B

Non-preemptive SJF can keep selecting a newly arrived short job and never pick a long job that is already waiting. Preemptive static priority can keep preempting a low-priority process for newcomers of better priority. Round robin with a positive quantum and FCFS both give each finite burst a turn; a process is not skipped forever in favor of newcomers.

### Q5

Answer: A

An I/O-bound process spends most of its time waiting for a device and uses the CPU in short bursts. A CPU-bound process occupies the CPU for long stretches. Priority numbers and round-robin eligibility are scheduler parameters, not part of the definition of I/O-bound.

### Q6

Answer: 16

FCFS Gantt chart: P1 from 0 to 7, P2 from 7 to 11, P3 from 11 to 12, P4 from 12 to 14.

| Process | Completion | Turnaround | Waiting |
|---|---|---|---|
| P1 | 7 | 7 − 0 = 7 | 7 − 7 = 0 |
| P2 | 11 | 11 − 2 = 9 | 9 − 4 = 5 |
| P3 | 12 | 12 − 3 = 9 | 9 − 1 = 8 |
| P4 | 14 | 14 − 9 = 5 | 5 − 2 = 3 |

Sum of waiting times: \(0 + 5 + 8 + 3 = 16\).

### Q7

Answer: C

From the FCFS table, P3 arrives at 3, runs from 11 to 12, and has burst 1. Waiting time = \(12 - 3 - 1 = 8\). The 9 in the options is P3's turnaround, not its waiting time.

### Q8

Answer: 13

P1 is alone at time 0, so it runs from 0 to 7 even though shorter jobs arrive during that burst. At time 7 the ready bursts are P2 with 4 and P3 with 1. SJF runs P3 from 7 to 8, then P2 from 8 to 12. P4 arrives at 9 and runs from 12 to 14.

| Process | Completion | Turnaround | Waiting |
|---|---|---|---|
| P1 | 7 | 7 | 0 |
| P2 | 12 | 10 | 6 |
| P3 | 8 | 5 | 4 |
| P4 | 14 | 5 | 3 |

Sum of waiting times: \(0 + 6 + 4 + 3 = 13\).

### Q9

Answer: A, B, C

SRTF Gantt chart:

- 0–2: P1 (remaining 5 at time 2)
- 2–3: P2 (P2's 4 is shorter than P1's 5)
- 3–4: P3 (burst 1 preempts P2)
- 4–7: P2 finishes its remaining 3
- 7–9: P1
- 9–11: P4 (remaining 2 is shorter than P1's remaining 3)
- 11–14: P1 finishes

P3 runs from 3 to 4, so its waiting time is 0. P1 completes at 14. P4 runs from 9 to 11, so its waiting time is 0. P2 is preempted at time 3 and resumes at time 4, so it does not run unbroken from 2 to 6.

### Q10

Answer: A, B, D

The SJF chart in Q8 runs P1, then P3, then P2, then P4. P3 runs before P2, and P4 does not run before P3. The waiting-time sum is 13. P1 starts at its arrival, so its waiting time is 0.

### Q11

Answer: C

SRTF turnaround times from the chart in Q9:

- P1: \(14 - 0 = 14\)
- P2: \(7 - 2 = 5\)
- P3: \(4 - 3 = 1\)
- P4: \(11 - 9 = 2\)

Sum: \(14 + 5 + 1 + 2 = 22\). The sum of waiting times is 8, which is a different total. 16 is the FCFS waiting sum, and 30 is the FCFS turnaround sum.

### Q12

Answer: 17

- 0–4: P1 uses a quantum. Remaining burst of P1 is 4. P2 arrived at 3 and waited.
- 4–8: P2 uses a quantum. Remaining burst of P2 is 1. P3 arrived at 6 and waited. P1 is already at the tail.
- 8–12: P1 finishes its remaining 4.
- 12–14: P3 finishes its burst of 2.
- 14–15: P2 finishes its last 1 ms.

| Process | Completion | Turnaround | Waiting |
|---|---|---|---|
| P1 | 12 | 12 | 12 − 8 = 4 |
| P2 | 15 | 12 | 12 − 5 = 7 |
| P3 | 14 | 8 | 8 − 2 = 6 |

Sum of waiting times: \(4 + 7 + 6 = 17\).

### Q13

Answer: A, B, C

Preemptive chart:

- 0–1: P1
- 1–5: P2 (priority 1 preempts priority 2) and P2 finishes
- 5–7: P4 (priority 0 preempts) and P4 finishes
- 7–14: P1 finishes its remaining 7 ms
- 14–17: P3

P4 does run from 5 to 7. P2 runs from its arrival at 1 until 5, so its waiting time is 0. P3 arrives at 3 and first runs at 14, then runs its whole burst: waiting time = \(14 - 3 = 11\). Check: completion 17, turnaround \(17 - 3 = 14\), waiting \(14 - 3 = 11\). P1 is preempted at time 1, so it does not occupy 0–8 continuously.

### Q14

Answer: 343

SCAN moves upward first: 40 → 50 → 85 → 120 → 160 → 199, then downward 199 → 25 → 15.

\[
\begin{align*}
&(50-40) + (85-50) + (120-85) + (160-120) + (199-160) \\
&\quad + (199-25) + (25-15) \\
&= 10 + 35 + 35 + 40 + 39 + 174 + 10 \\
&= 343.
\end{align*}
\]

### Q15

Answer: D

C-SCAN uses the same upward sweep to 199, then jumps to 0, then moves upward through 15 and 25.

\[
\begin{align*}
&10 + 35 + 35 + 40 + 39 + (199-0) + (15-0) + (25-15) \\
&= 159 + 199 + 15 + 10 \\
&= 383.
\end{align*}
\]

265 is LOOK, 275 is C-LOOK, and 343 is SCAN.

### Q16

Answer: B

SSTF from 40: the nearest request is 50 (distance 10), not 25 (distance 15). From 50 the nearest is 25. Then 15, then 85, 120, and 160.

\[
|50-40| + |25-50| + |15-25| + |85-15| + |120-85| + |160-120|
= 10 + 25 + 10 + 70 + 35 + 40 = 190.
\]

170 is FCFS on this queue. 265 is LOOK. 343 is SCAN.

### Q17

Answer: A

P2 arrives at time 3. P1 keeps the CPU until the quantum ends at time 4, which is when P2 first runs. Response time = \(4 - 3 = 1\). Waiting time is 7 and turnaround is 12; those measure the whole life of the process, not the delay until first dispatch. 5 is P2's burst.

### Q18

Answer: C

From the chart in Q12, P2's turnaround is 12 and its burst is 5, so

\[
\text{waiting} = 12 - 5 = 7.
\]

P2 also waits from 8 to 14 after its first quantum (6 ms) plus the 1 ms before its first dispatch, which is the same 7. An arrival at time 3 does not preempt P1, so the waiting time is not 0. Response time 1 and turnaround 12 are the other two traps.

### Q19

Answer: C

P1 starts at 0 with priority 2 and, because the policy is non-preemptive, runs to completion at time 8 even though P2 (priority 1) arrived at time 1. At time 8 the waiting processes are P4 (priority 0), P2 (priority 1), and P3 (priority 3). P4 runs from 8 to 10. P2 then runs from 10 to 14.

\[
\text{waiting of P2} = 14 - 1 - 4 = 9.
\]

Under the preemptive policy of Q13 this waiting time would be 0. 13 is P2's turnaround (\(14 - 1\)), and 3 is P4's waiting time on this non-preemptive chart.

### Q20

Answer: 275

C-LOOK services the upward requests 50, 85, 120, 160, then jumps from 160 to the lowest remaining request 15, then continues to 25.

\[
\begin{align*}
&(50-40) + (85-50) + (120-85) + (160-120) \\
&\quad + |15-160| + (25-15) \\
&= 10 + 35 + 35 + 40 + 145 + 10 \\
&= 275.
\end{align*}
\]

### Q21

Answer: A, B

LOOK's upward sweep is the same 120 cylinders as the start of C-LOOK, then it reverses from 160 down through 25 to 15:

\[
120 + (160-25) + (25-15) = 120 + 135 + 10 = 265.
\]

C-LOOK is 275, from Q20. FCFS movement is

\[
|15-40| + |25-15| + |50-25| + |85-50| + |120-85| + |160-120|
= 25 + 10 + 25 + 35 + 35 + 40 = 170.
\]

SSTF is 190, which is more than 170, so SSTF is not the shorter trip on this particular order. SCAN goes upward through 160 before it comes back to 15, so 15 is not served first.

### Q22

Answer: A

The FCFS sum in Q21 is 170. 190 is SSTF, 265 is LOOK, and 383 is C-SCAN.

# Processes — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which item is not part of a process control block?

A. The process state
B. The CPU registers saved when the process is switched out
C. The source text of the program
D. Information about the process's open files

---

## Q2 — MSQ

**Select all that apply.**

Which process-state transitions are possible in the standard five-state model (new, ready, running, waiting, terminated)?

A. Ready → Running
B. Running → Ready
C. Waiting → Ready
D. Ready → Waiting

---

## Q3 — MCQ

A process is in the waiting state because a disk read it issued has not finished. The disk controller then completes that read. The usual next transition is

A. Waiting → Running
B. Waiting → Ready
C. Ready → Waiting
D. Running → Terminated

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A process calls `fork`, and the call succeeds. Before either process writes a byte or seeks, which statement is correct?

A. The child and the parent have the same pid
B. The child's duplicated descriptors and the parent's descriptors refer to the same open-file descriptions, so a shared file offset is updated by a read in either process
C. The child starts with an empty file-descriptor table
D. The child receives a copy of the parent's pid as the return value of `fork`

---

## Q5 — NAT

Every `fork` succeeds. A child receives 0 and leaves the loop. The parent receives a positive pid and continues the loop.

```c
for (int i = 0; i < 3; i++) {
    if (fork() == 0)
        break;
}
```

The total number of processes that exist after the loop, including the original process, is ____.

---

## Q6 — MCQ

A zombie process is

A. a process that has terminated, whose exit status has not yet been collected by its parent
B. a process that has no process control block
C. a runnable process that the scheduler has placed permanently at the tail of the ready queue
D. a kernel thread that never leaves kernel mode

---

## Q7 — NAT

Each process control block occupies 128 bytes. The ready queue stores an 8-byte pointer for every ready process and nothing for processes that are not ready. At one instant the system has 9 processes, of which 5 are ready. The number of bytes occupied by all 9 process control blocks plus the ready-queue pointers is ____.

---

## Level 3 — Multi-Step

## Q8 — MCQ

Process P executes the following. `fork` and `waitpid` succeed. The grandchild is still inside `sleep`. P1 has already exited, and P has collected P1's status.

```c
pid_t p1 = fork();
if (p1 == 0) {
    pid_t p2 = fork();
    if (p2 > 0)
        _exit(0);
    sleep(100);
    _exit(0);
} else {
    waitpid(p1, NULL, 0);
}
```

While the grandchild is inside `sleep`, that grandchild is

A. a zombie whose parent is still P
B. an orphan that has been reparented to the init process (or its modern equivalent), and it is not a zombie
C. still a child of P1, which is waiting to be reaped
D. terminated, with its process control block already discarded

---

## Q9 — NAT

The process table has 64 slots. Three slots are already occupied: init, a shell, and one user process that is running. That user process and the children it creates call `fork` until `fork` fails. No process exits. The number of successful `fork` calls in this burst is ____.

---

## Q10 — MSQ

**Select all that apply.**

On a context switch away from process P, which of the following are recorded with P's process control block (or in the kernel state the PCB points at)?

A. The program counter
B. The general-purpose registers
C. A byte-for-byte copy of all of physical memory, stored inside the PCB
D. The information needed to locate P's page tables

---

## Level 4 — Tricky / Trap-Based

## Q11 — MSQ

**Select all that apply.**

`fork` has just returned successfully. Neither process has written a data page yet. The system uses copy-on-write.

A. The two processes have different pids
B. A later write by the child to a shared data page can force a private copy of that page
C. The parent and the child already have independent file offsets for every descriptor that was open at the `fork`, even though neither has called `lseek`
D. In the child, `fork` returned 0

---

## Q12 — MCQ

```c
int x = 3;
if (fork() == 0) {
    x = x + 2;
    _exit(0);
}
wait(NULL);
```

After `wait` returns, the parent's `x` is

A. 3
B. 5
C. 2
D. undefined, because `x` lives in the PCB and both processes update that one cell

---

## Level 5 — Challenge

## Q13 — NAT

Every `fork` succeeds. In C, the `&&` operator does not evaluate its right operand when the left operand is 0.

```c
if (fork() && fork())
    fork();
```

The total number of processes after this statement, including the original, is ____.

---

## Q14 — MCQ

A uniprocessor performs 1500 context switches per second. Saving and restoring the CPU state costs 4 microseconds per switch. In one second, the time spent on those switches is

A. 4 ms
B. 6 ms
C. 1500 ms
D. 6000 ms

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | C |
| 2 | MSQ | A, B, C |
| 3 | MCQ | B |
| 4 | MCQ | B |
| 5 | NAT | 4 |
| 6 | MCQ | A |
| 7 | NAT | 1192 |
| 8 | MCQ | B |
| 9 | NAT | 61 |
| 10 | MSQ | A, B, D |
| 11 | MSQ | A, B, D |
| 12 | MCQ | A |
| 13 | NAT | 4 |
| 14 | MCQ | B |

## Detailed Solutions

### Q1

Answer: C

The PCB holds the state, the saved CPU context, scheduling and accounting data, memory-management pointers, and the open-file information. The program text lives in the address space (and on the executable), not inside the PCB.

### Q2

Answer: A, B, C

The scheduler moves a process between ready and running. A running process that starts a slow operation moves to waiting. When that operation finishes, the process becomes ready and waits for the CPU; it does not jump straight to running if another process may be on the CPU. A process that is only ready has not started an operation that would put it in the waiting state, so Ready → Waiting does not occur.

### Q3

Answer: B

I/O completion makes the process eligible for the CPU. The transition is Waiting → Ready. Waiting → Running would skip the scheduler.

### Q4

Answer: B

`fork` gives the child a new pid and returns 0 to the child and the child's pid to the parent. The descriptor table is duplicated, but both copies point at the same kernel open-file descriptions. Those descriptions hold the file offset, so a read by either process advances one shared offset. The child does not start with an empty descriptor table.

### Q5

Answer: 4

Only the original process stays in the loop. Each iteration creates one child, and that child breaks immediately.

- `i = 0`: the original process creates C1. C1 breaks. The original process continues.
- `i = 1`: the original process creates C2. C2 breaks.
- `i = 2`: the original process creates C3. C3 breaks.

Processes: original, C1, C2, C3. Total = 4.

### Q6

Answer: A

After termination the PCB remains until the parent collects the exit status with `wait` (or the process is reparented and reaped). That leftover terminated process is a zombie. It still has a PCB; that is how the status is stored.

### Q7

Answer: 1192

PCB storage is \(9 \times 128 = 1152\) bytes. Ready-queue pointers are \(5 \times 8 = 40\) bytes. Total \(1152 + 40 = 1192\).

### Q8

Answer: B

P1 creates the grandchild and then exits. P reaps P1 only. The grandchild is still running inside `sleep`, so it is not a zombie and it cannot remain a child of the exited P1. The kernel reparents it to init, which will reap it later. P did not wait for the grandchild, and the grandchild's PCB is still live because the process has not exited.

### Q9

Answer: 61

Slots already used: 3. Free slots: \(64 - 3 = 61\). Each successful `fork` consumes one free slot. After 61 successes the table is full and the next `fork` fails.

### Q10

Answer: A, B, D

A switch saves the program counter and the general-purpose registers (and the rest of the CPU context, including the pointer used to find the page tables). The PCB does not contain a copy of physical memory. The process's pages stay where the memory manager put them.

### Q11

Answer: A, B, D

The child has its own pid, and `fork` returns 0 in the child. Copy-on-write may share the physical frames until a write, at which point the writer gets a private copy. The open-file offset is not copied into two independent offsets: both descriptor tables refer to the same open-file description. Option C describes a different mechanism (for example, opening the file again).

### Q12

Answer: A

The child receives its own address space. The assignment `x = x + 2` updates the child's copy. The parent still has 3 when `wait` returns.

### Q13

Answer: 4

Call the original process P.

- P evaluates the first `fork` and creates A. P receives a nonzero pid, so it evaluates the second `fork` and creates B. A receives 0, so `&&` stops and A does not call `fork` again and does not enter the body.
- B receives 0 from the second `fork`, so the condition is false and B does not enter the body.
- P receives a nonzero pid from the second `fork`, so P enters the body and creates C.

Processes: P, A, B, C. Total = 4.

### Q14

Answer: B

\[
1500 \times 4\ \mu\text{s} = 6000\ \mu\text{s} = 6\ \text{ms}
\]

in each second. 4 μs is the cost of one switch, and 6000 μs is the same quantity as 6 ms written in the wrong unit.

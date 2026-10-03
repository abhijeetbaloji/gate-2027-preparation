# Threads — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A process uses the many-to-one thread model: several user-level threads are multiplexed on one kernel thread. One of those user-level threads issues a blocking read system call. What happens?

A. Only that user-level thread blocks; the user-level scheduler runs another thread of the same process on the same kernel thread
B. The process's single kernel thread blocks, so no user-level thread of that process runs until the read completes
C. The kernel automatically creates a new kernel thread for each remaining user-level thread
D. The blocking read is converted into a non-blocking read by the many-to-one runtime

---

## Q2 — MSQ

**Select all that apply.**

For kernel threads of one process, which items are per thread rather than shared by the whole process?

A. Stack
B. Program counter
C. Address space
D. Register set

---

## Q3 — MCQ

What does the many-to-many model provide that many-to-one does not?

A. User threads can be mapped onto a smaller set of kernel threads, so one blocking kernel call need not freeze every user thread
B. Threads of one process are forbidden from sharing the heap
C. The kernel sees every user thread and needs no scheduler
D. Thread creation is performed by copying the entire address space

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Threads of the same process, compared with separate processes, typically

A. share code, data, and heap, and each has its own stack and register context
B. share nothing except the pid
C. share one stack and have private heaps
D. cannot be scheduled independently of one another

---

## Q5 — NAT

A process has 6 kernel threads, counting the original thread. Each thread reserves an 8 KB stack. The shared heap reservation is 64 KB and the code reservation is 16 KB. These regions do not overlap. The total reservation for stacks, heap, and code, in KB, is ____.

---

## Q6 — MCQ

Which operation is the cheapest on a typical system?

A. A switch between two kernel threads that belong to different processes
B. A switch between two user-level threads of the same process, done entirely by a user-level scheduler with no kernel entry
C. A `fork` of a large address space that copies every page immediately
D. Creating a new process and a user-level thread switch have the same cost by definition

---

## Level 3 — Multi-Step

## Q7 — MSQ

**Select all that apply.**

`x` is a global variable, initially 0. Three threads each execute the following with no lock. `y` is an automatic local variable.

```c
int y = 0;
x = x + 1;
y = y + 1;
```

A. Each thread's own `y` becomes 1
B. The final value of `x` is necessarily 3
C. The final value of `x` can be less than 3 because the increment of `x` is not atomic
D. The three threads share `x`

---

## Q8 — MCQ

A server has 4 CPUs and a pool of kernel threads. Twenty CPU-bound requests arrive together. Each request needs 100 ms of CPU and performs no I/O. The threads are scheduled so that the CPUs stay busy whenever work remains. The minimum time until all 20 requests are finished is

A. 100 ms
B. 500 ms
C. 1600 ms
D. 2000 ms

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Two threads of one process each enter a function that allocates a large automatic array. Which statement is correct?

A. The arrays overlap in memory because all threads of a process share one stack
B. Each thread has its own stack, so each automatic array is private to its thread
C. Automatic variables of a thread are allocated in the process-wide open-file table
D. A threaded process is not allowed to have automatic variables

---

## Q10 — MSQ

**Select all that apply.**

A. A detached thread cannot be joined to collect an exit status
B. Joining a joinable thread reaps its termination state
C. On a POSIX system, all threads of a process share one `errno` cell
D. Returning from a thread's start routine terminates that thread; the other threads of the process can continue

---

## Level 5 — Challenge

## Q11 — NAT

A process is many-to-one, with 12 user-level threads and 1 kernel thread. Five user-level threads are runnable inside the user runtime. Seven are blocked on user-level condition variables and have not entered the kernel. How many threads of this process can the kernel schedule independently?

---

## Q12 — MSQ

**Select all that apply.**

`counter` starts at 10. The main thread and one new thread each execute `counter = counter - 1` exactly once, with no lock. The generated code is a non-atomic load, subtract, and store. `main` joins the new thread before reading `counter`. Which values are possible?

A. 8
B. 9
C. 10
D. 7

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | MCQ | A |
| 5 | NAT | 128 |
| 6 | MCQ | B |
| 7 | MSQ | A, C, D |
| 8 | MCQ | B |
| 9 | MCQ | B |
| 10 | MSQ | A, B, D |
| 11 | NAT | 1 |
| 12 | MSQ | A, B |

## Detailed Solutions

### Q1

Answer: B

In many-to-one, the kernel knows only one thread of execution for the process. A blocking system call blocks that kernel thread. The user-level scheduler does not get control back until the kernel call returns, so every user-level thread of the process stalls with it.

### Q2

Answer: A, B, D

Each kernel thread has its own stack, program counter, and registers, because those are the CPU context of an independent execution. The address space and the open-file-descriptor table belong to the process and are shared.

### Q3

Answer: A

Many-to-many (and the similar two-level schemes) let the runtime and the kernel map many user threads onto several kernel threads. If one kernel thread blocks, another kernel thread of the same process can still run a different user thread. Many-to-one has only one kernel thread, so it cannot do that. Threads of one process still share the heap, and creating a thread does not copy the address space the way `fork` does.

### Q4

Answer: A

Code, global data, and the heap are process resources. Each thread needs a private stack for calls and automatic variables, and a private register set including the program counter. The kernel (or a user-level scheduler, for user threads) can schedule those contexts separately.

### Q5

Answer: 128

Stacks: \(6 \times 8 = 48\) KB. Heap: 64 KB. Code: 16 KB.

\[
48 + 64 + 16 = 128\ \text{KB}
\]

### Q6

Answer: B

A user-level switch saves and restores a few registers in user mode. A cross-process kernel-thread switch enters the kernel and also switches address spaces. An immediate full copy of a large address space moves every page. The user-level switch is the cheap one.

### Q7

Answer: A, C, D

`y` is allocated on the calling thread's stack, starts at 0, and is incremented once, so that thread's `y` is 1. `x` is in the shared data area. The read-modify-write of `x` can interleave: two threads can both read the same value and both store that value plus one, so one update disappears. The final `x` can therefore be 1, 2, or 3, and 3 is not guaranteed.

### Q8

Answer: B

Total CPU work is \(20 \times 100 = 2000\) ms. Four CPUs can apply 4 ms of CPU work in each millisecond of wall time, so the minimum makespan is

\[
2000 / 4 = 500\ \text{ms}.
\]

One CPU would need 2000 ms. The pool being larger than four does not shorten the 2000 ms of work.

### Q9

Answer: B

The stack pointer is part of the thread context. Each thread's automatic array is addressed relative to its own stack. Sharing one stack would make calls unusable; that is not how threads are implemented.

### Q10

Answer: A, B, D

Detached threads are not joinable; their status is released at termination. `pthread_join` on a joinable thread collects that status, which is the thread analogue of `wait`. POSIX requires `errno` to be thread-local, so one shared `errno` would be wrong. A thread that returns from its start function ends that thread only.

### Q11

Answer: 1

The kernel's schedulable entity for this process is the single kernel thread. The 12 user-level threads are switched by user code on top of that one kernel thread. Runnable versus blocked inside the user runtime does not create extra kernel threads. The kernel can schedule 1 thread of this process.

### Q12

Answer: A, B

If one decrement finishes before the other starts, both updates stick: \(10 \rightarrow 9 \rightarrow 8\).

If both threads load 10 before either stores, both store 9. The final value is 9.

There are only two decrements, so the result cannot be 7. It also cannot stay 10, because each store writes either 9 or 8.

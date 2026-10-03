# System Calls — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which of the following requires a system call on a UNIX-like operating system?

A. Computing the length of a string that already sits in a user-space buffer
B. Asking the kernel to replace the current process image with another executable
C. Adding two local integer variables
D. Copying bytes from one user-space array to another user-space array

---

## Q2 — MSQ

**Select all that apply.**

Which of the following actions cross into the kernel on a conventional UNIX-like system?

A. Opening a pathname
B. Taking the absolute value of an integer that is already in a register
C. Writing bytes through an open file descriptor
D. Comparing two characters in a user-space buffer

---

## Level 2 — Standard GATE Style

## Q3 — MCQ

A C library allocator sometimes satisfies a request from a free list that it keeps in the process's own address space, and sometimes asks the kernel to extend the data segment. A particular call is satisfied entirely from that free list. How many system calls does that call make?

A. 0
B. 1
C. 2
D. One per byte allocated

---

## Q4 — NAT

The following code runs in one process. Every `fork` succeeds. A process that receives a positive return value from `fork` executes `break`. A process that receives 0 continues the loop.

```c
for (int i = 0; i < 4; i++) {
    if (fork() > 0)
        break;
}
```

The number of child processes created is ____.

---

## Q5 — MCQ

A TCP server must be ready to accept a connection. Which order of successful calls is valid?

A. `socket`, `listen`, `bind`, `accept`
B. `socket`, `bind`, `listen`, `accept`
C. `bind`, `socket`, `accept`, `listen`
D. `listen`, `bind`, `socket`, `accept`

---

## Level 3 — Multi-Step

## Q6 — NAT

Every `fork` succeeds, and every process that reaches a `fork` executes it. No process exits before it has finished the statements that its control flow reaches.

```c
if (fork() == 0) {
    fork();
}
fork();
```

The total number of processes that exist after every process has passed the last `fork` it executes, including the original process, is ____.

---

## Q7 — MCQ

Which statement about entering the kernel is correct?

A. Every system call switches the CPU to a different user process
B. A system call moves the CPU from user mode to kernel mode; a switch to another user process may happen later, or the same process may resume
C. An ordinary call to a function linked into the same user executable always enters kernel mode
D. The return from every system call must dispatch a different runnable process

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

A process calls `printf("gate")`. The characters are still sitting in the user-space stdio buffer. The buffer has not been flushed, and the process has not exited. Which statement is correct?

A. A `write` system call has already transferred those characters to the kernel
B. Those characters can still be only in a user-space buffer, with no `write` system call yet
C. `printf` is itself the system call that copies bytes into a disk block
D. The kernel has already stored those characters in the file's inode

---

## Q9 — MSQ

**Select all that apply.**

Which of the following are system calls (or thin wrappers that directly invoke one), as opposed to pure user-space library routines?

A. `brk`
B. `memcpy`
C. `dup`
D. `atoi`

---

## Level 5 — Challenge

## Q10 — NAT

Every `fork` succeeds. Each process stores its own return values. No process exits early.

```c
int a = fork();
int b = fork();
if (a == 0 && b == 0)
    fork();
```

The total number of processes after all of these calls have been executed, including the original process, is ____.

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | B |
| 2 | MSQ | A, C |
| 3 | MCQ | A |
| 4 | NAT | 4 |
| 5 | MCQ | B |
| 6 | NAT | 6 |
| 7 | MCQ | B |
| 8 | MCQ | B |
| 9 | MSQ | A, C |
| 10 | NAT | 5 |

## Detailed Solutions

### Q1

Answer: B

Replacing the process image is the job of an `exec`-family system call: the kernel must tear down the old mapping and install a new one. String length, integer addition, and a user-space byte copy are ordinary instructions in the process. They do not need the kernel.

### Q2

Answer: A, C

`open` and `write` are kernel services. The absolute-value operation and a character comparison use only user-mode data and the ALU.

### Q3

Answer: A

The free list, the headers on free blocks, and the returned pointer are all in the process address space. Satisfying the request from that list performs no trap into the kernel, so the system-call count is 0. A later request that exhausts the list would call something like `brk` or `mmap`; this particular call does not.

### Q4

Answer: 4

The positive return belongs to the parent, so the parent leaves the loop. The child receives 0 and becomes the process that continues.

- `i = 0`: the original process creates child 1 and breaks. Child 1 continues.
- `i = 1`: child 1 creates child 2 and breaks. Child 2 continues.
- `i = 2`: child 2 creates child 3 and breaks. Child 3 continues.
- `i = 3`: child 3 creates child 4 and breaks. Child 4 finishes the loop.

That is 4 child processes. The original process is not a child of this loop.

### Q5

Answer: B

A TCP server creates a socket, binds it to a local address, marks it passive with `listen`, and then accepts a connection. `listen` before `bind`, or `accept` before `listen`, is not a valid setup sequence.

### Q6

Answer: 6

Call the original process P.

- P's first `fork` creates A. P receives a nonzero pid and skips the block. A's return is 0, so A enters the block.
- P then executes the final `fork` and creates B. B starts after that `fork`, so B creates nobody.
- A executes the inner `fork` and creates C. The inner call is the body of the `if`. After it, both A and C reach the final `fork`.
- A creates D. C creates E.

The processes are P, A, B, C, D, and E. Total = 6.

### Q7

Answer: B

The trap that implements a system call changes the processor from user mode to kernel mode and enters the kernel at a fixed entry point. The kernel may return to the same process. A context switch to another process is a separate decision made by the scheduler. A normal call inside the user binary pushes a return address and jumps; it does not change protection mode.

### Q8

Answer: B

`printf` writes into the C library's user-space buffer. A `write` system call happens when that buffer is flushed (a newline on a terminal, an explicit flush, a full buffer, or exit, depending on the stream). Until then the five characters need not have entered the kernel at all, and they are not yet recorded in an inode.

### Q9

Answer: A, C

`brk` changes the process break and is a system call. `dup` duplicates a file descriptor and is a system call. `memcpy` and `atoi` run entirely in user mode.

### Q10

Answer: 5

- P executes `a = fork()` and creates A. In P, `a ≠ 0`. In A, `a = 0`.
- P and A both execute `b = fork()`. P creates B (B has `a ≠ 0`, `b = 0`). A creates C (C has `a = 0`, `b = 0`).
- The condition `a == 0 && b == 0` is true only in C. C executes the last `fork` and creates D.
- P (`a ≠ 0`), A (`b ≠ 0`), and B (`a ≠ 0`) skip that `fork`.

Processes: P, A, B, C, D. Total = 5.

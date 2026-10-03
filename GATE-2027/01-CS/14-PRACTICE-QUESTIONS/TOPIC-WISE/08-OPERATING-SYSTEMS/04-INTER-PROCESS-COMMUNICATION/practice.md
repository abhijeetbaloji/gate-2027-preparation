# Inter-Process Communication — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Two processes have already established a shared-memory mapping. Further communication through that region works as follows.

A. The kernel copies every byte on each load or store after the mapping exists
B. The processes use ordinary loads and stores; the kernel does not copy each access
C. Shared memory can be used only for one word, and only inside a system call
D. A pipe is the same object as a shared mapping of anonymous pages

---

## Q2 — MSQ

**Select all that apply.**

Which statements describe an ordinary anonymous pipe?

A. It is a unidirectional byte stream
B. It is normally inherited across `fork` by a parent and a child
C. The reader always receives writes as separate messages with the original boundaries
D. The buffer is finite, so a write can block when the free space is insufficient

---

## Q3 — MCQ

Indirect communication through a mailbox means

A. every send names the receiving process explicitly
B. processes send to and receive from a mailbox, and a sender need not name the peer process
C. only the kernel is allowed to send, and user processes may only receive
D. the mailbox is usable only if the processes also share a writable data page

---

## Level 2 — Standard GATE Style

## Q4 — NAT

A pipe buffer holds 16 bytes and starts empty. A write of at most the pipe's atomic limit blocks until the entire write fits; it is not split. The writer performs a 4-byte write, then an 8-byte write, then a 6-byte write, with no read in between. The 6-byte write blocks. How many bytes are already stored in the pipe at that moment?

---

## Q5 — MCQ

After a shared-memory region is mapped read/write into two processes, data races on that region are avoided by

A. the kernel locking every individual load and store
B. synchronization that the processes apply themselves (locks, semaphores, or atomic operations)
C. making every shared mapping read-only after the first write
D. using the pipe buffer that is implied by every shared mapping

---

## Q6 — MCQ

Which name is looked up in the file-system namespace?

A. An anonymous pipe created by `pipe` and inherited by a child
B. A named pipe (FIFO) created at a pathname
C. An anonymous shared mapping that exists only because a child inherited it across `fork`
D. The register that holds a process id

---

## Level 3 — Multi-Step

## Q7 — NAT

A 400-byte message is delivered by copying message passing. The kernel copies the bytes from the sender into a kernel buffer and later copies them from that buffer to the receiver. How many bytes does the kernel copy for this one delivery?

---

## Q8 — MSQ

**Select all that apply.**

Which mechanisms preserve message boundaries (a reader can observe the units the sender wrote, rather than a raw byte stream)?

A. A POSIX message queue
B. A datagram socket
C. An anonymous byte-stream pipe
D. A TCP byte stream

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

A process creates an anonymous pipe and then calls `fork`. The call succeeds. Which statement is correct?

A. The parent and the child each receive a private pipe buffer
B. The duplicated descriptors in the two processes refer to the same pipe buffer
C. `fork` destroys the pipe
D. Only the child retains the write end

---

## Q10 — MSQ

**Select all that apply.**

A. A blocking receive waits until a message is available
B. A non-blocking receive returns at once if no message is waiting
C. A blocking write to a pipe waits when the write needs more free space than the buffer has
D. An ordinary load from a shared-memory mapping blocks inside the kernel until the other process executes a send system call

---

## Level 5 — Challenge

## Q11 — NAT

A pipe holds 32 bytes and starts empty. Writes are atomic for these sizes and block until the whole write fits. The writer writes 20 bytes. It then attempts another 20-byte write and blocks. The reader then reads 8 bytes, which frees enough space for the blocked write to finish. No further read occurs. How many bytes are in the pipe after that second write completes?

---

## Q12 — MCQ

Two processes map a shared region and then update a 512-byte record 10 times by ordinary stores. After the mapping exists, how many bytes does the kernel copy for those 10 updates?

A. 0
B. 512
C. 1024
D. 10240

---

## Answer Key

| Q | Type | Answer |
|---|---|---|
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | B |
| 4 | NAT | 12 |
| 5 | MCQ | B |
| 6 | MCQ | B |
| 7 | NAT | 800 |
| 8 | MSQ | A, B |
| 9 | MCQ | B |
| 10 | MSQ | A, B, C |
| 11 | NAT | 32 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

Setting up a shared mapping is a kernel operation. After the pages are mapped into both address spaces, each access is a normal load or store through the MMU. The kernel does not sit on that path and copy the byte. A pipe is a kernel buffer with read and write ends, which is a different mechanism.

### Q2

Answer: A, B, D

An anonymous pipe carries bytes in one direction, has a bounded kernel buffer, and is passed to a child by duplicating descriptors at `fork`. It does not preserve write boundaries: a reader can observe any nonempty prefix of the buffered bytes. Message queues and datagrams are the mechanisms that keep message boundaries.

### Q3

Answer: B

With a mailbox, the send and receive operations name the mailbox. The sender does not have to know which process will consume the message. Direct communication is the style that names the peer. A mailbox does not require a shared writable page.

### Q4

Answer: 12

The first write stores 4 bytes and the second stores 8. Occupied space is \(4 + 8 = 12\). Free space is \(16 - 12 = 4\). The 6-byte write does not fit in 4 bytes, so it blocks with 12 bytes already in the pipe.

### Q5

Answer: B

The mapping makes the same frames visible to both processes. The hardware does not turn each store into a critical section. If both processes update a shared structure, they need their own synchronization. The mapping also does not create a pipe.

### Q6

Answer: B

A FIFO is created at a path, and other processes open that path. An anonymous pipe and an anonymous shared mapping inherited across `fork` have no directory entry. A pid is not a file-system name.

### Q7

Answer: 800

Copying send/receive pays for two transfers of the payload:

\[
400 \times 2 = 800
\]

bytes.

### Q8

Answer: A, B

A POSIX message queue delivers each `mq_send` as one message. A datagram socket delivers one datagram per receive (when the buffer is large enough). A pipe and a TCP stream present a sequence of bytes; a read can return a portion of a write or the concatenation of several writes.

### Q9

Answer: B

`pipe` creates one buffer. `fork` duplicates the descriptor numbers, and the duplicates refer to that same buffer. The parent and the child do not get two independent pipes. Both still hold whichever ends they held, until one of them closes an end.

### Q10

Answer: A, B, C

Blocking and non-blocking receives differ in whether the caller waits for a message. A blocking pipe write waits when the free space cannot hold the write (for a write that is kept atomic). A load from a shared mapping does not become a receive. It reads memory directly and does not block in the kernel waiting for a send call.

### Q11

Answer: 32

After the first write the pipe holds 20 bytes, so 12 bytes are free. The second 20-byte write cannot fit and blocks. The read removes 8 bytes, leaving \(20 - 8 = 12\) and freeing \(12 + 8 = 20\) bytes. The blocked write then stores 20 bytes.

\[
12 + 20 = 32
\]

bytes are in the pipe, and the buffer is full.

### Q12

Answer: A

Once the pages are mapped, each update is a store by the CPU. The kernel copies 0 bytes for those 10 updates. A copying message-passing design would have copied \(10 \times 512 \times 2 = 10240\) bytes. That cost belongs to the other design, not to the shared-memory stores. 512 is one record, and 1024 is one record counted twice; neither is a kernel copy in this design.

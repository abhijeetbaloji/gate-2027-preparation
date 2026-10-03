# DMA — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

During a DMA transfer, the data path is

A. between the I/O device and memory, with the CPU off the transfer loop  
B. only between two general-purpose registers  
C. a user-level load instruction for every byte  
D. required to pass through the programmer-visible ALU of the interrupted program

---

## Q2 — MCQ

In cycle-stealing DMA, the controller

A. keeps the bus until an entire large block has moved  
B. takes the bus for a short transfer and then releases it  
C. moves data without using the system bus  
D. clears the interrupt mask permanently

---

## Q3 — NAT

A DMA memory-address register must name any byte in a 1 MB byte-addressable memory. Use \(1\text{ MB} = 2^{20}\) bytes. How many bits does that register need?

---

## Level 2 — Standard GATE Style

## Q4 — MSQ

Select all that apply.

A. Burst-mode DMA holds the bus for the whole block.  
B. Cycle stealing interleaves DMA transfers with CPU bus cycles.  
C. Programmed I/O uses the CPU to move every word.  
D. Every DMA design is forbidden to raise a completion interrupt.

---

## Q5 — NAT

A 50 MHz bus grants 2 percent of its cycles to DMA. Each granted cycle transfers 2 bytes. The steady-state DMA rate, in bytes per second, is ______.

---

## Q6 — MCQ

Before a block transfer starts, the memory address, device address, and word count are normally written by

A. the CPU, through the DMA controller’s command registers  
B. the cache replacement policy, with no CPU instruction  
C. the ALU status flags  
D. the page-replacement algorithm alone

---

## Level 3 — Multi-Step

## Q7 — NAT

A DMA engine moves \(4 \times 10^{6}\) bytes per second. Each byte consumes one memory cycle of 100 ns. If the CPU would otherwise use every memory cycle, what percentage of memory cycles remains for the CPU?

---

## Q8 — MCQ

Which description of DMA modes is correct?

A. Burst mode can move a large contiguous block at the device’s rate, while the CPU is stalled for the whole burst.  
B. Cycle stealing keeps the bus from the CPU until the entire file has moved.  
C. A DMA controller cannot write main memory.  
D. The CPU executes a load instruction for every byte that DMA transfers.

---

## Level 4 — Tricky / Trap-Based

## Q9 — NAT

A 2048-byte block is moved by two methods. Count every stolen bus cycle as a cycle the CPU cannot use.

- Programmed I/O costs 20 CPU cycles per byte.
- DMA costs 256 setup cycles, 1 stolen cycle per byte, and 256 cycles for the completion interrupt.

The programmed-I/O cycle count divided by the DMA cycle count equals ______.

---

## Q10 — MSQ

Select all that apply.

A. Transparent DMA transfers only in cycles when the CPU is not using the bus.  
B. A long burst can increase the worst-case time the CPU is kept off the bus.  
C. The DMA controller is the bus master while it transfers.  
D. Cycle stealing means the whole block occupies the bus without a release.

---

## Level 5 — Challenge

## Q11 — NAT

A disk transfers \(8 \times 10^{6}\) bytes per second. The bus moves 4 bytes in each 50 ns cycle. What percentage of the bus cycles does this DMA stream consume?

---

## Q12 — MCQ

A control loop must never be stalled continuously for more than 2 μs. One DMA memory cycle takes 100 ns and moves one byte. A 100-byte record can be moved either as one burst or by stealing one cycle at a time. Which choice keeps the longest continuous CPU stall within the limit?

A. One burst of all 100 cycles  
B. Cycle stealing, one memory cycle at a time  
C. A programmed transfer whose critical section lasts 10 μs  
D. Holding the bus idle for 100 μs before starting

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | NAT | 20 |
| 4 | MSQ | A, B, C |
| 5 | NAT | 2000000 |
| 6 | MCQ | A |
| 7 | NAT | 60 |
| 8 | MCQ | A |
| 9 | NAT | 16 |
| 10 | MSQ | A, B, C |
| 11 | NAT | 10 |
| 12 | MCQ | B |

## Detailed Solutions

### Q1

Answer: A

The DMA controller becomes bus master and moves data between the device and memory. The CPU programs the transfer and is usually interrupted when it finishes, but it does not execute a load or store for each byte.

### Q2

Answer: B

Cycle stealing takes one transfer opportunity, or a very short group, and gives the bus back. Holding the bus for the entire block is burst mode. The transfer still uses the bus, and it does not permanently change the interrupt mask.

### Q3

Answer: 20

A 1 MB byte-addressable memory has \(2^{20}\) addresses. The address register needs 20 bits.

### Q4

Answer: A, B, C

Burst mode retains the bus across the block. Cycle stealing returns it between transfers. Programmed I/O is the CPU-mediated alternative. Completion interrupts are allowed and are the usual way to report that DMA has finished, so D is false. If the processor hits in cache and does not need the bus, it can execute during a DMA tenure on a split or cache-equipped machine. E is qualified by that condition and is true as stated.

### Q5

Answer: 2000000

\[
0.02 \times 50 \times 10^{6} \times 2 = 2 \times 10^{6}
\]

The controller receives one million cycles per second and moves 2 bytes on each of them.

### Q6

Answer: A

The CPU writes the source, destination, direction, and count into the controller, then sets the start bit. Cache replacement and the ALU flags do not initialize a device transfer. Page replacement may decide which frame is used, but it is not the agent that loads the DMA registers.

### Q7

Answer: 60

DMA cycle demand per second:

\[
4 \times 10^{6} \times 100 \times 10^{-9} = 0.40
\]

The CPU receives the remaining

\[
1 - 0.40 = 0.60
\]

which is 60 percent.

### Q8

Answer: A

Burst mode trades a continuous CPU stall for a high device transfer rate. Cycle stealing does the opposite: it releases the bus between short transfers. DMA exists specifically to write or read memory without a per-byte CPU load. B, C, and D reverse those roles.

### Q9

Answer: 16

Programmed I/O:

\[
20 \times 2048 = 40960
\]

DMA:

\[
256 + 2048 + 256 = 2560
\]

\[
\frac{40960}{2560} = 16
\]

The stolen byte cycles are included in the DMA total because the question counts them as cycles unavailable to the CPU.

### Q10

Answer: A, B, C

Transparent mode waits for a cycle the CPU is not requesting. Burst lengthens the continuous stall. During the transfer the controller drives the bus as master. Cycle stealing releases the bus between transfers, so D is the definition of burst mode and is false. A completion interrupt returns attention to the CPU without making the CPU move the data.

### Q11

Answer: 10

Bus capacity:

\[
\frac{4}{50 \times 10^{-9}} = 8 \times 10^{7}\ \text{bytes/s}
\]

The disk uses

\[
\frac{8 \times 10^{6}}{8 \times 10^{7}} = 0.10
\]

which is 10 percent of the bus cycles. Equivalently, the disk needs \(8 \times 10^{6} / 4 = 2 \times 10^{6}\) bus cycles per second, and the bus supplies \(1 / (50 \times 10^{-9}) = 2 \times 10^{7}\) cycles per second.

### Q12

Answer: B

A 100-cycle burst lasts

\[
100 \times 100\ \text{ns} = 10\ \mu\text{s}
\]

which is longer than 2 μs. Stealing one cycle stalls the CPU for 100 ns at a time, and \(0.1\ \mu\text{s} < 2\ \mu\text{s}\). A 10 μs critical section and a 100 μs idle hold both violate the continuous-stall limit. The mode that satisfies the limit is cycle stealing.

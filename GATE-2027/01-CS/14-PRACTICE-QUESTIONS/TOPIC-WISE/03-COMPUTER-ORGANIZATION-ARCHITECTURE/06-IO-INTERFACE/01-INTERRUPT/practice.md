# Interrupt-Driven I/O — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A vectored interrupt supplies

A. an identifier that selects the device’s service routine  
B. one common routine address and no device identity  
C. a DMA bus grant  
D. the cache line that the device must invalidate

---

## Q2 — MCQ

In a non-vectored interrupt mechanism, the CPU

A. jumps directly through an address supplied separately by each device  
B. enters one fixed routine and then identifies the source  
C. moves a block between the device and memory without executing instructions  
D. disables the ALU until the next reset

---

## Q3 — NAT

Interrupt priority numbers run from 0 through 7 inclusive. How many distinct priority levels is that?

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

In a daisy-chain grant, the device electrically closest to the CPU sees the grant first and may claim it. Relative to devices farther along the chain, that closest device has

A. the highest priority  
B. the lowest priority  
C. no priority relationship  
D. priority equal to its I/O port address

---

## Q5 — MSQ

Select all that apply.

A. Interrupt-driven I/O removes the need for the CPU to busy-poll the device between events.  
B. The CPU still executes an interrupt service routine.  
C. If nesting is enabled, a higher-priority interrupt can preempt a lower-priority service routine.  
D. An interrupt transfer is the same mechanism as a DMA block transfer.

---

## Q6 — NAT

A device interrupts every 5 ms. Its service routine uses 40 μs of CPU time. Over one second, how many milliseconds of CPU time does this device consume?

---

## Q7 — MCQ

Which state must be preserved so that the interrupted program can resume correctly?

A. Only the cache tags  
B. The return address, plus any registers that the service routine will overwrite  
C. Only the DMA word-count register  
D. Nothing, when the interrupt is vectored

---

## Level 3 — Multi-Step

## Q8 — NAT

Device A interrupts 100 times per second and each service routine uses 200 μs. Device B interrupts 250 times per second and each service routine uses 100 μs. What percentage of CPU time, to one decimal place, is spent in these two service routines combined?

---

## Q9 — MCQ

A larger priority number means higher priority. The current levels are Disk 3, NIC 5, Timer 1, and Keyboard 2. The CPU is inside the keyboard service routine, and nesting is enabled. Which devices can preempt it?

A. Timer only  
B. Disk only  
C. Disk and NIC only  
D. NIC only

---

## Q10 — MSQ

Select all that apply.

A. A vector lets the processor select the device routine without a software poll of every device.  
B. A non-vectored interrupt enters a common routine that identifies the source.  
C. In a daisy-chain grant, a requesting device can claim the grant and identify itself; the CPU does not first poll every device.  
D. Daisy-chain arbitration requires the CPU to finish a programmed poll of every device before any service routine starts.

---

## Level 4 — Tricky / Trap-Based

## Q11 — NAT

Polling checks the device every 40 μs, and each poll costs 2 μs of CPU time. The interrupt alternative serves 200 events per second, and each event costs 50 μs of CPU time. The polling CPU fraction divided by the interrupt CPU fraction equals ______.

---

## Q12 — NAT

From interrupt recognition until the interrupted program resumes, the cycle counts are:

- hardware saves the PC: 2 cycles
- software saves 8 registers: 2 cycles each
- service-routine body: 40 cycles
- software restores those 8 registers: 2 cycles each
- return: 2 cycles

No other overhead occurs. What is the total number of cycles?

---

## Level 5 — Challenge

## Q13 — NAT

Each interrupt consumes 25 μs of CPU time, including entry and exit. The CPU may spend at most 20 percent of its time inside this service path. What is the maximum sustainable interrupt rate, in interrupts per second?

---

## Q14 — MSQ

A timer interrupts every 1 ms and its service routine uses 100 μs. A disk interrupts every 2 ms and its service routine uses 300 μs. The timer has higher priority. Select all that apply.

A. If both streams are sustained, their service routines together use 25 percent of the CPU.  
B. If the disk routine cannot be preempted, a timer request that arrives just after the disk routine starts can wait up to 300 μs of disk work.  
C. Vectored dispatch avoids a software poll of every attached device.  
D. Executing the return from an interrupt requires a DMA block transfer.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | B |
| 3 | NAT | 8 |
| 4 | MCQ | A |
| 5 | MSQ | A, B, C |
| 6 | NAT | 8 |
| 7 | MCQ | B |
| 8 | NAT | 4.5 |
| 9 | MCQ | C |
| 10 | MSQ | A, B, C |
| 11 | NAT | 5 |
| 12 | NAT | 76 |
| 13 | NAT | 8000 |
| 14 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: A

The vector, or the address derived from it, identifies the source so the CPU can enter that device’s routine. A single shared address is the non-vectored case. DMA grants and cache operations are different mechanisms.

### Q2

Answer: B

Non-vectored entry uses one fixed location. The common routine discovers the source, often by reading device status. A device-supplied address is the vectored case, and a transfer without instruction execution is DMA.

### Q3

Answer: 8

The integers \(0, 1, \ldots, 7\) are eight values.

### Q4

Answer: A

The grant walks away from the CPU. The first device that wants service takes it, so a closer device can block a farther one. Under the convention stated in the question, closest means highest priority.

### Q5

Answer: A, B, C

The CPU waits for the interrupt instead of spinning on status, but it still runs the service routine. Nesting lets a higher-priority request interrupt a lower-priority routine, and a mask can suppress a maskable request. DMA moves the block on the bus with the DMA controller as master; an interrupt only transfers control to a routine. D is false.

### Q6

Answer: 8

The device interrupts \(1 / 0.005 = 200\) times per second.

\[
200 \times 40\ \mu\text{s} = 8000\ \mu\text{s} = 8\ \text{ms}
\]

### Q7

Answer: B

The saved PC is the return address. Registers that the routine uses must also be saved and restored, either by hardware or by the routine. Cache tags are not the interrupted program’s architectural state, and a vector does not remove the need to resume the old PC.

### Q8

Answer: 4.5

\[
\begin{align*}
A &= 100 \times 200\ \mu\text{s} = 20000\ \mu\text{s} = 20\ \text{ms} \\
B &= 250 \times 100\ \mu\text{s} = 25000\ \mu\text{s} = 25\ \text{ms}
\end{align*}
\]

Together they use 45 ms in each second.

\[
\frac{45}{1000} \times 100 = 4.5\%
\]

### Q9

Answer: C

The keyboard runs at priority 2. Disk at 3 and the NIC at 5 are both higher, so both may preempt. The timer at 1 is lower and must wait. The answer is disk and NIC only.

### Q10

Answer: A, B, C

A vector carries source identity, while a non-vectored common routine has to discover it. A daisy-chain grant is claimed by the winning device; that is not the same as the CPU polling every status port before the grant. A priority encoder can present the winning request. D describes a poll loop, not daisy-chain grant logic, so it is false.

### Q11

Answer: 5

Polling fraction:

\[
\frac{2}{40} = 0.05
\]

Interrupt fraction:

\[
200 \times 50 \times 10^{-6} = 0.01
\]

\[
\frac{0.05}{0.01} = 5
\]

### Q12

Answer: 76

\[
2 + 8 \times 2 + 40 + 8 \times 2 + 2 = 2 + 16 + 40 + 16 + 2 = 76
\]

### Q13

Answer: 8000

Twenty percent of one second is \(0.20\) s. Each interrupt takes \(25 \times 10^{-6}\) s.

\[
\frac{0.20}{25 \times 10^{-6}} = 8000
\]

A higher rate would push the service path above the allowed 20 percent.

### Q14

Answer: A, B, C

Timer fraction:

\[
\frac{100\ \mu\text{s}}{1\ \text{ms}} = 0.10
\]

Disk fraction:

\[
\frac{300\ \mu\text{s}}{2\ \text{ms}} = 0.15
\]

The sum is 0.25, so A is true. If the disk routine runs to completion with nesting off, the timer can arrive immediately after it begins and then wait for the remaining 300 μs, so B and E are true. A vector selects the routine without polling every device. A return-from-interrupt restores CPU state; it does not perform a DMA transfer. D is false.

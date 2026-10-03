# Practice — I/O Interface and Interrupts

Original questions (not from any GATE paper and not copies of the existing practice file). Every question is solvable from
[`NOTES.md`](NOTES.md). Answers sit directly under each question — attempt first. MSQ = one or more options correct, no
partial marking. Unless stated: memory is byte-addressable, 1 K = 2¹⁰, 1 M = 2²⁰, 1 G = 2³⁰ for memory sizes.

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1
In a typical I/O module, which register does the CPU read in a polling loop to learn whether the device is ready?

A. Data register  
B. Control register  
C. Status register  
D. Address register of the DMA controller

**Answer:** C

**Solution:** The status register holds READY/BUSY/ERROR flags and is what a polling loop tests. The data register holds the word itself (reading it is the *next* step, after READY). The control register is written to start/configure the device. A DMA address register belongs to a different mechanism.

**Concept tested:** I/O module registers (NOTES §2).
**Difficulty:** Easy.
**Common trap:** Choosing "data register" because that is where the data is.

---

### Q2 — MSQ — Level 1
Select all correct statements (one or more).

A. Memory-mapped I/O lets ordinary load and store instructions access device registers.  
B. Isolated I/O does not reduce the memory address space available to RAM.  
C. Registers in a memory-mapped I/O region should be treated as uncacheable.  
D. In isolated I/O the device registers are reached by the same load/store instructions as RAM, with no extra bus control signal.

**Answer:** A, B, C

**Solution:** A, B, C are the defining properties (NOTES §3). D is false: isolated I/O uses a separate port space reached by special `IN`/`OUT` instructions and a bus signal that distinguishes I/O from memory. The cache statement C holds because a cached status register would never reflect the device's change.

**Concept tested:** memory-mapped vs isolated I/O.
**Difficulty:** Easy.
**Common trap:** Reversing the two schemes' properties.

---

### Q3 — MCQ — Level 1
Which of the following is an *asynchronous* event with respect to the program that is running?

A. A page fault on a load instruction  
B. A divide-by-zero detected in the ALU  
C. A disk controller signalling that a requested block has been read  
D. Execution of a system-call (trap) instruction

**Answer:** C

**Solution:** A, B and D are caused by the executing instruction itself (synchronous: same instruction, same cause, reproducible). The disk completion comes from outside, unrelated to which instruction is executing at that moment — asynchronous.

**Concept tested:** synchronous (exceptions/traps) vs asynchronous (external interrupts), NOTES §11.
**Difficulty:** Easy.
**Common trap:** Treating a page fault as an "interrupt from I/O" because it eventually involves the disk.

---

### Q4 — NAT — Level 1
A machine uses isolated I/O. There are 40 device controllers; each controller decodes an **aligned block of 8 ports** (it uses only 6 of them). What is the minimum number of port-address bits?

**Answer:** 9

**Solution:** Device select = ⌈log₂ 40⌉ = 6 bits. Register select inside an aligned block of 8 = log₂ 8 = 3 bits. Total = 6 + 3 = **9 bits** (512 ports). Counting only the 40 × 6 = 240 *used* ports would suggest 8 bits, but the aligned block layout forces 9.

**Concept tested:** port-address bit counting (NOTES §3.4, E2).
**Difficulty:** Easy–medium.
**Common trap:** ⌈log₂ 240⌉ = 8.

---

## Level 2 — Standard GATE

### Q5 — MCQ — Level 2
For a vectored external interrupt on a CPU whose hardware pushes PC and flags, consider these events:

(a) hardware loads PC with the ISR entry address obtained through the vector  
(b) the instruction that was executing completes  
(c) hardware pushes PC and flags on the stack  
(d) the ISR body services the device  
(e) the return-from-interrupt instruction pops flags and PC

Which order is correct?

A. b, c, a, d, e  
B. c, b, a, d, e  
C. b, a, c, d, e  
D. b, c, d, a, e

**Answer:** A

**Solution:** The running instruction finishes first (b). The old PC/flags must be saved (c) *before* PC is overwritten with the ISR address (a). Then the ISR body runs (d), and the return pops the state last (e). B starts saving before finishing the instruction; C loads the new PC before saving the old one (return address would be lost); D loads PC *after* the ISR body, which is impossible.

**Concept tested:** order of interrupt events (NOTES §6.3).
**Difficulty:** Easy–medium.
**Common trap:** swapping "save" and "load PC".

---

### Q6 — NAT — Level 2
A 32-bit-address, byte-addressable CPU uses memory-mapped I/O with a contiguous 16 MB I/O window. What is the largest amount of RAM, in MB, that can be addressed?

**Answer:** 4080

**Solution:** Total address space = 2³² B = 4096 MB. Subtract the 16 MB window: 4096 − 16 = **4080 MB**.

**Concept tested:** address-space cost of memory-mapped I/O (F1).
**Difficulty:** Easy.
**Common trap:** answering 4096 (assuming isolated I/O).

---

### Q7 — NAT — Level 2
Memory is byte-addressable. Instruction layout (address: instruction, size):

```
3000: MOV R1,#10        6 bytes
3006: ADD R2,R1         2 bytes
3008: STORE R2,[0x9000] 6 bytes
3014: DEC R1            2 bytes
3016: JNZ 3006          4 bytes
3020: HALT
```
An external maskable interrupt arrives while `STORE` is executing, interrupts are enabled, and the CPU recognises it at the end of that instruction. What return address is pushed (decimal)?

**Answer:** 3014

**Solution:** `STORE` completes; the PC then holds the address of the next instruction in program order: 3008 + 6 = 3014. That is the pushed value.

**Concept tested:** return address (NOTES §6.5, F13).
**Difficulty:** Easy.
**Common trap:** pushing 3008 (the interrupted instruction) or adding a fixed 4.

---

### Q8 — NAT — Level 2
An interrupt vector table starts at address 0x2000. Each entry is 8 bytes. A device supplies vector number 0x35. At what address (give the decimal value) is the entry?

**Answer:** 8616

**Solution:** 0x35 = 53. Offset = 53 × 8 = 424 = 0x1A8. Address = 0x2000 + 0x1A8 = 0x21A8 = 8192 + 424 = **8616**.

**Concept tested:** vector table addressing (F15).
**Difficulty:** Easy.
**Common trap:** forgetting the base, or using a 4-byte entry size.

---

### Q9 — MCQ — Level 2
A CPU is running an ISR at priority level 5 (larger number = higher priority; nesting is enabled; NMI is non-maskable and above all levels). New requests arrive: X at level 5, Y at level 6, Z at level 3, and an NMI. Which of them can preempt the running ISR?

A. Y only  
B. X and Y  
C. Y and the NMI  
D. X, Y and Z

**Answer:** C

**Solution:** Preemption needs a *strictly higher* level: Y (6 > 5) can. X (equal) must wait; Z (lower) waits. The NMI cannot be masked and preempts regardless. So Y and the NMI.

**Concept tested:** preemption rule with equal priority and NMI (NOTES §10.2).
**Difficulty:** Medium.
**Common trap:** letting an equal-priority request preempt, or forgetting NMI.

---

### Q10 — NAT — Level 2
A 2 GHz CPU spends, per interrupt: 60 cycles in hardware entry, 100 cycles saving and restoring registers (total), 640 cycles in the ISR body, and 40 cycles in the return. A device raises 150 000 interrupts per second. What percentage of CPU time is consumed (one decimal place)?

**Answer:** 6.3

**Solution:** Cycles per interrupt = 60 + 100 + 640 + 40 = 840. Time = 840 / (2 × 10⁹) = 0.42 μs. Time per second = 150 000 × 0.42 μs = 63 000 μs = 63 ms → 6.3 % of the second.

**Concept tested:** interrupt-fraction (F6, F8).
**Difficulty:** Medium.
**Common trap:** leaving out the entry/return cycles; treating GHz as MHz.

---

### Q11 — MCQ — Level 2
A system has the following interrupt sources, with no other information: (A) a power-supply "failing" warning, (B) a network card with a small receive FIFO, (C) a touch-screen controller, (D) a printer reporting an empty paper tray. Which is normally handled at the highest priority?

A. Power-supply warning  
B. Network card  
C. Touch-screen controller  
D. Printer

**Answer:** A

**Solution:** Priority follows consequences of delay: a power-failure warning needs immediate action (save state) and is usually non-maskable/highest. The network card is deadline-bound (FIFO overrun) — second. Human-speed devices (touch screen) and slow peripherals (printer) tolerate delay and are lowest.

**Concept tested:** priority assignment (NOTES §10.1).
**Difficulty:** Easy–medium.
**Common trap:** ranking by "importance to the user" or data volume.

---

### Q12 — MSQ — Level 2
Select all correct statements about the three data-transfer techniques.

A. Busy-wait programmed I/O keeps the CPU occupied for the whole wait for a slow device.  
B. Interrupt-driven I/O pays an entry/exit overhead for every word transferred.  
C. Interval polling of a device that is idle most of the time spends most polls finding nothing.  
D. DMA eliminates every interrupt, including the one at the end of a transfer, in all systems.

**Answer:** A, B, C

**Solution:** A, B, C follow directly from the definitions. D is false: a DMA transfer normally ends with a completion interrupt (setup + completion are the CPU's only costs), though no interrupt is needed per word.

**Concept tested:** comparison of techniques (NOTES §4.4).
**Difficulty:** Easy–medium.
**Common trap:** "DMA means the CPU is never involved".

---

## Level 3 — Multi-step numerical / reasoning

### Q13 — NAT — Level 3
A sensor produces one event every 2 seconds. In the polling design the CPU polls every 5 ms; each poll costs 20 μs; when a poll finds the event, 300 μs of processing follow. In the interrupt design each event costs 900 μs in total (service + processing). Let T₁ and T₂ be the average CPU time per second used by the polling and interrupt designs respectively. Compute T₁ / T₂ (one decimal place).

**Answer:** 9.2

**Solution:** Polls per second = 1 / 5 ms = 200 → 200 × 20 μs = 4000 μs/s. Events per second = 0.5 → processing 0.5 × 300 μs = 150 μs/s. T₁ = 4150 μs/s. T₂ = 0.5 × 900 μs = 450 μs/s. Ratio = 4150 / 450 = 9.22 → **9.2**.

**Concept tested:** polling vs interrupt ratio (NOTES §5, E6).
**Difficulty:** Medium.
**Common trap:** assuming one event per second (that would give 4300/900 ≈ 4.8); counting only the polls that succeed.

---

### Q14 — NAT — Level 3
Nesting is enabled; a larger number means higher priority; there is no overhead. Four ISRs:

| ISR | Priority | Length | Arrives at t |
|---|---|---|---|
| P | 1 | 10 | 0 |
| R | 2 | 6 | 4 |
| Q | 3 | 4 | 6 |
| S | 4 | 3 | 7 |

At what time does R finish?

**Answer:** 17

**Solution:** 0–4 P runs (6 left). t = 4: R (2) preempts P; R runs 4–6 (4 left). t = 6: Q (3) preempts R; Q runs 6–7 (3 left). t = 7: S (4) preempts Q; S runs 7–10 and finishes. Unfinished: Q(3), R(2), P(1): Q resumes 10–13 and finishes. Then R resumes 13–17 (4 left) → **R finishes at 17**. P finishes at 23 (total 10+6+4+3).

**Concept tested:** nested ISR timeline (NOTES §10.3, E15).
**Difficulty:** Medium.
**Common trap:** resuming P before R after S finishes; forgetting to carry the remaining length.

---

### Q15 — NAT — Level 3
A system has 45 interrupt request sources. It uses 8-input interrupt controller chips cascaded in one level: one master chip, with each slave chip occupying one master input. What is the minimum number of chips (master plus slaves) needed?

**Answer:** 7

**Solution:** With k slaves, lines = (8 − k) + 8k = 8 + 7k. k = 5 gives 43 < 45; k = 6 gives 50 ≥ 45. Chips = 6 + 1 = **7**.

**Concept tested:** cascaded PIC capacity (F21).
**Difficulty:** Medium.
**Common trap:** 45/8 → 6 chips (ignoring that master inputs used for slaves are lost as direct lines).

---

### Q16 — NAT — Level 3
A device overwrites its 1-byte data register 8 μs after it raises the interrupt request. The CPU runs at 100 MHz. Worst-case delay before interrupt entry begins (current instruction plus any critical section) = 180 cycles; hardware entry = 20 cycles; the ISR's software save of registers takes 30 cycles before any device access. What is the maximum number of additional ISR cycles that may precede the instruction that reads the data register so that no byte is lost? (Integer cycles.)

**Answer:** 570

**Solution:** Time budget = 8 μs × 100 MHz = 800 cycles. Used before the ISR proper: 180 + 20 + 30 = 230. Remaining = 800 − 230 = **570 cycles**.

**Concept tested:** latency and the deadline condition (F14, E10).
**Difficulty:** Medium.
**Common trap:** 8 μs → 80 cycles (unit slip: 1 cycle = 10 ns, so 8 μs = 800 cycles).

---

### Q17 — NAT — Level 3
A poll takes 3 μs of CPU time and is done every 100 μs, regardless of events. The interrupt design pays 40 μs of overhead per event; the processing of an event (identical in both designs) is ignored. At what event rate (events per second) do the two designs use equal CPU time?

**Answer:** 750

**Solution:** Polling fraction = 3 / 100 = 0.03. Interrupt fraction = λ × 40 μs. Equal when λ = 0.03 / 40 μs = **750 events/s**. Below this rate interrupts are cheaper; above it polling is.

**Concept tested:** crossover (F10).
**Difficulty:** Medium.
**Common trap:** including the processing cost on one side only.

---

### Q18 — NAT — Level 3
A device produces 4000 bytes/s into a 16-byte buffer that is empty at each poll. The CPU polls at the minimum fixed rate that never overruns the buffer. Each poll costs 40 μs (the cost of moving data is ignored). What percentage of the CPU is used by the polling? (one decimal place)

**Answer:** 1.0

**Solution:** The buffer fills in 16 / 4000 = 4 ms, so T_p ≤ 4 ms → f_p ≥ 250 polls/s. Cost = 250 × 40 μs = 10 000 μs/s = 10 ms/s = **1.0 %**.

**Concept tested:** minimum polling rate (F5) and polling cost (F4).
**Difficulty:** Medium.
**Common trap:** polling at the item rate (4000/s), which would waste 16 % of the CPU.

---

## Level 4 — Tricky / trap-based

### Q19 — MSQ — Level 4
Assume a CPU whose convention is: external interrupts and traps push the address of the next instruction to execute; faults push the address of the faulting instruction (which is re-executed after the handler). For which events is the pushed address that of the instruction that comes *after* the one being executed (in program order, ignoring branches)? Select all (one or more).

A. A timer interrupt arrives during an `ADD` instruction.  
B. A page fault occurs on the operand access of a `LOAD`; the handler maps the page.  
C. The program executes a system-call trap instruction.  
D. A divide instruction faults because the divisor is zero.

**Answer:** A, C

**Solution:** A (external interrupt) and C (trap) complete the instruction, so the next one is saved. B and D are faults: the instruction did not complete, and the saved PC points to the faulting instruction itself.

**Concept tested:** interrupt vs trap vs fault, saved PC (NOTES §6.5, §11).
**Difficulty:** Medium.
**Common trap:** assuming all exceptions behave like external interrupts.

---

### Q20 — MSQ — Level 4
Select all correct statements about a daisy-chain interrupt scheme (one or more).

A. The device nearest the CPU in the chain has the highest priority.  
B. A device that is requesting does not pass the acknowledge on to the devices behind it.  
C. Adding a new device requires a new dedicated request line and grant line at the CPU.  
D. A device that fails to pass the acknowledge on can prevent all devices behind it from being served.

**Answer:** A, B, D

**Solution:** A and B are the defining rules: the grant reaches the nearest requester first and is absorbed there. D follows because every later device depends on the grant passing through the earlier ones. C is false: all devices share a single request line and the acknowledge is chained — that is the main saving over a one-line-per-device scheme.

**Concept tested:** daisy chain properties (NOTES §9.2).
**Difficulty:** Medium.
**Common trap:** confusing daisy chain with parallel priority (per-device lines).

---

### Q21 — MCQ — Level 4
A process P is running. The disk controller raises an interrupt that signals completion of a read requested earlier by another process Q, which has lower priority than P. Which statement is correct?

A. The ISR can run and then control can return to P without any process context switch.  
B. P must now be moved to the ready queue.  
C. Q starts executing immediately, because its data has arrived.  
D. The ISR need not preserve P's registers because the ISR is part of the operating system.

**Answer:** A

**Solution:** An interrupt only makes the ISR run; whether the scheduler switches process is a separate decision, and with Q lower priority it normally resumes P. B and C assume an unconditional switch. D is false: whoever runs the ISR must preserve the state of the interrupted program (hardware PC/flags, ISR the registers it uses).

**Concept tested:** interrupts vs context switch (NOTES §13, §6.4).
**Difficulty:** Medium.
**Common trap:** "every interrupt causes a context switch".

---

### Q22 — NAT — Level 4
A parallel interrupt scheme has requests IR7…IR0. Pending register = `1011 0100`. Mask register (1 = masked) = `0000 0101`. IR0 has the highest priority and IR7 the lowest. Which line number is served first?

**Answer:** 4

**Solution:** Active = pending AND NOT mask = `1011 0100` AND `1111 1010` = `1011 0000` (IR7, IR5, IR4). Highest priority among them is the lowest index → **IR4**. Without the mask the winner would have been IR2 (lowest set bit of the pending register).

**Concept tested:** mask register and priority encoder (F19).
**Difficulty:** Medium.
**Common trap:** ignoring the mask (answer 2) or reading bit positions from the left.

---

## Level 5 — Challenge

### Q23 — NAT — Level 5
Nesting is enabled; larger number = higher priority; a request of **equal** priority does not preempt. Each ISR has an entry cost of 2 and an exit cost of 2 (time units) that are part of its effective length (and are preemptible like the rest of it). Bodies and arrivals:

| ISR | Priority | Body | Arrives at t |
|---|---|---|---|
| A | 1 | 12 | 0 |
| B | 3 | 5 | 5 |
| C | 2 | 4 | 6 |
| D | 3 | 3 | 8 |

At what time does D finish?

**Answer:** 21

**Solution:** Effective lengths: A = 16, B = 9, C = 8, D = 7. A runs 0–5 (11 left). t = 5: B (3) preempts A and runs 5–14. C (2) at t = 6 and D (3) at t = 8 arrive while B runs; D is equal to B so it does not preempt, C is lower. t = 14: pending D(3), C(2), A(1, 11 left) → D runs 14–21; **D finishes at 21**; then C runs 21–29; then A resumes 29–40 (A finishes at 40).

**Concept tested:** nesting with overheads and the equal-priority rule (NOTES §10.2–10.3, E16).
**Difficulty:** Hard.
**Common trap:** letting D preempt B at t = 8 (D would then finish at 15); forgetting the overheads (without them D finishes at 13).

---

### Q24 — NAT — Level 5
The main program must receive at least 80 % of the CPU. A timer interrupts 1000 times per second at 8 μs each; a disk interrupts 200 times per second at 90 μs each; a network card interrupts at rate λ with 15 μs each. What is the maximum integer λ (packets per second)?

**Answer:** 11600

**Solution:** The interrupt budget is 20 % = 0.20 s per second. Timer = 1000 × 8 μs = 8 ms = 0.008. Disk = 200 × 90 μs = 18 ms = 0.018. Remaining = 0.20 − 0.008 − 0.018 = 0.174 s. λ_max = 0.174 / 15 μs = **11 600** per second.

**Concept tested:** budgeted maximum rate with several sources (F7, F9).
**Difficulty:** Medium–hard.
**Common trap:** budgeting 80 % instead of 20 %; forgetting the other two sources.

---

### Q25 — NAT — Level 5
A disk delivers 2²⁰ bytes per second (use this exact value). The CPU runs at 1 GHz. Design I: interrupt per 4-byte word; each interrupt costs 2000 cycles. Design II: DMA with 4096-byte blocks; per block, 6000 cycles of setup plus 4000 cycles for the completion interrupt. What is (CPU percent of Design I) / (CPU percent of Design II)? (One decimal place.)

**Answer:** 204.8

**Solution:** Design I: words/s = 2²⁰ / 4 = 262 144; cycles/s = 262 144 × 2000 = 524 288 000 → 52.4288 %. Design II: blocks/s = 2²⁰ / 4096 = 256; cycles/s = 256 × 10 000 = 2 560 000 → 0.256 %. Ratio = 52.4288 / 0.256 = **204.8**. Equivalent shortcut: per-byte cost I = 500 cycles, II = 2.44 cycles; ratio = 2000/4 ÷ (10 000/4096) = 500 / 2.4414 = 204.8.

**Concept tested:** per-word interrupts vs per-block DMA (F6, F12).
**Difficulty:** Hard.
**Common trap:** treating the DMA setup as per word; using 10⁶ for MB.

---

### Q26 — NAT — Level 5
A 5-stage pipelined CPU (1 GHz, CPI 1) receives 10 000 interrupts per second. For each interrupt the 4 younger in-flight instructions are squashed and the pipeline refill costs k − 1 = 4 cycles; hardware state save costs 30 cycles; the ISR runs 200 cycles. What percentage of the CPU's cycles is lost to interrupts? (three decimal places)

**Answer:** 0.234

**Solution:** Per interrupt = 4 + 30 + 200 = 234 cycles. Per second = 10 000 × 234 = 2 340 000 cycles. Total available = 10⁹. Fraction = 0.00234 = **0.234 %**.

**Concept tested:** pipeline flush cost added to interrupt overhead (NOTES §12, F16).
**Difficulty:** Medium.
**Common trap:** using k = 5 refill cycles instead of k − 1 = 4; omitting the refill altogether.

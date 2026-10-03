# DMA — Practice (original questions, answers under each)

All questions are original (different numbers and scenarios from the PYQs and from the existing practice file in
`14-PRACTICE-QUESTIONS`). Every numeric answer was re-derived by script. Sizes: K = 2^10; frequencies MHz = 10^6 Hz;
1 byte = 8 bits. Study [NOTES.md](NOTES.md) first. Interrupt-side questions live in [../01-INTERRUPT](../01-INTERRUPT/NOTES.md).

---

## Level 1 — Conceptual

### Q1 (MCQ, Level 1)

In a DMA controller, which register reaching zero normally ends the transfer and triggers the completion interrupt?

A. Address register
B. Word/byte count register
C. Data buffer register
D. Control register

**Answer:** B

**Solution:** The count register is decremented after every unit; when it reaches 0 (terminal count) the controller sets the done bit and raises the interrupt. The address register changes at every unit but is not the end condition. The data buffer only holds data in transit. The control register holds mode and start bits.

**Concept tested:** DMA controller registers (NOTES 4.1).

**Difficulty:** Easy

---

### Q2 (MSQ, Level 1)

One or more options are correct (no partial marking). During a burst-mode DMA transfer on a single shared bus:

A. The DMA controller is the bus master.
B. The CPU may still execute an instruction whose operands and code are in registers or on-chip cache.
C. The CPU and the controller both drive the address lines at the same time.
D. A completion interrupt is still raised at the end of the transfer.

**Answer:** A, B, D

**Solution:** The controller owns the bus during the burst (A). Work that needs no bus can continue (B). Only one master drives the address and control lines at any instant, so C is false. DMA replaces per-unit interrupts by one per block, so D is true.

**Concept tested:** Bus master exclusivity, CPU activity during DMA, interrupts in DMA (NOTES 5.2-5.4).

**Difficulty:** Easy

**Common trap:** Believing that "CPU off the loop" means the CPU is completely frozen, or that DMA removes the completion interrupt.

---

### Q3 (NAT, Level 1)

A word-addressable memory has 64 M words of 32 bits each (M = 2^20). How many bits does the DMA address register need to name any word? (Integer.)

**Answer:** 26

**Solution:** 64 M = 2^6 × 2^20 = 2^26 words, so ⌈log₂ 2^26⌉ = 26 bits. The word size (32 bits) does not matter because the memory is word addressable.

**Concept tested:** Address register width (NOTES 4.2).

**Difficulty:** Easy

**Common trap:** Counting bytes (2^28 bytes -> 28 bits) when the memory is word addressable.

---

## Level 2 — Standard GATE

### Q4 (NAT, Level 2)

An 8 MHz processor has a DMA controller that moves 4 bytes in one cycle by cycle stealing at regular intervals. If 2.5 % of the processor cycles are used for DMA, what is the data transfer rate in bits per second? (Integer.)

**Answer:** 6400000

**Solution:**
- Cycles used per second = 8×10^6 × 0.025 = 200,000.
- Bytes per second = 200,000 × 4 = 800,000.
- Bits per second = 800,000 × 8 = 6,400,000.

**Concept tested:** R = f × p × w × 8 (NOTES 8.2).

**Difficulty:** Easy

**Common trap:** Stopping at bytes per second, or treating 2.5 % as 0.25 %.

---

### Q5 (NAT, Level 2)

A 20 MHz bus carries 2 bytes per cycle for a DMA stream from a device that delivers 600,000 bytes per second. What percentage of the bus cycles does the stream use? (Real number.)

**Answer:** 1.5

**Solution:**
- Cycles needed per second = 600,000 / 2 = 300,000.
- Cycles offered per second = 20×10^6.
- p = 300,000 / 20,000,000 = 0.015 = 1.5 %.

**Concept tested:** p = R / (f_b × w) (NOTES 8.3).

**Difficulty:** Easy

---

### Q6 (MCQ, Level 2)

Consider the events: (P) the CPU writes address, count and control registers of the controller; (Q) the device raises DREQ; (R) the controller raises HOLD (bus request); (S) the CPU asserts HLDA (bus grant); (T) the units are transferred, with address and count updated; (U) the controller raises the completion interrupt. Which order is the normal sequence?

A. P, Q, R, S, T, U
B. Q, P, R, S, T, U
C. P, R, Q, S, T, U
D. P, Q, S, R, T, U

**Answer:** A

**Solution:** The controller can serve no request before it has an address and a count, so P comes first. The device's request (Q) is what makes the controller ask for the bus (R); the grant (S) can only follow the request; transfer (T) follows the grant; the interrupt (U) follows terminal count. B has the device requesting before the controller is programmed; C raises the bus request before any device request; D has a grant before a request.

**Concept tested:** DMA sequence (NOTES 5.1).

**Difficulty:** Medium

---

### Q7 (MSQ, Level 2)

One or more options are correct. Which statements about DMA modes are correct?

A. In cycle stealing, the longest single CPU stall caused by DMA is about one bus cycle plus arbitration.
B. In burst mode the arbitration overhead is paid once per block.
C. In transparent mode DMA may be delayed indefinitely if the CPU uses every bus cycle.
D. For the same fraction p of cycles given to DMA, transparent mode slows the CPU by exactly as much as cycle stealing.

**Answer:** A, B, C

**Solution:** A and B follow from the definitions (NOTES 7.1, 8.6). C: transparent mode uses only idle bus cycles; if there are none, nothing moves. D is false: transparent mode takes only cycles the CPU did not want, so it adds no CPU delay (with p taken as the share DMA receives from idle cycles).

**Concept tested:** Mode properties (NOTES 7).

**Difficulty:** Medium

**Common trap:** Treating transparent mode as just "slow cycle stealing".

---

### Q8 (MSQ, Level 2)

One or more options are correct. Regarding centralised and distributed bus arbitration:

A. In a daisy chain, a device nearer the arbiter along the grant line has higher priority.
B. Adding another device to a daisy chain requires a new, separate request line and grant line pair from the arbiter.
C. In independent request/grant arbitration, the arbiter can implement a rotating priority without rewiring.
D. In a daisy chain, the worst-case grant propagation delay increases with the number of devices ahead of the requester.

**Answer:** A, C, D

**Solution:** A and D are properties of the chain (NOTES 9.2). C: with a dedicated request/grant pair per device the arbiter alone decides the policy. B is false: a daisy chain uses one shared request line and one chained grant line; a new device is simply inserted in the chain, which is also why it adds delay and has fixed priority.

**Concept tested:** Daisy chain vs independent request (NOTES 9.2).

**Difficulty:** Medium

---

## Level 3 — Multi-step numerical

### Q9 (NAT, Level 3)

A memory is byte addressable. A DMA controller moves 4 bytes per transfer. Its count register is 12 bits wide and counts transfers; one programming can therefore move up to 2^12 transfers, and each programming is carried out as one burst. A file of 600 KB (K = 2^10) is read from disk to memory. What is the minimum number of bursts (bus acquisitions)? (Integer.)

**Answer:** 38

**Solution:**
- File bytes = 600 × 1024 = 614,400.
- Bytes per programming = 2^12 × 4 = 16,384.
- 614,400 / 16,384 = 37.5, so ⌈37.5⌉ = 38 (the last burst is half full).

**Concept tested:** Count-register capacity and bus acquisitions (NOTES 8.9).

**Difficulty:** Medium

**Common trap:** Using 2^12 bytes per programming (ignoring the 4-byte unit) which gives 150; or rounding 37.5 down to 37.

---

### Q10 (NAT, Level 3)

A device produces 400,000 bytes per second. The DMA controller is of the detached type on a shared bus: every byte needs two bus cycles (device to controller, then controller to memory), each bus cycle lasting 250 ns. What percentage of bus time does the stream occupy? (Real number.)

**Answer:** 20

**Solution:**
- Bus cycles per byte = 2, so the bus is busy 2 × 250 ns = 500 ns per byte.
- Bus busy per second = 400,000 × 500 ns = 0.2 s.
- Fraction = 0.2 = 20 %.

**Concept tested:** Bus cycles per unit k = 2 (NOTES 6.1, 8.3).

**Difficulty:** Medium

**Common trap:** Using one cycle per byte (10 %).

---

### Q11 (NAT, Level 3)

A synchronous 80 MHz bus has 64-bit multiplexed address/data lines. A burst transfer of 8 data words uses 1 address cycle followed by 8 data cycles, with no wait states. Sustained bandwidth in MB/s (1 MB/s = 10^6 B/s), rounded to the nearest integer?

**Answer:** 569

**Solution:**
- Bytes per burst = 8 × 8 = 64.
- Cycles = 1 + 8 = 9; cycle time = 1/80 MHz = 12.5 ns; burst time = 112.5 ns.
- 64 B / 112.5 ns = 568.9 × 10^6 B/s, rounded 569. (Peak 8 × 80 = 640 MB/s.)

**Concept tested:** Sustained vs peak bandwidth, multiplexed bus (NOTES 9.5).

**Difficulty:** Medium

**Common trap:** Quoting the peak (640) or counting an address cycle for each word.

---

### Q12 (NAT, Level 3)

On an asynchronous bus using a fully interlocked four-phase handshake, each of the four signal edges takes 6 ns to propagate, and the slave needs 48 ns between receiving the request and having data ready (the access time is in addition to the first propagation, and no overlap occurs). One transfer moves 4 bytes and the time per transfer is 4 × 6 + 48 ns. Data rate in MB/s (10^6 B/s), nearest integer?

**Answer:** 56

**Solution:** Time per transfer = 24 + 48 = 72 ns. Rate = 4 B / 72 ns = 55.56 × 10^6 B/s ≈ 56 MB/s.

**Concept tested:** Handshake timing (NOTES 9.4).

**Difficulty:** Medium

**Common trap:** Forgetting the four edges and using only the 48 ns access time (83 MB/s).

---

### Q13 (NAT, Level 3)

Interrupt-driven I/O costs 120 CPU cycles per byte. DMA costs 500 set-up cycles, 700 completion cycles, and 1 stolen cycle per byte (counted as lost). What is the smallest block size (bytes) for which DMA costs strictly fewer cycles than interrupt-driven I/O? (Integer.)

**Answer:** 11

**Solution:**
- DMA cheaper when 1200 + n < 120 n, i.e. n > 1200/119 = 10.08.
- n = 10: interrupt-driven 1200, DMA 1210 (DMA worse). n = 11: 1320 vs 1211 (DMA better).
- Smallest n = 11.

**Concept tested:** Break-even block size (NOTES 3.2).

**Difficulty:** Medium

**Common trap:** Rounding 10.08 to 10, or forgetting that the stolen cycles reduce the per-byte saving to 119.

---

## Level 4 — Tricky / trap-based

### Q14 (NAT, Level 4)

A 25 MHz bus moves 4 bytes per cycle for the DMA controller by cycle stealing. An 8-bit device delivers 2 × 10^6 bytes per second; the controller assembles 4 bytes in its buffer before each bus cycle. The CPU needs the bus in every cycle (assume). A job that would take 49 s on the CPU alone takes how many seconds with the DMA running? (Real number.)

**Answer:** 50

**Solution:**
- Bus cycles needed = 2×10^6 / 4 = 500,000 per second; offered 25×10^6.
- p = 0.02 (2 %); without assembly it would be 8 %.
- CPU share = 0.98, so time = 49 / 0.98 = 50 s.

**Concept tested:** Wide DMA unit, narrow device, slowdown (NOTES 8.4, 8.5).

**Difficulty:** Hard

**Common trap:** Using the device width (1 byte) for the cycle: p = 8 %, 53.26 s.

---

### Q15 (NAT, Level 4)

A control task tolerates at most 1.5 µs of continuous bus denial. A DMA bus cycle is 60 ns, and each bus acquisition wastes 2 cycles in request, grant and release during which the CPU also cannot use the bus. What is the largest number of units that one burst may carry? (Integer.)

**Answer:** 23

**Solution:** The stall = (A + N) × 60 ns ≤ 1500 ns gives A + N ≤ 25. With A = 2, N ≤ 23.

**Concept tested:** Maximum burst length under a stall limit (NOTES 8.6).

**Difficulty:** Hard

**Common trap:** Answering 25 (ignoring arbitration overhead).

---

### Q16 (MSQ, Level 4)

One or more options are correct. A system has a write-back cache and a DMA controller without cache snooping. Assume that the write buffer, if any, is drained before DMA starts. Which statements are correct?

A. After a device-to-memory transfer into a buffer that the CPU had cached earlier, the CPU must invalidate (or bypass) the cached copies before reading the buffer.
B. Before a memory-to-device transfer, dirty cache lines of the source buffer must be written back to memory.
C. If the cache were write-through, invalidation after a device-to-memory transfer would no longer be needed.
D. If the cache were write-through, flushing before a memory-to-device transfer would no longer be needed.

**Answer:** A, B, D

**Solution:** A: DMA wrote memory directly, so the cached copy is stale. B: with write-back the newest data may exist only in the cache, so the device would read old memory. C is false: write-through keeps memory up to date after CPU writes but does not update the cache when DMA changes memory. D is true: memory is already current.

**Concept tested:** DMA and cache coherence (NOTES 10.1).

**Difficulty:** Hard

**Common trap:** Thinking write-through solves both directions.

---

### Q17 (NAT, Level 4)

A slow device delivers one byte every 80 µs. With interrupt-driven I/O, each byte costs 12 µs of CPU time (entry, ISR, return). With programmed I/O the CPU spins in a polling loop for the entire transfer. By how many percentage points does the CPU time free for other work differ (interrupt-driven minus programmed)? (Integer.)

**Answer:** 85

**Solution:**
- Interrupt-driven: 12/80 = 15 % busy, so 85 % free.
- Programmed (busy-wait): 100 % busy, 0 % free.
- Difference = 85 − 0 = 85 percentage points.

**Concept tested:** CPU utilisation comparison (NOTES 3.4, 11).

**Difficulty:** Medium

**Common trap:** Computing only the 15 % overhead and giving 15, or the 85 % as a ratio.

---

### Q18 (MCQ, Level 4)

A block of 512 words moves over the bus; each bus acquisition costs 3 non-productive cycles and each word moves in 1 cycle. How many more bus cycles does cycle stealing (one word per acquisition) occupy than a single burst?

A. 1533
B. 1536
C. 2048
D. 515

**Answer:** A

**Solution:** Burst: 3 + 512 = 515 cycles. Stealing: 512 × (3 + 1) = 2048 cycles. Difference 2048 − 515 = 1533. B is 512 × 3, the overhead part of stealing alone; C is the stealing total; D is the burst total.

**Concept tested:** Burst vs stealing occupancy (NOTES 8.6).

**Difficulty:** Medium

**Common trap:** Giving the stealing total or the pure overhead.

---

### Q19 (MCQ, Level 4)

An 8 KB user buffer occupies two virtual pages that are mapped to non-adjacent physical frames. The OS starts DMA for it. Which is the correct approach?

A. Program the controller with the physical address of each contiguous piece (two transfers, or scatter-gather), and keep both pages pinned in memory until the transfer completes.
B. Give the virtual address of the buffer start and a count of 8192, since the controller walks the page tables.
C. No pinning is needed as long as the cache holds the data.
D. The pages may be replaced during the transfer because the completion interrupt will fix any problem.

**Answer:** A

**Solution:** DMA controllers use physical addresses and do not walk page tables (B false). The frames are not contiguous, so one count over a start address would run into the wrong frame. Pages must stay resident while the device writes (D false); the cache has nothing to do with residency (C false).

**Concept tested:** DMA and virtual memory (NOTES 10.3).

**Difficulty:** Medium

---

## Level 5 — Challenge

### Q20 (NAT, Level 5)

A 100 MHz system. A disk streams 12.8 × 10^6 bytes per second through a DMA controller moving 4 bytes per bus cycle, in blocks of 4096 bytes. Each block costs 3000 CPU cycles of set-up and 5000 CPU cycles of completion processing. Assuming the CPU would use every bus cycle, what percentage of CPU capacity is lost altogether (stolen cycles plus set-up and completion)? (Real number, one decimal.)

**Answer:** 28.2

**Solution:**
- Stolen cycles per second = 12.8×10^6 / 4 = 3.2×10^6 -> 3.2 % of 10^8.
- Blocks per second = 12.8×10^6 / 4096 = 3125.
- Overhead cycles per second = 3125 × (3000 + 5000) = 25×10^6 -> 25 %.
- Total = 3.2 + 25 = 28.2 %.

**Concept tested:** Combined loss with set-up and completion overhead (NOTES 8.8).

**Difficulty:** Hard

**Common trap:** Reporting only the stolen share (3.2 %); the per-block overhead dominates here, which is why very small blocks are costly.

---

### Q21 (NAT, Level 5)

A 50 MHz bus carries 4 bytes per cycle. Each bus acquisition costs 1 non-productive cycle. Compute the ratio (maximum sustainable DMA rate in burst mode with 16 units per burst) / (maximum sustainable rate in cycle stealing, 1 unit per acquisition), assuming the DMA can use every bus cycle. (Two decimals.)

**Answer:** 1.88

**Solution:**
- Cycle stealing: 1 unit per (1 + 1) = 2 cycles -> 50×10^6 × 4 / 2 = 100×10^6 B/s.
- Burst: 16 units per 17 cycles -> 50×10^6 × 4 × 16/17 = 188.2×10^6 B/s.
- Ratio = (16/17)/(1/2) = 32/17 = 1.88.

**Concept tested:** Sustainable rate per mode (NOTES 8.11).

**Difficulty:** Hard

---

### Q22 (NAT, Level 5)

A device delivers a 4-byte word every 2 µs. A 256-word block is to be moved; the bus cycle is 50 ns and each acquisition wastes 2 cycles. Plan X: let the controller's buffer fill (256 words), then move all 256 words in one burst. Plan Y: steal one cycle per word as each word arrives. Find (longest continuous CPU stall in plan X) / (longest continuous CPU stall in plan Y). (Integer.)

**Answer:** 86

**Solution:**
- Plan X stall = (2 + 256) × 50 ns = 12,900 ns (the filling time of 512 µs does not stall the CPU, because the bus is not used then).
- Plan Y stall = (2 + 1) × 50 ns = 150 ns.
- Ratio = 12,900 / 150 = 86.

**Concept tested:** Device-limited burst, worst-case stall (NOTES 8.6, 8.7).

**Difficulty:** Hard

**Common trap:** Counting the 512 µs buffer fill as a stall; the CPU only loses the bus during bus tenure.

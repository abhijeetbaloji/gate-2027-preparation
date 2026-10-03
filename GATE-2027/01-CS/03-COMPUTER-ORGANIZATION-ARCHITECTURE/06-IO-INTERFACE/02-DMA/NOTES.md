# DMA (Direct Memory Access) and Bus Sharing — Complete Notes

> Scope: the DMA half of the syllabus phrase "I/O interface (interrupt and DMA)", plus the bus-sharing mechanics
> (bus master, arbitration, synchronous/asynchronous transfer, bus bandwidth) that DMA needs.
> The interrupt half (I/O interface basics, programmed I/O, interrupt-driven I/O, vectored/non-vectored
> interrupts, priority, memory-mapped vs isolated I/O) is owned by the sibling folder
> [../01-INTERRUPT](../01-INTERRUPT/NOTES.md). This file links there instead of repeating it.

Conventions used in this folder (state them in every answer you write):

- Sizes: 1 K = 2^10, 1 M = 2^20, 1 G = 2^30. A file "of 600 KB" has 600 × 1024 bytes.
- Frequencies and clock rates are decimal: 1 MHz = 10^6 Hz. A data rate written "bytes per second" is a plain count;
  if a rate is written "MB/s" it is 10^6 B/s unless the question says otherwise (this file always says which).
- Addressability (byte or word) is always stated explicitly. 1 byte = 8 bits.
- One "cycle" in a DMA question means one bus/memory cycle unless the question defines it otherwise.

---

## 0. Where this fits

| Item | Detail |
|---|---|
| Syllabus line | "I/O interface (interrupt and DMA)" (COA) |
| Prerequisites | Bus, registers, memory cycle (basic); the I/O interface and interrupt mechanism in [../01-INTERRUPT](../01-INTERRUPT/NOTES.md); clock/cycle arithmetic (iron law) |
| Prerequisite / bridge: caches | Cache hit/miss, write-through vs write-back: [../05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING](../../05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/NOTES.md) (needed for section 10) |
| Prerequisite / bridge: virtual memory | Page tables and frames: [../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY) (needed for section 10.3) |
| What depends on it | OS I/O scheduling and disk drivers ([../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING](../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING)), buffering; memory bandwidth reasoning in [../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE](../../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/NOTES.md); the interrupt sibling (completion interrupt) |

---

## 1. Evidence snapshot (what drives the depth)

Counted from the mapping file [questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/questions.md):
6 mapped entries (2016, 2020, 2021, 2022, 2024 CS1, 2024 CS2); all six are genuinely I/O-or-DMA; one (2020) is mixed
interrupt/polling/DMA. There are no mapped DMA entries for 2007-2015 or 2017-2019, 2023, 2025, 2026 (the two scanned
years 2019 and 2021 Set-1 are unreadable in the text extraction, so absence there is not evidence).

| Section | Rating | Evidence |
|---|---|---|
| 8.2 Transfer rate vs percentage of cycles (rate = clock × fraction × bytes per cycle) | HIGH-VALUE | 2 mapped numerical entries (2021 CS-2, 2024 CS2) share this exact skill; existing practice Q5, Q7, Q11 |
| 8.9 Count-register capacity and number of times the bus is acquired | HIGH-VALUE | 1 mapped numerical entry (2016 CS-1); existing practice Q3 (register sizing) |
| 7 Burst vs cycle stealing vs transparent | HIGH-VALUE | 2024 CS1 statement question, existing practice Q2, Q4, Q8, Q10, Q12 |
| 11 PIO vs interrupt vs DMA (which is best for what) | HIGH-VALUE | 2022 and 2024 CS1 entries; existing practice Q1, Q9 |
| 5 Transfer sequence, bus master, interrupts in DMA | HIGH-VALUE | 2020 statement entry (bus-master statement), existing practice Q1, Q6 |
| 9.1-9.3 Bus arbitration (daisy chain, polling, independent, distributed) | MEDIUM | 2020 entry touches daisy chaining (interrupt-priority flavour, shared with sibling); no mapped numerical arbitration question |
| 8.8 Setup + completion overhead and break-even | MEDIUM | existing practice Q9 (and the polling-vs-interrupt overhead style of numerics in the sibling folder) |
| 9.4-9.6 Synchronous/asynchronous buses, bandwidth, multiplexing | LOW-MEDIUM | in syllabus scope as "I/O interface"; no mapped PYQ here; needed to compute the "cycle" that DMA steals |
| 10 DMA, cache coherence, virtual memory | LOW | no mapped PYQ; conceptual; kept short as required by scope |

---

## 2. The idea in one picture

Imagine a manager (CPU) who must move 4096 boxes from a loading dock (device) to a warehouse (memory).

- Programmed I/O: the manager walks to the dock, checks whether a box is ready, carries it, returns, repeats 4096 times.
  The manager does nothing else.
- Interrupt-driven I/O: the manager does other work; each time a box arrives a bell rings; the manager stops, carries
  that one box, goes back. The bell and the walk cost time per box.
- DMA: the manager hands a work order to an assistant: "move 4096 boxes from the dock to shelf 0x4000". The assistant
  carries all boxes; the manager gets one bell at the end. The assistant needs the same corridor (the bus) as the
  manager, so the two must take turns.

```
 Programmed / interrupt I/O                     DMA
 -------------------------                      ---
 Device --> CPU register --> Memory             Device ----------------> Memory
              ^ every unit goes through the CPU        ^ CPU only starts it and hears the end
```

DMA changes the cost from "per byte, CPU does work" to "per block, CPU does a fixed set-up and a fixed finish",
paid for by "per byte, some bus cycles are used by the controller instead of the CPU".

---

## 3. Why DMA: the cost model

### 3.1 Three costs to keep apart

For a block of n units (usually bytes):

| Method | CPU work per unit | Fixed CPU work per block | Bus cycles not available to CPU |
|---|---|---|---|
| Programmed I/O (polling) | poll loop + read device register + store to memory + update pointer/counter; plus waiting if the device is slow | ~0 | the CPU's own transfers |
| Interrupt-driven I/O | whole interrupt entry, ISR body (read device, store, update), return (see [../01-INTERRUPT](../01-INTERRUPT/NOTES.md)) | ~0 | the CPU's own transfers |
| DMA | none | set-up S (write address, count, control) + completion C (interrupt entry, ISR, status check) | one (or a few) bus cycles per unit, taken by the controller |

Important distinction: with polling the CPU is occupied for the whole elapsed time of the transfer (it spins), so the
"CPU cost" of programmed I/O is the elapsed time n × T_dev when the device is slow. With interrupts the CPU is
occupied only for the ISR time per unit; the rest is free for other processes. With DMA the CPU is occupied only for
S + C plus whatever it loses when the controller holds the bus.

### 3.2 Break-even block size (derivation)

Let c_int = CPU cycles per unit for interrupt-driven I/O, c_st = bus cycles per unit that the DMA controller takes from
the CPU (count as "lost" cycles), S = set-up cycles, C = completion cycles.

```
Interrupt-driven cost  = n × c_int
DMA cost               = S + C + n × c_st
DMA is cheaper  <=>  S + C + n·c_st < n·c_int  <=>  n > (S + C) / (c_int − c_st)
Smallest whole n at which DMA is strictly cheaper = ⌊(S + C)/(c_int − c_st)⌋ + 1
```

(If the ratio is an exact integer, n equal to that ratio is a tie, so add 1. If it is not an integer, take the ceiling;
the formula "floor + 1" handles both.) The same works against programmed I/O with c_pio per unit in place of c_int.

Assumptions: a fixed S and C per block, no cache effects, each DMA unit costs exactly c_st lost cycles. If the question
counts the stolen cycles as lost (as most do), keep c_st in; if it says "CPU cycles spent", the stolen cycles may not
be counted. Read the wording.

### 3.3 Worked example W6 — break-even

Interrupt-driven I/O costs 90 CPU cycles per byte. DMA costs 300 cycles set-up, 500 cycles completion, 1 stolen cycle
per byte.

```
n > (300 + 500) / (90 − 1) = 800/89 = 8.988...
n = 8 :  interrupt 720   DMA 808   -> interrupt cheaper
n = 9 :  interrupt 810   DMA 809   -> DMA cheaper
Smallest n = 9
```

Against programmed I/O at 30 cycles per byte: n > 800/29 = 27.59, so smallest n = 28 (28 × 30 = 840 > 828;
27 × 30 = 810 < 827).

### 3.4 Worked example W13 — CPU time left by interrupt-driven I/O

A device delivers one byte every 200 µs. The ISR (entry, body, return) takes 25 µs of CPU time per byte.

```
fraction of CPU time used by I/O = 25/200 = 12.5 %
fraction free for other work     = 87.5 %
Programmed I/O with busy-wait polling: the CPU is busy 100 % of the elapsed time, 0 % free.
```

Limit: if the ISR time exceeds the device inter-arrival time (say ISR 250 µs, device every 200 µs) the CPU cannot keep
up: bytes are lost (overrun) and the free fraction would be negative, which means the device must be buffered or
handled by DMA. That is a typical reason to choose DMA for fast devices.

---

## 4. The DMA controller

### 4.1 Registers and signals

```
              +---------------------------------------------+
   CPU  ----> |  Address register (AR)  : next memory address |
 (programs    |  Count register   (CR)  : units still to go   | ---- DREQ <---- Device
  it via      |  Control / status reg   : start, direction,   | ---- DACK ----> Device
  I/O ports)  |        mode, interrupt-enable, done, error    |
              |  Data buffer / data register (some designs)   |
              |  Control logic + bus-master logic             |
              +---------------------------------------------+
                  |  HOLD / BR (bus request)  --> CPU / arbiter
                  |  HLDA / BG (bus grant)    <-- CPU / arbiter
                  |  INTR                     --> interrupt controller / CPU
                  v  drives address, read/write control and data lines when bus master
```

| Part | Job | After each transferred unit |
|---|---|---|
| Address register | holds the memory address of the next unit | incremented (or decremented) by the unit size |
| Count (word/byte count) register | holds number of units remaining | decremented by 1 |
| Control / status register | direction (device to memory or memory to device), mode, start, interrupt-enable; status: busy, done, error | done bit set when count reaches 0 |
| Data buffer / register | holds one unit between device and memory; in some designs absent (direct fly-by transfer, section 6) | refilled |
| DREQ / DACK | device asks for a transfer; controller acknowledges and tells the device to put/take data | per unit |
| HOLD (BR) / HLDA (BG) | controller asks the CPU or arbiter for the bus; grant returns | per bus acquisition (per burst or per stolen cycle) |

Terminal count (TC): the event "count register reaches 0". It ends the transfer and normally raises the completion
interrupt.

### 4.2 Sizing the registers

```
Address register width  = ⌈log₂(number of addressable units in memory)⌉     (units = bytes if byte addressable,
                                                                             words if word addressable)
Count register width    ≥ ⌈log₂(largest block size in units)⌉   if the register is loaded with the block size
Block capacity of one programming = 2^(count width) units   (convention; see 4.3)
Bytes per programming   = 2^(count width) × bytes per unit
```

Examples (W16): word-addressable memory with 32 M words needs ⌈log₂(2^25)⌉ = 25 bits in the address register;
a byte-addressable 1 M memory needs 20 bits.

### 4.3 Count-register convention (state it)

Real controllers (the classic Intel 8237 is a standard example) store "number of transfers − 1", so an n-bit count
register covers 2^n transfers. Textbook-style GATE solutions normally use 2^n units per programming. A stricter reading
("the largest count value you can load is 2^n − 1") gives a different answer only when the block is an exact multiple
of 2^n units, see W7. When a question gives data size and register width and does not say, use 2^n units per
programming and write that assumption.

### 4.4 Multi-channel controllers

A controller can serve several devices; each channel has its own address and count registers, and the controller
resolves priority between channels (fixed or rotating) before asking the CPU for the bus. A GATE question, if it
mentions channels at all, only needs "each channel is independent; one grants the bus at a time".

---

## 5. The transfer sequence, and the CPU's role

### 5.1 Step list

```
1. CPU programs the controller (writes AR, CR, control: direction, start). One short I/O-port burst.
2. CPU goes back to useful work (another instruction stream or another process).
3. Device becomes ready and raises DREQ (a unit is available, or it can accept one).
4. Controller raises HOLD (bus request) to the CPU/arbiter.
5. CPU finishes its current bus cycle, releases the bus lines (tri-state), raises HLDA (bus grant).
6. Controller is now bus master: drives address (AR), control (read/write), and moves the unit(s).
   AR += unit, CR −= 1, per unit.
7. Burst/cycle stealing/transparent decides when the bus is given back (section 7).
8. When CR = 0: controller sets done, raises the completion interrupt.
9. CPU runs the ISR: checks status (OK or error), wakes the waiting process, may program the next block.
```

Timeline (single block, cycle stealing; "C" = CPU bus cycle, "D" = DMA bus cycle):

```
CPU:  setup  C C C C C C C C C C C C C C C C C ... ISR
DMA:                C              C              C   (one stolen cycle per device unit)
         |-- 1 --|     |-- 2 --|      |-- 3 --|
 1 = CPU programs controller   2 = unit transfers interleaved with CPU   3 = done -> interrupt
```

### 5.2 What the CPU does meanwhile

- Internal work that needs no bus (register-to-register, instructions and data already in the on-chip cache) can go on
  during a DMA bus tenure. Any instruction fetch or load/store that must reach main memory waits until the bus is back.
- In burst mode, therefore, the CPU is effectively stalled for the duration of the burst except for cache-resident work.
- In cycle stealing, the CPU is delayed by one bus cycle per stolen cycle, and otherwise runs normally.
- In transparent mode the CPU is never delayed, but DMA gets only the idle bus cycles.

### 5.3 Bus master: exactly one at a time

On a single shared bus, at any instant only one master drives the address and control lines. While the controller is
bus master the CPU is a (non-driving) bystander; it cannot also perform a bus transaction at the same time. The CPU
and the controller alternate. (The CPU may still execute operations that do not use the shared bus.)

### 5.4 Where interrupts still appear in a DMA world

| Situation | What happens |
|---|---|
| Normal completion (terminal count) | controller interrupts the CPU once per programmed block (the main one) |
| Error (device error, bus/parity error, invalid address) | error-status interrupt |
| Other devices (keyboard, timer, network, ...) | still interrupt the CPU during a DMA transfer; the CPU can recognise the interrupt at the next instruction boundary, but in burst mode a memory-bound ISR fetch waits until the burst ends |
| Per-unit device readiness | not an interrupt to the CPU: it is a DREQ to the DMA controller |

So DMA does not eliminate interrupts. It replaces "one interrupt per unit" by "one interrupt per block". For the
interrupt side (vectors, masking, priority) see [../01-INTERRUPT](../01-INTERRUPT/NOTES.md).

---

## 6. Data path organisations

### 6.1 Fly-by (direct) vs store-and-forward within the controller

```
Fly-by (one bus cycle per unit)           Two-cycle (device -> DMA buffer -> memory)
Device ======data bus======> Memory        Device ==cycle 1==> [DMA buffer] ==cycle 2==> Memory
(controller only drives address/control)    (both hops use the system bus, 2 cycles per unit)
```

In a numerical question, count the bus cycles per unit exactly as the question says ("each transfer takes two bus
cycles" means the effective cost is doubled). If it just says "one word per cycle", use one.

### 6.2 System organisations (conceptual)

| Organisation | Shape | Bus cycles per unit |
|---|---|---|
| Detached DMA on shared system bus | CPU, memory, DMA controller, devices all on one bus; device data goes device to controller to memory | 2 |
| DMA integrated with device interfaces | one controller (or several devices with DMA logic) between device and system bus | 1 |
| Separate I/O bus | devices on their own bus; controller bridges to the system bus | 1 on the system bus |

---

## 7. Transfer modes

### 7.1 Definitions

| Mode | Bus tenure | Effect on CPU | Throughput of DMA |
|---|---|---|---|
| Burst (block) mode | controller keeps the bus for the whole block (or until the device pauses it) | CPU can be locked out of memory for the whole burst | highest: arbitration overhead paid once per burst |
| Cycle stealing | controller takes the bus for one unit (one bus cycle or a very short group), releases it, repeats | CPU delayed by one bus cycle each time; longest stall = one cycle | lower: arbitration overhead paid per unit |
| Transparent (hidden) | controller uses only bus cycles that the CPU is not using (e.g. while the CPU decodes/executes with no memory access) | zero delay to CPU | lowest and not guaranteed; may starve if CPU is memory-busy |

In the Intel 8237 vocabulary: single transfer mode is cycle stealing, block transfer is burst, demand transfer mode
is "burst while the device keeps DREQ active, pause when it stops, resume when it returns". Demand mode is the
natural answer when a fast bus meets a slow device: you do not hold the bus while waiting for data.

### 7.2 Timelines (device much faster than needed to keep up, buffer available)

```
Burst:           CPU CPU CPU | D D D D D D D D | CPU CPU CPU        longest CPU stall = 8 bus cycles (+ arbitration)
Cycle stealing:  CPU CPU D CPU CPU D CPU CPU D CPU CPU D ...         longest CPU stall = 1 bus cycle (+ arbitration)
Transparent:     CPU CPU [D in an idle slot] CPU CPU [D] ...        CPU stall = 0, DMA waits for idle slots
```

### 7.3 Trade-off rule (what a statement-type question tests)

- Throughput of DMA: burst > cycle stealing, because per-grant overhead is paid once, not per unit
  (W5 below puts numbers on it).
- Worst-case CPU delay (latency to the CPU): cycle stealing < burst. A real-time control loop that cannot tolerate long
  stalls forbids long bursts (section 8.6 gives the max burst length).
- Average CPU slowdown is determined mainly by the fraction of bus cycles the DMA uses, not by the mode; mode shapes the
  distribution of the delay (many small vs few large).
- "In a stolen cycle, one unit (word) moves between device and memory": yes, that is the defining property of cycle stealing.
- Burst mode is only useful if data is ready: a slow device must have its buffer filled first (section 8.7).

---

## 8. The calculation toolkit

### 8.1 Symbols

```
f      CPU clock (Hz)               T = 1/f cycle time
f_b    bus (memory) cycle rate      T_b = 1/f_b      (if CPU cycle = bus cycle, f_b = f)
w      bytes moved per DMA bus cycle ("DMA unit")
k      bus cycles needed per unit (1 for fly-by, 2 for store-and-forward on the system bus)
p      fraction of bus (or CPU) cycles used by DMA
R      data rate of the device or DMA stream (bytes per second)
A      arbitration overhead in cycles per bus acquisition
```

### 8.2 Rate <-> fraction of cycles (HIGH-VALUE)

If the DMA takes a fraction p of the cycles and each stolen cycle moves w bytes (k = 1):

```
cycles used per second = p × f_b
R (bytes/s)            = p × f_b × w
R (bits/s)             = p × f_b × w × 8
inverse:  p = R / (f_b × w)             (k cycles per unit: p = k × R / (f_b × w))
```

Why: the bus offers f_b cycles every second; p of them belong to DMA; each moves w bytes.

Worked example W1. A 5 MHz processor; the DMA controller moves 2 bytes in one cycle by cycle stealing at regular
intervals; 1.2 % of cycles go to DMA.

```
cycles/s = 5 × 10^6 × 0.012 = 60,000
bytes/s  = 60,000 × 2       = 120,000
bits/s   = 120,000 × 8      = 960,000
```

Worked example W2 (inverse). A 25 MHz bus; a device streams 750,000 bytes/s; DMA moves 1 byte per bus cycle.

```
p = 750,000 / (25×10^6 × 1) = 0.03 -> 3 %
If each byte needed 2 bus cycles (store-and-forward): p = 6 %
```

Trap: the question gives "bits" for the answer but "bytes" per cycle; or "8-bit character" (w = 1 byte) versus
"8 bytes" (w = 8 bytes = 64 bits). Write w with its unit before you multiply.

### 8.3 Fraction of the bus consumed by a device (HIGH-VALUE)

```
Bus capacity  = f_b × (bytes per bus cycle)           = bytes/s the bus can move
p             = R / bus capacity                       (k = 1)
Equivalent:   cycles needed per second = R / w ; cycles offered per second = f_b ; p = (R/w)/f_b
```

Worked example W12 (detached DMA, k = 2). A device produces 300,000 bytes/s; each byte takes two bus cycles of
100 ns on a shared bus; cycle rate = 1/100 ns = 10^7 per second.

```
cycles needed per second = 300,000 × 2 = 600,000
p = 600,000 / 10,000,000 = 6 %
```

### 8.4 Wide DMA unit, narrow device

A device that gives 1 byte at a time can be assembled in the controller's data buffer; one bus cycle then moves w bytes.

Worked example W3. An 8-bit device gives 1.6 × 10^6 B/s; the DMA controller assembles 2 bytes and moves them in one
10 MHz bus cycle.

```
cycles needed per second = 1.6×10^6 / 2 = 800,000
p = 800,000 / 10×10^6 = 8 %        (without assembly, byte by byte: 16 %)
```

Rule: p depends on bytes per bus cycle, not on the device width. Check also that the buffer can hold w bytes while
waiting for the bus.

### 8.5 CPU slowdown (assumption-sensitive)

If the CPU needs the bus in every cycle and DMA takes fraction p of the cycles, the CPU gets (1 − p) of the cycles:

```
CPU execution time = T_alone / (1 − p)            slowdown factor 1/(1 − p)
```

Worked example W4. p = 8 %; a job needing 46 s alone: 46 / 0.92 = 50 s (factor 1.087).

Assumption: the CPU would use the bus in every cycle. If a cache absorbs most CPU accesses, the real slowdown is much
smaller (and transparent mode can steal almost nothing). State "assuming the CPU uses every cycle" in an answer.

### 8.6 Burst vs cycle stealing: time, overhead, worst stall (MEDIUM)

Let A be the non-productive cycles per bus acquisition (request, grant, release), N the units, T_b the bus cycle.

```
Burst: bus occupied  = (A + N) cycles         = (A + N) × T_b      one stall of that length
Stealing: bus occupied = N × (A + 1) cycles                         N stalls of (A + 1) cycles each
Worst-case CPU stall: burst (A + N) cycles ; stealing (A + 1) cycles
Max burst length under a stall limit L:  N_max = ⌊L / T_b⌋ − A
```

Worked example W5. A 2 KB block moved as 4-byte words: N = 512. T_b = 40 ns, A = 2.

```
Burst:    (2 + 512) × 40 ns = 20.56 µs, one stall of 20.56 µs
Stealing: 512 × (1 + 2) = 1536 cycles = 61.44 µs of bus time, longest stall 3 × 40 ns = 120 ns
```

Worked example W14 (stall limit). A control loop tolerates at most 2 µs of continuous bus denial; T_b = 50 ns, A = 3.

```
L/T_b = 2000/50 = 40 cycles ; N_max = 40 − 3 = 37 words
```

### 8.7 Device-limited transfers

Burst mode moves the block at bus speed only if the device has the data ready. A device that delivers one word per 1 µs
fills a 512-word buffer in 512 µs. Choices: (a) fill the controller's buffer first, then burst the whole buffer at bus speed
(CPU stall ≈ burst length only); (b) cycle stealing / demand mode, one cycle per word as it appears (CPU stalls are
short, total bus time larger because of A per word). Elapsed time of the whole block is ≥ N × device period either way;
the mode changes only how much of that time the CPU loses.

### 8.8 Set-up and completion overhead; combined CPU loss

Worked example W8. A 50 MHz system; a disk streams 6.4 × 10^6 B/s through DMA, 4 bytes per bus cycle, 8192-byte blocks;
set-up costs 2000 CPU cycles per block and completion (interrupt and ISR) 3000 cycles per block.

```
stolen cycles: 6.4×10^6 / 4 = 1.6×10^6 per s  -> 1.6×10^6 / 50×10^6 = 3.2 %
blocks per second: 6.4×10^6 / 8192 = 781.25
overhead cycles per second: 781.25 × (2000 + 3000) = 3,906,250 -> 7.8125 %
total CPU capacity lost = 3.2 + 7.8125 = 11.0125 %
```

Set-up and completion are real CPU work; stolen cycles are bus cycles the CPU cannot use. The two add up as a loss of
CPU capacity only under the assumption that the CPU would otherwise use every bus cycle; state that assumption.

### 8.9 Count-register capacity and number of bus acquisitions (HIGH-VALUE)

The controller can transfer at most 2^m units per programming (m = count register width; convention of 4.3). When the
count reaches 0 it stops, interrupts the CPU, and the CPU must reprogram it for the next piece.

```
bytes per programming   = 2^m × (bytes per unit)
programmings needed     = ⌈ total bytes / (2^m × bytes per unit) ⌉
```

Number of times the controller must obtain the bus from the processor depends on the mode:

| Mode (assumption) | Bus acquisitions |
|---|---|
| Burst mode, one burst per programming | = programmings needed = ⌈total / capacity⌉. This is the minimum |
| Cycle stealing, one unit per acquisition | = number of units = total bytes / bytes per unit |
| Transparent | one acquisition per idle slot; not a fixed number |

"Minimum number of times" therefore pairs with burst: each acquisition transfers a full count-register's worth.

Worked example W7. Byte-addressable memory; the controller moves one byte per transfer; count register 16 bits;
file 1000 KB.

```
total bytes = 1000 × 1024 = 1,024,000
capacity    = 2^16 = 65,536 bytes per programming
ratio       = 15.625  -> ⌈15.625⌉ = 16 bursts (last one partial)
```

Variant: the controller moves 4-byte words (count register still 16 bits, counts words):

```
capacity = 65,536 × 4 = 262,144 bytes ; 1,024,000 / 262,144 = 3.906 -> 4
```

Convention edge: file 256 KB = 262,144 bytes, one byte per transfer. With 2^16 units per programming: exactly 4. With
the stricter "max loadable 2^16 − 1": ⌈262,144 / 65,535⌉ = 5. Always write the convention.

Trap: using the word-count when the capacity is in bytes, forgetting KB = 1024 bytes, rounding down instead of up, or
treating "address register" size as a limit on block size.

### 8.10 Step-by-step GATE procedure

```
1. Identify the unit moved per DMA cycle (bits or bytes) and bus cycles per unit (k).
2. Identify the cycle rate: CPU clock if "% of processor cycles"; bus clock if "% of bus cycles".
3. Fraction p given -> R = p·f·w/k . Rate given -> p = k·R/(f·w).
4. Convert units last: bytes -> bits (×8), cycles -> seconds (× T), KB -> bytes (× 1024).
5. For block problems add S, C, and A overhead; count the stolen cycles if the question calls them lost.
6. For register / acquisition counts use ceilings and state the 2^m convention.
7. Sanity check: p must be ≤ 1 (otherwise the bus cannot sustain the device).
```

### 8.11 Additional worked example — maximum sustainable device rate

A 50 MHz bus, 4 bytes per cycle. If the DMA could use every bus cycle the bus peak is 200 × 10^6 B/s. With arbitration
cost A = 1 cycle per acquisition: cycle stealing gives 1 unit per 2 cycles, so 100 × 10^6 B/s; a burst of 16 units gives
16 units per 17 cycles = 188.2 × 10^6 B/s. A device faster than the figure for the chosen mode cannot be sustained in that mode.

---

## 9. Bus arbitration and bus transfer mechanics

### 9.1 Vocabulary

- Bus master: the unit that currently initiates transfers and drives address/control lines. Slave: responds.
- Bus arbitration: deciding which requesting master gets the bus next. CPU, DMA controllers and other bus-capable
  devices are masters; memory is a slave.
- DMA usually has higher bus priority than the CPU: a device cannot wait indefinitely or data is lost; the CPU can be
  delayed a little. When nothing else wants the bus the CPU is the default master.

### 9.2 Centralised arbitration schemes

```
Daisy chain                       Polling                           Independent request / grant
CPU/arbiter BG -> D1 -> D2 -> D3  Arbiter polls with a counter       Each device has its own BR_i, BG_i
BR is a shared wired-OR line      (log₂N poll lines) until the       lines to the central arbiter
                                  requester recognises its number
```

| Scheme | Lines (typical textbook counts; the question's count wins) | Priority | Speed | Weak point |
|---|---|---|---|---|
| Daisy chain | 3 (BR shared, BG daisy-chained, BBSY), independent of N | fixed by position: nearest the arbiter wins | slowest: grant ripples through up to N − 1 devices | starvation of far devices; a failed device breaks the chain; adding devices lengthens the delay |
| Polling | BR + BBSY + ⌈log₂ N⌉ poll-address lines | software/hardware programmable: poll order or rotating start | medium: polling takes up to N poll steps | more lines than daisy chain; delay of polling |
| Independent request/grant | 2N (N request + N grant) plus busy | any policy in the arbiter: fixed, rotating, round-robin | fastest: arbiter sees all requests at once | most wiring; the arbiter is complex |
| Distributed (self-selection) | no central arbiter; each requester drives its ID on shared open-collector arbitration lines (about ⌈log₂ N⌉ ID lines plus start/busy; text-dependent) | highest ID wins | one arbitration phase | fixed-priority starvation unless IDs rotate; text-dependent line counts |

Fairness. Fixed priority gives starvation to the lowest priority device under constant load. Rotating or round-robin
priority (arbiter, or polling counter that restarts after the last winner) gives bounded waiting.

Worked example W10 (daisy-chain delay). 8 devices; each device (including the one that finally takes it) adds 25 ns when
passing the grant. The grant reaches device 8 after 8 × 25 ns = 200 ns, and device 1 after 25 ns. Some texts count only the
devices passed through (k − 1 stages); state the count you use. The delay grows linearly with position, which is why a
daisy chain is the slowest scheme.

Worked example W11 (line count, N = 16): daisy chain 3 lines; polling 4 poll lines + BR + BBSY = 6; independent 2 × 16 = 32 request/grant lines.

Daisy chain here (bus grant) is the same idea as the interrupt-acknowledge daisy chain: see
[../01-INTERRUPT](../01-INTERRUPT/NOTES.md) for the interrupt-priority use of it. Both rely on "closest device has
highest priority" and on the grant being passed on by devices that did not ask.

### 9.3 Sequence of a bus grant (DMA example)

```
1. Controller asserts BR (HOLD).
2. Arbiter / CPU completes the current bus cycle, then asserts BG (HLDA); the grant is passed down the chain.
3. The requesting master asserts BBSY (bus busy) when the bus becomes free and starts using it.
4. When done, the master releases BBSY (and BR); the arbiter may grant again.
```

### 9.4 Synchronous vs asynchronous transfer

| | Synchronous bus | Asynchronous bus |
|---|---|---|
| Timing | every action is tied to a common clock; fixed number of cycles per transfer | master and slave handshake; no common clock |
| Speed | set by the slowest device: insert wait states for slow slaves | adapts to each slave's speed |
| Hardware | simpler | more complex control lines |
| Limit | clock skew with long buses | handshake delay |

Full (interlocked) four-phase handshake for a read:

```
1. Master puts address, asserts REQ                    (edge 1 propagates to slave)
2. Slave decodes, reads memory, puts data, asserts ACK (edge 2 propagates to master)
3. Master latches data, deasserts REQ                  (edge 3)
4. Slave deasserts ACK, bus is free                    (edge 4)
Time per transfer (no overlap) = 4 × t_prop + t_access
```

Worked example. t_prop = 5 ns, t_access = 40 ns: 4 × 5 + 40 = 60 ns per word, 4 bytes / 60 ns = 66.7 × 10^6 B/s
(decimal MB/s). Here "4 × t_prop" is a model; if a question lists the edges differently, add the listed delays.

### 9.5 Bus bandwidth

```
Peak bandwidth      = (bus width in bytes) × (bus clock)                  [one transfer per cycle]
Sustained bandwidth = bytes per transaction / time per transaction        [includes address, wait, turnaround cycles]
Wait states: a slave needing t_access on a clock T needs ⌈t_access / T⌉ cycles for the data phase
```

Worked examples.

- Synchronous 100 MHz bus, 32-bit data, separate address lines: peak = 4 × 10^8 B/s = 400 × 10^6 B/s.
- The same bus multiplexed (address and data share lines), a burst of 8 words: 1 address cycle + 8 data cycles = 9 cycles of
  10 ns: sustained = 32 bytes / 90 ns = 355.56 × 10^6 B/s (89 % of peak). A non-burst single word transfer would take
  2 cycles (address, data): 4 B / 20 ns = 200 × 10^6 B/s.
- 50 MHz bus (T = 20 ns), memory access 70 ns: ⌈70/20⌉ = 4 cycles per word: 4 B / 80 ns = 50 × 10^6 B/s versus a 200 × 10^6 B/s peak. With
  access 45 ns the data phase is ⌈45/20⌉ = 3 cycles.

### 9.6 Multiplexed vs separate buses

Multiplexing (address and data on the same lines at different times) saves pins and wiring and costs an extra cycle per
transaction unless amortised over a burst. This is the reason sustained bandwidth < peak, and why burst DMA raises
bus efficiency even on a multiplexed bus.

---

## 10. DMA with caches and virtual memory

### 10.1 Coherence: the stale-data problem (concept level)

DMA reads and writes main memory directly and normally does not look into the CPU cache. Two failures:

```
Device -> memory (input)   : memory block changes, a cached copy of an old version stays valid-looking
                             -> CPU reads stale data.   Fix: invalidate those cache lines before the CPU reads them.
Memory -> device (output)  : with write-back, the newest data sits dirty in the cache, memory is old
                             -> device reads old data.  Fix: flush (write back) dirty lines before starting DMA.
```

| Remedy | Notes |
|---|---|
| Write-through cache | solves the output case (memory already current, assuming the write buffer is drained); does not solve the input case |
| Flush / clean before output DMA; invalidate before or after input DMA | done by the driver; costs time proportional to the buffer size |
| Mark the I/O buffer non-cacheable | simple, slow for the CPU |
| Hardware coherence (bus snooping, coherent DMA) | the cache sees the DMA writes and invalidates or updates its copy; no software step |

### 10.2 Hit under DMA

A cache-resident working set lets the CPU keep executing during a DMA burst (it does not need the bus), so burst mode
costs less than "CPU stalled" suggests. The CPU, however, cannot service a miss until the bus returns.

### 10.3 Virtual memory (two lines)

DMA controllers work with physical addresses; the OS must give the controller the physical frame addresses, and keep
(pin) the buffer's pages in memory until the transfer ends; a buffer that crosses non-contiguous frames needs one
transfer per contiguous piece (or scatter-gather). Details belong to
[../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY](../../../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY).

---

## 11. Programmed I/O vs interrupt-driven I/O vs DMA

| Aspect | Programmed I/O (polling) | Interrupt-driven I/O | DMA |
|---|---|---|---|
| Who moves each unit | CPU | CPU (inside ISR) | DMA controller |
| CPU busy-waits | yes (whole transfer) | no | no |
| CPU work per unit | high | high (interrupt overhead per unit) | none |
| CPU work per block | ~0 | ~0 | S + C (small, fixed) |
| Interrupts | none | one per unit | one per block (plus errors) |
| Bus use | CPU's transfers | CPU's transfers | controller steals or bursts |
| Hardware | simplest | interrupt logic | controller with AR, CR, bus-master logic |
| Best for | very slow, rare, simple devices; tiny transfers | slow or sporadic devices where responsiveness matters | bulk and high-speed transfers (disk, network, graphics) |

Decision rules:

1. Bulk data from a fast device (disk to memory): DMA gives the highest throughput and leaves the CPU free.
2. Interrupt-driven vs programmed (polling) I/O on CPU utilisation: with a slow device the interrupt-driven CPU is free
   between events (section 3.4), while a polling CPU spins; so interrupt-driven gives more useful CPU time. The
   comparison reverses only in special cases (a device that is almost always ready, or interrupt overhead larger than the
   event spacing). Read the stated assumptions before accepting a "better CPU utilisation" claim either way.
3. Very small blocks: the fixed S + C of DMA can exceed the savings: use break-even n* from 3.2.
4. Real-time with hard stall limits: prefer cycle stealing or short bursts (8.6).
5. If the device rate exceeds what interrupt-per-byte can sustain (ISR time > inter-arrival time), DMA is required, not optional.

---

## 12. PYQ patterns (methods only; no answers)

Source: [questions.md](../../../13-PYQ-TOPIC-MAPPING/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/questions.md); see also [PYQ.md](PYQ.md).
The mapping marks every answer "VERIFICATION REQUIRED"; solve each from the paper.

| # | Pattern | Recognise it by | Recipe | Trap |
|---|---|---|---|---|
| 1 | Data rate from processor clock and percentage of cycles (2024 CS2, 2021 CS-2) | "x MHz processor", "y % of cycles used for DMA", "z bytes/bits per cycle", asks bits per second | 8.2: cycles/s = f × y; × unit size; convert to bits if asked | bytes vs bits; "8-bit character" vs "8 bytes"; percentage as 1/100 or 1/1000; "bits per second" vs "bytes per second" |
| 2 | Minimum number of bus takeovers for a file (2016 CS-1) | count register width, file size in KB, byte-addressable memory | 8.9: total bytes / (2^m × unit) rounded up; state 2^m convention | KB = 1024; unit size (byte vs word); rounding down; confusing bus acquisitions with registers |
| 3 | True/false statements on DMA modes, interrupt styles, I/O methods (2024 CS1) | "which statement is FALSE", mixes cycle stealing, burst, programmed vs interrupt I/O, vectored vs non-vectored | go option by option with sections 7, 11 and the interrupt sibling; test each against definitions and the conditional-ness of "better CPU utilisation" | words like "always"; mixing DMA throughput (bus view) with CPU utilisation (CPU view) |
| 4 | Which mechanism for bulk data (2022 CS) | "bulk transfer", "highest throughput", options list DMA, interrupt, polling, programmed | section 11 decision rules | confusing "lowest CPU involvement" with "simplest" |
| 5 | Multi-statement truth on daisy chaining, vectored interrupts, polling and DMA bus mastership (2020 CS) | four roman-numeral statements spanning interrupts and DMA | check each statement separately: daisy chain priority (9.2 and sibling), polling definition, vectored interrupt (sibling), bus master exclusivity (5.3) | treating a statement as true because it sounds like a related true statement; DMA vs CPU simultaneous master |

Note on partial overlap: the 2020 entry is half interrupt-owned; treat it as a joint DMA/interrupt skill.

---

## 13. Traps and misconceptions

1. "DMA removes all interrupts." It removes per-unit interrupts, not the completion (and error) interrupt.
2. "Cycle stealing means the CPU is stopped." Only for the stolen cycles; the CPU runs between them.
3. "Burst mode is always better." It maximises DMA throughput but raises the worst-case CPU stall; unusable under hard latency limits.
4. "Transparent mode is free and fast." It never delays the CPU, but gets only leftover bus cycles, so DMA throughput is not guaranteed.
5. "CPU and DMA controller can be bus masters at once." On a shared bus only one drives the bus at a time.
6. Bytes vs bits (×8) at the end; cycles per unit k (1 vs 2); word width w vs device width.
7. Percent of "processor cycles" vs of "bus cycles" (same only if CPU cycle = bus cycle).
8. KB vs bytes in the count-register problem, and floor instead of ceiling.
9. Address register width depends on memory size, not on transfer size; count register width depends on block size.
10. Write-through cache fixes only the output direction; input still needs invalidation.
11. Forgetting that DMA uses physical addresses.
12. Daisy chain priority is fixed by wiring position, not by device speed or number.

---

## 14. Edge cases and assumptions to state

- Cycle assumption: CPU cycle = bus cycle? Does the CPU use the bus in every cycle?
- Unit size and units per cycle; k = 1 or 2.
- Count-register convention (2^m units vs 2^m − 1).
- Arbitration overhead A included or ignored.
- Whether setup/completion cycles and stolen cycles are counted as "CPU cycles" in a break-even question.
- Decimal vs binary prefixes for rates ("MB/s"); the clock in MHz is decimal.
- Device buffering: does the controller have a buffer large enough for the assembled unit or the burst?
- Cache: are CPU accesses hitting in cache (so stalls are smaller)?
- Whether "percentage used for DMA" refers to the whole transfer duration or an average.

---

## 15. Connections to other COA topics

- [../01-INTERRUPT](../01-INTERRUPT/NOTES.md): completion interrupt, polling vs interrupts, daisy-chain priority, memory-mapped vs isolated I/O (how the CPU writes DMA registers).
- [../05-MEMORY-INTERFACING-AND-HIERARCHY](../../05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/NOTES.md): bus/memory bandwidth, cache coherence.
- [../07-INSTRUCTION-PIPELINING](../../07-INSTRUCTION-PIPELINING/NOTES.md): bus stall delays a memory stage similarly to a structural hazard (conceptual only).
- OS: I/O scheduling, buffering, pinned pages, device drivers ([../../../08-OPERATING-SYSTEMS](../../../08-OPERATING-SYSTEMS)).

---

## 16. Existing practice coverage map

Existing file: [practice.md](../../../14-PRACTICE-QUESTIONS/TOPIC-WISE/03-COMPUTER-ORGANIZATION-ARCHITECTURE/06-IO-INTERFACE/02-DMA/practice.md).

| Q# | Section | Skill |
|---|---|---|
| 1 | 2, 5.1, 6 | data path in DMA bypasses CPU registers |
| 2 | 7.1 | cycle stealing definition |
| 3 | 4.2 | address register width from memory size |
| 4 | 3, 5.4, 7.1, 11 | burst vs stealing, PIO uses CPU, completion interrupt allowed |
| 5 | 8.2 | bytes/s from clock, fraction, bytes per cycle |
| 6 | 5.1 | CPU programs controller via command registers |
| 7 | 8.2, 8.3 | fraction of cycles used and remaining for CPU |
| 8 | 7.1, 7.3 | burst vs stealing properties |
| 9 | 3.2, 8.8 | set-up/completion overhead; cost ratio |
| 10 | 5.3, 7.1, 7.3 | transparent, long burst stall, bus master, stealing definition |
| 11 | 8.3 | fraction of bus consumed by a device |
| 12 | 7.3, 8.6 | max continuous stall, burst vs stealing |

---

## 17. Self-check

1. List the DMA controller's registers and say what each does after every unit.
2. Write the nine-step DMA sequence in order and mark where the interrupt occurs.
3. What is the worst-case CPU stall in burst mode and in cycle stealing, for N units and arbitration A?
4. A device gives R bytes/s, bus f_b cycles/s moves w bytes per cycle: what fraction of the bus does it use?
5. What is a transparent DMA transfer and why can its throughput not be guaranteed?
6. Compute the number of bursts for a file of F KB with an m-bit count register and u-byte units.
7. Derive the break-even block size between interrupt-driven I/O and DMA.
8. Why is p ≤ 1 a feasibility test for a device?
9. Compare daisy chain, polling, independent request and distributed arbitration on lines, priority and speed.
10. How do DMA writes make a cached copy stale, and what two actions fix input and output directions?
11. Difference between peak and sustained bus bandwidth; where wait states enter.
12. Why does DMA need physical addresses and pinned pages?

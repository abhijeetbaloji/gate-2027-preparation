# I/O Interface and Interrupts — Complete Notes

Topic path: `03-COMPUTER-ORGANIZATION-ARCHITECTURE / 06-IO-INTERFACE / 01-INTERRUPT`

This folder is the home of **I/O-interface fundamentals** (I/O module, ports, memory-mapped vs isolated I/O,
programmed / interrupt-driven transfer, CPU-time numerics) and of the **interrupt mechanism** (recognition,
state saving, vectors, priority, nesting, exceptions). DMA and bus arbitration live in the sibling folder
[`../02-DMA`](../02-DMA/NOTES.md); this file only previews DMA where a comparison is needed.

---

## 0. Where this fits

**Syllabus line (COA):** "… I/O interface (interrupt and DMA) …".

| Direction | What |
|---|---|
| Prerequisites | Instruction cycle (fetch–decode–execute) and registers (PC, flags, SP) → [`../../01-INSTRUCTION-SET`](../../01-INSTRUCTION-SET); micro-operations (MAR, MBR) → [`../../04-DESIGN-OF-CONTROL-UNIT`](../../04-DESIGN-OF-CONTROL-UNIT); address-bit counting (2ⁿ, ⌈log₂⌉) → [`../../05-MEMORY-INTERFACING-AND-HIERARCHY`](../../05-MEMORY-INTERFACING-AND-HIERARCHY) |
| Siblings | DMA, cycle stealing, bus arbitration → [`../02-DMA`](../02-DMA/NOTES.md) |
| Depends on this topic | Pipelining and precise interrupts → [`../../07-INSTRUCTION-PIPELINING`](../../07-INSTRUCTION-PIPELINING), [`../../08-PIPELINE-HAZARDS`](../../08-PIPELINE-HAZARDS); OS system calls, processes, I/O scheduling → [`../../../08-OPERATING-SYSTEMS/01-SYSTEM-CALLS`](../../../08-OPERATING-SYSTEMS/01-SYSTEM-CALLS), [`../../../08-OPERATING-SYSTEMS/02-PROCESSES`](../../../08-OPERATING-SYSTEMS/02-PROCESSES), [`../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING`](../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING) |

**Conventions used throughout** (COA-folder-wide):

- 1 K = 2¹⁰, 1 M = 2²⁰, 1 G = 2³⁰ for memory/address sizes. For **device data rates and clock rates** the
  problems here always give plain numbers (bytes/s, Hz); if a question writes "MB/s" without comment, state
  whether you used 10⁶ or 2²⁰ and note that the final answer changes by ≈ 4.9 %.
- Memory is **byte-addressable** unless a problem says otherwise; addresses are decimal unless written `0x…`.
- CPU time consumed by an activity at rate r (events/s) with cost c (s/event) is the fraction **r × c** of
  one second.
- "Priority number" direction (larger = higher, or smaller = higher) is **always read from the question**.

---

## 0.1 Evidence snapshot (what drives the depth)

Counted from the mapping file (`questions.md`, 13 entries, 2007–2026 — see [`PYQ.md`](PYQ.md)): 10 distinct
questions once the four 2013 booklet copies are merged; of these 7 are on-topic COA interrupt questions, 2 are
only partly COA (OS-flavoured) and 1 is misfiled (thread/shared-variable concurrency). One extra interrupt-sequence question (2025)
and one "which I/O method gives highest throughput" question (2022) were found in the paper text extraction
but are **not** in the mapping; they are mentioned for completeness only.

| Section | Rating | Evidence |
|---|---|---|
| §6 Interrupt recognition, ordering of events, return address | **HIGH-VALUE** | Mapped questions on "when is the interrupt serviced", "order of events after a device interrupts", "which return address is pushed", and a micro-operation sequence for interrupt entry; the unmapped 2025 paper repeats the ordering pattern |
| §5 CPU-time numerics (polling vs interrupt) | **HIGH-VALUE** | One mapped NAT with exact polling/interrupt fractions; existing practice has 6 of 14 questions of this type (Q6, Q8, Q11, Q12, Q13, Q14) |
| §8–§10 Vectored / non-vectored, daisy chain, priority, nesting | **HIGH-VALUE** | Newest mapped question (2026) is a two-statement true/false on exactly these; a 2011 question on which source has highest priority; existing practice Q1–Q5, Q9, Q10 |
| §2–§4 I/O module, memory-mapped vs isolated, transfer techniques | MEDIUM | Prerequisite for the numerics; one mapped question on synchronous vs asynchronous I/O; a 2022 PYQ (unmapped) compares I/O techniques; not directly numerical in the mapping |
| §11 Exceptions, traps, faults | MEDIUM | Needed to answer "what return address / does context switch always happen" style questions (2024 CS2 mapped entry, partly OS) |
| §12 Pipeline / cache interplay | LOW | Concept-level only; no mapped question; needed to link topics |
| §13 OS bridge | LOW | Only to explain 2008 / 2024 mapped OS-flavoured entries |

---

## 1. The big picture

A CPU executes ~10⁹ instructions per second. A keyboard delivers ~10 key presses per second. A disk delivers
data in bursts after milliseconds of positioning. Somebody must **notice that a device needs attention** and
**move the data**. The three possible answers are the three transfer techniques of §4:

```
 Who notices?                         Who moves the data?            Technique
 ------------------------------------ ------------------------------ ----------------------
 CPU asks repeatedly (polling)        CPU, one word at a time        Programmed I/O
 Device taps CPU on the shoulder      CPU, one word at a time        Interrupt-driven I/O
 Device taps the DMA controller       DMA controller, whole block    DMA (see ../02-DMA)
```

**Analogy.** You are cooking (the main program). *Polling* = you walk to the oven every 2 minutes to look.
*Interrupt* = you set a timer that rings; when it does you stop chopping, **remember where you were**, take the
tray out, and return to chopping exactly where you were. *DMA* = a helper takes the tray out and puts it on the
table; you are only told when everything is done.

The rest of this file is the engineering behind the timer: what the "tap" looks like electrically, what the CPU
saves, how it finds the right helper routine, what happens when several devices tap at once, and what all this
costs in CPU time.

---

## 2. The I/O module (device controller / interface)

A CPU never talks to a disk head or a keyboard matrix directly. Every device sits behind an **I/O module**
(also called device controller or interface), which hides electrical and timing details and presents a few
registers to the CPU.

```
              system bus  (address | data | control)
   ---------------+-------------------------------+---------------
                  |                               |
          +-------+---------------+               |
          |  I/O MODULE           |               |
          |  address decoder  <---+ (port address)|
          |  +-------------+      |               |
          |  | STATUS reg  | ready / busy / error flags
          |  | CONTROL reg | start, direction, enable-interrupt bit
          |  | DATA reg(s) | one word of buffered data (or a FIFO)
          |  +-------------+      |
          |  interrupt-request line ---------> to CPU / interrupt controller
          +-------+---------------+
                  |
              DEVICE (keyboard, printer, disk drive, sensor …)
```

Terminology:

| Term | Meaning |
|---|---|
| **Port** | One addressable register (or small group) in an I/O module. "Device has 4 ports" = 4 register addresses. |
| **Status register** | Read-only flags: READY/DONE, BUSY, ERROR. Polling reads this. |
| **Control (command) register** | Written by the CPU: start operation, direction, **interrupt-enable (IE) bit**, mode. |
| **Data register / buffer** | Holds the word being transferred. Fast devices have FIFOs. |
| **Device driver** | OS software that knows these registers. (The OS bridge, §13.) |
| **Speed mismatch** | CPU ns-scale vs device μs–ms-scale (or longer). The *buffer* in the module absorbs the mismatch; the *handshake* (READY/ACK) coordinates it. |

**Handshake for an input device (read):**

```
 device puts data in DATA reg -> sets READY in STATUS
 CPU reads DATA reg            -> module clears READY (device may produce the next item)
```
If the CPU is late and the device produces again before the old value is read, the old value is **overrun**
(lost). Overrun is the failure that sets the *deadline* in polling and interrupt problems (§5.5, §7.3).

---

## 3. Addressing I/O ports: memory-mapped vs isolated (port-mapped) I/O

How does the CPU name a port?

### 3.1 Memory-mapped I/O

Device registers occupy **part of the ordinary memory address space**. The CPU reads/writes them with the
ordinary `LOAD`/`STORE` instructions; the address decoder routes those addresses to I/O modules instead of RAM.

```
  address space (32-bit, byte addressable)
  0x0000_0000 +---------------------+
              |        RAM          |
              +---------------------+
  0xFFFF_F000 |  I/O registers 4 KB |  <- loads/stores here go to devices
  0xFFFF_FFFF +---------------------+
```

- **No special I/O instructions**; any addressing mode and any ALU-memory instruction works (e.g. test a
  status bit directly with a memory-operand instruction).
- **Cost: address space.** Every port address is an address that RAM cannot use.
- Caches must **not** cache these addresses (a cached status value would never change) → the region is
  marked uncacheable (link: cache folder).

### 3.2 Isolated I/O (port-mapped)

I/O ports have a **separate address space**, reached with special instructions (`IN port`, `OUT port`) and
distinguished on the bus by a control line (e.g. an M/IO̅ signal).

```
  memory space:  2^32 bytes of RAM only          I/O space: e.g. 2^16 ports
  access by LOAD / STORE                         access by IN / OUT   (control line says "I/O")
```

- Memory address space is **not** reduced.
- Needs extra instructions and a bus control signal; fewer addressing modes for I/O; privileged in most
  systems (user programs cannot execute `IN`/`OUT`).

### 3.3 Comparison

| Aspect | Memory-mapped | Isolated |
|---|---|---|
| Instructions | ordinary load/store/ALU-memory | special IN/OUT |
| RAM addresses available | reduced by the I/O region | unchanged |
| Extra control signal | no | yes (memory vs I/O) |
| Instruction-set size | smaller | larger |
| Programming convenience | high | lower |
| Cache | I/O region must be marked uncacheable | not an issue (separate space) |

### 3.4 Address-bit counting (two recurring numerics)

**Reserved RAM.** If the I/O window is W bytes, usable RAM addresses = 2ⁿ − W.

**Selecting a port.** If a system has D controllers and each decodes an aligned block of R ports (R a power of
two), the port address needs `⌈log₂ D⌉ + log₂ R` bits: high bits choose the controller, low bits choose the
register. *Aligned blocks matter*: 40 controllers × 6 registers is **not** ⌈log₂ 240⌉ = 8 bits if each controller
occupies an 8-port aligned block (that needs ⌈log₂ 40⌉ + 3 = 9 bits).

### Worked example E1 (memory-mapped cost)
A 32-bit byte-addressable CPU reserves the top 4 KB for I/O.
Usable RAM addresses = 2³² − 2¹² = 4 294 967 296 − 4096 = **4 294 963 200 bytes**, i.e. 4 GB − 4 KB.

### Worked example E2 (port bits)
32 controllers, each with 8 aligned registers: device-select bits = log₂ 32 = 5, register bits = 3, so **8 bits**
(256 ports). Port address = `[5-bit device][3-bit register]`.

---

## 4. The three data-transfer techniques

### 4.1 Programmed I/O (polling, busy-wait)

The CPU runs a loop that reads the status register until READY, then moves one word.

```
 wait:  IN   R0, STATUS       ; read status port
        AND  R0, #READY_BIT   ; isolate the flag
        JZ   wait             ; not ready -> loop
        IN   R1, DATA         ; ready -> take the word
        STORE R1, [buffer++]
```

- CPU is **100 % occupied** for the whole wait. Simple, no hardware support beyond the registers.
- Variant: **interval polling** — the main program checks the device every T_poll (e.g. from a timer).
  Cheaper than a busy loop, but adds *latency up to T_poll* and wastes the polls that find nothing.

**Busy-wait cost example E3.** A printer needs 2 ms per character. The wait loop is 6 instructions at CPI 1.5 on
a 1 GHz CPU → one pass = 6 × 1.5 ns = 9 ns. Passes ≈ 2 ms / 9 ns = **≈ 222 222 passes** wasted per character.
(For a 1 GHz CPU that is about 2 million clock cycles doing nothing useful.)

### 4.2 Interrupt-driven I/O

The CPU starts the operation (writes the control register with IE = 1) and **continues with other work**. When
READY is set, the module raises an **interrupt request (IRQ)**. The CPU finishes its current instruction,
saves the state, runs an **interrupt service routine (ISR)** that moves one word and acknowledges the device, and
returns.

```
 time ->
 main program  ======|==========================|==========
 ISR                 [entry][ move 1 word ][exit]
                     ^ IRQ                      ^ resume at saved PC
```
No time is wasted waiting, but **every word costs a full entry/exit overhead** (§7).

### 4.3 DMA (preview; full treatment in ../02-DMA)

A DMA controller becomes bus master and moves a whole block between device and memory without executing
CPU instructions. The CPU spends time only to **program the transfer (setup)** and to **handle one completion
interrupt per block**.

### 4.4 Comparison table

| | Programmed I/O (busy wait) | Interval polling | Interrupt-driven | DMA |
|---|---|---|---|---|
| Who detects readiness | CPU, continuously | CPU, periodically | Device (IRQ) | Device → DMA controller |
| Who moves each word | CPU | CPU | CPU (in ISR) | DMA controller |
| CPU use while device is idle | 100 % | polls × cost | 0 | 0 |
| CPU use per transferred word | poll + move | poll(s) + move | full interrupt overhead + move | ≈ 0 (setup+completion amortised over the block) |
| Extra hardware | none | timer | interrupt line/controller | DMA controller |
| Best for | very fast, predictable devices; tiny systems | slow devices with relaxed latency | slow/bursty devices | high-rate block devices (disk, network) |

Key fact to remember: **interrupt-driven I/O is not always cheaper than polling**. For a device that is always
busy, a poll that finds data ready costs less than a full interrupt entry+exit; for a device that is idle most of
the time, polls that find nothing are pure waste while an interrupt costs nothing until something happens
(see E5, E6).

---

## 5. CPU-time numerics — the fraction family

This is the most computational part of the topic. All formulas come from one idea:

> CPU fraction consumed by an activity = (events per second) × (CPU seconds per event).

### 5.1 Polling cost

Let the CPU poll at rate f_p (polls/s), each poll costing c_p seconds. If events arrive at rate λ and each
event needs c_e seconds of processing once found:

```
 polling fraction  = f_p × c_p  +  λ × c_e
 (polls that find nothing cost c_p; the processing is paid only when an event is found)
```

If the poll interval is T_p = 1/f_p: `f_p × c_p = c_p / T_p`.

**Minimum polling rate (no data loss).** If the device buffers B items and produces at rate λ items/s, the buffer
fills in B/λ seconds; to avoid overrun the CPU must poll at least every B/λ:

```
 T_p ≤ B / λ        f_p ≥ λ / B
```
With a one-item buffer (B = 1) this says: poll at least as fast as events arrive.

### 5.2 Interrupt-driven cost

```
 interrupt fraction = λ × c_i      where c_i = entry + save + ISR body + restore + return (all CPU time per interrupt)
```
Only events cost anything; idle time costs nothing.

### 5.3 DMA cost (preview)

For blocks of S bytes and device rate R bytes/s: blocks/s = R / S, and fraction = (R / S) × (c_setup + c_complete).

### 5.4 Maximum sustainable rate

If the CPU may spend at most a fraction β on this activity, the largest event rate is

```
 λ_max = β / c        (β = 1 if the CPU can be fully devoted; c = total CPU time per event)
```

For polling where each poll collects one item: c = c_p + c_e (if the poll always finds data).

### 5.5 Crossover rate

Polling at fixed f_p vs interrupts: they cost the same when `f_p × c_p = λ × (c_i − c_e)`
(the processing c_e is common to both and cancels; in the problem state "ignore processing").

```
 λ* = f_p × c_p / (c_i − c_e)        interrupts are cheaper for λ < λ*, polling cheaper for λ > λ*
```

### 5.6 GATE solving procedure

1. Convert **everything to seconds per second** (or μs per second). Write every cost as a number of seconds.
2. Identify the **rate** of each activity (events/s, polls/s). Poll rate = 1 / poll interval.
3. For each scheme write `fraction = Σ rate × cost`. Check whether processing cost is charged in both schemes
   (the question usually says so explicitly).
4. If the question asks a **ratio**, compute both fractions in the same unit, divide last; round at the end.
5. Sanity check: fractions must be ≤ 1 (or ≤ the stated budget).

### Worked example E4 — polling fraction for a slow sensor
CPU 500 MHz. A sensor produces one byte every 4 ms (λ = 250 B/s, one-byte buffer) so we must poll at ≥ 250 polls/s.
A poll costs 400 cycles = 400 / 500 × 10⁶ = **0.8 μs**.
Fraction = 250 × 0.8 μs = 200 μs/s = **0.02 %** (processing excluded).

### Worked example E5 — a fast, always-busy device (interrupts lose)
Device: 400 000 B/s, 4-byte words → λ = 100 000 words/s. CPU: polling pass that finds data = 0.6 μs total (poll +
move); interrupt per word = 3 μs; DMA with 2048-byte blocks: setup 3000 cycles + completion interrupt 5000 cycles
at 500 MHz = 16 μs per block.

```
 polling   : 100 000 × 0.6 μs = 0.06   -> 6.0 %
 interrupts: 100 000 × 3 μs   = 0.30   -> 30.0 %
 DMA       : blocks/s = 400 000 / 2048 = 195.3125 ; 195.3125 × 16 μs = 0.003125 -> 0.3125 %
 max sustainable rate with interrupts (β = 1): 1 / 3 μs = 333 333 words/s
```
Moral: for a busy device polling beats per-word interrupts; DMA beats both.

### Worked example E6 — GATE-2023-style pattern (original numbers)
An event arrives once per second. Polling every 20 ms costs 50 μs per poll; when the poll sees the event, 400 μs of
extra processing follow. Interrupt alternative: total 1.5 ms per event. Let T₁ = fraction of a second for polling
+ processing, T₂ = for interrupt + processing.

```
 polls per second = 1 / 20 ms = 50
 T₁ = 50 × 50 μs + 400 μs = 2500 + 400 = 2900 μs = 0.0029
 T₂ = 1500 μs = 0.0015
 T₁ / T₂ = 2900 / 1500 = 1.9333… ≈ 1.9
```
Traps: forgetting that the 50 polls happen every second **whether or not** an event arrives; adding the
processing cost to T₂ again (the 1.5 ms already includes it); mixing ms and μs.

### Worked example E7 — slowdown of the main program
Interrupts arrive at 5 000 /s, each costs 12 μs. Fraction = 5000 × 12 μs = 0.06 = 6 %. A job needing 10 s of CPU
when undisturbed now needs 10 / (1 − 0.06) = **10.638 s** (the non-interrupt CPU share is 94 %).
(Reason: f is the share of **wall-clock** time; only 1 − f of each second is left for the job, so time = work / (1 − f),
not work × (1 + f). If a question instead says "the job's own CPU demand rises by 6 %", read it as stated.)

---

## 6. The interrupt mechanism

### 6.1 What an interrupt is

An **interrupt** is a signal that makes the CPU suspend the current program at a safe point, run a handler (ISR),
and resume. Sources:

| Kind | Raised by | Examples | Timing |
|---|---|---|---|
| **Hardware interrupt, maskable** | external device through INTR/IRQ line | disk done, timer, keyboard | asynchronous to the program |
| **Hardware interrupt, non-maskable (NMI)** | external critical event | power failing, memory parity error, watchdog | asynchronous, cannot be disabled |
| **Software interrupt / trap** | instruction `INT n`, `SYSCALL` | system call, breakpoint | synchronous (caused by that instruction) |
| **Exception** | the CPU itself | divide by zero, page fault, illegal opcode | synchronous (§11) |

### 6.2 Where in the instruction cycle the CPU looks

The basic cycle gets an extra phase:

```
          +-------+     +--------+     +---------+     +-----------------------+
  ------> | FETCH | --> | DECODE | --> | EXECUTE | --> | INTERRUPT CHECK       |
  |       +-------+     +--------+     +---------+     |  IRQ pending & enabled?|
  |                                                    +-----------+-----------+
  |                              no  <---------------------------- | yes
  +-----------------------------------------------------------------+     |
                                                                         v
                                                  interrupt (entry) sequence, then fetch from ISR
```

**Rule: a maskable external interrupt is recognised only at an instruction boundary** (after the current
instruction completes), and only if interrupts are enabled (IF/mask) and no higher-or-equal-priority service is in
progress. It is **not** acted on:
- immediately when raised (the CPU does not abandon the instruction half-executed),
- "at the end of the fetch cycle" (an instruction that has been fetched must still be executed),
- at fixed time intervals (the CPU samples the line every instruction; nothing is periodic).

The request line is **latched** by the device/controller until acknowledged, so a request that arrives mid-instruction
is not lost; it just waits.

**Long (multi-cycle / multi-step) instructions.** The response is delayed until the instruction ends, so one
very long instruction directly lengthens the worst-case latency (§7). Processors with block/string
instructions (repeat-prefixed copy) therefore make them **interruptible between iterations**: the PC and the
count register are kept so that the instruction continues where it stopped. Concept to remember: *the atomic unit
for recognising an interrupt is "an instruction", or "an iteration" for restartable block instructions*.
Divide-by-zero and page-fault exceptions, in contrast, are detected **during** an instruction (§11).

### 6.3 The canonical sequence of events

Using a vectored, hardware-saves-PC design (what GATE questions assume):

```
 step  actor      event
 ----  ---------  -------------------------------------------------------------
  1    device     asserts IRQ
  2    CPU        finishes executing the current instruction
  3    CPU        checks IRQ and enable/mask -> accepts; sends INTA (acknowledge)
  4    device     (vectored) places its vector number on the bus
  5    CPU hw     saves return state: pushes PC (and flags/PSW) on the control stack
  6    CPU hw     disables further maskable interrupts (clears IF) unless the design allows nesting
  7    CPU hw     loads PC with the ISR entry address (from the vector table / fixed address)
  8    ISR        (software) saves the general registers it will overwrite
  9    ISR        services the device (read/write data register, acknowledge to deassert IRQ)
 10    ISR        restores the saved registers
 11    CPU        executes return-from-interrupt (IRET/RTI): pops flags and PC
 12    CPU        resumes the interrupted program with the next instruction
```

Two ordering facts that are exactly what ordering questions test:

1. **Finish the instruction first** (step 2) → *then* save state.
2. **Save the old PC before loading the new PC** (5 before 7) — otherwise the return address is destroyed.
   And "pop" happens **after** the ISR body, as the very last thing.

Generic micro-operation shape of an interrupt entry on a simple machine (register names invented for illustration):

```
 TMP  <- PC            ; copy the return address into a data register
 ADR  <- SAVE_SLOT     ; address where the return address will be stored (a stack slot or a fixed location)
 PC   <- HANDLER       ; overwrite PC with the new address
 MEM[ADR] <- TMP       ; write the saved PC to memory
```
How to recognise this shape in an exam question: the old PC is **copied out and written to memory**, and PC is
overwritten with a different value in the same sequence. Compare:

| Sequence feature | Interrupt entry / call-like | Instruction fetch | Operand fetch | Conditional branch |
|---|---|---|---|---|
| Old PC written to memory? | **yes** | no | no | no |
| PC overwritten by an unrelated value? | **yes** | no (PC just incremented) | no | yes, but only if a flag/condition decides it |
| Memory access in the sequence | **write** of the saved PC | read (PC → MAR, then read) | read | none |

### 6.4 What state is saved and by whom

| State | Saved by | Why |
|---|---|---|
| **PC** | hardware, automatically | the address where execution must resume |
| **Flags / PSW (status word)** | hardware (usually together with PC) | the ISR will change condition codes; also holds the interrupt-enable bit and mode |
| **General registers** that the ISR overwrites | the **ISR** (software push/pop) or hardware in some designs | a register changed by the ISR would corrupt the interrupted program |
| Cache contents, TLB | not saved | not architectural state (but ISR may evict useful lines — §12) |

Cost: saving k registers at 2 cycles each costs 2k cycles on entry and 2k on exit (E8). Designs reduce this with
**banked/shadow registers** (a second register set; switching is one cycle) at the cost of hardware.

### 6.5 The return address — which instruction does the stack hold?

For an **external (asynchronous) interrupt** or a **trap** (software interrupt), the instruction that was running
**completes**, and the saved PC is the address of the **instruction that would have executed next** in the original
program order. Therefore:

```
 saved PC = (address of interrupted instruction) + (its length)           if it falls through
 saved PC = branch/jump/call target                                        if it was a taken control transfer
```
For a **fault** (page fault, divide error, illegal opcode) the saved PC is that of the **faulting instruction
itself**, because it has not completed and must be **re-executed** after the handler fixes the cause (x86-style
convention; textbook machines vary, and a question normally states its convention).

Byte-addressable memory, variable-length instructions → the length is in **bytes** (a "32-bit word" means 4 bytes);
an instruction occupying two words adds 8 to the address.

### Worked example E9 — return address (original listing)

```
 1200: LOAD  R1,[A]       (4 B)  -> next 1204
 1204: ADD   R1,#7        (6 B)  -> next 1210
 1210: CALL  1500         (4 B)  -> next 1214 (target 1500)
 1214: STORE R1,[B]       (4 B)  -> next 1218
 1218: JMP   1200         (4 B)  -> target 1200
```
- External interrupt while `ADD` executes → ADD completes → saved PC = **1210**.
- External interrupt while `CALL` executes → CALL completes (it pushed its own return address 1214 and set PC =
  1500) → saved PC = **1500**, *not* 1214.
- External interrupt while `JMP` executes → saved PC = **1200**.
- Page fault on the `LOAD`'s data access → saved PC = **1200** (the LOAD itself will be re-executed).
- If the instruction at 1210 were a system-call trap (4 B) → saved PC = **1214**.

Trap in exams: using "interrupted address + 4" when instructions have different lengths, or ignoring that the
interrupted instruction was a taken branch.

### 6.6 Enabling and disabling

- **Interrupt-enable flag (IF)**: when 0, maskable requests are ignored (kept pending). Set/cleared by
  instructions (`EI/DI`, `STI/CLI`) and by the hardware at entry/IRET (entry clears it; IRET restores it from the
  saved flags).
- **Mask register**: one bit per interrupt source; a masked source cannot interrupt even if IF = 1 (§9.3).
- **NMI** bypasses both.
- Why disable during entry: the CPU must finish saving PC/flags before another interrupt overwrites them.
- **Level-triggered vs edge-triggered request lines.** A level-triggered line stays asserted until the ISR
  acknowledges the device; if the ISR forgets, the interrupt re-fires immediately after IRET. An edge-triggered
  request is a transition; two edges while the first is still pending may merge into one (a lost interrupt).

---

## 7. Interrupt latency, response time, and per-interrupt overhead

Definitions (textbooks vary; **state yours**):

```
 interrupt latency   = time from IRQ assertion until the first instruction of the ISR starts
                     = wait for current instruction to end
                     + (time spent with interrupts disabled / masked, if any)
                     + hardware entry (save PC/flags, fetch vector)
 service (response) time = latency + software save + ISR body + restore + return
 CPU time per interrupt c_i = everything the CPU spends on this interrupt (this is the c of §5.2)
```

Worst-case latency (for real-time deadlines) = longest non-interruptible stretch (longest instruction, or longest
disabled-interrupts critical section) + hardware entry.

### Worked example E8 — per-interrupt overhead
1 GHz CPU. Hardware entry 20 cycles; software saves 12 registers at 2 cycles = 24; ISR body 300; restores 24; IRET 20.

```
 total = 20 + 24 + 300 + 24 + 20 = 388 cycles = 0.388 μs
 overhead (everything but the body) = 88 cycles   -> 22.7 % of the total
 rate that would use 25 % of the CPU: 0.25 / 0.388 μs ≈ 644 330 interrupts/s
```

### Worked example E10 — worst-case latency and a deadline (200 MHz CPU)
Longest interrupts-disabled section 120 cycles, longest instruction 40 cycles, hardware entry 12 cycles.
Worst-case latency = 120 + 40 + 12 = 172 cycles = 172 / 200 MHz = **0.86 μs**.
The two worst cases do not necessarily stack in a real machine; the conservative bound adds them.

If the device holds one byte and overwrites it 5 μs after raising the request, the ISR must read the data register
within 5 μs of the request. With a 60-cycle ISR prefix before the read: 0.86 μs + 60/200 MHz (0.30 μs) = 1.16 μs ≤ 5 μs → safe.

---

## 8. Identifying the source: non-vectored vs vectored interrupts

When the CPU accepts an interrupt it must know **which ISR to run**.

### 8.1 Non-vectored (single common entry point)

All interrupts enter **one fixed routine** (fixed address). That routine must **find out the source in software**
— typically by reading each device's status register in priority order (a software poll).

- Hardware: very simple.
- Time to reach the *device-specific* service code: **longer**, because of the software search; the search order
  also sets the priority.

### 8.2 Vectored

The interrupting device (or the interrupt controller on its behalf) supplies a **vector**: a number or address
that selects the ISR. No software search.

- Faster to reach the device-specific routine; hardware must supply the vector during the acknowledge cycle.
- Variants: the device provides the **ISR address itself**, or an **index** into the interrupt vector table.

### 8.3 Interrupt vector table (IVT)

```
 IVT (base B)       entry n holds the ISR address (or a gate/descriptor)
 +--------+
 |  0     | -> ISR for vector 0
 |  1     | -> ISR for vector 1
 |  …     |
 | 255    | -> ISR for vector 255
 +--------+
 address of entry n = B + n × (entry size)
 table size         = (number of vectors) × (entry size)
```

### Worked example E11 — vector table arithmetic
(a) 256 vectors, 4-byte entries, table at address 0: size = 256 × 4 = 1024 B = 1 KB. Vector 0x21 (= 33): entry at
33 × 4 = 132 = 0x84.
(b) Base 0x4000, 8-byte entries, vector 0x2A = 42: address = 0x4000 + 42 × 8 = 16384 + 336 = 16720 = **0x4150**.

Vectored does **not** mean "no software at all": the ISR still saves registers and services the device; what is
saved is the *search*. Non-vectored does **not** mean polling by the CPU of *all* devices before every interrupt: the
CPU is interrupted first; only then does the common routine look for the source.

---

## 9. Many devices, one CPU: identification and priority schemes

### 9.1 Software polling of sources (non-vectored)
Common routine tests status registers in a fixed order. **Priority = order of testing.** Cheap in hardware; slow
with many devices.

### 9.2 Daisy chain (hardware, serial)

All devices share **one request line** to the CPU. The CPU's acknowledge (grant) signal is wired through the devices
in series:

```
          IRQ (wired-OR, shared by all devices)
   +------<---------<-----------<-----------<---+
   |                                             |
 +-----+  INTA   +------+  PO->PI  +------+  PO->PI  +------+
 | CPU |-------->| Dev1 |--------->| Dev2 |--------->| Dev3 |---> ...
 +-----+         +------+          +------+          +------+
   ^ data bus: the device that *accepts* the grant puts its vector here
```
Rules:
1. A device that **is not requesting** passes the acknowledge on to the next device.
2. A device that **is requesting** *absorbs* the acknowledge (does not pass it on) and places its vector on the
   bus.
3. Therefore **priority is the physical position**: the device closest to the CPU wins; devices behind it cannot
   get the grant while it is requesting.

Properties: the CPU does **not** poll devices — the grant propagates and the winning device identifies itself
(this is what separates daisy-chain identification from software polling); it needs only one request line and one
grant line, so adding devices is cheap; but priority is fixed by wiring, a failed/missing device that fails to pass the
grant can cut off everything behind it, and the grant ripples through k devices so the delay for the k-th device
grows linearly (E12).

*Do not confuse*: "daisy chain" (hardware, serial grant, device identifies itself) vs "polling" (software,
CPU reads each status register).

### 9.3 Parallel (independent request/grant lines) with priority encoder and mask

Each device has its own request line. A **mask register** can disable lines individually; a **priority
encoder** picks the highest-priority active line and outputs its number (= the vector index).

```
  IR0 ─┐
  IR1 ─┤   pending reg  ──AND── NOT(mask) ──>  priority encoder ──> vector number + IRQ to CPU
  …    │   (1 = request)  (1 = masked)         (lowest index = highest priority here)
  IR7 ─┘
```
Active requests = `pending AND NOT mask`; the winner is the highest-priority set bit among them.

**Worked example E13.** IR7…IR0 pending = `1100 1010`, mask = `1000 0010` (IR7 and IR1 masked), IR0 highest priority:
active = `1100 1010 AND 0111 1101` = `0100 1000` → IR6 and IR3 active → winner **IR3**. Without the mask the winner
would have been IR1 — the mask changes the outcome.

### 9.4 Programmable interrupt controller (PIC; 8259-style, concept level)

A PIC chip collects up to 8 request lines, holds them in registers (request/in-service/mask), resolves priority
(fixed or rotating), asks the CPU for an interrupt, and on acknowledge supplies the vector. Key ideas:

- **IRR** (requests), **ISR-register** (in service), **IMR** (mask) per chip; the ISR must send an **EOI**
  (end-of-interrupt) command so the controller lets lower-priority requests through.
- **Cascading:** a master PIC has some of its inputs connected to slave PICs. With k slaves on a master with 8
  inputs: `lines = (8 − k) + 8k = 8 + 7k`. A master with 8 slaves handles 64 lines.

**Worked example E14.** To connect 20 sources with 8-input PICs: 8 + 7k ≥ 20 → k ≥ 1.71 → k = 2 slaves, so 1 master + 2
slaves = 3 chips (capacity 22).

### 9.5 Comparing the schemes

| Scheme | Who finds the source | Priority set by | Cost / speed |
|---|---|---|---|
| Software poll (non-vectored) | CPU software | poll order | cheapest hardware, slowest |
| Daisy chain | the device (on grant) | wiring position | one request line; fixed priority; ripple delay; one failure cuts the chain |
| Parallel + encoder | hardware encoder | encoder wiring / programmable | fastest, most wires |
| PIC (cascaded) | PIC supplies vector | programmable | flexible; extra chip(s) |

### Worked example E12 — daisy-chain delay
8 devices in series; each passes the grant in 10 ns. The grant reaches the 8th device after 8 × 10 = **80 ns** (the
k-th device waits k × 10 ns). Priority-wise: if Dev2 and Dev4 both request, Dev2 absorbs the grant and Dev4 waits; a
non-requesting Dev3 just passes the grant.

---

## 10. Priority, masking, and nesting

### 10.1 Which source should have the highest priority?
Principles (these decide "which interrupt is served first" questions):

1. **Non-maskable/critical hardware events** (power failure, CPU temperature, memory error) are highest — losing
   the response means damage or loss of the machine state.
2. Then sources with **tight deadlines and loss on delay** (timers, fast network/disk controllers with small
   buffers).
3. **Human-speed devices** (keyboard, mouse) are lowest: a 10-ms delay changes nothing the user can notice and
   their data rate is tiny.

### 10.2 Nesting rule

The CPU has a **current priority level** (the priority of the running ISR, or the base level for ordinary code).
Nesting enabled means:

```
 new request preempts the running ISR   iff   priority(new) is STRICTLY higher than the current level
 equal or lower priority                ->   stays pending until the running ISR (and anything above it) finishes
```
When an ISR finishes, the CPU resumes the **most recent still-unfinished** routine; among pending requests it
serves the highest priority first. Ties in simultaneous arrival are broken by a fixed rule (e.g. wiring order /
lower line number) — a problem that matters will state it.

Counting levels: priority numbers from a to b inclusive give `b − a + 1` levels (0…7 → 8).

If nesting is **disabled**, an ISR runs to completion even if a more urgent request arrives, so the urgent request
can wait up to the **entire remaining length** of the running ISR (worst case ≈ the full ISR length if the request
arrives just after it starts).

### 10.3 Timeline method (GATE nested-ISR problems)

Draw a time axis; at each event ("arrival", "ISR finishes") look at the **set of unfinished routines** and run the
highest-priority one. Track remaining execution time for preempted routines. Ignore overhead unless stated;
if entry/exit overheads are given, add them to each ISR's effective length.

**Worked example E15 — nesting enabled.** Higher number = higher priority.
A: priority 2, length 6, arrives t = 0. C: priority 3, length 5, arrives t = 2. B: priority 4, length 4, arrives t = 3.

```
 t=0..2   A runs                       (A has 4 left)
 t=2      C(3) > A(2) -> preempt       C runs 2..3 (C has 4 left)
 t=3      B(4) > C(3) -> preempt       B runs 3..7  -> B finishes at 7
 t=7      pending/unfinished: C(3), A(2) -> C resumes 7..11 -> C finishes at 11
 t=11     A resumes 11..15 -> A finishes at 15
 finish times: B=7, C=11, A=15      (total busy = 6+5+4 = 15, no gaps)
```
Same input with nesting **disabled**: A runs 0..6; then pending B(4), C(3): B 6..10, C 10..15 → finish A=6, B=10, C=15.

**Worked example E16 — equal priority does not preempt.** X: prio 1, length 5, t = 0. Y: prio 2, length 3, t = 1.
Z: prio 2, length 2, t = 2.
```
 t=0..1 X ; t=1 Y(2)>X(1) preempts: Y 1..4 ; at t=2 Z(2) is NOT > Y(2) -> waits
 t=4 Y done; pending Z(2), X(1): Z 4..6 ; X 6..10
 finish: Y=4, Z=6, X=10
```

**Worked example E17 — simultaneous arrival.** P (prio 3, len 4), Q (prio 5, len 2), R (prio 3, len 1) all arrive at t = 0;
tie between P and R broken in favour of P. Order: Q (0..2), then P (2..6), then R (6..7).

### 10.4 Interrupt-driven I/O and priority in the CPU

During an ISR the CPU raises its level, so lower sources are held off while higher ones can still get in. The
ISR writes EOI (or re-enables interrupts) at the right moment: re-enabling too late makes nesting ineffective;
re-enabling before the device's request line is cleared causes a re-entry storm.

---

## 11. Exceptions, traps, faults, software interrupts (COA viewpoint)

All of these use **the same entry mechanism** (save PC/flags, vector through a table, handler, return); they differ
in **who raises them, when, and where the saved PC points**.

| Category | Raised by | Synchronous? | Saved PC (typical) | Resumed? | Examples |
|---|---|---|---|---|---|
| **Interrupt** (external) | device, timer | asynchronous | next instruction | yes, at the next instruction | disk done, timer, keyboard |
| **Trap** (software interrupt) | an instruction on purpose | synchronous | next instruction | yes | system call, breakpoint |
| **Fault** | instruction cannot complete (recoverable) | synchronous | **the faulting instruction** | **re-executes** it | page fault, divide error, (illegal opcode in many designs) |
| **Abort** | severe hardware error | synchronous/async | may be imprecise | usually not | machine check |

- **Synchronous = caused by the instruction stream**; reproducible at the same instruction. **Asynchronous = from
  outside**, unrelated to which instruction is running.
- **System call:** the program executes a trap instruction; the CPU switches to kernel mode and enters the
  OS via the vector table (details: OS folder).
- **Page fault:** the MMU finds the page not in memory; the instruction stops, the handler (OS) brings the page in,
  and the **same instruction restarts**. This is why the saved PC must point at the faulting instruction.
- **Divide by zero:** detected in the ALU/divider; on x86-style machines it is a fault (saved PC = the dividing instruction).
- Exceptions are **not maskable** by the interrupt-enable flag (they come from the instruction itself).

### 11.1 Precise vs imprecise (concept)
An interrupt/exception is **precise** if, at the moment the handler starts, all instructions before the saved PC
have completed and none at or after it has modified architectural state. This is easy on a non-pipelined
CPU; on a pipelined CPU with out-of-order completion it needs extra mechanisms (§12).

---

## 12. Interplay with pipelining and cache (concept level)

**Pipelining** (details in [`../../07-INSTRUCTION-PIPELINING`](../../07-INSTRUCTION-PIPELINING)):
- At an instruction boundary several later instructions are already in the pipeline. When the interrupt is
  taken, they are **squashed (flushed)** and will be refetched after IRET. Cost ≈ refill time of k − 1 cycles for a
  k-stage pipeline (plus entry/ISR costs).
- A fault in a late stage (e.g. a page fault in MEM) must stop the **older** instructions only to the extent they
  can complete, and must cancel **younger** ones. Keeping exceptions precise means exceptions are *reported in program order* (e.g. by flagging and
  acting at write-back/commit).
- Delay-slot or branch-in-flight cases mean the saved PC must account for the branch outcome (as in E9).

**Cache** (details in [`../../05-MEMORY-INTERFACING-AND-HIERARCHY`](../../05-MEMORY-INTERFACING-AND-HIERARCHY)):
- Memory-mapped I/O addresses must be **uncacheable** (§3.1).
- The ISR often runs with cold cache/TLB state: its real cost exceeds the "ideal" cycle count, and after IRET the
  main program may have lost cache lines. Numerics in GATE usually ignore this; mention as an assumption.
- DMA writing memory behind the CPU's back raises coherence issues (see DMA folder).

**Worked example E18 — pipeline flush on interrupt.** 5-stage pipeline, interrupt recognised when an instruction
leaves write-back, so the 4 younger instructions in flight are discarded; refilling after the ISR costs
k − 1 = 4 cycles. With entry 10 cycles: interrupt overhead from pipelining + entry = 4 + 10 = 14 cycles (ISR extra).
(If a question gives per-interrupt flush cost explicitly, use theirs.)

---

## 13. Prerequisite / bridge: OS view of interrupts (owned by the OS folders)

*Included only to answer the partly-OS mapped entries; follow the links for depth.*

- **An interrupt does not by itself mean a context switch.** The ISR runs on behalf of whatever was executing; the
  scheduler (invoked at the end of the ISR, e.g. after a timer tick or when an I/O completion makes a higher-priority
  process ready) *decides* whether to switch. An interrupt that merely hands control to the OS (another process's I/O completion, a timer tick) does not
  force a switch. By contrast, an event that makes the *running process itself* wait (a blocking call, a fault that
  needs disk I/O before the instruction can complete) must take it out of the running state.
- **Synchronous vs asynchronous I/O (OS meaning):** whether the *calling process waits* for completion.
  Hardware-wise, an interrupt-driven device raises its completion interrupt in both cases, and the ISR handles it; what
  differs is whether the process was put to sleep and woken by the ISR path or continued running. (Link:
  [`../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING`](../../../08-OPERATING-SYSTEMS/07-CPU-AND-IO-SCHEDULING).)
- Kernel mode and the privileged `IN`/`OUT`/`DI` instructions: user code cannot disable interrupts.

---

## 14. PYQ patterns (methods only — no answers; mapped list in [`PYQ.md`](PYQ.md))

| # | Pattern | Recognise by | Recipe | Trap |
|---|---|---|---|---|
| P1 | **When is an interrupt serviced?** | "CPU generally handles an interrupt by …" | End of the **current instruction**, if enabled/unmasked (§6.2) | choosing "as soon as raised", "end of fetch", or a fixed time interval |
| P2 | **Order of events after an interrupt** | list of lettered events (finish instruction, push status, load new PC, run ISR, pop status) | Use §6.3: finish instruction → save state → load new PC → ISR → restore | putting "load PC" before "save"; popping before the ISR body |
| P3 | **Return address** | byte-addressable listing, interrupt "during" some instruction, asks the pushed address | next-instruction address after completion (§6.5); length in bytes; branch target if taken; faulting instruction for faults | adding the wrong length; a missing listing in the mapping (see PYQ.md) |
| P4 | **Micro-operation sequence for interrupt entry** | register-transfer lines: PC copied out, PC overwritten with a fixed value, memory write | §6.3 recognition table | confusing it with a branch (a branch does not store the old PC) |
| P5 | **Polling vs interrupt CPU-time ratio** | rates, poll interval, μs per poll, μs per interrupt | §5.6; count polls per second even when no event | ignoring processing cost on one side, ms/μs mix-up |
| P6 | **Which interrupt is highest priority?** | list of devices including a hardware-fault/temperature source | §10.1: critical hardware condition first, human-speed devices last | ranking by "importance to the user" |
| P7 | **Vectored vs non-vectored; daisy chain true/false** | two statements S1, S2 | §8–§9: non-vectored needs software search; daisy chain = hardware grant propagation, not CPU polling every device | equating daisy chain with polling |
| P8 | **Synchronous vs asynchronous I/O statements** | statements about ISR invoked / process waits | §13: ISR is the hardware completion path; sync/async is about the caller | thinking that "asynchronous" means "no interrupt" |
| P9 | **Context-switch consequences of interrupts/system calls** | MSQ on "which events always move the running process out of the running state" | §13: for each event ask "does the process itself have to wait for something?" (then it leaves running) or "does the OS merely get control?" (then the scheduler decides) | assuming every interrupt switches process |
| P10 | **Compare I/O techniques for bulk data** (unmapped 2022) | "highest throughput for bulk transfer" | §4.4: DMA | picking interrupt-driven because it "frees the CPU" |

---

## 15. Traps and misconceptions

1. "Interrupts are handled **immediately**." No — at the end of the current instruction.
2. "Vectored = the CPU polls less devices." No — the device supplies the identifier; no search.
3. "Daisy chain = CPU polls all devices." No — a grant propagates and the winner identifies itself.
4. "Closest to the CPU = lowest priority." Reverse: the closest device sees the grant first.
5. "Interrupt-driven I/O is always cheaper than polling." Not for a busy device (E5).
6. "Equal priority preempts." Preemption needs a **strictly higher** level.
7. "Saved PC = interrupted instruction's address." Only for faults; interrupts/traps save the **next** one, and the
   next one may be a branch target.
8. Interrupt vs DMA: an interrupt transfers **control**; DMA transfers **data** without CPU instructions.
9. Unit slips: μs vs ms; cycles vs ns; per-interrupt cost already includes processing.
10. Forgetting to charge polls that find nothing.
11. Memory-mapped I/O does not mean the data is cached, nor that I/O needs no instructions at all — it uses load/store.
12. "Masking an interrupt discards it." The request stays pending (latched) unless the line is edge-triggered and lost.
13. "NMI can be disabled with IF." It cannot.
14. "A page fault is an external interrupt." It is a synchronous exception (fault), saved PC = the faulting instruction.

## 16. Edge cases and assumptions to state

- State direction of priority numbers; tie-break rule for simultaneous arrivals.
- State whether nesting is allowed and whether interrupts are re-enabled inside the ISR.
- State whether entry/exit costs are included in "ISR time".
- State bytes per instruction and byte vs word addressing.
- State whether the CPU runs other work while polling (interval polling) or only polls (busy wait).
- State your definition of latency (to first ISR instruction) vs response time.
- If a mapped PYQ's figure/listing is missing, do not guess its numbers; use the method only.

## 17. Connections to other COA topics

| Topic | Link |
|---|---|
| DMA, cycle stealing, bus arbitration (daisy-chain bus grant has the same wiring idea) | [`../02-DMA`](../02-DMA/NOTES.md) |
| Pipelining: flush, precise interrupts | [`../../07-INSTRUCTION-PIPELINING`](../../07-INSTRUCTION-PIPELINING), [`../../08-PIPELINE-HAZARDS`](../../08-PIPELINE-HAZARDS) |
| Addressing: memory-mapped I/O is ordinary load/store addressing | [`../../02-ADDRESSING-MODES`](../../02-ADDRESSING-MODES) |
| Control unit: interrupt cycle as extra state in the control FSM/microprogram | [`../../04-DESIGN-OF-CONTROL-UNIT`](../../04-DESIGN-OF-CONTROL-UNIT) |
| Cache: uncacheable I/O regions, cold ISR | [`../../05-MEMORY-INTERFACING-AND-HIERARCHY`](../../05-MEMORY-INTERFACING-AND-HIERARCHY) |
| OS: system calls, processes, I/O scheduling | OS folders linked in §0 |

---

## 18. Existing practice coverage map

The existing practice file has 14 questions; this table points to the NOTES section that equips each skill.

| Q# | Skill | NOTES section |
|---|---|---|
| 1 | What a vectored interrupt supplies | §8.2 |
| 2 | Non-vectored: one fixed routine, then identify the source | §8.1 |
| 3 | Count of priority levels in an inclusive range | §10.2 (counting levels) |
| 4 | Daisy chain: closest = highest priority | §9.2 |
| 5 | Interrupt vs poll vs DMA statements; nesting | §4, §10.2 |
| 6 | Interrupt rate from period; CPU time = rate × cost | §5.2, §5.6 |
| 7 | What state must be preserved | §6.4 |
| 8 | Sum of two devices' service costs → % of CPU | §5.2, §5.6 |
| 9 | Which devices can preempt (priority direction) | §10.2 |
| 10 | Vector vs non-vectored vs daisy chain statements | §8, §9.2 |
| 11 | Polling fraction / interrupt fraction ratio | §5.1, §5.2, §5.5 |
| 12 | Cycle-count of the whole service path | §7 (E8), §6.3 |
| 13 | Maximum sustainable interrupt rate for a CPU budget | §5.4 |
| 14 | Combined utilisation; non-preemptible wait; vectored dispatch; return ≠ DMA | §5.2, §10.2, §8.2, §6.3 |

## 19. Self-check

1. At which point in the instruction cycle is a maskable interrupt recognised, and why not mid-instruction?
2. Write the 12-step event sequence from IRQ assertion to resuming the main program.
3. Why must the old PC be saved before the new PC is loaded?
4. Which return address is saved for (a) an external interrupt, (b) a taken branch being interrupted, (c) a page fault?
5. Difference between memory-mapped and isolated I/O in instructions, address space and caching?
6. Give the CPU-fraction formulas for polling and interrupts; when does polling win?
7. How is the maximum sustainable interrupt rate computed from a CPU budget?
8. What does a vector supply, and how does non-vectored identification differ?
9. Describe daisy-chain operation; where does priority come from; why isn't it "CPU polling"?
10. State the preemption rule for nested interrupts, including the equal-priority case.
11. Which interrupt is served first among {temperature alarm, disk, keyboard, timer}, and by what principle?
12. How many 8-input PICs must be cascaded (one master, rest slaves) to serve 30 request lines?

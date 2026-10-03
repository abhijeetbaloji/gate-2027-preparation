# Hardwired Control Unit — Notes

## 0. Where this fits

- **Syllabus line:** "Design of control unit – hardwired and microprogrammed" (this folder = the *hardwired* half).
- **Study before:** instruction formats and RISC/CISC vocabulary ([../../01-INSTRUCTION-SET](../../01-INSTRUCTION-SET)), addressing modes ([../../02-ADDRESSING-MODES](../../02-ADDRESSING-MODES)), the ALU as a block with function-select lines ([../../03-ARITHMETIC-AND-LOGIC-UNIT](../../03-ARITHMETIC-AND-LOGIC-UNIT)), and decoders / counters / flip-flops from Digital Logic ([../../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS](../../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS)).
- **Study after / alongside:** the sibling [../02-MICROPROGRAMMED](../02-MICROPROGRAMMED) (same job, done with a stored program instead of gates), then pipelining ([../../07-INSTRUCTION-PIPELINING](../../07-INSTRUCTION-PIPELINING), [../../08-PIPELINE-HAZARDS](../../08-PIPELINE-HAZARDS)) where the control signals are produced once per stage, and interrupts ([../../06-IO-INTERFACE/01-INTERRUPT](../../06-IO-INTERFACE/01-INTERRUPT)) which add inputs to the control unit.
- **Conventions used here (same as the whole COA folder):** 1 K = 2¹⁰; CPU time = IC × CPI × clock period = IC × CPI / f; byte-addressable memory with 4-byte instructions unless a question says otherwise (so "PC ← PC + 4"; with word-addressable memory it would be +1).

## 1. Evidence snapshot (why this depth)

| Section | Rating | Evidence |
|---|---|---|
| §5 Micro-operations of fetch / execute, §4 datapath | **HIGH** | Needed directly by existing practice Q3, Q4, Q7, Q8, Q9 and Q10 (all talk about steps/states/cycles). Also the skill behind two *cross-filed* PYQ kinds: a data-path step-ordering question (2020, filed under ALU) and a micro-operation-sequence question (2013, 4 booklet copies, filed under Interrupt). |
| §6–§8 Control-unit organisation, signal equations, state/one-hot/ROM methods | **HIGH** | Existing practice Q1, Q2, Q3, Q5, Q6, Q8 (counter bits, ROM size, decoder inputs, state counting). The mapped syllabus clause is literally "hardwired control". |
| §9 Steps → CPI, memory wait | **MEDIUM** | Not in the one mapped PYQ, but the iron-law CPU-time formula is examined elsewhere in COA; practice Q10-style timing needs §10. |
| §10 Clock-period constraint | **MEDIUM** | Existing practice Q10. |
| §11 Single-cycle vs multi-cycle vs pipelined | **MEDIUM** | Bridge to pipelining topics; no mapped entry in this folder. |
| §12 Hardwired vs microprogrammed, RISC link | **HIGH** | The only mapped PYQ in this topic (GATE 2018, 1 entry) is a RISC-characteristics question that includes "hardwired control unit" as one statement. Existing practice Q1, Q5 also test the contrast. |
| §13 Flags and interrupts as control inputs | **LOW** | One-paragraph treatment; practice Q1 only mentions flags as a distractor. |

Mapped-entry count for this folder: **1** (2018). Cross-references (not in this folder's mapping, mapping files untouched): **1** entry in the ALU folder (2020) and **4 booklet copies of 1 question** in the Interrupt folder (2013).

---

## 2. Intuition first: what the control unit is

A processor has two parts:

- **Datapath** — registers, ALU, buses, memory interface. It *can* do many things (move R2 to the bus, add, write memory) but does nothing by itself.
- **Control unit** — decides, **clock cycle by clock cycle**, which of those capabilities are switched on.

Analogy: the datapath is a set of water pipes with valves. Each valve is a **control signal**. The control unit is the person who opens exactly the right valves in exactly the right order for each instruction. "Hardwired" means that person is a fixed arrangement of logic gates; "microprogrammed" means the person reads the valve settings from a memory.

Tiny example: to execute `ADD Ra, Rb, Rc` on a one-bus machine the valves must be opened in three clock cycles:

```
cycle 1: let Rb flow onto the bus, and let the ALU's left-input register Y catch it
cycle 2: let Rc flow onto the bus, ALU adds Y + bus, result is caught by Z
cycle 3: let Z flow onto the bus, let Ra catch it
```

Which valves open in a given cycle depends on **(a) which instruction it is** (opcode in IR), **(b) which cycle of that instruction it is** (a step counter), and sometimes **(c) a flag or an interrupt line**. A hardwired control unit is exactly a Boolean function

```
every control signal = f(opcode, step, flags)
```

built from gates. That single sentence answers most conceptual questions on this topic.

---

## 3. Definitions and terminology

| Term | Meaning |
|---|---|
| **Control signal** | A single wire from the control unit that enables one action: a register's load enable (`Xin`), a register's gate onto the bus (`Xout`), an ALU function select (`Add`, `Sub`), a memory command (`Read`, `Write`), a multiplexer select (`Select4`). |
| **Micro-operation** | One elementary register-transfer action done in one control step, written in register-transfer notation, e.g. `MAR ← PC`, `Z ← Y + bus`. |
| **Control step (T-step, timing state)** | One clock cycle of the control sequence for an instruction: T1, T2, T3, … The control signals asserted in one step are all active together during that cycle. |
| **Instruction cycle** | Fetch → decode → (operand/indirect fetch) → execute → write back → (check interrupt). |
| **Step counter** | A counter that holds the current step number; reset by `End` at the end of each instruction. |
| **Step decoder** | n-to-2ⁿ decoder turning the counter value into one-hot lines T1 … Tm. |
| **Instruction decoder** | Decoder on the opcode field of IR giving one-hot lines ADD, LD, ST, BR, … |
| **Control signal generator** (control-code generator) | The combinational AND-OR (or PLA) network producing every control signal from decoder outputs and flags. |
| **End** | A control signal asserted in the last step of an instruction; it resets the step counter so the next clock starts a new fetch at T1. |
| **WMFC** | "Wait for Memory Function Complete": the control step is stretched until the memory raises MFC. Needed because memory is slower than the processor clock. |
| **Hardwired control** | Control signals are generated by fixed logic (gates, PLA, counters/flip-flops). |

**Prerequisite / bridge — decoders and counters** (owner: [Digital Logic](../../../02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS)). A k-bit binary counter has 2ᵏ states; a k-to-2ᵏ decoder has k inputs and 2ᵏ outputs, exactly one of which is 1. A ring (one-hot) counter of n flip-flops has a single 1 that circulates; it has n states and needs n flip-flops. We use only these three facts.

---

## 4. The reference datapath: single internal bus

All step counts below are defined *for this datapath*. If a question draws a different datapath, count steps for **that** drawing; the method is the same.

```
   ══════════════════════ single internal bus ══════════════════════════
     ▲▼        ▲▼        ▲▼        ▲▼        ▲▼         ▲ Zout      │ Yin
     PC        MAR       MDR       IR     R0 … R7        │           ▼
  (in/out)   (in only) (in/out) (in/out)  (in/out)      ┌┴──┐       ┌───┐
                │         │↕                            │ Z │       │ Y │
                ▼         ▼ memory data bus             └─▲─┘       └─┬─┘
        memory address bus                                │ Zin       │ left input
                                                        ┌─┴───────────▼─┐
        bus ── right input ────────────────────────────►│      ALU      │
        constant 4 (Select4) replaces Y as left input ─►│  (Add, Sub …) │
                                                        └───────────────┘
   Each register has an "in" control (bus → register, latched at end of step)
   and, where drawn "in/out", an "out" control (register → bus, tri-state gate).
   IR also supplies the offset field (IRoffsetout) and the register-number
   fields Ra, Rb, Rc.
```

Rules of this datapath (they drive every step count):

1. **One bus ⇒ only one `…out` per step.** Two gates driving the bus at once is a conflict. Any number of registers may *load* (`…in`) from the bus in the same step.
2. **ALU inputs:** the left input comes from register **Y** (or the constant 4 when `Select4`), the right input is the **bus**. So an operation `A op B` needs A in Y in an *earlier* step, and B on the bus in the step where the ALU is used.
3. **ALU output goes to register Z**, never directly onto the bus. A later step does `Zout`.
4. A register loads at the **end** of the step in which its `…in` is asserted. A value loaded in step Tk can be used (put on the bus) from Tk+1, not within Tk.
5. **Memory commands convention (used throughout):** `Read` is asserted in the step that loads MAR; `Write` is asserted in the step that loads MDR from the bus. The memory starts working at the end of that step. `WMFC` in a later step waits for completion; for a read it also loads MDR from the memory data bus when MFC arrives.
6. Register numbers in IR fields (`Ra`, `Rb`, `Rc`) pass through small decoders; "`Rbout`" means "gate onto the bus the register whose number is in field Rb". That decoder is part of the control logic but is not a timing step.
7. Decoding the opcode is combinational logic hanging off IR, so it needs **no separate step** in this model; after `IRin` at the end of T3, the instruction decoder outputs are valid early in T4.

---

## 5. Instruction cycle and its micro-operations

### 5.1 The instruction cycle as a state diagram

```
 ┌───────┐   ┌────────┐   ┌───────────────────┐   ┌─────────┐   ┌────────────┐
 │ FETCH │──►│ DECODE │──►│ OPERAND / INDIRECT│──►│ EXECUTE │──►│ WRITE-BACK │
 └───▲───┘   └────────┘   │ FETCH (if needed) │   └─────────┘   └─────┬──────┘
     │                    └───────────────────┘                       │
     │        no interrupt pending                                    ▼
     └─────────────────────────────────────────── interrupt pending? ─┘
                                                   yes → interrupt sequence, then FETCH
```

In a hardwired unit, **fetch is the same micro-operation sequence for every instruction** (it cannot depend on the opcode because the opcode is not known yet). From the end of fetch onward the sequence depends on the opcode.

### 5.2 Fetch (common to all instructions): 3 steps

| Step | Micro-operations (register-transfer) | Control signals asserted |
|---|---|---|
| T1 | `MAR ← PC;  Read;  Z ← PC + 4` | `PCout, MARin, Read, Select4, Add, Zin` |
| T2 | `PC ← Z;  wait for memory;  MDR ← M[MAR]` | `Zout, PCin, WMFC` |
| T3 | `IR ← MDR` | `MDRout, IRin` |

Note how T1 does two useful things at once: it sends the address to memory *and* uses the otherwise idle ALU to increment the PC. T2 hides the PC update under the memory wait. This is the standard way to get fetch down to 3 steps on one bus.

### 5.3 Execute: the five instructions used in these notes

Instruction formats: `ADD Ra,Rb,Rc` means Ra ← Rb + Rc. `LD Ra,(Rb)` means Ra ← M[Rb]. `ST Ra,(Rb)` means M[Rb] ← Ra. `BR off` means PC ← PC + off (offset taken from IR, PC already incremented by fetch). `LDI Ra,(Rb)` is memory-indirect: Ra ← M[ M[Rb] ] (Rb holds the address of a pointer).

**ADD Ra, Rb, Rc** — 3 execute steps

| Step | Micro-op | Signals |
|---|---|---|
| T4 | `Y ← Rb` | `Rbout, Yin` |
| T5 | `Z ← Y + Rc` | `Rcout, Add, Zin` |
| T6 | `Ra ← Z` | `Zout, Rain, End` |

**LD Ra, (Rb)** — 3 execute steps

| Step | Micro-op | Signals |
|---|---|---|
| T4 | `MAR ← Rb;  Read` | `Rbout, MARin, Read` |
| T5 | wait; `MDR ← M[MAR]` | `WMFC` |
| T6 | `Ra ← MDR` | `MDRout, Rain, End` |

**ST Ra, (Rb)** — 3 execute steps

| Step | Micro-op | Signals |
|---|---|---|
| T4 | `MAR ← Rb` | `Rbout, MARin` |
| T5 | `MDR ← Ra;  Write` | `Raout, MDRin, Write` |
| T6 | wait for write to finish | `WMFC, End` |

(Compare with the existing practice file: its STORE is the same 3 execute steps — address to MAR, data to MDR together with Write, then wait. `Read` is never asserted in a store.)

**BR off** — 3 execute steps (PC-relative; PC was already advanced in fetch)

| Step | Micro-op | Signals |
|---|---|---|
| T4 | `Y ← PC` | `PCout, Yin` |
| T5 | `Z ← Y + offset(IR)` | `IRoffsetout, Add, Zin` |
| T6 | `PC ← Z` | `Zout, PCin, End` |

**LDI Ra, (Rb)** (memory-indirect) — 5 execute steps: the memory is used twice.

| Step | Micro-op | Signals |
|---|---|---|
| T4 | `MAR ← Rb;  Read` | `Rbout, MARin, Read` |
| T5 | wait; `MDR ← M[MAR]` (this is the *pointer*) | `WMFC` |
| T6 | `MAR ← MDR;  Read` | `MDRout, MARin, Read` |
| T7 | wait; `MDR ← M[MAR]` (this is the *data*) | `WMFC` |
| T8 | `Ra ← MDR` | `MDRout, Rain, End` |

Rule of thumb: **each trip to memory costs a "set address + command" step and a "wait" step**; indirection adds a whole trip.

### 5.4 Step-count table (ideal memory: each WMFC step lasts 1 cycle)

```
 instruction  fetch  execute  total steps (= cycles)
 ADD            3       3         6
 LD             3       3         6
 ST             3       3         6
 BR             3       3         6
 LDI            3       5         8
```

### 5.5 Variants you must be ready to recount

- **Datapath without Z (practice-style variant).** Suppose the ALU has two input registers A and B, both loaded from the single bus, and the result goes directly to the destination register in the same cycle as the add. For `ADD Ra,Rb,Rc`: T4 `Rbout, Ain`; T5 `Rcout, Bin`; T6 `ALU add, ALUout, Rain`. Still **3** execute steps, because the two operands must arrive over one bus in different cycles. Rule: *k operands arriving over one bus need k transfers*.
- **Displacement load `LD Ra, d(Rb)`:** T4 `Rbout, Yin`; T5 `IRoffsetout, Add, Zin`; T6 `Zout, MARin, Read`; T7 `WMFC`; T8 `MDRout, Rain, End` → **5** execute steps (address arithmetic costs 2 steps more than register-indirect).
- **Conditional branch `BRZ off`:** same three steps as BR, but `PCin` in T6 is qualified by the flag: `PCin = … + BRZ·T6·Zflag`. Alternatively a designer may assert `End` already in T4 when the condition is false; that makes branch-not-taken shorter (instruction-dependent step count).
- **Register-to-register `MOV Ra, Rb`:** T4 `Rbout, Rain, End` → 1 execute step.

### 5.6 Ordering shuffled micro-operations (data-path ordering skill)

Cross-reference only: a data-path ordering question of this kind is filed in [../../03-ARITHMETIC-AND-LOGIC-UNIT](../../03-ARITHMETIC-AND-LOGIC-UNIT) (GATE 2020, see [PYQ.md](PYQ.md)); the mapping file there has a garbled figure, so check the PDF. Method (no answers asserted for any actual PYQ):

1. Write the **dependencies**: a value must be *produced* in an earlier step than the step that *consumes* it (rules 2, 3, 4 of §4).
2. If the list contains fetch micro-ops (PC→MAR + read, memory→IR), they come **before** any operand step because the opcode is needed to know what to do.
3. The step that does the ALU operation needs the left operand already in the ALU-input latch, so the "load the first operand into the latch" step precedes it. **Operand order matters for non-commutative operations** (subtract): the minuend goes into the latch, the subtrahend is on the bus when the ALU runs.
4. The write-back step (temp/result register → destination) is the last arithmetic step.
5. Memory: command step precedes wait step precedes use of MDR.

**Worked example (original).** `ST Ra, d(Rb)` means M[Rb + d] ← Ra. After fetch, the following steps are listed in shuffled order:

```
(1) Zout, MARin
(2) WMFC
(3) Raout, MDRin, Write
(4) Rbout, Yin
(5) IRoffsetout, Add, Zin
```

- (5) needs Y loaded → (4) before (5).
- (1) uses the Z produced by (5) → (5) before (1).
- (3) asserts `Write`, which needs MAR already loaded (convention 5) → (1) before (3).
- (2) waits for the write → last.

Order: **(4), (5), (1), (3), (2)**. Check: only one `out` per step ✓.

### 5.7 Reading a partial datapath figure (bridge skill)

An unmapped GATE 2025 question (see [PYQ.md](PYQ.md)) shows a *partial* datapath with registers RA, RB, RZ and asks which operand combinations the arithmetic can use. The figure is not in the extracted text, so this is only the method:

1. For **each ALU input**, list every source wired to it (register, bus, immediate/constant, multiplexer input).
2. An operation "register ⊕ register" needs both ALU inputs to be reachable from registers; "register ⊕ immediate" needs one input fed from a register and the other from an immediate path; "immediate ⊕ immediate" needs both inputs reachable from immediate paths simultaneously.
3. Multiplexers matter: a mux with an immediate input on only *one* ALU side restricts which operand slot can hold the immediate.
4. A statement of the form "can *only* implement …" is false as soon as one counter-example operand pair is reachable.

---

## 6. Organisation of a hardwired control unit

```
   IR (opcode field)                         external inputs
        │                                    (condition flags Z,N,C,V;
        ▼                                     interrupt request; MFC)
  ┌───────────────┐                                  │
  │ instruction   │ ADD LD ST BR LDI …               │
  │   decoder     ├─────────────┐                    │
  └───────────────┘             ▼                    ▼
                          ┌─────────────────────────────────┐
  ┌───────────────┐       │   CONTROL SIGNAL GENERATOR      │──► PCout, MARin, Read,
  │ step counter  │       │   (AND-OR network / PLA)        │    Yin, Add, Zin, Rain,
  │   + decoder   ├──────►│   each output = OR of terms     │    Write, WMFC, End …
  │  T1 T2 … Tm   │ T1…Tm │   (instr · step · flag)         │
  └──▲────────▲───┘       └─────────────────────────────────┘
     │ clock  │ reset by End
```

Parts and what each fixes:

- **Instruction decoder** — one output per opcode value (m_i lines). Opcode bits = k ⇒ up to 2ᵏ outputs.
- **Step counter + step decoder** — counter width = ⌈log₂ (number of steps in the longest instruction, *fetch included*)⌉; decoder has that many inputs and one output per step actually used.
- **Control signal generator** — a two-level AND-OR network. The AND terms are `instruction·step` (or just `step` for the fetch steps); the OR collects every place the signal is needed.
- **`End`** resets the step counter (to T1); without `End` the counter would run on.
- **Clock** increments the counter. Each step is one clock period, except the `WMFC` step which is stretched until MFC (§9).

Because the opcode comes from IR and the step from the counter, **a hardwired controller is a finite-state machine** whose state is (IR, step counter, flags) and whose outputs are the control signals.

---

## 7. Deriving the control-signal equations from the micro-operation table

### 7.1 Recipe

1. Write the table of micro-operations for fetch and every instruction (done in §5).
2. For each control signal, scan all rows and note **every (instruction, step)** where it appears. Fetch rows have no instruction qualifier.
3. OR those terms; factor common steps: `ADD·T4 + LD·T4 + ST·T4 = (ADD + LD + ST)·T4`.
4. Add flag qualifiers to those terms that are conditional.
5. Don't-cares: opcode values not used by any instruction can be treated as don't-cares if you minimise further.

### 7.2 Result for the five-instruction machine (verified by script against the tables of §5)

```
PCout       = T1 + BR·T4
MARin       = T1 + (LD + ST + LDI)·T4 + LDI·T6
Read        = T1 + (LD + LDI)·T4 + LDI·T6
Select4     = T1
Add         = T1 + (ADD + BR)·T5
Zin         = T1 + (ADD + BR)·T5
Zout        = T2 + (ADD + BR)·T6
PCin        = T2 + BR·T6
WMFC        = T2 + (LD + LDI)·T5 + ST·T6 + LDI·T7
MDRout      = T3 + (LD + LDI)·T6 + LDI·T8
IRin        = T3
Yin         = (ADD + BR)·T4
Rbout       = (ADD + LD + ST + LDI)·T4
Rcout       = ADD·T5
Raout       = ST·T5
MDRin       = ST·T5
Write       = ST·T5
Rain        = (ADD + LD)·T6 + LDI·T8
IRoffsetout = BR·T5
End         = (ADD + LD + ST + BR)·T6 + LDI·T8
```

Observations that GATE-style questions exploit:

- `Select4`, `IRin` depend on the step only — pure fetch signals; their equations contain no instruction term.
- `Read` and `Write` never share a term: a `Write` term never contains `LD` or `LDI`.
- `Add` and `Zin` have identical equations in this machine, but they are different wires with different jobs (select the ALU function vs enable the Z register).
- In every row at most one `…out` appears per step: checking this is the quickest way to catch a wrong equation.
- `End` is asserted at different steps for different instructions (T6 for four of them, T8 for LDI). If all instructions had the same length, `End` would simply be that one Tk.

### 7.3 Gate counting (state the assumption)

Counting gates depends on how you share logic, so questions must say. Under the usual assumptions:

- A **k-to-n decoder using n of its 2ᵏ outputs** needs n AND gates of k inputs (plus up to k inverters) ⇒ n·(k − 1) two-input ANDs with no sharing.
- The distinct **instruction·step AND terms** are shared by all signals that use them. For this machine the distinct pairs (instruction, step) with some signal asserted are 3 + 3 + 3 + 3 + 5 = **17**, i.e. 17 shared 2-input ANDs; the pure-T terms (T1, T2, T3) need no AND at all.
- The number of OR inputs for a signal = number of product terms in its (flattened) equation. Flattened, `End` has 5 terms (4 at T6, 1 at T8), `WMFC` has 5 (`T2`, `LD·T5`, `ST·T6`, `LDI·T5`, `LDI·T7`).
- Total flattened product terms over the 20 signals: **52** (script count).

**Worked example 7-A (decoders).** The step counter must reach T8 (3 fetch + 5 LDI execute) ⇒ 8 steps ⇒ ⌈log₂ 8⌉ = **3 counter bits**; the step decoder is 3-to-8 using all 8 outputs ⇒ 8 × (3 − 1) = **16** two-input ANDs (no sharing). The opcode field needs ⌈log₂ 5⌉ = **3 bits**; the instruction decoder is 3-to-8 with 5 outputs used ⇒ 5 × 2 = **10** two-input ANDs.

**Worked example 7-B (build one equation).** Signal `Yin` loads the ALU's left register. Scan the table: ADD at T4, BR at T4, nowhere else ⇒ `Yin = ADD·T4 + BR·T4 = (ADD + BR)·T4`. If a new instruction `INC Ra` is added with T4 `Raout, Yin`, then `Yin = (ADD + BR + INC)·T4` and also `Raout = ST·T5 + INC·T4`. **Adding an instruction changes the logic (new AND/OR terms)** — that is the cost of hardwiring.

---

## 8. Design methods for the sequencing part

All three describe the same behaviour; they differ in where "which step am I in" is stored.

### 8.1 Method A — instruction decoder × step counter (the organisation of §6)

- State = step number only (instruction identity comes from IR).
- Number of timing states = length of the longest instruction (fetch included); counter bits = ⌈log₂ that⌉.
- Pro: small counter, easy to reason about. Con: every signal equation has to AND the instruction with the step.

### 8.2 Method B — state table / finite-state machine (one state per distinct control state)

Here the controller does not keep the opcode "outside": the state itself says "I am in the 2nd execute step of ADD". The number of states is

```
S = (fetch states) + Σ over instructions (private execute states)
    − (states that are merged because they assert identical signals and have identical next-state behaviour)
state bits = ⌈log₂ S⌉
```

**Worked example 8-A (five-instruction machine).** Fetch 3; execute 3 + 3 + 3 + 3 + 5 = 17 private states ⇒ S = 20 ⇒ ⌈log₂ 20⌉ = **5 bits**. If LD and LDI are allowed to share their first two states (they assert identical signals in T4 and T5 and only diverge afterwards) then S = 20 − 2 = **18** ⇒ still 5 bits. Contrast with Method A on the same machine: only **3 bits** (the step counter), because the instruction identity is *not* stored in the counter. **Trap:** do not apply Method B's state count when the question describes a step counter, and vice-versa; read which design is described.

### 8.3 Method C — delay-element / one-hot ("sequence" or ring) method

One flip-flop per state; exactly one flip-flop holds 1 at any time, and that 1 moves to the next flip-flop each clock (a chain of delay elements). The flip-flop outputs are the T-lines directly, so **no decoder and no decoder delay**. A signal is just the OR of the delay-element outputs where it is needed; at the end of fetch the 1 is steered by the instruction decoder into the chain of the decoded instruction (an AND per instruction), and the last element of each chain feeds back to T1 (this is `End`).

```
 T1 ─► T2 ─► T3 ─┬─(·ADD)─► A4 ─► A5 ─► A6 ──┐
                 ├─(·LD )─► L4 ─► L5 ─► L6 ──┤
                 ├─(·ST )─► S4 ─► S5 ─► S6 ──┤──► back to T1
                 ├─(·BR )─► B4 ─► B5 ─► B6 ──┤
                 └─(·LDI)─► I4 ► I5 ► I6 ► I7 ► I8 ┘
 each box is a D flip-flop; Yin = A4 + B4,  Zout = T2 + A6 + B6, End = A6 + L6 + S6 + B6 + I8
```

Counting (five-instruction machine): flip-flops = **20** (one per distinct state; 18 if the LD/LDI prefix is shared). A binary state register would need 5; a binary step counter with T1…T8 would need 3; a one-hot *step* ring T1…T8 would need 8.

Trade-off summary: binary = fewest flip-flops, needs decoders (slower, more gates); one-hot = more flip-flops, almost no decoding (fastest, simplest equations, regular layout).

**Worked example 8-B (compare encodings).** An accumulator machine has a 4-state fetch and four instructions with execute lengths 2, 4, 6 and 3 (no sharing). S = 4 + 2 + 4 + 6 + 3 = 19. Binary state register: ⌈log₂ 19⌉ = 5 (2⁴ = 16 < 19 ≤ 32). One-hot: 19. Difference 19 − 5 = **14** extra flip-flops, bought to save decoder delay.

### 8.4 Method D — ROM / PLA implementation of the same truth table

The function "(opcode, step) → control signals" is a truth table; it can be stored in a ROM or implemented in a PLA instead of random AND-OR gates.

```
ROM bits = 2^(opcode bits + step bits) × (number of control signals)
```

**Worked example 8-C.** 5-bit opcode, 4-bit step counter, 26 control signals: address = 9 bits ⇒ 2⁹ = 512 words × 26 = 13 312 bits = 13 312 / 8 = **1664 bytes**. (Units: say "bits" unless asked bytes. Divide by 8 only at the end.)

Why this is *not* microprogramming: the ROM has no next-address field and no sequencing logic of its own; the step counter and the fixed instruction decoder still dictate the order, and the ROM is addressed by (opcode, step), so most words would be wasted (most opcode/step combinations never occur). A real microprogram ROM stores a *sequence* of microinstructions, each carrying (or implying) its successor — see [../02-MICROPROGRAMMED](../02-MICROPROGRAMMED).

---

## 9. Control steps, memory wait and CPI

### 9.1 Steps → cycles → CPI

In a multi-cycle hardwired design, **one control step = one clock cycle** (WMFC steps may last longer). Therefore

```
cycles for an instruction = Σ (cycles of each step)
CPI = Σ_i  fraction_i × cycles_i
CPU time = IC × CPI × T_clk = IC × CPI / f
```

### 9.2 Memory wait

Let the memory need **L** whole clock cycles after the edge that loads the address. A WMFC step then lasts `max(1, L)` cycles; the other work in that step (e.g. PC update in fetch T2) overlaps. With `L = ⌈T_mem / T_clk⌉`.

Cycles per instruction (five-instruction machine):

```
fetch = 1 (T1) + max(1,L) (T2) + 1 (T3)
ADD  = fetch + 3
LD   = fetch + 1 + max(1,L) + 1
ST   = fetch + 1 + 1 + max(1,L)
BR   = fetch + 3
LDI  = fetch + 1 + max(1,L) + 1 + max(1,L) + 1
```

**Worked example 9-A (ideal memory, L = 1).** Step table: 6, 6, 6, 6, 8. Mix: ADD 40 %, LD 25 %, ST 15 %, BR 15 %, LDI 5 %.
CPI = 0.40·6 + 0.25·6 + 0.15·6 + 0.15·6 + 0.05·8 = 0.95·6 + 0.05·8 = 5.70 + 0.40 = **6.10**.

**Worked example 9-B (slow memory, L = 3).** Fetch = 1 + 3 + 1 = 5. ADD = 8, LD = 5 + 1 + 3 + 1 = 10, ST = 5 + 1 + 1 + 3 = 10, BR = 8, LDI = 5 + 1 + 3 + 1 + 3 + 1 = 14.
CPI = 0.40·8 + 0.25·10 + 0.15·10 + 0.15·8 + 0.05·14 = 3.2 + 2.5 + 1.5 + 1.2 + 0.7 = **9.10**.
Observe: memory latency inflates CPI; the hardwired logic is the same.

**Worked example 9-C (CPU time).** With CPI = 9.10, f = 200 MHz, IC = 4 × 10⁶: time = 4×10⁶ × 9.10 / 200×10⁶ = **0.182 s = 182 ms**.

### 9.3 Fixed vs instruction-dependent step counts

- Simple RISC-style controllers often give **every instruction the same number of steps** (then `End` is a single `Tk`). CPI is that fixed number.
- If lengths differ (as above) you must use the *weighted* CPI. Don't average the step counts unweighted unless the question says "equally likely".

---

## 10. Timing: the clock period constraint

Within one step the following chain must complete before the next clock edge:

```
step register / IR clk→Q  →  decoders  →  control logic (AND-OR)  →  gate onto bus (register out-enable)
   →  bus propagation  →  ALU (if used)  →  setup time of the destination register
```

The instruction decoder and step decoder work **in parallel**, so only the **slower** of the two counts. Hence

```
T_clk ≥ t_clk→Q + max(t_instr-dec, t_step-dec) + t_logic + t_reg-out + t_bus + t_ALU + t_setup
```

(drop the ALU term for steps that don't use it — but the clock is set by the *worst* step.)

**Worked example 10-A.** t_clk→Q = 0.5 ns, instruction decoder 1.0 ns, step decoder 0.7 ns, control logic 1.8 ns, register out-gate 0.4 ns, bus 0.8 ns, ALU 2.4 ns, setup 0.3 ns.
Control ready: 0.5 + max(1.0, 0.7) + 1.8 = 3.3 ns. Data path: 0.4 + 0.8 + 2.4 + 0.3 = 3.9 ns. Period ≥ **7.2 ns** ⇒ f ≤ 138.9 MHz. (A step that is only a register move needs 3.3 + 0.4 + 0.8 + 0.3 = 4.8 ns, but the ALU step dictates the clock.)
Trap: adding both decoder delays gives 7.9 ns — wrong, they run side by side.

Edge case (the T4 step): the opcode is only valid after `IRin` at the end of T3, so for T4 the opcode path starts at the IR's clk→Q, just like the step counter's. In later steps IR has been stable for several cycles. A question that says "the opcode in IR is already stable at the clock edge" means the instruction decoder starts early and can only matter if it is slower than the step path — in a parallel arrangement you still take the max of the two branches, never their sum.

**Equivalent view — what limits the clock:** the longest single micro-operation path. To speed up the clock you split a long step into two (more steps, shorter period): this raises CPI but lowers T_clk (see Worked example 11-B).

---

## 11. Single-cycle vs multi-cycle vs pipelined

A hardwired controller can drive any of the three. The difference is how many cycles an instruction occupies and how long the cycle is.

| Design | Cycle time | CPI | Control unit |
|---|---|---|---|
| Single-cycle | longest *instruction* path (+ register overhead) | 1 | purely combinational function of opcode (no step counter) |
| Multi-cycle | longest *step* (+ overhead) | average steps per instruction (≥ 3 typically) | opcode + step counter / FSM |
| Pipelined | longest *stage* + pipeline-register overhead | 1 + average stall cycles | per-stage control derived from the opcode and carried along with the instruction |

**Worked example 11-A (classic five-stage datapath, original numbers).** Stage delays: IF 200 ps, ID 100 ps, EX 150 ps, MEM 200 ps, WB 100 ps; register overhead 20 ps per cycle.

- Path lengths: R-type uses IF+ID+EX+WB = 550; LW uses all five = 750; SW uses IF+ID+EX+MEM = 650; BR uses IF+ID+EX = 450.
- **Single-cycle:** clock = 750 + 20 = **770 ps**, CPI = 1 ⇒ 770 ps/instruction.
- **Multi-cycle:** clock = max stage + overhead = 200 + 20 = **220 ps**. Steps: R-type 4, LW 5, SW 4, BR 3. Mix 45 % / 25 % / 15 % / 15 % ⇒ CPI = 0.45·4 + 0.25·5 + 0.15·4 + 0.15·3 = 1.8 + 1.25 + 0.6 + 0.45 = **4.10**. Time = 4.10 × 220 = **902 ps/instruction**.
- **Pipelined:** clock 220 ps, assume 0.25 stall cycles/instruction ⇒ CPI = 1.25 ⇒ **275 ps/instruction**.
- Speed ratios: single/multi = 770 / 902 = **0.854** (multi-cycle is *slower* here — the stages are unbalanced, 200 ps slowest vs. 150 ps average, and every step pays the 20 ps overhead); single/pipelined = 770 / 275 = **2.8**; multi/pipelined = 902 / 275 = **3.28**.

Lesson: "multi-cycle is faster than single-cycle" is **not automatic**. It wins only when the average instruction needs enough less time than the longest instruction to pay for the per-cycle overhead and stage imbalance. Pipelining is what really changes throughput (k + N − 1 cycles for N instructions in an ideal k-stage pipeline; see [../../07-INSTRUCTION-PIPELINING](../../07-INSTRUCTION-PIPELINING)).

**Worked example 11-B (split a long step).** Suppose the longest step (ALU, 6.0 ns) sets the clock; the next-longest step is 4.4 ns. Splitting the ALU operation into two steps adds 0.5 ns latch overhead, so each half takes (6.0 + 0.5)/2 = 3.25 ns and the new clock is max(4.4, 3.25) = 4.4 ns. If the average instruction contains 1.4 ALU steps and the old CPI was 6.1, the new CPI is 6.1 + 1.4 = 7.5.
Old time/instruction = 6.1 × 6.0 = 36.6 ns; new = 7.5 × 4.4 = 33.0 ns ⇒ speed-up = 36.6/33.0 = **1.11**. Always compute both effects.

---

## 12. Hardwired vs microprogrammed; the RISC link

### 12.1 Comparison table (typical, not absolute)

| Aspect | Hardwired | Microprogrammed |
|---|---|---|
| Where the control "program" lives | In gates / PLA / flip-flop sequencer | In a control store (ROM/RAM) read each cycle |
| Speed | Faster: delay = decoders + a few gate levels | Slower: each step needs a control-store access (+ next-address logic) |
| Modifying or adding an instruction | Redesign / re-wire logic (new AND/OR terms) | Change/add microroutines (rewrite ROM, or reload if writable) |
| Complexity vs ISA size | Grows quickly; hard for hundreds of instructions with many steps | Scales more gracefully; regular structure |
| Design effort & errors | High for complex ISAs; fixing after fabrication is impossible | Lower; can patch microcode |
| Hardware cost | Random logic; area grows with ISA | Control store area + sequencer; roughly independent of logic complexity |
| Best fit | RISC (few simple instructions, fixed formats) | CISC (many complex, variable-length instructions) |
| Instruction-dependent step counts | Natural (different `End` points) | Natural (microroutines of different lengths) |
| Emulation of other ISAs / field upgrade | Not possible | Possible |

Typical exam statements: "hardwired is faster"; "microprogrammed is easier to modify / more flexible"; "hardwired suits RISC, microprogrammed suits CISC"; "control memory exists only in microprogrammed control". All of these are *typical* statements; exceptions exist in real chips (modern CISC processors decode most instructions in hardwired logic into simple internal operations and keep microcode only for rare complex ones — if a question demands the textbook contrast, use the table).

**Worked example 12-A (time comparison, original numbers).** One instruction needs 5 control steps. Hardwired: 5 × 2 ns = 10 ns. Microprogrammed: 7 microinstructions, each costing a 3 ns control-store access + next-address cycle: 7 × 3 = 21 ns. Ratio = 21/10 = **2.1×** slower. (Microprogram internals — formats, sequencing — are in the sibling topic.)

### 12.2 Why RISC and hardwired go together

RISC processors aim at **one simple instruction per pipeline slot at a high clock rate**. Each classic RISC design characteristic helps either the decode logic or the pipeline, which in turn makes hardwired control cheap:

| RISC characteristic | Why it helps | Link to hardwired control |
|---|---|---|
| **Register-to-register arithmetic (load/store architecture)**: only `load` and `store` touch memory; ALU instructions take their operands from registers and put the result in a register | Every ALU instruction has the same short step sequence; the memory stage is used by only two instruction types; no memory-to-memory operations, no multi-trip indirections | Few distinct (instruction, step) combinations ⇒ small AND-OR network; control signals per stage are simple |
| **Fixed-length instruction format** (e.g. 32 bits) | Next-PC is known without decoding; register fields at fixed bit positions can be read in parallel with the opcode decode; no multi-word fetch | Decoder is a small fixed-width decode; no logic to find instruction boundaries |
| **Few instruction formats and addressing modes** | Less decoding; effective-address logic is just base+offset | Fewer rows in the micro-operation table |
| **Hardwired control unit** | Short control path ⇒ higher clock rate; most instructions complete in one pipeline slot | The topic of this note |
| **Large register file** | Keeps operands out of memory | Fewer memory steps per instruction |
| **Pipelining-friendly (uniform instruction timing)** | Uniform stages | Per-stage control generated from opcode early and carried down the pipeline |

CISC contrast: variable-length instructions, memory-to-memory and indirect operands, many addressing modes, many instructions ⇒ long and instruction-specific step sequences ⇒ the hardwired table becomes huge, which pushes designers to microprogramming.

How to answer a "which of the following are RISC characteristics" question: evaluate **each** statement separately against the table above (the three typical statements are "register-register arithmetic / load-store", "fixed-length instructions", "hardwired control"), then combine. Do not assume the answer by elimination of options you are unsure of, and confirm the official key before trusting any answer (the mapping file for the 2018 entry says "VERIFICATION REQUIRED").

---

## 13. Flags and interrupts as control inputs (brief)

- **Condition flags** (Z, N, C, V from the ALU) enter the control signal generator as extra AND-inputs *only on the terms that depend on them*, e.g. `PCin = T2 + BRZ·T6·Z`. Careful: the *fetch* term `T2` must stay unconditional, otherwise a zero flag at the wrong time would stop PC from advancing. (A form like `(T2 + BRZ·T6)·Z` is wrong for that reason.)
- **Interrupt request:** sampled at the end of an instruction (usually when `End` would be asserted). If an enabled interrupt is pending, the controller starts an *interrupt sequence* (save PC and flags, load the handler address) instead of fetching T1. Hardware effect: extra states / steps and one more input; details belong to [../../06-IO-INTERFACE/01-INTERRUPT](../../06-IO-INTERFACE/01-INTERRUPT).
- **MFC** (memory function complete) from memory is also an input: it ends a stretched WMFC step.

---

## 14. Step-by-step GATE solving procedure

1. **Identify the machine:** which datapath is described (single bus? separate buses? Y/Z?). Write the rules (§4) in your head: one `out` per step on a single bus; ALU left operand in a latch; result in a latch; registers load at the end of the step.
2. **Draw the micro-operation table** for the instruction(s) asked, step by step. Keep fetch separate (3 steps unless the question gives its own).
3. **Decide what is counted:** execute steps only, or fetch + execute; steps or cycles (WMFC may take L cycles); average or worst case.
4. **For "bits" questions** decide *which* register: step counter (log₂ of longest sequence) vs one-state-per-state register (log₂ of total distinct states) vs one-hot (number of states).
5. **For signal equations:** list rows where the signal appears, OR them, factor.
6. **For clock-period questions:** draw the path timeline; take the max of parallel branches, then add serial delays.
7. **For comparisons:** compute CPI, T_clk, then time/instruction = CPI × T_clk; do not compare CPI or clock alone.
8. **Units:** ns vs ps, bits vs bytes (÷ 8 at the end), K = 2¹⁰.

---

## 15. PYQ patterns (this topic + cross-filed)

(No answers are stated for any actual PYQ; the mapping lists "VERIFICATION REQUIRED" for all.)

| Pattern | Recognise by | Recipe | Trap |
|---|---|---|---|
| **P1 — RISC design characteristics (GATE 2018, in this folder)** | A list of design features I/II/III incl. "hardwired control unit", answer options are combinations | Check each feature independently (§12.2): register-register arithmetic ↔ load/store, fixed-length ↔ simple decode, hardwired ↔ short control path | Judging on partial knowledge or by elimination; thinking "hardwired" is a CISC feature; thinking RISC may not have register-register arithmetic because loads exist |
| **P2 — Data-path step ordering (GATE 2020, filed under ALU)** | Figure of a bus with registers + ALU + temporaries; a shuffled list of register-transfer steps for one instruction | §5.6 dependency method | Operand order; putting a fetch micro-op after execute micro-ops; mapping text and figure are garbled — check the PDF, don't guess |
| **P3 — Interpret a micro-operation sequence (GATE 2013, 4 booklet copies filed under Interrupt)** | A list like `MBR ← PC; MAR ← X; PC ← Y; Memory ← MBR` and a question "which operation is this?" | Read each transfer: what is *saved to memory*, what *address* is formed, what is *loaded into PC*. Compare with how fetch (§5.2) and store (§5.3) look. Use register-transfer reading skill of §5 | Mapping lists the same question four times (one question); choose by what each micro-op does, not by names alone |

Existing-practice style (not PYQ): step/state counting, ROM size, clock period, execute-cycle counting — covered by §7–§10.

---

## 16. Traps and misconceptions

1. **"Hardwired" ≠ "no flexibility in the programs it runs".** It means the *control logic* is fixed; the machine still runs any program in its ISA.
2. **Counting fetch steps in "execute steps"** (or forgetting fetch in a total).
3. **Step-counter bits vs state-register bits.** Counter: ⌈log₂ longest sequence⌉. FSM with unshared states: ⌈log₂ total states⌉. One-hot: total states flip-flops. (Existing Q3 vs Q8 are the two different readings.)
4. **Two decoders in series?** No — instruction decoder and step decoder are parallel.
5. **Two `…out` in the same step on a single bus** (bus conflict). A valid step has ≤ 1 `out`, any number of `in`.
6. **Using a register in the step that loads it.** Loaded values are available from the next step.
7. **`Read` asserted in a store.** `Write`, not `Read`; `Read` belongs to loads and fetch.
8. **ROM size: forgetting that the ROM is addressed by both opcode and step bits**, or giving bits when bytes are asked.
9. **Multi-cycle always beats single-cycle.** False when the longest step is long compared with the average and overhead is large (§11).
10. **Unweighted CPI.** Use instruction-mix weights.
11. **Memory wait ignored**: a trip to memory is a command step + WMFC step; slow memory stretches WMFC to ⌈T_mem/T_clk⌉ cycles.
12. **Putting a flag on the whole `PCin`** instead of only on the branch term.
13. **Hardwired is not "always better".** It is faster but harder to modify and design for large ISAs.

## 17. Edge cases and assumptions to state

- Datapath (single bus, Y/Z, or other) and the rule "one out per step".
- Byte-addressable memory, 4-byte instructions ⇒ PC + 4 (word-addressable ⇒ +1).
- Whether decoding is a separate step (here: no, combinational).
- Memory latency in cycles L; whether fetch's WMFC step also hides the PC update.
- Whether register overhead is added per cycle in every design (single-cycle too).
- Whether state sharing between instructions is allowed in state counts.
- Whether `End` can come earlier for some outcomes (e.g. branch not taken).

## 18. Connections to other COA topics

- **Instruction set / addressing modes:** every addressing mode adds micro-operations (register-indirect adds a MAR load, displacement adds an ALU step, memory-indirect adds a whole memory trip) ⇒ longer sequences, larger control logic.
- **ALU:** `Add/Sub/And…` select lines and the flags it produces are control-unit interfaces.
- **Microprogrammed control:** same micro-operation tables, different implementation (§12).
- **Pipelining:** the control signals of an instruction are generated once and passed down the pipeline registers; the same micro-operation thinking gives the stage work (IF, ID, EX, MEM, WB).
- **Interrupts / DMA:** extra inputs to the control unit and extra control sequences.
- **Digital logic:** decoders, counters, one-hot rings, PLAs/ROMs are the components.

---

## 19. Existing practice coverage map

| Existing Q# | Skill | NOTES section |
|---|---|---|
| Q1 | What produces control signals (logic from opcode + step) | §2, §6 |
| Q2 | Role of step counter / timing state | §3, §6 |
| Q3 | Binary bits for N timing states | §6, §8.1, Example 7-A |
| Q4 | Which actions belong to fetch (opcode-independent) | §5.1–§5.2 |
| Q5 | Properties of hardwired vs microprogrammed (opcode as input, change = change logic, no microprogram ROM) | §6, §7.3 (adding an instruction), §12 |
| Q6 | ROM size from (opcode+state) address bits × signals | §8.4, Example 8-C |
| Q7 | Execute cycles of reg-reg ADD on a one-bus datapath | §4 rule 1, §5.3, §5.5 (Z-less variant) |
| Q8 | State register width with shared fetch + private execute states | §8.2, Example 8-A/8-B |
| Q9 | Reading a STORE micro-op sequence (address→MAR, data→MDR+Write) | §5.3 (ST), §4 rule 5 |
| Q10 | Clock period with parallel decoders, clk→Q, logic, setup | §10, Example 10-A |

## 20. Self-check

1. Write "every control signal = f(…)" and name the three kinds of inputs.
2. List the fetch micro-operations and say why fetch cannot depend on the opcode.
3. Why can't two registers drive a single bus in the same step, and how many registers may load?
4. Derive the number of execute steps of `LD Ra, d(Rb)` on the reference datapath.
5. How many bits does the step counter need if the longest instruction has 11 steps in total?
6. Distinguish step-counter bits, FSM state bits and one-hot flip-flops for the same machine.
7. Write the equation of a signal that is asserted at T4 of ADD and BR and at T1.
8. Why do the two decoders not add up in the clock-period formula?
9. Compute a weighted CPI when a WMFC step lasts 3 cycles.
10. Give three reasons hardwired control is preferred for RISC and one reason against it for a large CISC.
11. When is multi-cycle slower than single-cycle?
12. Why is a ROM addressed by (opcode, step) not a microprogrammed control unit?

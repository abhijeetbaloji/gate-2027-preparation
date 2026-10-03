# Hardwired Control — Last-Minute Revision

Full explanations: [NOTES.md](NOTES.md). Formulas: [FORMULAS.md](FORMULAS.md). Sibling topic: [../02-MICROPROGRAMMED](../02-MICROPROGRAMMED).

## Key definitions

- **Control unit** = produces control signals (register `in`/`out`, ALU function, `Read`/`Write`, mux selects) each clock cycle.
- **Hardwired:** every control signal = Boolean function of **(opcode from IR, step from step counter, flags)**, built from decoders + AND-OR gates (or PLA / one-hot flip-flop chain). No control store.
- **Control step (T-step)** = one clock cycle; **`End`** resets the step counter; **`WMFC`** stretches a step until memory is done.
- Fetch is **identical for every instruction** (opcode unknown yet): `MAR←PC, Read, Z←PC+4` | `PC←Z, wait` | `IR←MDR`.

## Reference one-bus datapath rules

1. One `…out` per step; many `…in` allowed.
2. ALU = (Y or constant 4) op **bus**; result → Z; `Zout` next step.
3. A register loaded in Tk is usable from Tk+1.
4. Memory trip = command step (+`Read`/`Write`) + wait step.

## Step counts (execute only; fetch = 3 more)

```
ADD Ra,Rb,Rc : Rbout,Yin | Rcout,Add,Zin | Zout,Rain          → 3
LD  Ra,(Rb)  : Rbout,MARin,Read | WMFC | MDRout,Rain          → 3
ST  Ra,(Rb)  : Rbout,MARin | Raout,MDRin,Write | WMFC         → 3
BR  off      : PCout,Yin | IRoffsetout,Add,Zin | Zout,PCin    → 3
LDI (memory-indirect): two memory trips                       → 5
LD  Ra,d(Rb) : address ALU step adds 2 steps                  → 5
```

## Must-remember formulas

```
step-counter bits  = ⌈log₂ (steps of longest instruction, fetch included)⌉
FSM state bits     = ⌈log₂ (fetch + Σ private execute states − merged)⌉ ;  one-hot = #states flip-flops
decoder gates      = n·(k−1) 2-input ANDs for n used outputs of a k-input decoder
ROM bits           = 2^(opcode bits + step bits) × #signals     (÷8 for bytes)
CPI                = Σ fraction × cycles ;  L = ⌈T_mem/T_clk⌉ ; WMFC step = max(1,L) cycles
T_clk ≥ clk→Q + max(instr-dec , step-dec) + logic + reg-out + bus + ALU + setup
CPU time           = IC × CPI × T_clk ;  time/instr = CPI × T_clk
```

## Single vs multi vs pipelined

| | Cycle time | CPI |
|---|---|---|
| single | longest instruction | 1 |
| multi | longest step | weighted steps |
| pipeline | longest stage + overhead | 1 + stalls |

Multi-cycle is **not** automatically faster than single-cycle.

## Hardwired vs microprogrammed

| | Hardwired | Microprogrammed |
|---|---|---|
| Speed | faster | slower (control-store access per step) |
| Change / add instruction | redesign logic | edit microcode |
| Large complex ISA | costly, hard | manageable |
| Fits | RISC | CISC |
| Has control memory | no | yes |

RISC pattern: register-register arithmetic (load/store), fixed-length instructions, few formats/modes, hardwired control — each helps decode/pipelining. Judge each statement separately.

## Fast-solve checklist

1. Draw the micro-op table (fetch + instruction). 2. Decide what is counted (fetch? cycles? weighted?). 3. Which "bits": counter vs state register vs one-hot. 4. Parallel decoders → max. 5. Time per instruction = CPI × T_clk. 6. Bits vs bytes at the end.

## Top traps

- Two `out` in one step; using a value in the step that loads it.
- Counting only execute steps (or only fetch).
- State-register width vs step-counter width.
- Adding both decoder delays.
- Unweighted CPI; ignoring memory wait; forgetting ⌈ ⌉ in L.
- Flag on the whole `PCin` instead of just the branch term.
- `Read` in a store.

## Evidence-based concept priority

1. RISC characteristics ↔ hardwired control (mapped 2018 entry).
2. Micro-operation / data-path step sequences (2020 ordering question filed under ALU; 2013 micro-operation sequence filed under Interrupt).
3. Counting questions (steps, bits, ROM, decoders), CPI and clock-period arithmetic (existing practice only).

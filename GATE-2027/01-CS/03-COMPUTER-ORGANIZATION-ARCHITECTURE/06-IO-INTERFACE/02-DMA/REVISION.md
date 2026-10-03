# DMA — Last-minute Revision

Full treatment: [NOTES.md](NOTES.md). Interrupt side: [../01-INTERRUPT](../01-INTERRUPT/NOTES.md).

## Key ideas

- DMA = a controller moves data between device and memory; the CPU only programs it (address, count, control) and gets one
  completion interrupt per block. Cost moves from per unit to per block.
- Controller: address register (+unit each time), count register (−1 each time, 0 = terminal count), control/status, data buffer;
  signals DREQ/DACK (device side), HOLD/HLDA or BR/BG (bus side), INTR.
- Sequence: CPU programs -> DREQ -> HOLD -> HLDA -> transfers (AR+, CR−) -> CR = 0 -> interrupt -> ISR.
- Only one bus master drives the shared bus at a time. DMA normally outranks the CPU in arbitration.

## Modes

```
Burst:           keeps bus for whole block   best DMA throughput    longest CPU stall (A + N cycles)
Cycle stealing:  one unit per grant          lower throughput       shortest stall (A + 1 cycles)
Transparent:     only idle bus cycles        zero CPU delay         DMA throughput not guaranteed
```

## Must-remember formulas

```
R (B/s)  = p × f_b × w / k          bits/s = ×8          p = k·R / (f_b·w)     (p ≤ 1 feasibility)
slowdown = 1/(1 − p)  (CPU uses every cycle)
burst occupancy A + N ;  stealing N(A + 1) ;  N_max = ⌊L/T_b⌋ − A
break-even n_min = ⌊(S + C)/(c_int − c_st)⌋ + 1
bursts = ⌈ file bytes / (2^m × u) ⌉      (KB = 1024 bytes; 2^m units per programming)
address register = ⌈log₂ addressable units⌉
peak BW = width × clock ; sustained = bytes / time per transaction ; data phase = ⌈t_access / T⌉ cycles
```

## Arbitration at a glance

| Scheme | Lines | Priority | Note |
|---|---|---|---|
| Daisy chain | 3 (BR, BG, BBSY) | by position | slow, can starve, one fault breaks chain |
| Polling | ⌈log₂N⌉ + BR + BBSY | by poll order (rotating possible) | |
| Independent | 2N | any, in arbiter | fastest, most wiring |
| Distributed | ID lines, no arbiter | highest ID | text-dependent line count |

## PIO vs interrupt vs DMA

PIO: CPU moves each unit, busy-waits. Interrupt: CPU moves each unit inside ISR, free between. DMA: no CPU per unit,
best for bulk/fast devices. Interrupt-driven beats polling on CPU use only if ISR time ≪ device period.

## DMA and caches/VM

Input DMA: invalidate stale cache lines. Output DMA with write-back: flush dirty lines first. Write-through helps
output only. DMA uses physical addresses; pages pinned during transfer.

## Fast-solve checklist

1. Unit per cycle w and cycles per unit k? 2. Which clock does the % refer to? 3. Bytes -> bits last. 4. KB = 1024. 5. Ceil for counts.
6. State 2^m convention for count register. 7. Include A for burst vs stealing. 8. p > 1 is impossible.

## Top traps

Bytes vs bits; unit width (device 8-bit vs DMA 4 bytes); k = 2 for store-and-forward DMA; floor instead of ceil; "DMA = no interrupts";
"cycle stealing stops the CPU"; "burst always best"; "two masters at once"; write-through fixes both directions.

## What the mapped PYQs tested (evidence only)

Rate from clock, percent of cycles and bytes per cycle (2 entries); bus takeovers for a file given a count register (1); true/false on
DMA modes and I/O methods (1); best mechanism for bulk transfer (1); mixed daisy chain/polling/vectored/DMA bus-master statements (1).

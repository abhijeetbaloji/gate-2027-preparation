# DMA — Formulas

Derivations and context: [NOTES.md](NOTES.md). Conventions: K = 2^10, M = 2^20 for sizes; clock in MHz = 10^6 Hz; 1 byte = 8 bits;
a data rate in "MB/s" = 10^6 B/s unless stated.

Symbols: f clock (Hz); f_b bus-cycle rate; T_b = 1/f_b; w bytes per DMA bus cycle; k bus cycles per unit; p fraction of cycles
used by DMA; R data rate (B/s); A arbitration cycles per bus acquisition; N units in a block; S, C set-up and completion cycles.

---

## 1. Rate and fraction of cycles

### 1.1 Rate from percentage of cycles  <a id="rate-from-fraction"></a>

```
cycles used per second = p × f_b
R (bytes/s) = p × f_b × w / k          R (bits/s) = 8 × p × f_b × w / k
```

- When: cycle stealing at regular intervals, p given as a fraction of processor (or bus) cycles.
- Why: bus offers f_b cycles per second, p of them are DMA's, each moves w bytes (if one unit takes k cycles then one unit per k cycles).
- Example: f_b = 5 MHz, p = 1.2 %, w = 2, k = 1: 60,000 cycles/s; 120,000 B/s; 960,000 b/s (verified).
- Misuse: using bytes when the answer asks for bits; p as percent without dividing by 100; CPU clock when the question states a different bus clock.

### 1.2 Fraction of the bus consumed  <a id="bus-fraction"></a>

```
p = k × R / (f_b × w)            (bus capacity = f_b × w bytes/s)
```

- When: device rate R is given and the bus clock and width are known.
- Why: cycles needed per second = k·R/w; cycles offered = f_b.
- Example: R = 750,000 B/s, f_b = 25 MHz, w = 1, k = 1: p = 3 %; k = 2: p = 6 %. R = 300,000 B/s, T_b = 100 ns, k = 2: p = 6 %.
- Feasibility: p ≤ 1 is required; if p > 1 the bus cannot sustain the device.
- Misuse: forgetting k = 2 for store-and-forward DMA; using device width instead of bytes per bus cycle.

### 1.3 Narrow device, wide DMA unit  <a id="wide-narrow"></a>

```
p = R / (f_b × w_bus)        (w_bus = bytes moved per bus cycle after assembling in the controller's buffer)
```

- Example: device 1.6 × 10^6 B/s, 2-byte unit, 10 MHz: p = 8 % (16 % if byte at a time).

### 1.4 Remaining CPU share and slowdown  <a id="slowdown"></a>

```
CPU share of cycles = 1 − p              time = T_alone / (1 − p)           slowdown = 1/(1 − p)
```

- When: the CPU would use the bus every cycle. Overestimates the slowdown if a cache absorbs CPU accesses.
- Example: p = 8 %, T_alone = 46 s -> 50 s.

---

## 2. Burst vs stealing

### 2.1 Bus occupancy of a block  <a id="burst-vs-stealing"></a>

```
Burst:     (A + N) cycles, in one stall
Stealing:  N × (A + 1) cycles, in N stalls of (A + 1) cycles
```

- Why: the arbitration overhead A is paid once per acquisition; burst has one acquisition, stealing has N.
- Example: N = 512, A = 2, T_b = 40 ns: burst 514 cycles = 20.56 µs; stealing 1536 cycles = 61.44 µs.
- Misuse: ignoring A makes both modes look equal in total cycles.

### 2.2 Worst-case CPU stall and maximum burst  <a id="max-burst"></a>

```
stall_burst = (A + N) × T_b          stall_steal = (A + 1) × T_b
N_max = ⌊L / T_b⌋ − A                (L = longest tolerable continuous stall)
```

- Example: L = 2 µs, T_b = 50 ns, A = 3: N_max = 40 − 3 = 37.
- Misuse: forgetting to subtract A; not flooring.

### 2.3 Sustainable device rate per mode  <a id="sustainable-rate"></a>

```
Cycle stealing: R_max = f_b × w / (A + 1)
Burst of N:     R_max = f_b × w × N / (A + N)
```

- Example: f_b = 50 MHz, w = 4, A = 1: stealing 100 × 10^6 B/s; N = 16: 188.2 × 10^6 B/s; ratio = 2N/(N + 1) = 32/17 = 1.88.
- Assumes DMA may use all bus cycles (an upper bound).

---

## 3. Overhead and break-even

### 3.1 CPU cost per block  <a id="block-cost"></a>

```
Programmed I/O (device always ready):   n × c_pio       (with a slow device: elapsed time n × T_dev, the CPU spins)
Interrupt-driven:                       n × c_int
DMA:                                    S + C + n × c_st    (c_st = stolen cycles per unit, counted as lost)
```

### 3.2 Break-even block size  <a id="break-even"></a>

```
DMA cheaper  <=>  n > (S + C) / (c_int − c_st)       smallest n = ⌊(S + C)/(c_int − c_st)⌋ + 1
```

- Example: c_int = 90, S = 300, C = 500, c_st = 1: ratio 8.988; n = 9 (810 vs 809). vs c_pio = 30: ratio 27.59; n = 28.
- Requires c_int > c_st (otherwise DMA never wins on CPU cost).
- Misuse: rounding to the nearest integer; using ≥ when the ratio is an integer (that is a tie, not a win).

### 3.3 Fraction of CPU time used by interrupt-driven I/O  <a id="interrupt-fraction"></a>

```
busy fraction = t_isr / T_dev          free fraction = 1 − t_isr / T_dev
```

- Example: t_isr = 25 µs, T_dev = 200 µs: busy 12.5 %, free 87.5 %. If t_isr ≥ T_dev the CPU cannot keep up (overrun).

### 3.4 Combined loss per second with DMA  <a id="combined-loss"></a>

```
stolen share        = (R / w) / f_b
block overhead share = (R / block_bytes) × (S + C) / f
total               = stolen + overhead     (assumes the CPU would use every bus cycle)
```

- Example: f = 50 MHz, R = 6.4 × 10^6, w = 4, block 8192, S = 2000, C = 3000: 3.2 % + 7.8125 % = 11.0125 %.

---

## 4. Register sizing and block counts

### 4.1 Register widths  <a id="register-width"></a>

```
Address register bits = ⌈log₂(addressable units)⌉          (bytes if byte addressable, words if word addressable)
Count register bits   = ⌈log₂(max units per programming)⌉   (units per programming = 2^m by convention)
```

- Example: 1 M bytes: 20 bits; 32 M words (word addressable): 25 bits.

### 4.2 Programmings (bursts) for a file  <a id="acquisitions"></a>

```
capacity per programming = 2^m × u           (u bytes per unit)
programmings = ⌈ file bytes / (2^m × u) ⌉
```

- Burst mode: bus acquisitions = programmings (the minimum). Cycle stealing: acquisitions = file bytes / u.
- Example: 1000 KB, m = 16, u = 1: 1,024,000 / 65,536 = 15.625 -> 16. u = 4: 3.906 -> 4. 256 KB, u = 1: exactly 4 (2^m convention) or 5 (2^m − 1 convention).
- Misuse: floor, KB as 1000, mixing words and bytes.

---

## 5. Bus mechanics

### 5.1 Daisy-chain delay and lines  <a id="daisy-chain"></a>

```
grant delay to device k = k × t_stage (or (k − 1) × t_stage; state the counting)
lines (typical): daisy chain 3; polling ⌈log₂N⌉ + 2; independent 2N; distributed ≈ ⌈log₂N⌉ ID lines + control (text dependent)
```

- Example: t_stage = 25 ns, k = 8: 200 ns. N = 16: daisy 3, polling 6, independent 32.

### 5.2 Peak and sustained bandwidth  <a id="bandwidth"></a>

```
peak      = (data width in bytes) × f_bus
sustained = bytes per transaction / time per transaction
burst on multiplexed bus: bytes = N × width ; cycles = 1 + N
```

- Example: 100 MHz, 32-bit: peak 400 × 10^6 B/s; 8-word burst on a multiplexed bus: 32 B / 90 ns = 355.56 × 10^6 B/s.
- Misuse: quoting peak as sustained; counting the address cycle once per word on a burst.

### 5.3 Wait states  <a id="wait-states"></a>

```
data-phase cycles = ⌈ t_access / T_clock ⌉         wait states = that number − 1 (for a 1-cycle minimum phase)
```

- Example: T = 20 ns, t_access = 70 ns: 4 cycles; 4 B / 80 ns = 50 × 10^6 B/s.

### 5.4 Asynchronous handshake time  <a id="handshake"></a>

```
time per transfer (no overlap) = (number of edges) × t_prop + t_access     (full four-phase: 4 edges)
```

- Example: t_prop = 5 ns, t_access = 40 ns: 60 ns; 4 B per 60 ns = 66.7 × 10^6 B/s.
- Model-dependent: use the edge delays listed in the question.

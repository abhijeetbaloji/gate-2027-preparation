# Memory Hierarchy Performance — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question gives a different formula, use

\[
\text{AMAT} = T_{\text{hit}} + (\text{miss rate}) \times (\text{miss penalty})
\]

where \(T_{\text{hit}}\) is always paid and the miss penalty is the extra time after the miss is known.

## Level 1 — Conceptual

## Q1 — MCQ

A cache is useful because programs tend to reuse data and to use data near a recent reference. Those two effects are

A. spatial locality only  
B. temporal locality only  
C. spatial and temporal locality  
D. write buffering only

---

## Q2 — MCQ

A cache has hit rate 0.90. Its miss rate is

A. 0.09  
B. 0.10  
C. 0.90  
D. 0.99

---

## Q3 — NAT

A cache hits on 92 percent of references. What is the miss rate, in percent?

---

## Level 2 — Standard GATE Style

## Q4 — NAT

Hit time is 2 ns, miss rate is 0.05, and miss penalty is 40 ns. Using the stated AMAT formula, what is the AMAT in nanoseconds?

---

## Q5 — MCQ

Start from Q4: hit time 2 ns, miss rate 0.05, and miss penalty 40 ns. The miss rate then doubles, and the other two quantities stay the same. The AMAT increases by

A. 1 ns  
B. 2 ns  
C. 4 ns  
D. 6 ns

---

## Q6 — MSQ

Select all that apply.

A. A larger block can capture more spatial locality.  
B. A larger block can increase the miss penalty because more data move on a miss.  
C. A compulsory miss is the first reference to a block that has never been loaded.  
D. Making a cache fully associative removes capacity misses even when the working set is larger than the cache.

---

## Q7 — NAT

Hit time is 5 ns, hit rate is 0.96, and miss penalty is 100 ns. What is the AMAT in nanoseconds?

---

## Level 3 — Multi-Step

## Q8 — NAT

A two-level hierarchy uses the extra-latency model

\[
\text{AMAT} = T_{L1} + m_{L1}\bigl(T_{L2} + m_{L2}\, T_{\text{mem}}\bigr)
\]

\(T_{L1} = 1\) cycle, \(m_{L1} = 0.05\), the extra L2 hit time is \(T_{L2} = 6\) cycles, the local L2 miss rate is \(m_{L2} = 0.5\), and the extra memory penalty is \(T_{\text{mem}} = 40\) cycles. The AMAT, in cycles to one decimal place, is ______.

---

## Q9 — MCQ

A pipeline’s base CPI is 1.5, and that base already includes every cache hit. Misses add extra stall cycles. The instruction-cache miss rate is 2 percent and the data-cache miss rate is 5 percent. Thirty percent of instructions make one data reference. The miss penalty at either cache is 50 cycles. There is no miss-under-miss overlap. The effective CPI is

A. 1.75  
B. 2.25  
C. 3.25  
D. 4.75

---

## Q10 — NAT

A memory reference takes 200 ns when the page is resident. A page fault adds an extra penalty of \(10^{7}\) ns. The page-fault rate is \(10^{-6}\) faults per reference. Using AMAT = resident time + fault rate × extra fault penalty, the average reference time in nanoseconds is ______.

---

## Level 4 — Tricky / Trap-Based

## Q11 — NAT

Without a cache, every reference takes 50 ns. With a cache, hit time is 2 ns, miss rate is 0.04, and the extra miss penalty is 50 ns. Use the standard AMAT formula. The speedup of the cache over the no-cache machine, \(50 / \text{AMAT}\), is ______.

---

## Q12 — MSQ

Select all that apply at the level of write policy.

A. Write-through updates main memory on every store that hits the cache.  
B. Write-back copies a block to main memory when a dirty block is replaced.  
C. A correct write-through cache must keep a dirty bit.  
D. A write buffer can hide some write-through delay from the processor.

---

## Level 5 — Challenge

## Q13 — NAT

Three levels use extra latencies only when they are reached:

\[
\text{AMAT} = 2 + 0.10\bigl(12 + 0.20\bigl(40 + 0.10 \times 200\bigr)\bigr)
\]

The numbers are nanoseconds or local miss rates, in that expression. The first term is the L1 hit time. Each parenthesized term is entered only on a miss of the level outside it. What is the AMAT in nanoseconds, to one decimal place?

---

## Q14 — MCQ

A single-level cache has hit time 2 ns and, initially, miss rate 0.10 and miss penalty 40 ns.

- Design A cuts the miss rate to 0.05 and leaves the penalty at 40 ns.
- Design B leaves the miss rate at 0.10 and cuts the penalty to 20 ns.

Using the standard AMAT formula, which conclusion is correct?

A. Design A has the smaller AMAT.  
B. Design B has the smaller AMAT.  
C. The two designs have the same AMAT.  
D. The AMATs cannot be compared because the hit time differs.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | C |
| 2 | MCQ | B |
| 3 | NAT | 8 |
| 4 | NAT | 4 |
| 5 | MCQ | B |
| 6 | MSQ | A, B, C |
| 7 | NAT | 9 |
| 8 | NAT | 2.3 |
| 9 | MCQ | C |
| 10 | NAT | 210 |
| 11 | NAT | 12.5 |
| 12 | MSQ | A, B, D |
| 13 | NAT | 4.4 |
| 14 | MCQ | C |

## Detailed Solutions

### Q1

Answer: C

Reuse of the same block is temporal locality. Use of nearby addresses is spatial locality. A cache depends on both. A write buffer is an optimization for stores, not the reason a cache has hits.

### Q2

Answer: B

\[
\text{miss rate} = 1 - 0.90 = 0.10
\]

### Q3

Answer: 8

\[
100 - 92 = 8
\]

### Q4

Answer: 4

\[
\text{AMAT} = 2 + 0.05 \times 40 = 2 + 2 = 4 \text{ ns}
\]

### Q5

Answer: B

The new miss rate is 0.10.

\[
\text{AMAT} = 2 + 0.10 \times 40 = 6 \text{ ns}
\]

The increase from the original 4 ns is 2 ns. Doubling the miss rate doubles the miss component from 2 ns to 4 ns; the 2 ns hit time does not change.

### Q6

Answer: A, B, C

Larger blocks bring in neighbours, which helps spatial locality, but they take longer to transfer. The first touch of a block is compulsory. Capacity misses remain whenever the working set exceeds the cache, including a fully associative cache; associativity removes conflict misses, not capacity misses. Direct mapping creates conflict misses when two live blocks want the same line. D is false.

### Q7

Answer: 9

The miss rate is \(1 - 0.96 = 0.04\).

\[
\text{AMAT} = 5 + 0.04 \times 100 = 5 + 4 = 9 \text{ ns}
\]

### Q8

Answer: 2.3

On an L1 miss the processor pays 6 cycles for an L2 hit, and half of those L1 misses also pay 40 more cycles.

\[
T_{L2} + m_{L2} T_{\text{mem}} = 6 + 0.5 \times 40 = 26
\]

\[
\text{AMAT} = 1 + 0.05 \times 26 = 1 + 1.3 = 2.3 \text{ cycles}
\]

### Q9

Answer: C

Every instruction has one instruction fetch. Data references occur on 30 percent of instructions.

\[
\begin{align*}
\text{stalls}
&= (0.02)(50) + (0.30)(0.05)(50) \\
&= 1 + 0.75 \\
&= 1.75
\end{align*}
\]

\[
\text{CPI} = 1.5 + 1.75 = 3.25
\]

### Q10

Answer: 210

\[
200 + 10^{-6} \times 10^{7} = 200 + 10 = 210 \text{ ns}
\]

The rare fault still adds 10 ns to the average because its penalty is \(10^{7}\) ns.

### Q11

Answer: 12.5

\[
\text{AMAT} = 2 + 0.04 \times 50 = 2 + 2 = 4 \text{ ns}
\]

\[
\frac{50}{4} = 12.5
\]

### Q12

Answer: A, B, D

Write-through sends each store to memory, so it does not need a dirty bit to know whether a replacement must be written back. Write-back does need that bit, and it avoids repeated memory writes to a block that stays cached. A write buffer lets the CPU continue while a write-through update drains. C is false.

### Q13

Answer: 4.4

Work from the inside of the expression.

\[
0.10 \times 200 = 20
\]

\[
40 + 20 = 60
\]

\[
0.20 \times 60 = 12
\]

\[
12 + 12 = 24
\]

\[
0.10 \times 24 = 2.4
\]

\[
\text{AMAT} = 2 + 2.4 = 4.4 \text{ ns}
\]

Only 10 percent of references leave L1. Of those, 20 percent leave L2, and of that subset 10 percent reach memory.

### Q14

Answer: C

\[
\begin{align*}
\text{AMAT}_A &= 2 + 0.05 \times 40 = 4 \text{ ns} \\
\text{AMAT}_B &= 2 + 0.10 \times 20 = 4 \text{ ns}
\end{align*}
\]

Halving the miss rate and halving the miss penalty have the same effect here because the original miss component is \(0.10 \times 40 = 4\) ns in both designs before the improvement, and each design cuts that component in half. The hit time is 2 ns in both.

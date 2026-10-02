# Mode — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Mode of 2,3,3,5,5,5,7?

**2.** Bin(10,0.3) mode?

**3.** Normal(50,4) mode?

**4.** Exp(λ) mode?

**5.** Uniform{1,2,3,4} mode?

---

## Level 2 — Standard GATE

**6.** Find mode of: 4,4,7,7,7,9,9,12.

**7.** Poisson(λ=5): mode(s)?

**8.** Grouped: 0–10(3), 10–20(8), 20–30(5), 30–40(2). Modal class?

**9.** X~Bin(7,0.5). Mode?

**10.** Bimodal dataset example: 1,2,2,3,3,4. What are the modes?

---

## Level 3 — Multi-Step

**11.** PMF: P(0)=0.1, P(1)=0.3, P(2)=0.4, P(3)=0.2. Find mode, mean, and which measure of center is largest?

**12.** For Bin(n,p), derive mode formula floor((n+1)p) for p not making (n+1)p integer.

**13.** Continuous X with PDF f(x)=3x² on [0,1]. Find mode.

**14.** Compare mode, median, mean for right-skewed income data conceptually.

**15.** Two dice summed. Mode of sum distribution?

---

## Level 4 — Trap Questions

**16.** Every dataset has a unique mode:
(a) true  (b) false

**17.** Mode of N(μ,σ²) is:
(a) μ  (b) 0  (c) σ  (d) undefined

**18.** For discrete uniform on {1,2,3,4,5,6}:
(a) unique mode  (b) no mode  (c) all modes  (d) mode=3.5

**19.** Adding 10 to every value changes mode by:
(a) 0  (b) 10  (c) depends  (d) doubles

**20.** Mode equals median for:
(a) all symmetric distributions  (b) normal only  (c) never guaranteed  (d) uniform discrete always

---

## Level 5 — Challenge

**21.** X~Bin(20,0.45). Find mode and compare to np.

**22.** Triangular PDF on [0,2] with peak at 1. Find mode and mean.

**23.** Can mean < median < mode? Give a distribution shape.

**24.** Sample: 2,2,3,3,3,4,4,4,4. Find mode; is it unimodal?

**25.** For Poisson(λ) integer, modes are at λ−1 and λ. Verify for λ=3.

---

## Answers (Full Reasoning)

**A1.** **5** (appears 3 times).

**A2.** floor(3.3) = **3**.

**A3.** **50** (peak of symmetric normal at μ).

**A4.** **0** (PDF maximum at x=0).

**A5.** **No unique mode** — all values tie.

**A6.** **7** (frequency 3).

**A7.** Modes at **4 and 5** (integer λ: λ−1 and λ).

**A8.** **10–20** (highest frequency 8).

**A9.** (7+1)·0.5=4 (integer) → modes at **3 and 4** (both (n+1)p and (n+1)p−1).

**A10.** Modes at **2 and 3** (bimodal).

**A11.** Mode = **2** (max prob 0.4). Mean = 0.3+0.6+0.8=**1.7**. Largest: **mode (2)** vs mean 1.7.

**A12.** Mode k maximizes C(n,k)p^k(1−p)^{n−k}; ratio gives k≈(n+1)p → **floor((n+1)p)**.

**A13.** f'(x)=6x=0 at x=0; max on [0,1] at **x=1** (endpoint; check: f(1)=3 > f(0)=0). Mode = **1**.

**A14.** Typically **mode < median < mean** for right skew.

**A15.** Sum 7 has most combinations (6 ways) → mode = **7**.

**A16.** **(b) false** — can be bimodal or no unique mode.

**A17.** **(a) μ** — bell curve peaks at mean.

**A18.** **(c) all values tie** — no unique mode (all are modes).

**A19.** **(b) 10** — mode shifts by same constant.

**A20.** **(c) never guaranteed** — symmetric helps but discrete uniform ties.

**A21.** (21)·0.45=9.45 → mode **9**. np=9 — close agreement.

**A22.** Mode = **1**. Mean = 1 (symmetric triangle) = **1**.

**A23.** **Yes** — right-skewed: mode < median < mean.

**A24.** **4** (four times). **Unimodal**.

**A25.** P(2) and P(3) both maximal for Poi(3): e^{−3}·9/2 vs e^{−3}·27/6 = both **9e^{−3}/2** — equal modes at **2 and 3**.

# Poisson Distribution — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Poisson(3): E, Var, P(0)?

**2.** λ=2: P(X≥1)?

**3.** 4/hr, 30min: P(0)?

**4.** Bin(1000,0.002) approx?

**5.** Poi(5)+Poi(3) independent?

---

## Level 2 — Standard GATE

**6.** X~Poi(4). Find P(X=2) and P(X≤1).

**7.** Typo rate 0.5/page, 10 pages. P(exactly 3 typos)?

**8.** Calls arrive at 12/hr. P(more than 15 in one hour)?

**9.** X~Poi(λ). If E[X]=Var(X)=6, find λ and P(X=0).

**10.** Splitting: 10 Poi(λ) into two independent streams with prob 0.3 and 0.7. Distributions?

---

## Level 3 — Multi-Step

**11.** Website hits ~Poi(20/hr). P(0 hits in 15 min)? P(at least 1 in 15 min)?

**12.** X~Poi(3), Y~Poi(5) independent. Find P(X+Y=4) and distribution of X+Y.

**13.** Defects ~Poi(2) per meter. Find P(0 defects in 2 meters) and P(≥2 in 1 meter).

**14.** Given X~Poi(λ) and P(X=0)=0.1, find λ and P(X≥2).

**15.** Thinning: each event kept with prob p. If X~Poi(λ), distribution of kept count?

---

## Level 4 — Trap Questions

**16.** For Poisson(λ), E[X²] equals:
(a) λ  (b) λ²  (c) λ+λ²  (d) λ²+λ

**17.** Poisson is memoryless:
(a) true  (b) false

**18.** Var(X) for Poi(λ) when λ=0:
(a) 0  (b) 1  (c) undefined  (d) λ

**19.** Bin(n,p) → Poi(λ) when:
(a) n large, p small, np=λ  (b) n small  (c) p=0.5  (d) always

**20.** If X~Poi(2), mode is:
(a) 1  (b) 2  (c) 1 or 2  (d) 0

---

## Level 5 — Challenge

**21.** X~Poi(λ). Find P(X even) in terms of λ.

**22.** Two independent Poi processes: rates 3 and 5. P(first event from process A before B)?

**23.** X~Poi(10). Use normal approximation for P(8≤X≤12) with continuity correction.

**24.** Prove E[X]=Var(X)=λ for Poisson.

**25.** Compound: N~Poi(5), each item has weight W~{1,2} equally. Find E[total weight].

---

## Answers (Full Reasoning)

**A1.** E=Var=**3**. P(0)=e^{−3}.

**A2.** P(X≥1)=1−e^{−2}.

**A3.** λ=2 for 30 min. P(0)=**e^{−2}**.

**A4.** np=2 → **Poisson(2)** approximation.

**A5.** **Poisson(8)** (sums of independent Poissons).

**A6.** P(X=2)=e^{−4}·16/2 ≈ **0.147**. P(X≤1)=e^{−4}(1+4) ≈ **0.092**.

**A7.** λ=5 for 10 pages. P(3)=e^{−5}·125/6 ≈ **0.140**.

**A8.** X~Poi(12). P(X>15)=1−P(X≤15) ≈ **0.228** (table/software).

**A9.** λ=**6**. P(0)=**e^{−6}**.

**A10.** Each stream: **Poi(0.3λ)** and **Poi(0.7λ)** independently.

**A11.** λ=5 per 15 min. P(0)=e^{−5} ≈ **0.0067**. P(≥1)=**1−e^{−5}**.

**A12.** X+Y~Poi(8). P(X+Y=4)=e^{−8}·4096/24 ≈ **0.043**.

**A13.** λ=4 for 2 meters: P(0)=**e^{−4}**. P(≥2 in 1m)=1−e^{−2}(1+2) ≈ **0.323**.

**A14.** e^{−λ}=0.1 → λ=**ln 10 ≈ 2.303**. P(X≥2)=1−e^{−λ}(1+λ) ≈ **0.441**.

**A15.** Kept count ~ **Poi(pλ)**.

**A16.** **(c) λ+λ²** — E[X²]=Var+E²=λ+λ².

**A17.** **(b) false** — exponential is memoryless, not Poisson counts.

**A18.** **(a) 0** — degenerate at 0 when λ=0.

**A19.** **(a)** — law of rare events.

**A20.** **(c)** — mode is floor(λ) or λ when λ is integer; for λ=2, modes at **1 and 2** (or 2 when λ integer: both λ−1 and λ).

**A21.** P(even)=e^{−λ}·cosh(λ)=**e^{−λ}(e^λ+e^{−λ})/2=(1+e^{−2λ})/2**.

**A22.** P(A first)=3/(3+5)=**3/8** (exponential race).

**A23.** μ=10, σ=√10. z: (7.5−10)/√10 to (12.5−10)/√10 → P ≈ **0.588** with correction.

**A24.** E[X]=Σk·e^{−λ}λ^k/k! = λ·Σ e^{−λ}λ^{k−1}/(k−1)! = λ. Similarly Var=λ (standard derivation).

**A25.** E[W]=1.5. E[total]=E[N]·E[W]=5·1.5=**7.5**.

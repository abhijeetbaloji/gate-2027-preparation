# Normal Distribution — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** X~N(100,25). σ?

**2.** Z=(X−100)/5. P(X≤110)?

**3.** X~N(0,4). Var(3X+1)?

**4.** P(Z>0)?

**5.** Within 2σ of μ?

---

## Level 2 — Standard GATE

**6.** X~N(50,16). Find P(46≤X≤54).

**7.** Scores ~N(70,100). Top 10% cutoff? (Use z₀.₁₀≈1.28)

**8.** X~N(μ,9). If P(X>40)=0.1587, find μ. (Φ(1)=0.8413)

**9.** Independent X~N(2,1), Y~N(3,4). Distribution of X+Y?

**10.** If Z~N(0,1), find P(|Z|≤1.96).

---

## Level 3 — Multi-Step

**11.** Heights ~N(170,36) cm. Find P(160<H<180) and P(H>180).

**12.** Two machines: A~N(100,4), B~N(102,9) independent. P(A output > B output)?

**13.** X~N(0,1). Find P(X²<1) and P(X²>4).

**14.** Sample mean X̄ of n=25 from N(μ,25). P(|X̄−μ|>2)?

**15.** 95% symmetric interval around μ=200 with σ=10. Find endpoints.

---

## Level 4 — Trap Questions

**16.** X~N(5,4) means σ²=4, so σ equals:
(a) 2  (b) 4  (c) ±2  (d) 16

**17.** If X~N(μ,σ²), then X/σ is:
(a) N(0,1)  (b) N(μ/σ,1)  (c) N(μ,1)  (d) not normal unless μ=0

**18.** P(Z>1)+P(Z<−1) equals:
(a) P(|Z|>1)  (b) 2P(Z>1)  (c) both  (d) 0.32

**19.** Normal PDF can exceed 1:
(a) never  (b) always  (c) yes, when σ small  (d) only at μ

**20.** Median of N(μ,σ²) is:
(a) μ  (b) 0  (c) σ  (d) mode only, not median

---

## Level 5 — Challenge

**21.** X~N(0,1). Find E[max(X,0)] (half-normal mean).

**22.** X~N(μ,σ²). Find the value k such that P(X≤μ+kσ)=0.975.

**23.** Central Limit: 100 fair coins. Approximate P(45≤X≤55) using normal.

**24.** X~N(0,1), Y=X². Find E[Y] and Var(Y).

**25.** If Φ(1.5)=0.9332, find P(−1.5<Z<1.5) without tables.

---

## Answers (Full Reasoning)

**A1.** σ²=25 → σ = **5**.

**A2.** Z=(110−100)/5=2. P(X≤110) = **Φ(2)**.

**A3.** Var(3X+1) = 9·4 = **36**.

**A4.** Symmetry: **0.5**.

**A5.** Empirical rule: **≈95%** within 2σ.

**A6.** z-scores: (46−50)/4=−1, (54−50)/4=1. P = Φ(1)−Φ(−1) = **0.6827**.

**A7.** 70+1.28·10 = **82.8** (top 10%).

**A8.** P(X>40)=0.1587 → z=1, so (40−μ)/3=1 → μ = **37**.

**A9.** X+Y ~ **N(5, 5)** (means add, variances add).

**A10.** P(|Z|≤1.96) = 2Φ(1.96)−1 ≈ **0.95**.

**A11.** z: −10/6=−1.67, 10/6=1.67. P(160<H<180) ≈ **0.905**. P(H>180)=P(Z>1.67) ≈ **0.0475**.

**A12.** D=A−B ~ N(−2, 13). P(D>0)=P(Z>2/√13) ≈ P(Z>0.555) ≈ **0.29**.

**A13.** P(X²<1)=P(−1<X<1)=**0.6827**. P(X²>4)=P(|X|>2)=**0.0456**.

**A14.** X̄~N(μ,1). P(|X̄−μ|>2)=2(1−Φ(2)) ≈ **0.0456**.

**A15.** 200±1.96·10 → **[180.4, 219.6]**.

**A16.** **(a) 2** — σ=√4=2.

**A17.** **(d)** — (X−μ)/σ ~ N(0,1); X/σ ~ N(μ/σ, 1).

**A18.** **(c)** — symmetry: both equal 2Φ(−1) ≈ 0.3174.

**A19.** **(c)** — PDF peak 1/(σ√2π) > 1 when σ < 1/√2π.

**A20.** **(a)** — normal is symmetric; median = mean = μ.

**A21.** E[max(X,0)] = ∫₀^∞ x·φ(x)dx = **1/√(2π) ≈ 0.399**.

**A22.** k = **1.96** (two-tailed 5% → one-tailed 2.5%).

**A23.** X~Bin(100,0.5), μ=50, σ=5. z=±1. P ≈ **0.6827**.

**A24.** E[Y]=E[X²]=**1**. Var(Y)=E[X⁴]−1; E[X⁴]=3 for N(0,1) → Var = **2**.

**A25.** P(−1.5<Z<1.5) = 2·0.9332−1 = **0.8664**.

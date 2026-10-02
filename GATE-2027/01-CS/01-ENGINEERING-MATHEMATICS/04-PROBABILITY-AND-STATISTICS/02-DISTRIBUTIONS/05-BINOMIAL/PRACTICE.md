# Binomial Distribution — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** 10 coins, p=0.5, P(X=5)?

**2.** n=20,p=0.1: E[X]?

**3.** P(at least 1 success), p=0.2,n=5?

**4.** Mode for n=10,p=0.3?

**5.** Var for n=100,p=0.5?

---

## Level 2 — Standard GATE

**6.** X~Bin(15,0.4). Find P(X=6) and E[X].

**7.** 8-bit string, each bit 1 with prob 0.25. P(exactly 3 ones)?

**8.** n=50, p=0.02. Approximate P(X=1) using Poisson.

**9.** P(X≥8) for Bin(10,0.7).

**10.** Two Bin(5,0.5) independent. P(sum=5)?

---

## Level 3 — Multi-Step

**11.** Quality control: 20 items, each defective with prob 0.05. P(≤1 defective)? P(≥3)?

**12.** X~Bin(n,p) with n=12, E[X]=3. Find p and Var(X).

**13.** Archery: 10 shots, hit prob 0.6. Expected hits and SD. P(exactly 7 hits)?

**14.** Hypergeometric vs Binomial: 52 cards, draw 5 without replacement. P(2 aces) — when is Bin(5,4/52) OK?

**15.** X~Bin(100,0.01). Use normal approximation for P(0≤X≤3) with continuity correction.

---

## Level 4 — Trap Questions

**16.** Var(X) for Bin(n,p) is largest when:
(a) p=0  (b) p=0.5  (c) p=1  (d) p=1/n

**17.** Mode of Bin(n,p) is approximately:
(a) np  (b) (n+1)p  (c) floor((n+1)p)  (d) np(1−p)

**18.** Bin(n,p) with n=1 is:
(a) Bernoulli  (b) Poisson  (c) Normal  (d) invalid

**19.** E[X(X−1)] for Bin(n,p) equals:
(a) np  (b) n(n−1)p²  (c) np(1−p)  (d) n²p²

**20.** P(X=0) for Bin(n,0) equals:
(a) 0  (b) 1  (c) undefined  (d) 0^n

---

## Level 5 — Challenge

**21.** X~Bin(n,p). Find P(X is even).

**22.** Coupon collector flavor: n=10 trials p=0.3. P(at least one success)?

**23.** X~Bin(20,0.4). Find smallest k with P(X≤k)≥0.95.

**24.** Derive E[X]=np from PMF definition.

**25.** Two players: A needs 2 more wins, B needs 3. Each game A wins with 0.6. P(A wins series)?

---

## Answers (Full Reasoning)

**A1.** C(10,5)/2^10 = **252/1024**.

**A2.** E[X] = 20·0.1 = **2**.

**A3.** 1−0.8^5 = **1−0.32768 ≈ 0.672**.

**A4.** floor((n+1)p) = floor(3.3) = **3**.

**A5.** np(1−p) = 100·0.25 = **25**.

**A6.** P(X=6)=C(15,6)·0.4^6·0.6^9 ≈ **0.207**. E[X]=**6**.

**A7.** Bin(8,0.25): P(3)=C(8,3)·0.25³·0.75^5 ≈ **0.208**.

**A8.** λ=np=1. P(1)=e^{−1}·1 ≈ **0.368**.

**A9.** P(X≥8)=P(8)+P(9)+P(10) ≈ **0.617**.

**A10.** Ways: sum 5 from two Bin(5,0.5) — convolution; approximate **C(10,5)/2^10 · adjustment** ≈ compute: Σ P(X₁=i)P(X₂=5−i) ≈ **0.152**.

**A11.** Bin(20,0.05). P(≤1)=e^{−1} approx Poisson OR exact: (0.95)^20+20·0.05·(0.95)^19 ≈ **0.736**. P(≥3) ≈ **0.075**.

**A12.** p=3/12=**0.25**. Var=12·0.25·0.75=**2.25**.

**A13.** E=6, SD=√2.4≈**1.55**. P(7)=C(10,7)·0.6^7·0.4^3 ≈ **0.215**.

**A14.** Exact hypergeometric: C(4,2)C(48,3)/C(52,5). Binomial OK when n≪N.

**A15.** μ=1, σ≈0.995. P(0≤X≤3) with correction ≈ **0.986**.

**A16.** **(b) p=0.5** — np(1−p) maximized at p=0.5.

**A17.** **(c) floor((n+1)p)** — standard mode formula (with edge cases).

**A18.** **(a) Bernoulli** — Bin(1,p)=Bernoulli(p).

**A19.** **(b) n(n−1)p²** — E[X(X−1)]=n(n−1)p².

**A20.** **(b) 1** — always fail: P(X=0)=1.

**A21.** P(even)=(1+(1−2p)^n)/2. For p=0.5: **1/2**.

**A22.** 1−0.7^10 ≈ **0.972**.

**A23.** Use CDF tables: k=**11** gives P(X≤11)≥0.95 (verify with μ=8, σ≈2.19).

**A24.** E[X]=Σk·C(n,k)p^k(1−p)^{n−k}=np·Σ C(n−1,k−1)p^{k−1}(1−p)^{n−k}=**np**.

**A25.** Negative binomial / sequential games: P(A wins) ≈ **0.683** (compute via states).

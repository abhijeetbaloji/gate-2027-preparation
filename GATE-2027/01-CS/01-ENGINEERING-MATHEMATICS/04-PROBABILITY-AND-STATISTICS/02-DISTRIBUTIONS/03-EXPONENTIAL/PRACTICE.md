# Exponential Distribution — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** λ=2. E[X]?

**2.** P(X>1) for Exp(1)?

**3.** Mean=10. λ?

**4.** Memoryless: waited 5, P(3 more)?

**5.** Rate 4/hr. P(no event in 15min)?

---

## Level 2 — Standard GATE

**6.** X~Exp(λ=0.5). Find Var(X), median, and P(X≤4).

**7.** Server lifetime ~Exp(mean=500 hrs). P(fails within 100 hrs)?

**8.** E[X²] for X~Exp(λ).

**9.** Min of two independent Exp(λ) variables: distribution?

**10.** P(X>5 | X>3) for X~Exp(λ)?

---

## Level 3 — Multi-Step

**11.** Call center: 6 calls/hour (~Exp). P(no call in 20 min)? P(exactly 2 calls in 1 hr)? (Use Poisson for count.)

**12.** X~Exp(2). Find P(1<X<3) and the 90th percentile.

**13.** Two components in series, lifetimes Exp(λ₁), Exp(λ₂) independent. P(system up at time t)?

**14.** X~Exp(λ). Find P(X > E[X]).

**15.** Bus inter-arrival ~Exp(5 min). You arrive at random. Expected wait for next bus?

---

## Level 4 — Trap Questions

**16.** Exp(λ) is memoryless, so P(X>s+t | X>s) equals:
(a) P(X>t)  (b) P(X>s+t)  (c) P(X>s)  (d) P(X<t)

**17.** Mode of Exp(λ) is:
(a) 1/λ  (b) 0  (c) λ  (d) undefined

**18.** Var(X) for Exp(λ) equals:
(a) 1/λ  (b) 1/λ²  (c) λ  (d) λ²

**19.** Sum of two independent Exp(λ) is:
(a) Exp(2λ)  (b) Exp(λ/2)  (c) Gamma(2,λ)  (d) Normal

**20.** If mean=5, then P(X=5) for continuous Exp equals:
(a) 1/5  (b) e^{−1}  (c) 0  (d) 0.2

---

## Level 5 — Challenge

**21.** n independent Exp(λ). Find distribution of X₁+⋯+Xₙ.

**22.** X~Exp(1). Find P(X > ln 10).

**23.** Reliability: 3 parallel components each Exp(λ). P(system fails by time t)?

**24.** Prove: for Exp(λ), median m satisfies m = (ln 2)/λ.

**25.** X~Exp(λ). Find Cov(X, 1/X) — does a simple closed form exist? Discuss.

---

## Answers (Full Reasoning)

**A1.** E[X] = 1/λ = **0.5**.

**A2.** P(X>1) = e^{−1·1} = **e^{−1}**.

**A3.** λ = 1/mean = **0.1**.

**A4.** Memoryless: P(X>3) = **e^{−3λ}** (same as unconditional).

**A5.** λ=4/hr=1 per 15 min. P(0) = **e^{−1}**.

**A6.** Var = 1/0.25 = **4**. Median = ln(2)/0.5 = **ln 4**. P(X≤4) = 1−e^{−2} ≈ **0.865**.

**A7.** λ=1/500. P(X≤100) = 1−e^{−0.2} ≈ **0.181**.

**A8.** E[X²] = 2/λ².

**A9.** Min ~ **Exp(2λ)** (sum of rates).

**A10.** Memoryless: **e^{−5λ}** / e^{−3λ} = **e^{−2λ}** = P(X>2).

**A11.** λ=6/hr=0.1/min. P(0 in 20 min) = e^{−2} ≈ **0.135**. Count in 1 hr ~ Poi(6): P(2) = e^{−6}·36/2 ≈ **0.0446**.

**A12.** P(1<X<3) = e^{−2}−e^{−6} ≈ **0.125**. 90th percentile: 1−e^{−2t}=0.9 → t = −ln(0.1)/2 ≈ **1.15**.

**A13.** P(both alive) = e^{−λ₁t}·e^{−λ₂t} = **e^{−(λ₁+λ₂)t}**.

**A14.** P(X>1/λ) = e^{−1} ≈ **0.368** (same for all λ).

**A15.** Random arrival: E[wait] = E[X] = **1/5 min = 12 sec** (or 1/λ for rate λ).

**A16.** **(a) P(X>t)** — definition of memoryless property.

**A17.** **(b) 0** — PDF λe^{−λx} is maximum at x=0.

**A18.** **(b) 1/λ²**.

**A19.** **(c) Gamma(2,λ)** — also Erlang; not Exp unless n=1.

**A20.** **(c) 0** — continuous distribution.

**A21.** Sum ~ **Gamma(n, λ)** (Erlang with shape n).

**A22.** P(X>ln 10) = e^{−ln 10} = **0.1**.

**A23.** P(all fail) = (1−e^{−λt})³. System up if at least one alive: **1−(1−e^{−λt})³**.

**A24.** 1−e^{−λm}=0.5 → e^{−λm}=0.5 → m = **(ln 2)/λ**.

**A25.** Cov(X,1/X) requires E[1]−E[X]E[1/X]; integral diverges at 0 for E[1/X]. **No finite mean for 1/X** — covariance undefined.

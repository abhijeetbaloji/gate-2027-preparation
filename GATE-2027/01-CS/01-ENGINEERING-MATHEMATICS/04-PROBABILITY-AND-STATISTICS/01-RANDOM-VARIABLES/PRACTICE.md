# Random Variables — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** X: 0,1,2 with probs 1/4,1/2,1/4. E[X]?

**2.** E[X]=3, E[X²]=13. Var(X)?

**3.** Var(X)=4, Var(Y)=9 independent. Var(X+Y)?

**4.** f(x)=x/2 on [0,2]. Valid PDF?

**5.** F(5)=0.7 means?

---

## Level 2 — Standard GATE

**6.** X~Uniform(0,4). E[X], Var(X)?

**7.** P(X>3) if X~Exp(λ=1)?

**8.** E[3X−2] if E[X]=5?

**9.** Var(2X) if Var(X)=3?

**10.** Two independent, E[XY] if E[X]=2,E[Y]=3?

---

## Level 3 — Multi-Step

**11.** X has PMF: P(X=0)=0.2, P(X=1)=0.5, P(X=2)=0.3. Find E[X], E[X²], and Var(X).

**12.** X~Uniform(0,6). Let Y = X². Find E[Y] and Var(Y).

**13.** X and Y are independent with E[X]=2, Var(X)=1, E[Y]=3, Var(Y)=4. Find E[2X−3Y+5] and Var(2X−3Y).

**14.** Continuous X has PDF f(x)=3x² on [0,1]. Find F(x), P(0.5≤X≤0.8), and E[X].

**15.** A fair die is rolled. Let X = outcome and Y = 1 if X is even, else 0. Find E[X], E[Y], and E[XY].

---

## Level 4 — Trap Questions

**16.** If f(x)=2x on [0,1], then P(X=0.5) equals:
(a) 0  (b) 1  (c) 0.5  (d) cannot determine

**17.** Var(X)=0 implies:
(a) X is always 0  (b) X is constant a.s.  (c) E[X]=0  (d) X is discrete

**18.** For independent X,Y: E[X/Y] equals:
(a) E[X]/E[Y] always  (b) E[X]·E[1/Y] always  (c) both (a) and (b)  (d) neither (a) nor (b) always

**19.** If F(x)=0 for x<1 and F(x)=1 for x≥1, then X is:
(a) Uniform(0,1)  (b) degenerate at 1  (c) invalid  (d) Normal

**20.** Var(X+Y)=Var(X)+Var(Y) is guaranteed when:
(a) always  (b) X,Y independent  (c) Cov(X,Y)=0  (d) both (b) and (c)

---

## Level 5 — Challenge

**21.** X~Exp(λ). Find E[X³] in terms of λ.

**22.** Two independent Uniform(0,1) variables X,Y. Find PDF of Z = max(X,Y).

**23.** X has PMF P(X=k)=c/k for k=1,2,3,4. Find c, E[X], and Var(X).

**24.** Chebyshev: E[X]=50, Var(X)=25. Minimum P(40≤X≤60)?

**25.** X~Bin(10,0.3). Verify E[X²]=Var(X)+E[X]² numerically.

---

## Answers (Full Reasoning)

**A1.** E[X] = 0·(1/4)+1·(1/2)+2·(1/4) = **1**.

**A2.** Var(X) = E[X²]−E[X]² = 13−9 = **4**.

**A3.** Independent: Var(X+Y) = 4+9 = **13**.

**A4.** ∫₀² (x/2)dx = [x²/4]₀² = 1. **Yes**, valid PDF.

**A5.** **P(X≤5) = 0.7** by definition of CDF.

**A6.** E[X] = (0+4)/2 = **2**. Var(X) = (4−0)²/12 = **4/3**.

**A7.** P(X>3) = e^{−λ·3} with λ=1 → **e^{−3}**.

**A8.** E[3X−2] = 3·5−2 = **13**.

**A9.** Var(2X) = 4·Var(X) = 4·3 = **12**.

**A10.** Independent: E[XY] = E[X]E[Y] = 2·3 = **6**.

**A11.** E[X] = 0.5+0.6 = **1.1**. E[X²] = 0+0.5+1.2 = **1.7**. Var(X) = 1.7−1.21 = **0.49**.

**A12.** E[X²] = Var(X)+E[X]² = 3+9 = **12**. E[X⁴] = ∫₀⁶ x⁴/6 dx = 6⁴/5 = 259.2/5 = **129.6**. Var(Y) = 129.6−144 = **115.2** (or **576/5**).

**A13.** E[2X−3Y+5] = 4−9+5 = **0**. Var(2X−3Y) = 4·1+9·4 = **40**.

**A14.** F(x)=x³ for 0≤x≤1. P(0.5≤X≤0.8) = 0.512−0.125 = **0.387**. E[X] = ∫₀¹ 3x³ dx = **3/4**.

**A15.** E[X] = **3.5**. E[Y] = P(even) = **0.5**. E[XY] = (2+4+6)/6 = **2**.

**A16.** **(a) 0** — continuous RV has zero point mass.

**A17.** **(b)** — Var(X)=0 iff X is constant almost surely (not necessarily 0).

**A18.** **(d)** — independence gives E[XY]=E[X]E[Y], but E[X/Y]≠E[X]/E[Y] in general.

**A19.** **(b)** — CDF jumps from 0 to 1 at x=1 → degenerate at 1.

**A20.** **(d)** — independence implies Cov=0; both (b) and (c) suffice, but not always.

**A21.** E[X³] = 3!/λ³ = **6/λ³** (Gamma function or integration by parts).

**A22.** P(Z≤z)=z² for 0≤z≤1. PDF f_Z(z) = **2z** on [0,1].

**A23.** c(1+1/2+1/3+1/4) = 25c/12 = 1 → c = **12/25**. E[X] = (12/25)·4 = **48/25**. E[X²] = (12/25)·10 = **24/5**. Var(X) = 24/5 − (48/25)² = **696/625**.

**A24.** P(|X−50|≥10) ≤ 25/100 = 0.25, so P(40≤X≤60) ≥ **0.75**.

**A25.** E[X]=3, Var(X)=2.1. E[X²] = 2.1+9 = **11.1** (matches direct summation).

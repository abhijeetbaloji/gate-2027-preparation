# Mean — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Mean of 2,4,6,8?

**2.** E[X] from P(1)=0.3,P(2)=0.7?

**3.** E[2X+3], E[X]=4?

**4.** Weighted: 80(w=2), 60(w=3)?

**5.** Bin(10,0.4) mean?

---

## Level 2 — Standard GATE

**6.** Find mean of grouped data: 10(×2), 20(×5), 30(×3).

**7.** X~Poi(7). E[3X−2]?

**8.** E[X] for Uniform(−4,8)?

**9.** If every value increases by 5, new mean?

**10.** Sample: 12,15,18,21. If 15 is replaced by 25, change in mean?

---

## Level 3 — Multi-Step

**11.** Two classes: Class A (n=30, mean=72), Class B (n=20, mean=78). Combined mean?

**12.** X PMF: P(0)=0.1, P(1)=0.2, P(2)=0.4, P(3)=0.3. Find E[X] and E[X²].

**13.** Frequency table: 0–10(5), 10–20(15), 20–30(10). Use midpoints for approximate mean.

**14.** E[aX+bY] where E[X]=2,E[Y]=5, a=3,b=−1. If X,Y independent, E[XY]?

**15.** Geometric(p=0.2): E[X] (trials until first success)?

---

## Level 4 — Trap Questions

**16.** Median always equals mean:
(a) true  (b) false

**17.** Adding outlier increases mean:
(a) always  (b) never  (c) usually  (d) only if positive

**18.** E[X²] equals (E[X])² when:
(a) always  (b) X constant  (c) X symmetric  (d) never

**19.** Mean of {1,2,3,4,5} after multiplying all by −2:
(a) −3  (b) −15  (c) 3  (d) −6

**20.** Weighted mean with equal weights equals:
(a) arithmetic mean  (b) median  (c) geometric mean  (d) mode

---

## Level 5 — Challenge

**21.** Prove E[aX+b]=aE[X]+b for discrete X.

**22.** X~Exp(λ). Find E[X | X>c] using memoryless property.

**23.** n numbers with mean μ. One new value added. Express new mean in terms of μ, n, and new value.

**24.** Jensen: for convex f, E[f(X)] vs f(E[X]) for X~{1,3} equally likely, f(x)=x².

**25.** Law of large numbers intuition: 1000 fair coins. Expected sample mean?

---

## Answers (Full Reasoning)

**A1.** (2+4+6+8)/4 = **5**.

**A2.** 1·0.3+2·0.7 = **1.7**.

**A3.** 2·4+3 = **11**.

**A4.** (160+180)/5 = **68**.

**A5.** np = 10·0.4 = **4**.

**A6.** (20+100+90)/10 = **21**.

**A7.** 3·7−2 = **19**.

**A8.** (−4+8)/2 = **2**.

**A9.** Old mean + **5**.

**A10.** Old mean=16.5. New sum increases by 10; new mean=(66+10)/4 = **19.5** (change +3).

**A11.** (30·72+20·78)/50 = **74.4**.

**A12.** E[X]=0.1+0.8+1.2=**2.1**. E[X²]=0+0.2+1.6+2.7=**4.5**.

**A13.** Midpoints 5,15,25: (25+225+250)/30 = **16.67**.

**A14.** E[aX+bY]=6−5=**1**. E[XY]=2·5=**10** (independent).

**A15.** E[X]=1/p = **5**.

**A16.** **(b) false** — e.g. skewed data.

**A17.** **(c) usually** — direction depends on outlier value.

**A18.** **(b)** — equality iff X constant a.s.

**A19.** Original mean = 3. After scaling by −2: new mean = −2·3 = **−6** → answer **(d)**.

**A20.** **(a)** — equal weights → arithmetic mean.

**A21.** E[aX+b]=Σ(ax+b)P(x)=aΣxP(x)+bΣP(x)=**aE[X]+b**.

**A22.** E[X|X>c]=c+1/λ (memoryless: extra time ~ Exp(λ)).

**A23.** New mean = **(nμ+x_new)/(n+1)**.

**A24.** E[X²]=(1+9)/2=5. (E[X])²=4. E[f(X)]=5 > f(E[X])=4 — **E[f(X)]≥f(E[X])** for convex f.

**A25.** Expected sample mean = **0.5** (unbiased for p).

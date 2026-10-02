# Uniform Distribution — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Fair die E[X]?

**2.** X~Uniform(0,10). P(X≤3)?

**3.** X~Uniform(2,8). P(4≤X≤6)?

**4.** {1,…,100} discrete uniform. P(X=50)?

**5.** E[X] for Uniform(5,15)?

---

## Level 2 — Standard GATE

**6.** X~Uniform(−2,4). Find PDF, E[X], and Var(X).

**7.** Discrete uniform on {1,2,…,n}. Express E[X] and Var(X) in terms of n.

**8.** X~Uniform(0,8). P(X>5 | X>2)?

**9.** Two independent Uniform(0,1) variables. P(X+Y ≤ 1)?

**10.** X~Uniform(a,b). For what value c is P(X≤c)=0.75?

---

## Level 3 — Multi-Step

**11.** Bus arrives uniformly between 8:00 and 8:30. You arrive at 8:10. What is the expected waiting time until the bus comes?

**12.** X~Uniform(0,12). Find P(|X−6|>3) and E[|X−6|].

**13.** Discrete uniform on {10,11,…,20}. Find P(X is even) and E[X²].

**14.** X~Uniform(−1,3). Find the CDF and P(−0.5<X<2).

**15.** Y = 2X+3 where X~Uniform(0,5). Find the distribution of Y (support, PDF, mean).

---

## Level 4 — Trap Questions

**16.** X~Uniform(0,10) continuous. P(X=5) equals:
(a) 0.1  (b) 0  (c) 1/10  (d) 0.5

**17.** Var(X) for discrete uniform on {1,2,3,4,5,6} equals:
(a) 35/12  (b) 2.917  (c) both (a) and (b)  (d) 25/12

**18.** If X~Uniform(0,1), then X² is:
(a) Uniform(0,1)  (b) Uniform(0,1) scaled  (c) not uniform  (d) Bernoulli

**19.** Median of Uniform(a,b) is:
(a) (a+b)/2  (b) a+(b−a)/2  (c) both same  (d) (b−a)/2

**20.** For Uniform(2,8), P(3≤X≤5) using length formula gives:
(a) 1/3  (b) 2/6  (c) both (a) and (b)  (d) 1/6

---

## Level 5 — Challenge

**21.** X~Uniform(0,1), Y~Uniform(0,1) independent. Find PDF of Z = X+Y.

**22.** n points chosen independently Uniform(0,1). Expected length of the largest gap?

**23.** X~Uniform(−θ,θ). Method of moments: estimate θ from one observation x=4.

**24.** X~Uniform(0,L). Find L such that P(X>L/3)=0.6.

**25.** Order statistic: X₁,X₂ i.i.d. Uniform(0,1). P(X₁<X₂) and E[X₂−X₁]?

---

## Answers (Full Reasoning)

**A1.** E[X] = (1+6)/2 = **3.5**.

**A2.** P(X≤3) = 3/10 = **0.3**.

**A3.** P(4≤X≤6) = (6−4)/(8−2) = **1/3**.

**A4.** **1/100** for discrete uniform.

**A5.** E[X] = (5+15)/2 = **10**.

**A6.** PDF = 1/6 on [−2,4]. E[X] = 1. Var = 36/12 = **3**.

**A7.** E[X] = **(n+1)/2**. Var(X) = **(n²−1)/12**.

**A8.** P(X>5|X>2) = P(5<X≤8)/P(X>2) = 3/6 = **0.5**.

**A9.** Region x+y≤1 in unit square has area **1/2**.

**A10.** c = a + 0.75(b−a) = **(3b+a)/4**.

**A11.** Given you are at 8:10, bus time ~ Uniform(10,30) minutes past 8:00. E[wait] = (30−10)/2 = **10 minutes**.

**A12.** P(|X−6|>3) = P(X<3)+P(X>9) = 3/12+3/12 = **0.5**. E[|X−6|] = ∫₀¹² |x−6|/12 dx = **3**.

**A13.** 6 even values out of 11 → **6/11**. E[X²] = Var+E²; E[X]=15, Var=10 → **235**.

**A14.** F(x)=0 (x<−1), (x+1)/4 (−1≤x<3), 1 (x≥3). P(−0.5<X<2) = F(2)−F(−0.5) = 3/4−1/8 = **5/8**.

**A15.** Y ~ Uniform(3,13). PDF = 1/10 on [3,13]. E[Y] = **8**.

**A16.** **(b) 0** — continuous uniform has zero point probability.

**A17.** **(c)** — (n²−1)/12 = 35/12 ≈ 2.917 for n=6.

**A18.** **(c)** — X² concentrates near 0; PDF is 1/(2√y), not constant.

**A19.** **(c)** — median = (a+b)/2 = midpoint.

**A20.** **(c)** — (5−3)/(8−2) = 2/6 = 1/3.

**A21.** f_Z(z)=z on [0,1], 2−z on [1,2], 0 otherwise (triangle distribution).

**A22.** For n=2: E[max gap] = **1/3**. General: grows as **1/(n+1)** for largest gap expectation ≈ 1/(n+1) (standard order-statistics result).

**A23.** E[X]=0, so one observation doesn't estimate θ well; |x|=4 suggests θ≥4. MoM with E[|X|]=θ/2 (for symmetric) gives θ̂=**8** if using |X| moment.

**A24.** P(X>L/3) = 1−L/(3L) = 2/3 ≠ 0.6. Actually P(X>L/3)=(L−L/3)/L=**2/3** always — trick: probability is **2/3** regardless of L.

**A25.** P(X₁<X₂) = **1/2** by symmetry. E[X₂−X₁] = E[X₂]−E[X₁] but dependent: E[|X₂−X₁|]=**1/3** for Uniform(0,1).

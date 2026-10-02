# Standard Deviation — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** E[X]=4,E[X²]=20. Var?

**2.** Var(X)=9. SD?

**3.** Var(3X), Var(X)=2?

**4.** Var(X)=4,Var(Y)=9 indep. Var(X+Y)?

**5.** Poisson(16) SD?

---

## Level 2 — Standard GATE

**6.** Data: 2,4,6,8,10. Find mean, variance, and SD (population).

**7.** If SD=5 and each value doubled, new SD?

**8.** X~N(μ,25). SD and P(|X−μ|<10)?

**9.** Sample SD vs population SD: divide by n or n−1?

**10.** Coefficient of variation: mean=50, SD=10. CV?

---

## Level 3 — Multi-Step

**11.** Compute SD for: 10,12,14,16,18 using σ²=Σ(x−μ)²/n.

**12.** X,Y independent: SD(X+Y) if SD(X)=3, SD(Y)=4?

**13.** Frequency: 5(×2), 10(×3), 15(×5). Mean and SD.

**14.** All values transformed: Y=2X−3. If SD(X)=4, find SD(Y).

**15.** Bin(100,0.25): mean and SD. Compare SD to √np.

---

## Level 4 — Trap Questions

**16.** SD can be negative:
(a) true  (b) false

**17.** Var(aX+b) equals:
(a) a·Var(X)  (b) a²Var(X)  (c) a²Var(X)+b²  (d) aVar(X)+b

**18.** Adding constant to all data changes SD:
(a) yes  (b) no

**19.** SD of {1,2,3,4,5} equals SD of {11,12,13,14,15}:
(a) true  (b) false

**20.** If Var(X)=0, SD is:
(a) 0  (b) undefined  (c) 1  (d) μ

---

## Level 5 — Challenge

**21.** Prove Var(X)=E[X²]−E[X]².

**22.** Chebyshev: μ=100, σ=15. At least what fraction within 60–140?

**23.** Two datasets same mean 50. A: SD=5, B: SD=20. Which is more predictable?

**24.** X~Uniform(0,1). SD(X) and SD(X²)?

**25.** Portfolio: two stocks SD 20% and 30%, correlation 0.5, equal weights. Portfolio SD?

---

## Answers (Full Reasoning)

**A1.** Var = 20−16 = **4**.

**A2.** SD = **3**.

**A3.** Var(3X) = 9·2 = **18**.

**A4.** Var(X+Y) = 4+9 = **13**.

**A5.** SD = √16 = **4**.

**A6.** Mean = **6**. Var = (16+4+0+4+16)/5 = 8. SD = **√8 ≈ 2.83**.

**A7.** SD scales: **10**.

**A8.** SD = **5**. P(|X−μ|<10)=P(|Z|<2) ≈ **0.9545**.

**A9.** Population: **n**. Sample unbiased: **n−1** (Bessel).

**A10.** CV = 10/50 = **0.2 or 20%**.

**A11.** μ=14. σ²=(16+4+0+4+16)/5=8. SD=**√8**.

**A12.** Var sum = 9+16=25. SD=**5**.

**A13.** μ=(10+30+75)/10=11.5. Σf(x−μ)²=84.5+6.75+61.25=152.5. σ²=15.25. SD≈**3.91**.

**A14.** SD(Y)=|2|·SD(X)=**8** (shift doesn't affect spread).

**A15.** μ=25, Var=np(1−p)=18.75. SD≈**4.33**.

**A16.** **(b) false** — SD=√Var≥0.

**A17.** **(b) a²Var(X)** — constant b doesn't affect variance.

**A18.** **(b) no** — translation invariant.

**A19.** **(a) true** — same spread; shift doesn't change SD.

**A20.** **(a) 0**.

**A21.** Expand E[(X−μ)²]=E[X²−2Xμ+μ²]=E[X²]−μ².

**A22.** |X−μ|<40 → k=40/15≈2.67. Fraction within ≥1−1/k²≈1−1/7.11≈**0.86**.

**A23.** **A** (lower SD → less variability).

**A24.** SD(X)=1/√12≈**0.289**. SD(X²)≈**0.298** (compute via E[X⁴]−E[X²]²).

**A25.** Var = 0.25(400+900+2·0.5·20·30)=0.25(1300+600)=475. SD≈**21.8%**.

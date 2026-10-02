# Median — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Median of 3,1,4,2,5?

**2.** Median of 1,3,4,7?

**3.** Uniform(0,10) median?

**4.** 1,2,3,4,100: mean vs median?

**5.** F(m)=0.5 for continuous means?

---

## Level 2 — Standard GATE

**6.** Find median of: 8, 3, 12, 5, 9, 3, 7.

**7.** Even count: 2,4,6,8,10,12 — median?

**8.** X~Exp(λ). Median in terms of λ?

**9.** Normal(μ,σ²): relation between median and μ?

**10.** Grouped data (use interpolation): 0–10(8), 10–20(12), 20–30(5). Approximate median class?

---

## Level 3 — Multi-Step

**11.** Salaries: 5,6,7,8,9 (lakhs) plus CEO at 200. Compare mean and median. Which is better central tendency?

**12.** X~Uniform(a,b). Prove median = (a+b)/2.

**13.** Discrete: P(X=1)=0.2, P(X=2)=0.3, P(X=3)=0.3, P(X=4)=0.2. Find median.

**14.** Two datasets same median 50. Set A: 48,49,50,51,52. Set B: 10,20,50,80,90. Compare spreads.

**15.** n=101 sorted values. Which position is the median? What if one outlier removed (n=100)?

---

## Level 4 — Trap Questions

**16.** Median is always one of the data values:
(a) always  (b) only for odd n  (c) never for even n  (d) only for discrete

**17.** Median unaffected by adding constant c to all values:
(a) true  (b) false

**18.** For skewed right data, typically:
(a) mean > median  (b) mean < median  (c) mean = median

**19.** Median of Bin(10,0.5) is:
(a) 5  (b) 4.5  (c) 5 or 6  (d) 0

**20.** If 50th percentile = 40, then:
(a) median = 40  (b) mean = 40  (c) mode = 40

---

## Level 5 — Challenge

**21.** Prove: for any dataset, Σ|xᵢ−m| is minimized when m is the median.

**22.** X~N(0,1). Is median of X² equal to 1? Explain.

**23.** Trimmed mean (drop min and max of 5 values 1,2,3,4,100). Compare to median.

**24.** Empirical CDF: 5,10,15,20,25. Find smallest x with F(x)≥0.5.

**25.** Two groups medians m₁,m₂ with n₁,n₂ observations. Is combined median (n₁m₁+n₂m₂)/(n₁+n₂)?

---

## Answers (Full Reasoning)

**A1.** Sorted: 1,2,3,4,5 → **3**.

**A2.** Even: (3+4)/2 = **3.5**.

**A3.** **5** (midpoint).

**A4.** Mean = 22, median = **4** — outlier pulls mean up.

**A5.** **Yes** — m satisfies F(m)=0.5.

**A6.** Sorted: 3,3,5,7,8,9,12 → **7** (4th of 7).

**A7.** (6+8)/2 = **7**.

**A8.** 1−e^{−λm}=0.5 → m = **(ln 2)/λ**.

**A9.** Median = **μ** (symmetric).

**A10.** Cumulative: 8, 20, 25. Median in **10–20** class (20th value of 25).

**A11.** Mean ≈ 39.5, median = **8**. Median better for skewed income.

**A12.** F(m)=(m−a)/(b−a)=0.5 → m=(a+b)/2.

**A13.** CDF: 0.2, 0.5, 0.8, 1.0 at x=1,2,3,4. Smallest x with F≥0.5 is **2**.

**A14.** Same median; B has **larger spread** (IQR/range).

**A15.** Position **51** (middle of 101). n=100 → median is average of positions **50 and 51**.

**A16.** **(b)** — odd n: always a data value; even n: may be average of two middle values.

**A17.** **(a) true** — shifts all values equally; relative order unchanged.

**A18.** **(a) mean > median** — right tail pulls mean.

**A19.** **(c) 5 or 6** — symmetric binomial around 5.

**A20.** **(a) median = 40**.

**A21.** Standard proof: deviation from median splits sums; any move from m increases total absolute deviation.

**A22.** **No** — X² is chi-square(1); median ≈ **0.455**, not 1 (mean of X² is 1).

**A23.** Trimmed mean of 2,3,4 = **3**. Median of full set = **3**. Same here; not always.

**A24.** F(15)=0.6≥0.5, F(10)=0.4. Smallest x: **15**.

**A25.** **No** — weighted average of medians is not the combined median; must merge and find middle.

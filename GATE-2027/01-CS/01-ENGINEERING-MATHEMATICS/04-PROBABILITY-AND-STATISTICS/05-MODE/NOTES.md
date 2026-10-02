# Mode — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is the mode?

The **mode** is the value (or values) that occur **most frequently** in a dataset, or the value where the PMF/PDF attains its **maximum** for a distribution.

**Prerequisite:** `03-MEAN/NOTES.md`, `04-MEDIAN/NOTES.md`.

**Links:** Third measure of central tendency; distribution-specific modes (e.g., binomial ⌊(n+1)p⌋) in `05-BINOMIAL/NOTES.md`.

---

## 2. Mode from frequency data

### Rule

Find the value with **highest frequency**. If tie for highest, distribution is **multimodal**.

### Worked Example 1 — Unimodal

Colors: R(3), G(5), B(2). Mode = **G** (frequency 5).

### Worked Example 2 — Bimodal

Scores: 7(2), 8(4), 9(4), 10(1). Modes = **8 and 9** (bimodal).

---

## 3. Mode from PMF (discrete)

### Rule

Mode = value k that **maximizes P(X = k)**.

### Worked Example 3 — Binomial

X ~ Bin(10, 0.3). Mode ≈ ⌊(10+1)×0.3⌋ = ⌊3.3⌋ = **3**.

See `05-BINOMIAL/NOTES.md` for mode formula derivation.

### Worked Example 4 — Poisson

X ~ Poisson(4). PMF peaks near k = 4 (since mean = λ = 4). Mode is **3 or 4** (check: P(3) vs P(4) — for λ integer, two modes often tie at λ−1 and λ).

---

## 4. Mode from PDF (continuous)

### Concept

Mode = point where **f(x) is maximum** (peak of density curve).

**P(X = exact mode) = 0** for continuous X — mode is not "most probable point" in point-mass sense; it is where density is highest.

### Worked Example 5 — Exponential

f(x) = λe^{−λx}, x ≥ 0. Maximum at x = **0** (decreasing PDF). Mode = 0, but mean = 1/λ > 0.

### Worked Example 6 — Normal

N(μ, σ²): symmetric bell peaks at **μ**. Mode = median = mean.

---

## 5. Uniform — no unique mode

### Discrete uniform on {1,…,n}

Every value has probability 1/n — **all values tie**. Every value is a mode (or "no unique mode" depending on convention).

### Continuous uniform on [a,b]

Flat PDF — **every point** has same density. No unique mode; interval is sometimes said to be "uniformly modal."

### GATE Connection

Don't force a single mode when all values are equally likely.

---

## 6. Mode vs mean vs median

| Measure | Definition | Outliers? |
|---------|------------|-----------|
| Mode | Most frequent / peak density | Unaffected |
| Median | Middle of ordered data | Robust |
| Mean | Average | Sensitive |

### Worked Example 7 — Skewed data

Income: most earn 5L, few earn 50L.

Mode ≈ **5L** (most common); mean pulled toward 50L; median in between.

---

## 7. Multimodal distributions

### Concept

**Bimodal:** two peaks (e.g., mixture of two groups).

**Unimodal:** one peak.

GATE may ask "how many modes" from a histogram or PMF sketch.

---

## 8. GATE syllabus note

**Zero dedicated PYQ rows** mapped to Mode alone in the archive (2007–2026).

Still on syllabus; learn with mean and median. May appear in MSQs on "measures of central tendency" or distribution properties.

---

## 9. Mode for grouped data

In class intervals, the **modal class** is the class with highest frequency. Exact mode within class may use interpolation (beyond typical GATE depth unless specified).

For exam: identify class with max frequency.

---

## 10. GATE Connection

- Discrete: max of PMF.
- Continuous: max of PDF (set derivative to 0 if needed).
- Normal: mode = μ.
- Binomial: mode ≈ ⌊(n+1)p⌋.
- Uniform discrete: all values modal.
- Mode need not be near mean or median.

---

## 11. Common traps

1. Mode is **not** necessarily near mean/median.
2. Continuous: mode ≠ "value with highest probability" (point prob = 0).
3. Ties → multimodal; don't report single mode incorrectly.
4. Confusing mode with **median** (position) or **mean** (average).

---

## 12. Summary checklist

- [ ] Mode = highest frequency (data) or max PMF/PDF (distribution).
- [ ] Can be multimodal or absent (flat uniform).
- [ ] Normal: mode = μ.
- [ ] Binomial mode ≈ ⌊(n+1)p⌋.
- [ ] Exponential: mode at 0.
- [ ] Compare with mean and median for skewed data.

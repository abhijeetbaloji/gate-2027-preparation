# Median — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is the median?

The **median** is the value that splits ordered data into two equal halves — **50th percentile**. Half the observations are below (or equal to) the median; half are above (or equal).

**Prerequisite:** Basic data ordering; `03-MEAN/NOTES.md` for comparison.

**Links:** With **mode** (`05-MODE/NOTES.md`) and **mean**, forms the trio of central tendency. Robust alternative when mean is distorted by outliers.

---

## 2. Median for raw data

### Odd number of observations (n odd)

1. Sort data ascending.
2. Median = value at position **(n+1)/2**.

### Even number of observations (n even)

1. Sort data ascending.
2. Median = **average of the two middle values** at positions n/2 and n/2+1.

### Why average for even n

No single middle value; convention uses midpoint between the two central values.

### Worked Example 1 — Odd n

Data: 3, 1, 4, 2, 5 → sorted: 1, 2, 3, 4, 5. n = 5.

Median = value at position 3 = **3**.

### Worked Example 2 — Even n

Data: 4, 1, 7, 3 → sorted: 1, 3, 4, 7. n = 4.

Median = (3 + 4)/2 = **3.5**.

---

## 3. Why median is robust to outliers

### Concept

Median depends only on **order**, not exact values of extreme points.

### Worked Example 3 — Outlier comparison

Data: 2, 3, 4, 5, 100.

Mean = 114/5 = **22.8** (skewed by 100).  
Median = **4** (unchanged if 100 were 6 or 1000).

### When to prefer median

- Skewed income/response-time data.
- Data with extreme values or suspected errors.

---

## 4. Median for grouped / frequency data

### Method

1. Find cumulative frequencies.
2. Locate class where cumulative frequency first reaches or exceeds n/2.
3. Use interpolation within that class (if GATE gives class boundaries).

For simple GATE problems, data lists are usually small — sort and pick middle.

### Worked Example 4 — Frequency table

Value: 1(2), 2(3), 3(5), 4(2) → 12 values sorted mentally.

Positions 6–7 are in the block of 3s → median = **3**.

---

## 5. Median of a continuous distribution

### Definition

**m** is a median if **P(X ≤ m) ≥ 0.5** and **P(X ≥ m) ≥ 0.5**.

Equivalently: **F(m) = 0.5** when CDF is continuous and strictly increasing.

### Why CDF = 0.5

Half the probability mass below m, half above.

### Worked Example 5 — Uniform

X ~ Uniform(0, 10). Median m: F(m) = m/10 = 0.5 → m = **5**.

Same as mean for symmetric uniform — (0+10)/2 = 5.

---

## 6. Median vs mean for symmetric distributions

### Rule

For **perfectly symmetric** distributions about μ: **median = mean = mode**.

Examples: Normal N(μ,σ²), symmetric Uniform.

### Skewed distributions

- **Right-skewed:** mean > median (tail pulls mean right).
- **Left-skewed:** mean < median.

Exponential is right-skewed: mean = 1/λ > median = (ln 2)/λ.

---

## 7. GATE syllabus note

**Zero dedicated PYQ rows** mapped to Median alone in the archive (2007–2026).

Still on the official syllabus; may appear embedded in combined statistics questions or alongside mean/SD. Do not skip — examiners can test ordering rules and robustness concept.

---

## 8. Median of two numbers

For two values a ≤ b: median = **(a+b)/2**.

Special case of even-n rule.

---

## 9. GATE Connection

- Sort first — median is undefined on unsorted raw data without sorting step.
- Even n: average two middles.
- Compare with mean for skewed data questions.
- Continuous: solve F(m) = 0.5.
- Links to **percentiles** (median = 50th percentile).

---

## 10. Common traps

1. Forgetting to **sort** before finding middle.
2. Even n: taking only one middle value instead of **average of two**.
3. Confusing median with **mode** (most frequent).
4. Using mean formula on ordered positions.

---

## 11. Relation to other topics

| Topic | Connection |
|-------|------------|
| Mean | Alternative center; compare robustness |
| Mode | Another center; may differ from median |
| Normal | Median = μ |
| Random Variables | Median from CDF |
| Standard Deviation | Spread around mean, not median (usually) |

---

## 12. Summary checklist

- [ ] Sort data ascending first.
- [ ] Odd n: middle at (n+1)/2.
- [ ] Even n: average of positions n/2 and n/2+1.
- [ ] Robust to outliers vs mean.
- [ ] Continuous: F(median) = 0.5.
- [ ] Symmetric → median = mean.

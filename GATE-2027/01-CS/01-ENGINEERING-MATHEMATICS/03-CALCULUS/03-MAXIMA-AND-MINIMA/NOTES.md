# Maxima and Minima — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is optimization in GATE?

**Maxima and minima** find where a function reaches its largest or smallest values — locally (near a point) or globally (on a domain). Requires **derivatives** from `02-CONTINUITY-AND-DIFFERENTIABILITY/NOTES.md`.

GATE tests:
- Critical points and derivative tests
- Absolute extrema on closed intervals
- Applied problems (area, cost, distance)
- Link to **MVT** (derivative zero somewhere)

---

## 2. Critical points

**Critical point** c: where **f'(c) = 0** or **f'(c) does not exist**.

These are **candidates** for local extrema — not guaranteed (e.g. x³ at 0).

### Worked Example 1

f(x) = x³ − 3x.

f'(x) = 3x² − 3 = 3(x² − 1) = 0 ⇒ x = **±1**.

Critical points: x = −1, 1.

---

## 3. First derivative test

Examine sign of f' around c:

| Sign change of f' | Conclusion |
|-------------------|------------|
| + → − | **Local maximum** at c |
| − → + | **Local minimum** at c |
| Same sign | **No local extremum** (inflection) |

### Worked Example 2 — f(x) = x³ − 3x

- x = −1: f' goes + → − ⇒ **local max**, f(−1) = 2.
- x = 1: f' goes − → + ⇒ **local min**, f(1) = −2.
- x = 0: f'(0) = −3 ≠ 0, not critical — but shows f' always negative between −1 and 1.

---

## 4. Second derivative test

If f'(c) = 0 and f'' exists:

| Condition | Conclusion |
|-----------|------------|
| f''(c) > 0 | **Local minimum** (concave up) |
| f''(c) < 0 | **Local maximum** (concave down) |
| f''(c) = 0 | **Inconclusive** — use first derivative test |

### Why it works (sketch)

f''(c) > 0 means f' is increasing at c; f' was negative before and positive after (for min) — concave up bowl.

### Worked Example 3

f(x) = x⁴ − 4x².

f' = 4x³ − 8x = 4x(x² − 2) ⇒ x = 0, ±√2.

f'' = 12x² − 8.

- x = 0: f'' = −8 < 0 ⇒ **local max**, f(0) = 0.
- x = ±√2: f'' = 16 > 0 ⇒ **local min**, f(±√2) = −4.

---

## 5. Absolute extrema on closed interval [a, b]

**Extreme Value Theorem:** continuous f on [a,b] attains absolute max and min.

**Procedure:**
1. Find critical points in (a,b).
2. Evaluate f at each critical point and at **endpoints a, b**.
3. Largest value = absolute max; smallest = absolute min.

### Worked Example 4

f(x) = x² on [−1, 2].

Critical: f' = 2x = 0 ⇒ x = 0.

f(−1) = 1, f(0) = 0, f(2) = 4.

**Absolute min = 0** at x = 0; **absolute max = 4** at x = 2.

---

## 6. Applied optimization — GATE word problems

**Strategy:**
1. Draw diagram / define variable x.
2. Express quantity Q to optimize as Q(x).
3. Find domain of x (physical constraints).
4. Q'(x) = 0, test, compare endpoints.

### Worked Example 5 — Rectangle of fixed perimeter

Perimeter 2(x + y) = 20 ⇒ y = 10 − x. Area A = x(10 − x) = 10x − x².

A' = 10 − 2x = 0 ⇒ x = 5, y = 5.

**Square 5×5** gives maximum area 25.

### Worked Example 6 — Minimize distance

Minimize d² = x² + (x² − 4)² rather than d (same minimizer, no square root).

---

## 7. Concavity and inflection

- **f'' > 0:** concave up (holds water).
- **f'' < 0:** concave down.
- **Inflection point:** f'' changes sign.

x³ at 0: f''(0) = 0 but no local extremum — inflection.

---

## 8. GATE Connection

- Critical points of polynomials and rationals.
- Closed-interval comparison — **never forget endpoints**.
- Applied: area, volume, cost with one variable.
- Distinguish local vs global extrema.
- Link: Rolle's theorem (f(a)=f(b) ⇒ some c with f'(c)=0).

---

## 9. Common traps

1. Critical point need not be extremum (x³ at 0).
2. f''(c) = 0 inconclusive.
3. On [a,b], endpoint values can beat interior critical points.
4. Wrong domain (e.g. x must be positive).

---

## 10. Summary checklist

- [ ] Find f' = 0 and f' undefined.
- [ ] First derivative test: sign change.
- [ ] Second derivative test when f'(c) = 0.
- [ ] On [a,b]: evaluate f at critical points + a + b.
- [ ] Applied: one variable, state domain.

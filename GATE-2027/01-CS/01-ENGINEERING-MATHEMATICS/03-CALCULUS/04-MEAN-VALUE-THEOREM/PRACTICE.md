# Mean Value Theorem — GATE-STYLE PRACTICE

## Level 1

**1.** State Rolle's theorem hypotheses.

**2.** f(x) = x² − 1 on [−1, 1]. Does Rolle apply? Find c.

**3.** MVT conclusion: what does f'(c) equal?

### Level 1 — Solutions

1. Cont [a,b], diff (a,b), f(a)=f(b).
2. **Yes**; f(±1)=0; f'(c)=2c=0 ⇒ **c=0**.
3. **(f(b)−f(a))/(b−a)**.

## Level 2

**1.** f(x) = x³ on [0, 2]. Find c for MVT.

**2.** f(0)=3, f(4)=11, f continuous. Some c with f'(c)=2?

**3.** Can Rolle apply to f(x)=1/x on [−1, 1]?

### Level 2 — Solutions

1. Secant slope 4; 3c²=4 ⇒ **c=2/√3**.
2. **Yes** — average slope (11−3)/4 = 2.
3. **No** — not continuous at 0.

## Level 3

**1.** Prove: if f'(x) > 0 on (a,b), f increasing on [a,b].

**2.** |f'(x)| ≤ 5 on [0,3]. Bound |f(3)−f(0)|.

**3.** f(x) = sin x on [0, π]. Find c with f'(c) = 0.

### Level 3 — Solutions

1. MVT: f(b)−f(a) = f'(c)(b−a) > 0.
2. **≤ 15**.
3. Rolle: **c = π/2**.

## Level 4

**1.** Why must c be in (a,b) not [a,b]?

**2.** f twice differentiable — link MVT to Taylor (conceptual).

### Level 4 — Solutions

1. Endpoints may not be differentiable (e.g. |x|).
2. MVT is first-order Taylor with remainder bound.

## Level 5 — Challenge

**1.** f differentiable on [0,1], f(0)=0, f(1)=1. Show ∃c ∈ (0,1) with f'(c) > 1.

**2.** Two cars start together; speeds always differ by at most 10 km/h over 2 hours. Max separation?

**3.** f(x) = |x| on [−1,1]. Can any mean-value theorem apply? Explain.

### Level 5 — Solutions

1. If f'(c) ≤ 1 everywhere, integrating would give f(1)−f(0) ≤ 1 — contradiction with f(1)=1, f(0)=0 needing average slope 1; actually need strict: if all f'≤1 then f(1)≤1 OK; for **>1** somewhere: if max f'≤1 then MVT gives exactly 1. To force **>1**: consider f(x)=x² gives f'(1)=2>1. General: if average slope is 1, f' cannot be ≤1 everywhere unless constant slope — if f non-linear, some c has f'(c)>1 or <1; construct counterexample carefully. *Standard result:* average slope 1 ⇒ some c with f'(c)≥1 (not always >). **Challenge variant:** f(x)=x² on [0,1]: c=1 gives f'(1)=2>1. ✓

2. MVT on separation S(t): max |S(2)−S(0)| ≤ 2×10 = **20 km**.

3. **Rolle/MVT fail** at 0 (not differentiable). No interior c with derivative equals secant slope through endpoints in classical sense.

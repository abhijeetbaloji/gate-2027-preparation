# Standard Deviation — Shortcuts

## 1. E[X²] − (E[X])²

- **Why it works**: Computational variance without μ in each term
- **When to use**: PMF/PDF given
- **Trap**: Need E[X²] correctly

## 2. SD scales by |a| only

- **Why it works**: Shift b doesn't affect spread
- **When to use**: SD(aX+b) problems
- **Trap**: Don't add b to SD

## 3. Independent sum: squares add

- **Why it works**: Variances add, then sqrt
- **When to use**: SD(X+Y)
- **Trap**: Not σ_X + σ_Y

## 4. Poisson SD = √λ

- **Why it works**: Mean = variance = λ
- **When to use**: Poisson spread
- **Trap**: λ not √λ for variance

## 5. Binomial Var = np(1−p)

- **Why it works**: Memorize; max at p=0.5
- **When to use**: Bin SD problems
- **Trap**: Don't use np for variance

# Bayes' Theorem — Shortcuts

## 1. Compute P(B) first

- **Why it works**: Total probability before dividing
- **When to use**: Any Bayes problem
- **Trap**: Wrong denominator ruins answer

## 2. Tree diagram

- **Why it works**: Joint = product on path; marginal = sum paths
- **When to use**: Factory/test problems
- **Trap**: Label every branch

## 3. Rare disease sanity check

- **Why it works**: Posterior << sensitivity when prior small
- **When to use**: Medical MCQs
- **Trap**: 95% test ≠ 95% diseased

## 4. Two-factory template

- **Why it works**: P(F_i|D)=P(D|F_i)P(F_i)/P(D)
- **When to use**: Defect source problems
- **Trap**: Include all factories in P(D)

## 5. Table method

- **Why it works**: Joint cells then normalize column
- **When to use**: Algebra error prevention
- **Trap**: Rows must sum to priors

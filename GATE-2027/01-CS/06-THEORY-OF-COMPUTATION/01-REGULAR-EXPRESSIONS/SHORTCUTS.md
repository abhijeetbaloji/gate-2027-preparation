# Regular Expressions — Shortcuts

Each shortcut below is a valid rule, not a guess. The limitation line says exactly where it stops working.

## 1. Boundary-string elimination

- **Solves**: "Which RE denotes language L?" with four options.
- **When**: always, as the first pass.
- **Why it works**: two languages that differ on any string are different. Short strings are where most wrong options differ.
- **Example**: "odd number of 1s". Test `1` (must be in), `ε` and `11` (must be out), `0 1 0` (must be in). An option of the form `(…)*1` that cannot produce `10` is eliminated by `10`.
- **Limitation**: surviving one test is not a proof; if two options survive, find a distinguishing string or argue both directions.

## 2. Complement for "does not contain"

- **Solves**: counting or describing strings avoiding a pattern.
- **When**: the forbidden pattern is short.
- **Why**: over `{a, b}`, a string avoids `ab` exactly when no `a` precedes a `b`, i.e. it is in `b*a*`.
- **Example**: length-6 strings containing `ab`: `2^6 − 7 = 57`.
- **Limitation**: the `b*a*` description is special to a two-symbol pattern of distinct symbols over a two-letter alphabet. For `aa` or for larger alphabets use a DFA or a recurrence.

## 3. Adjacency for "contains both symbols"

- **Solves**: "at least one 0 and at least one 1".
- **Why**: if a string has both symbols, somewhere a `0` is next to a `1`, so it contains `01` or `10`. Conversely `01` or `10` supplies both symbols.
- **Example**: `(0+1)*(01 + 10)(0+1)*` is correct even though it looks too narrow.
- **Limitation**: applies to "contains both symbols"; it does not give "contains both `00` and `11`".

## 4. Star absorbs `ε` and subsets

- **Solves**: simplifying options quickly.
- **Rule**: `(ε + r)* = r*`; if `L(s) ⊆ L(r*)` then `(r + s)* = r*`.
- **Why**: everything `s` adds is already a concatenation of `r`-pieces.
- **Example**: `(a + aa)* = a*`; `(0 + 1 + 01)* = (0+1)*`.
- **Limitation**: the subset condition must be checked; `(a + ab)*` is not `a*`.

## 5. Mod-k DFA → RE instead of guessing

- **Solves**: "RE for binary numbers divisible by k" or "count of a symbol ≡ r (mod k)".
- **When**: k = 2 or 3 (state elimination is short).
- **Why**: a mod-k DFA is easy to write (`r → (2r + b) mod k`), and state elimination is mechanical.
- **Example**: remainder 0 mod 3 gives `(0 + 1(01*0)*1)*`.
- **Limitation**: decide whether `ε` is counted as divisible; the RE includes it.

## 6. Unambiguous-star counting

- **Solves**: "how many strings of length n are in `(p1 + … + pm)*`".
- **When**: no string has two different parses into pieces. A sufficient check: no piece is a prefix of another (prefix code).
- **Why**: then strings and parses are in bijection, so `t(n) = Σ t(n − |p_i|)`.
- **Example**: `(aa + ab + b)*`: lengths 1, 2, 2 → `t(n) = t(n−1) + 2t(n−2)`, `t(6) = 43`.
- **Limitation**: with ambiguous pieces the recurrence over-counts. `(a + aa)*` has exactly one string, `a^n`, of each length, while the recurrence gives Fibonacci numbers.

## 7. Inclusion–exclusion per length

- **Solves**: "strings of length ≤ n not in `r` or `s`".
- **Why**: `|A ∪ B| = |A| + |B| − |A ∩ B|` at each length.
- **Example**: `0*1* + 1*0*` at length `n ≥ 1` has `2(n + 1) − 2 = 2n` strings.
- **Limitation**: the overlap must be found exactly; at length 0 both contain only `ε`.

## 8. Arden direction check

- **Solves**: avoiding the reversed answer when solving state equations.
- **Rule**: unknown on the left of the coefficient (`X = Q + XP`) → `QP*`; on the right (`X = Q + PX`) → `P*Q`.
- **Example**: `X = b + Xa` gives `ba*`; check: `b ∈ X`, `ba ∈ X`, `ab ∉ X`.
- **Limitation**: needs `ε ∉ L(P)`.

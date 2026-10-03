# Regular Expressions — MISTAKES

Typical mistakes for this topic (general error patterns, not records of any person's errors). Theory: [NOTES.md](NOTES.md).

## 1. Conceptual confusions

| Mistake | Correct idea |
|---|---|
| `∅* = ∅` | `L^0 = {ε}` is always in the star, so `∅* = {ε}` |
| `{ε}` treated as empty | `{ε}` has one string; `∅` has none |
| `L · ∅ = L` | Concatenation with `∅` is `∅` |
| `L+ = L*` always | Equality holds if and only if `ε ∈ L` |
| `ε` is a symbol of `Σ` | `ε` is a string of length 0, not a letter |
| `(ab)*` = `a*b*` | Left is `(ab)(ab)…`; right is `a`s then `b`s |
| `(a+b)*` = `a* + b*` | Left contains `ab`; right does not |
| Star distributes over concatenation | `(rs)* ≠ r*s*` |
| “Contains `00` and `11`” = “contains `0011` or `1100`” | The blocks need not be adjacent, and either order is allowed |
| “At least two `0`s” = “contains `00`” | `010` has two `0`s and no `00` |
| “Even number of `1`s” excludes `ε` | Zero is even; `ε` and `000` are members |

## 2. Parsing / algebra mistakes

- Ignoring precedence: `ab + c` is `{ab, c}`, not `{ab, ac}`. `a + b*c` is `{a} ∪ {b^n c}`.
- Solving `X = Q + XP` as `P*Q` instead of `QP*`.
- Using Arden when `ε ∈ L(P)`; uniqueness fails.
- Claiming `r*r = r*` for every `r`. Counterexample: `r = a` misses `ε` on the left.
- Counting parses of an ambiguous RE as if they were distinct strings.

## 3. Construction mistakes

- Thompson star missing the bypass `ε`-edge: `ε` is then rejected even though `ε ∈ L(r*)`.
- State elimination: forgetting a pair `(incoming, outgoing)` through the removed state, or forgetting to merge with an existing parallel edge.
- Mod-3 RE: forgetting that the usual elimination includes `ε`, or assuming a remainder-1 string must end with `1`.

## 4. PYQ-derived traps (mapped stems only)

| Year / Q# | Trap pattern |
|---|---|
| 2024 Q.61 | Forgetting `ε`; misidentifying the overlap of `0*+1*` with `01*+10*`; counting length 5 only |
| 2023 Q.19 | ε-NFA that accepts a digit-first identifier, or that cannot accept a single letter |
| 2021 Q.47 | Dropping `ε` from “divisible by 3”; an option that looks similar but is not the mod-3 language |
| 2020 Q.7 | An RE that cannot generate `10`, or that generates `ε` / `11` |
| 2016 Q.18 | Forcing `00` and `11` to be adjacent, or requiring only one of the two blocks |
| 2009 Q.15 | Reading two literal `0`s as the substring `00` |
| 2008 Q.52, 2007 Q.74 | Matching by appearance of the figure instead of tracing short strings |

## 5. Examination-time mistakes

- Not testing `ε` and the single-symbol strings in every option.
- Proving two REs equal by checking three strings and stopping.
- Using a DFA path count when an unambiguous decomposition is available — or the reverse, using a decomposition on an ambiguous RE.

## 6. How to check yourself

1. Did I parse with `*` > concatenation > `+`?
2. Did I write the shortest members and one forbidden string?
3. For a “contains both patterns” RE, did I allow both orders and a gap?
4. For counting, did I count strings once (complement, inclusion–exclusion, or a DFA)?
5. For Arden, which side is the unknown on, and is `ε` out of `P`?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|------|--------|----------|---------|------------|------------|
|      |        |          |         |            |            |

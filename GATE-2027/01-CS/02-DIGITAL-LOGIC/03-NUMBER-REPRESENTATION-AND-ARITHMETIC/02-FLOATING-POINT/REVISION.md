# Floating Point — Revision

Single precision: 1 sign, 8 exponent, 23 fraction. Bias **127**.

## Value

| Kind | When | Value |
|------|------|-------|
| Normal | \(1 \le E \le 254\) | \((-1)^s (1.f) 2^{E-127}\) |
| Zero | \(E=0, f=0\) | \(\pm 0\) |
| Subnormal | \(E=0, f \neq 0\) | \((-1)^s (0.f) 2^{-126}\) |
| Infinity | \(E=255, f=0\) | \(\pm \infty\) |
| NaN | \(E=255, f \neq 0\) | not a number |

## Landmarks

| Word | Value |
|------|-------|
| `0x00000000` | \(+0\) |
| `0x80000000` | \(-0\) |
| `0x00800000` | smallest positive normal, \(2^{-126}\) |
| `0x00000001` | smallest positive subnormal, \(2^{-149}\) |
| `0x3F800000` | \(+1\) |
| `0x40000000` | \(+2\) |
| `0x7F800000` | \(+\infty\) |
| `0x7F7FFFFF` | largest finite (exponent 254, fraction all 1s) |

## Arithmetic

- Add: right-shift the smaller significand by the exponent difference, add, normalise, round.
- Multiply: sign = XOR; biased exponent \(E_1+E_2-127\); multiply \(1.f\) fields; if the product significand is \(\ge 2\), shift right and add 1 to the exponent.

## Traps

Bias 128. Hidden 1 on a subnormal. Infinity treated as a finite \(2^{128}\). \(-0\) treated as a large magnitude. Smallest normal called \(2^{-149}\). Forgetting to subtract 127 when adding biased exponents.

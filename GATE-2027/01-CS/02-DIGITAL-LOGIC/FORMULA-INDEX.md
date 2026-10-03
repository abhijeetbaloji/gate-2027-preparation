# Digital Logic — Formula Index

The condition for each formula is in the linked file. The reason is in that topic’s `NOTES.md`.

## Boolean algebra

[Algebraic technique](01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/01-ALGEBRAIC-TECHNIQUE/FORMULAS.md)

- \(2^{2^n}\) functions; \(2^{2^{n-1}}\) self-dual functions
- Absorption, covering \(x+x'y=x+y\), consensus, both distributive laws, De Morgan
- XOR \(x'y+xy'\); XNOR \(xy+x'y'\)
- Shannon expansion \(F = x F(1) + x' F(0)\)

## Karnaugh map

[Karnaugh map](01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/02-KARNAUGH-MAP/FORMULAS.md)

- \(2^n\) cells, \(n\) neighbours, groups of size \(2^k\) only
- A group of \(2^k\) cells has \(n-k\) literals
- SOP: complement a variable that is constantly 0
- POS, from the 0s: complement a variable that is constantly 1

## Tabular method

[Tabular method](01-BOOLEAN-ALGEBRA-AND-MINIMIZATION/03-TABULAR-METHOD/FORMULAS.md)

- Combine strings at distance 1 with dashes aligned: \(Px+Px'=P\)
- Primes are the unticked strings
- Essential primes are the single-mark columns of the onset chart
- Don’t-cares are combined, then omitted from the chart

## Combinational circuits

[Combinational circuits](02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/01-COMBINATIONAL-CIRCUITS/FORMULAS.md)

- Half adder \(S=A\oplus B\), \(C=AB\); full adder sum \(A\oplus B\oplus C_{in}\), carry majority
- Lookahead \(C_{i+1}=G_i+P_i C_i\), with \(G_i=A_i B_i\), \(P_i=A_i\oplus B_i\)
- \(2^n\)-to-1 mux has \(n\) selects; a 2-to-1 tree uses \(2^n-1\) muxes
- Active-low decoder pins, NAND-ed, rebuild a sum of minterms
- Binary to Gray: copy the MSB, XOR adjacent bits downward

## Sequential circuits

[Sequential circuits](02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/02-SEQUENTIAL-CIRCUITS/FORMULAS.md)

- \(Q^+=D\); \(Q^+=T\oplus Q\); \(Q^+=JQ'+K'Q\); SR only while \(SR=0\)
- Minimum flip-flops \(\lceil \log_2 N \rceil\) for \(N\) states
- Binary up counter: \(T_0=1\), \(T_i=\) AND of the lower \(Q\) bits
- Johnson main cycle \(2n\); one-hot ring cycle \(n\)
- Clock period \(t_{cq}+t_{pd}+t_{su}\); hold \(t_{cq}(\min)+t_{cd}\ge t_{hold}\)

## Fixed point

[Fixed point](03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT/FORMULAS.md)

- Two’s-complement range \(-2^{n-1}\) through \(2^{n-1}-1\)
- Value \(-b_{n-1}2^{n-1}+\sum_{i<n-1} b_i 2^i\)
- Signed overflow: carry into the sign differs from carry out of the sign
- Unsigned overflow: carry out of the MSB
- Fixed-point value \(N/2^f\) with \(f\) fractional bits
- Booth: add on \(01\), subtract on \(10\), \(Q_{-1}=0\)

## Floating point

[Floating point](03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT/FORMULAS.md)

- Single precision, bias 127: \((-1)^s(1.f)2^{E-127}\) for \(E\) from 1 to 254
- Subnormal: \((-1)^s(0.f)2^{-126}\)
- Smallest positive normal \(2^{-126}\); smallest positive subnormal \(2^{-149}\)
- Product biased exponent \(E_1+E_2-127\), then +1 if the significand product is at least 2

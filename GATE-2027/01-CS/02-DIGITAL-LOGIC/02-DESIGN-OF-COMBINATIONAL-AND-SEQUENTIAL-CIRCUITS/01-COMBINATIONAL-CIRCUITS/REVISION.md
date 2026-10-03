# Combinational Circuits — Revision

## Adders

| Block | Sum | Carry |
|-------|-----|-------|
| Half | \(A \oplus B\) | \(AB\) |
| Full | \(A \oplus B \oplus C_{in}\) | \(AB + BC_{in} + AC_{in}\) |

Carry also equals \(AB + C_{in}(A \oplus B)\). Two half adders and one OR make one full adder.

Ripple: carry delay adds across bits. If one carry takes \(d\), \(n\) bits take \(n d\) from \(C_0\) to \(C_n\).

Lookahead: \(G_i = A_i B_i\), \(P_i = A_i \oplus B_i\),

\[
C_1 = G_0 + P_0 C_0, \quad C_2 = G_1 + P_1 G_0 + P_1 P_0 C_0.
\]

\(n\)-bit adder with \(C_0 = 0\): 1 half adder and \(n-1\) full adders.

## Mux

- \(2^n\)-to-1 has \(n\) selects. \(Y = S'I_0 + S I_1\) for 2-to-1.
- Data tie is the cofactor in the leftover variables: \(0\), \(1\), \(x\), or \(x'\).
- \(2^n\)-to-1 built from 2-to-1 muxes: \(2^n - 1\) of them.
- Any function of \(n\) variables: one \(2^{n-1}\)-to-1 mux, plus an inverter if complements are not free.

## Decoder

- \(n\)-to-\(2^n\). Active-high \(Y_i = m_i\). Input value is the index.
- Active-low pin \(m_i'\). NAND of selected pins = SOP of those minterms.
- 6-to-64 from 3-to-8 with enable and no extra gates: 9.
- 5-to-32 using one 2-to-4 as the enable decoder: four 3-to-8 decoders.

## Encoder

Priority: highest asserted index wins. \(V=0\) when no input is asserted; the index is then meaningless.

## Gray

\(G_{msb} = B_{msb}\), \(G_i = B_{i+1} \oplus B_i\). Inverse: \(B_{msb}=G_{msb}\), \(B_i = B_{i+1} \oplus G_i\). Successive integers differ in one Gray bit.

## Traps

Carry is not XOR. \(C_{out}\) is not signed overflow. Active-low outputs are not OR-ed to form a SOP. A group of 6 is not a mux select width.

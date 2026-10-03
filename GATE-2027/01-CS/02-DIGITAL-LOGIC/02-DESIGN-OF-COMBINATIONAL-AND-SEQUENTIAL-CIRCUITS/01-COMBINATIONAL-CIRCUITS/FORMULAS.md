# Combinational Circuits — Formulas

Reasons are in `NOTES.md`.

## Adders

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(S = A \oplus B\), \(C = AB\) | Half adder | No carry in |
| \(S = A \oplus B \oplus C_{in}\) | Full-adder sum | Odd parity of the three bits |
| \(C_{out} = AB + BC_{in} + AC_{in}\) | Full-adder carry | At least two of the three bits are 1 |
| \(C_{out} = AB + C_{in}(A \oplus B)\) | Same carry | Used by the two-half-adder construction |
| Ripple delay \(n d\) | \(C_n\) after \(C_0\) | Each bit’s carry costs \(d\), and the carry chain is the critical path |
| \(G_i = A_i B_i\), \(P_i = A_i \oplus B_i\) | Generate and propagate | Lookahead, per bit |
| \(C_{i+1} = G_i + P_i C_i\) | Next carry | Unroll it when the option is expanded |

**Example.** \(C_2 = G_1 + P_1 G_0 + P_1 P_0 C_0\). The term \(P_1 G_0\) is the carry generated at bit 0 and propagated through bit 1.

## Mux and decoder

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(n\) select lines | On a \(2^n\)-to-1 mux | Selects encode the data index |
| \(Y = S' I_0 + S I_1\) | 2-to-1 mux | Active-high, \(S=1\) selects \(I_1\) |
| \(2^n - 1\) | Number of 2-to-1 muxes in a \(2^n\)-to-1 | Full tree, no larger mux used |
| \(2^{n-1}\)-to-1 | Smallest mux for any function of \(n\) variables | One variable left for the data pins, complements available as ties |
| \(n\)-to-\(2^n\) | Decoder shape | One output per minterm |
| NAND of active-low minterm pins | SOP of those minterms | Pins carry \(m_i'\) |
| \(1 + 2^{n-k}\) | Count of \(k\)-to-\(2^k\) decoders with enable building an \(n\)-to-\(2^n\) decoder | One block decodes the high \(n-k\) bits, and \(n-k \le k\) so that block is one decoder. For \(n=6, k=3\): \(1+8=9\) |

## Gray

| Formula | Condition |
|---------|-----------|
| \(G_{n-1} = B_{n-1}\), \(G_i = B_{i+1} \oplus B_i\) | Binary to Gray, bit \(n-1\) is MSB |
| \(B_{n-1} = G_{n-1}\), \(B_i = B_{i+1} \oplus G_i\) | Gray to binary |

**Example.** Binary \(1011\) maps to Gray \(1110\).

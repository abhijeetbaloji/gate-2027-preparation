# Sequential Circuits — Revision

## Equations

| FF | \(Q^+\) | Note |
|----|---------|------|
| D | \(D\) | No don’t-care in the excitation |
| T | \(T \oplus Q\) | \(T=1\) toggles |
| JK | \(JQ' + K'Q\) | \(J=K=1\) toggles |
| SR | \(S + R'Q\) | Only while \(SR=0\). NOR latch: \(S=R=1\) forbidden; hold is \(S=R=0\) |

Excitation \(0\to 1\): D=1, T=1, J=1 K=X, S=1 R=0.

Conversions: \(J=D, K=D'\) makes D. \(D = T \oplus Q\) makes T.

## How many flip-flops

\(k = \lceil \log_2 N \rceil\) states in binary code. Count states, not distinct printed numbers. \((0,0,1,1,2,2,3,3)\) has 8 states, so 3 flip-flops. Five Moore states need 3.

## Counters

| Kind | States on the main cycle | Input idea |
|------|--------------------------|------------|
| Binary up, T FFs | \(2^n\) | \(T_0=1\), \(T_1=Q_0\), \(T_2=Q_1 Q_0\) |
| Ring, one-hot | \(n\) | Rotate a single 1 |
| Johnson | \(2n\) | Shift, feed back the complement |
| Saturating up | stays at \(11\ldots 1\) | Hold, do not wrap |
| Ripple binary | MSB period \(= 2^n\) clocks | Next FF clocked by previous \(Q\) |

4-bit Johnson from 0000, new MSB \(= Q_0'\), shift toward LSB: \(0,8,12,14,15,7,3,1\).

Both T inputs 1: from 00 the cycle has length 2, not 4.

## Timing

\[
T \ge t_{cq} + t_{pd} + t_{su}
\]

\[
t_{cq}(\min) + t_{cd} \ge t_{hold}
\]

Hold slack \(= t_{cq}(\min) + t_{cd} - t_{hold}\). Do not add hold into \(T\).

## Traps

\(K'\) not \(K\) in the JK equation. Johnson is \(2n\), ring is \(n\). Repeated outputs can be different states. Mux feedback is a latch.

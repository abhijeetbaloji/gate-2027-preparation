# Sequential Circuits — Formulas

Reasons are in `NOTES.md`.

## Flip-flops

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(Q^+ = D\) | D flip-flop | Edge that the device uses |
| \(Q^+ = T \oplus Q\) | T flip-flop | \(T=0\) holds, \(T=1\) complements |
| \(Q^+ = JQ' + K'Q\) | JK flip-flop | \(J=K=1\) gives \(Q^+\!=Q'\) |
| \(Q^+ = S + R'Q\) | SR | Valid only when \(SR=0\) |
| \(T = Q \oplus Q^+\) | T excitation | No don’t-care: the bit is determined |
| \(J = Q'\cdot Q^+\), with \(K\) free when \(Q=0\) and \(Q^+=1\) | One legal reading of the JK table | The X entries may be set to 0 or 1 |

**Example.** \(J=D\), \(K=D'\) gives \(Q^+ = D\). \(D = T \oplus Q\) gives a T flip-flop from a D flip-flop.

## State count

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(k = \lceil \log_2 N \rceil\) | Minimum flip-flops, binary encoding | \(N\) is the number of distinct states, not the number of distinct output symbols |
| Ring cycle length \(n\) | One-hot rotate | Start state has a single 1; other starts can have other cycles |
| Johnson cycle length \(2n\) | Complement fed back around a shift register | Length of the cycle that contains the given start state. \(2n\) is the main cycle |
| MSB period \(= 2^n T_{clk}\) | Binary ripple or synchronous up counter | \(n\) bits, counting through all codes |

**Example.** Eight steps \((0,0,1,1,2,2,3,3)\) need \(\lceil \log_2 8 \rceil = 3\) flip-flops. A 3-bit Johnson counter’s main cycle has 6 states.

## Synchronous binary up counter

\[
T_0 = 1,\quad T_1 = Q_0,\quad T_i = \prod_{j=0}^{i-1} Q_j.
\]

**Example.** From \(011\), every \(T\) is 1, so the next state is \(100\).

## Timing

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(T_{clk} \ge t_{cq} + t_{pd} + t_{su}\) | Minimum clock period | Worst-case logic delay \(t_{pd}\). Hold is not added |
| \(t_{cq}(\min) + t_{cd} \ge t_{hold}\) | Hold constraint | Minimum delays. A slow clock does not repair a violation |
| Slack \(= t_{cq}(\min) + t_{cd} - t_{hold}\) | Hold slack | Negative means the constraint fails |

**Example.** \(t_{cq}=8\), \(t_{pd}=12\), \(t_{su}=3\) gives period \(23\). Units are the stem’s units.

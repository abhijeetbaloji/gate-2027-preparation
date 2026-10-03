# Sequential Circuits — Shortcuts

## 1. Successors distinguish states

- **Solves.** Minimum number of flip-flops for a counting sequence that repeats numbers.
- **When.** The printed cycle contains the same integer more than once.
- **Why.** A state is identified by what happens next. Two visits that share a code but have different successors cannot be the same stored state.
- **Example.** \((0,0,1,1,2,2,3,3)\) has 8 states, so 3 JK flip-flops. Four distinct integers would have suggested 2, which is short.
- **Limit.** If the same code really is always followed by the same next code, it is one state. Do not split it just because it appears twice in a written trace of a loop.

## 2. Johnson length is \(2n\), ring length is \(n\)

- **Solves.** How many distinct states a shift-register counter visits.
- **When.** The feedback is identified and the start state lies on the main cycle.
- **Why.** Johnson feeds back a complement, so the register fills with 1s and then with 0s: \(n\) steps each way. A ring rotates one 1 and returns after \(n\) steps.
- **Example.** 4-bit Johnson from 0000 visits 8 states. 4-bit ring from 1000 visits 4.
- **Limit.** A start state off the main cycle can have a shorter period. \(2n\) is not \(2^n\).

## 3. \(T_i\) is the AND of the lower bits

- **Solves.** The T inputs of a synchronous binary up counter.
- **When.** The flip-flops are T and the count is binary, increasing, synchronous.
- **Why.** Bit \(i\) must flip exactly on the roll-over of the lower bits, which is the clock when those bits are all 1.
- **Example.** \(T_0=1\), \(T_1=Q_0\), \(T_2=Q_1 Q_0\).
- **Limit.** A down counter ANDs the complements of the lower bits. Tying every \(T\) to 1 is a different counter: from 00 it has period 2.

## 4. Hold is not part of the period

- **Solves.** Minimum clock period versus hold slack.
- **When.** Setup, hold, clock-to-\(Q\), and logic delays are all given.
- **Why.** The period must leave time for the slow path before the next edge. Hold fails when the fast path is too fast; stretching the clock does not slow that path.
- **Example.** Period \(t_{cq}+t_{pd}+t_{su}\). Slack \(t_{cq}(\min)+t_{cd}-t_{hold}\).
- **Limit.** Use the maximum delay in the period and the minimum delay in the hold check. Swapping them is not conservative in the useful direction: it answers a different question.

## 5. MSB frequency is the clock divided by \(2^n\)

- **Solves.** A ripple-counter waveform question.
- **When.** The counter is binary, \(n\) bits, and one period is given.
- **Why.** Each stage toggles once per two toggles of the previous stage, so the last stage sees \(2^n\) clocks per cycle.
- **Example.** 4-bit counter, last-stage period \(64\,\mu s\): clock frequency \(16/(64\times 10^{-6}) = 250\,\text{kHz}\), last-stage frequency \(15.625\,\text{kHz}\).
- **Limit.** The shortcut gives the relationship. The stem must still say which of the two frequencies it wants. A Johnson or ring counter does not divide by \(2^n\).

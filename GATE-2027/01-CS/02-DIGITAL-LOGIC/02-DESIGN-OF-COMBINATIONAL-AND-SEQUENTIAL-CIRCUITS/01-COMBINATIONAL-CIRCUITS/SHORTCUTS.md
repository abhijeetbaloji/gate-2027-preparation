# Combinational Circuits — Shortcuts

## 1. Mux tree size is one less than the number of data inputs

- **Solves.** How many 2-to-1 muxes build a \(2^n\)-to-1 mux.
- **When.** The only component allowed is a 2-to-1 mux.
- **Why.** The first rank has \(2^{n-1}\) muxes and \(2^{n-1}\) outputs, the next rank halves that, and the sum \(2^{n-1}+\cdots+1 = 2^n-1\).
- **Example.** 8-to-1 uses 7. 16-to-1 uses 15.
- **Limit.** A design that is allowed to use a 4-to-1 mux uses fewer packages. The shortcut is for a pure 2-to-1 tree.

## 2. Data pin from two rows

- **Solves.** What to tie to a mux data input.
- **When.** The selects are some of the variables, and the other variable is \(x\).
- **Why.** The two rows are the cofactor. Both 0 → tie 0. Both 1 → tie 1. \(01\) in order \((x=0, x=1)\) → tie \(x\). \(10\) → tie \(x'\).
- **Example.** Selects \(AB=01\), and \(F\) is 1 only on \(C=0\) in that pair: tie \(C'\).
- **Limit.** The row order must put \(x=0\) first. Reversing \(C\) reverses \(C\) and \(C'\).

## 3. Decoder count by enables

- **Solves.** How many small decoders build a wide one.
- **When.** The small decoder has an enable, and no extra gates are allowed.
- **Why.** Each output block corresponds to one combination of the high bits, so it needs its own enabled decoder. Something must decode those high bits into enables.
- **Example.** 6-to-64 from 3-to-8: 8 output blocks plus 1 enable decoder = 9.
- **Limit.** If extra gates are allowed, the enable decoder can be replaced by gates and the count of decoder ICs drops. The 2007 stem forbids other gates.

## 4. Priority is a downward scan

- **Solves.** The output index of a priority encoder.
- **When.** More than one input is 1.
- **Why.** By definition the highest index suppresses the lower ones. The binary output is that index, not the OR of the indexes and not the lowest index.
- **Example.** \(I_3 I_2 I_1 I_0 = 0110\) with \(I_3\) highest yields index 2, bits \(10\).
- **Limit.** If the stem says \(I_0\) is highest, scan the other way. “Priority” without a direction is incomplete; the usual GATE wording names the highest index.

## 5. Carry delay follows the carry, not the sum XOR

- **Solves.** Propagation delay of a ripple-carry adder’s final carry.
- **When.** Each full adder has a stated carry delay.
- **Why.** \(C_{i+1}\) depends on \(C_i\). The sum XOR of bit \(i\) does not sit on the path to \(C_n\) unless the stem’s gate diagram puts it there.
- **Example.** Carry delay 2 per bit, 4 bits: 8 gate delays from \(C_0\) to \(C_4\).
- **Limit.** A full adder built from two half adders has an internal path. Use the given XOR, AND, and OR delays on that path. Do not add the sum’s second XOR if the question asks only for carry-out.

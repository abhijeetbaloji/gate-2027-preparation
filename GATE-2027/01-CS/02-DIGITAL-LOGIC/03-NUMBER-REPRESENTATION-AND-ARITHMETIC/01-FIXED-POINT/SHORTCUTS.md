# Fixed Point — Shortcuts

## 1. MSB test, then a positive conversion

- **Solves.** Decimal value of a two’s-complement pattern.
- **When.** The width is given and the MSB is visible.
- **Why.** If the MSB is 0 the weights are all positive. If it is 1, flip-and-add-1 is the magnitude, because negation is an involution on every pattern except the most negative one, and on that one pattern the magnitude you would write is \(2^{n-1}\), which you then negate.
- **Example.** \(11000011\). Flip \(00111100\), add 1 gives \(00111101 = 61\). Value \(-61\).
- **Limit.** The shortcut assumes two’s complement. Sign-magnitude of the same bits is \(-67\), because the low bits are already the magnitude.

## 2. Same signs in, opposite sign out

- **Solves.** Signed overflow without drawing every carry.
- **When.** Both operands are two’s complement and you can see the three sign bits.
- **Why.** Opposite-sign addends cannot leave the representable interval. Same-sign addends overflow exactly when the sum bit cannot keep that sign.
- **Example.** \(0101+0100\) both start with 0, the sum starts with 1: overflow. \(1101+1101\) both start with 1, the sum \(1010\) starts with 1: no overflow.
- **Limit.** This does not detect unsigned overflow. \(0101+0100 = 1001\) overflows as signed and does not overflow as unsigned. Also, subtraction must be rewritten as addition of the negation before the test.

## 3. Sign extension is a copy, zero extension is a different number

- **Solves.** Widening a signed pattern.
- **When.** The stem says two’s complement and the new width is larger.
- **Why.** Copying the sign keeps every new weight consistent with the negative MSB weight. Inserting zeros changes the sign.
- **Example.** 5-bit \(10110 = -10\) becomes 8-bit \(11110110\), still \(-10\).
- **Limit.** Unsigned widening inserts zeros. Applying sign extension to an unsigned pattern above \(2^{n-1}-1\) changes the value.

## 4. Booth transitions

- **Solves.** How many additions and subtractions Booth performs.
- **When.** The multiplier bits are given. The multiplicand does not matter.
- **Why.** Only a change from the previous bit, including the initial 0, produces an add (\(01\)) or a subtract (\(10\)).
- **Example.** Multiplier \(0110\) with an appended low 0 has transitions at two positions: one subtract and one add.
- **Limit.** Do not count arithmetic shifts. Do not scan the multiplicand. A string of 1s is not “one operation per 1”; a whole run is one add and one subtract.

## 5. Point shift is a division by a power of two

- **Solves.** An unsigned fixed-point pattern with the point printed.
- **When.** There are \(f\) bits to the right of the point and no exponent.
- **Why.** Each step of the point across one bit divides the integer reading by 2.
- **Example.** Three fractional bits: divide the 8-bit integer by 8. \(00101100\) is \(44/8 = 5.5\).
- **Limit.** A signed fixed-point pattern needs the two’s-complement integer first, then the same division. Do not treat the MSB as \(2^{n-1}\) after the point has moved; the weight of the MSB is \(2^{n-1-f}\).

# Floating Point — Previous Year Questions

Question text stays in the mapping file. Stored answers are `VERIFICATION REQUIRED`. This page follows the `Paper` line. Decimal values of the paper’s hex words are not copied here, because the mapping does not record a verified key.

Mapping file: `../../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT/questions.md`

Papers: `../../../12-PYQ/`.

## Recognizable IEEE-754 stems

Every recent stem in this file is single precision: 1 sign bit, 8 exponent bits, 23 fraction bits.

| Paper | Question | Type | Pattern |
|-------|----------|------|---------|
| GATE 2026 CS-1 | Q.36 | MCQ | Two hex values \(X\) and \(Y\); a property of \(Z = X+Y\) |
| GATE 2026 CS-2 | Q.34 | NAT | One hex word to a decimal, rounded to two places |
| GATE 2025 CS-2 | Q.49 | MCQ | Three hex registers; which statement about them holds |
| GATE 2024 CS2 | Q.14 | MCQ | Which of several sign/exponent/fraction fields is the largest number |
| GATE 2023 CS | Q.45 | MCQ | Product of two hex values, as a hex result |
| GATE 2022 CS | Q.41 | MCQ | Three hex registers; a relation among the values |
| GATE 2021 CS Set-1 | Q.24 | NAT | Given sign, exponent, and fraction bits; a decimal of that word |
| GATE 2021 CS Set-2 | Q.4 | MCQ | Smallest positive normalised single-precision value |
| GATE 2020 CS | Q.29 | MCQ | Two hex registers and \(R3\) related to them; the resulting word or value |
| GATE 2017 CS Session 2 | Q.12 | MCQ | One binary single-precision word; closest decimal |
| GATE 2014 CS SET-2 | Q.45 | MCQ | A float variable in IEEE-754; what a shown bit pattern or assignment represents |
| GATE 2012 CS | Q.7 | MCQ | How \(0.5\) sits in IEEE single precision |
| GATE 2008 CS | Q.4 | MCQ | What hex `0x00000000` represents |

## Row that is not an encoding question

| Paper | Question | Why it is not this topic |
|-------|----------|--------------------------|
| GATE 2018 CS | Q.51 | Instruction format with integer and floating-point registers. The registers are named; no IEEE word is decoded |

## Gap

No row is stored for 2019, 2016, 2015, 2013, 2011, 2010, 2009, or 2007. Double precision is not a separate stored stem. Subnormals are not named in the short extracts above; the 2021 Set-2 stem is the smallest **normalised** positive number, which is the normal minimum \(2^{-126}\), not the subnormal minimum. The practice questions add the subnormal boundary because the special-case table is what those “smallest” and “largest” stems are testing around.

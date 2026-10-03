# CIDR Notation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Host addresses exclude the network address and the directed broadcast address. A prefix is aligned when its starting address is a multiple of the block size.

## Level 1 — Conceptual

## Q1 — MCQ

The prefix 172.16.5.0/26 has

A. 26 host bits
B. 6 host bits
C. 26 bytes of network number
D. a block of 26 addresses

---

## Q2 — MSQ

Select all that apply. Which statements about a prefix \(a.b.c.d/p\) are correct?

A. The first \(p\) bits identify the block, and the remaining \(32-p\) bits identify an address inside the block.
B. The block contains \(2^{32-p}\) addresses, including the network address and the broadcast address.
C. Two prefixes with a longer and a shorter length can both match one destination; the longer match is preferred.
D. The notation /p means the host field is p bits long.

---

## Q3 — MCQ

The network address of a block is the address in which

A. all host bits are 0
B. all host bits are 1
C. the first host bit is 1 and the rest are 0
D. every bit of the 32-bit address is 0

---

## Q4 — NAT

Enter the number of usable host addresses in a /26 prefix. Exclude the network address and the directed broadcast address.

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

One /24 prefix is split into equal /27 prefixes. The number of such /27 prefixes is

A. 8
B. 3
C. 2
D. 32

---

## Q6 — MCQ

The network address of 10.20.30.40/18 is

A. 10.20.0.0
B. 10.20.30.0
C. 10.20.64.0
D. 10.0.0.0

---

## Q7 — MSQ

Select all that apply. The block 192.168.4.0/22 covers which of these addresses?

A. 192.168.4.1
B. 192.168.5.10
C. 192.168.7.255
D. 192.168.8.1

---

## Q8 — NAT

The address 10.20.30.40 belongs to a /18 block. Enter the number of usable host addresses in that block.

---

## Q9 — MCQ

The four prefixes 172.20.8.0/24, 172.20.9.0/24, 172.20.10.0/24, and 172.20.11.0/24 can be aggregated as

A. 172.20.8.0/22
B. 172.20.8.0/23
C. 172.20.8.0/21
D. 172.20.10.0/22

---

## Level 3 — Multi-Step

## Q10 — MCQ

A router has these routes:

- 0.0.0.0/0 → eth0
- 198.51.100.0/24 → eth1
- 198.51.100.128/25 → eth2
- 198.51.100.160/28 → eth3

A packet to 198.51.100.170 is forwarded on

A. eth3
B. eth2
C. eth1
D. eth0

---

## Q11 — NAT

Enter the number of addresses in a /19 block, counting the network address and the broadcast address.

---

## Q12 — MSQ

Select all that apply. Four /24 prefixes can be aggregated into one /22 when

A. they are numerically contiguous
B. the combined block starts on a multiple of 4 in the relevant octet, so the /22 is aligned
C. there are exactly four of them, a power of two
D. they have different prefix lengths and need not be contiguous

---

## Q13 — MCQ

For 172.16.45.70/20, the network address and the directed broadcast address are

A. 172.16.32.0 and 172.16.47.255
B. 172.16.45.0 and 172.16.45.255
C. 172.16.48.0 and 172.16.63.255
D. 172.16.0.0 and 172.16.255.255

---

## Level 4 — Tricky / Trap-Based

## Q14 — NAT

Enter the number of usable host addresses in a /28 prefix.

---

## Q15 — MCQ

An administrator assigns interface addresses from a /26. The maximum number of interfaces that can be given an address in that block is

A. 62
B. 64
C. 63
D. 32

---

## Q16 — MSQ

Select all that apply. Inside 10.20.0.0/18, which statements are true?

A. 10.20.0.0 is the network address and is not assigned to a host.
B. 10.20.63.255 is the directed broadcast and is not assigned to a host.
C. 10.20.63.255 is the first usable host address.
D. The usable host range runs from 10.20.0.1 through 10.20.63.254.

---

## Level 5 — Challenge

## Q17 — MCQ

A packet is destined to 200.15.67.90. The routing table is

- 200.15.64.0/19 → I1
- 200.15.64.0/20 → I2
- 200.15.68.0/22 → I3
- 200.15.66.0/23 → I4

The packet is forwarded on

A. I4
B. I3
C. I2
D. I1

---

## Q18 — MSQ

Select all that apply. Which prefixes contain 172.16.45.70?

A. 172.16.0.0/16
B. 172.16.32.0/20
C. 172.16.48.0/20
D. 172.16.45.0/24

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MSQ | A, B, C |
| 3 | MCQ | A |
| 4 | NAT | 62 |
| 5 | MCQ | A |
| 6 | MCQ | A |
| 7 | MSQ | A, B, C |
| 8 | NAT | 16382 |
| 9 | MCQ | A |
| 10 | MCQ | A |
| 11 | NAT | 8192 |
| 12 | MSQ | A, B, C |
| 13 | MCQ | A |
| 14 | NAT | 14 |
| 15 | MCQ | A |
| 16 | MSQ | A, B, D |
| 17 | MCQ | A |
| 18 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: B

A /26 leaves \(32 - 26 = 6\) host bits. It does not have 26 host bits, it is not 26 bytes, and the block holds \(2^6 = 64\) addresses rather than 26.

### Q2

Answer: A, B, C

The prefix length is the network part. The block size is \(2^{32-p}\) addresses, and that count includes both reserved ends. Longest-prefix match is the forwarding rule when several routes match. D reverses the meaning of \(p\): \(p\) is the network length, not the host length.

### Q3

Answer: A

Host bits of all zeros name the network. Host bits of all ones name the directed broadcast. C is just one host address inside the block. D is only the address 0.0.0.0, not the network address of a general prefix.

### Q4

Answer: 62

\[
2^{32-26} - 2 = 64 - 2 = 62
\]

The trap is to stop at 64, which counts the network address and the broadcast address as hosts.

### Q5

Answer: A

\[
2^{27-24} = 2^3 = 8
\]

Each extra prefix bit doubles the number of subnets. The difference of the lengths is 3, not the subnet count itself, so B is wrong. One extra bit would make 2 subnets. 32 is the host-bit count of an unprefixed address, not the number of /27s in a /24.

### Q6

Answer: A

A /18 fixes the first 18 bits. In the third octet, only the top 2 bits are network bits, and the mask in that octet is 192. Then \(30 \mathbin{\&} 192 = 0\), so the network address is 10.20.0.0. B keeps the whole third octet. C would be the network if the third octet had fallen in the next /18, which starts at 64. D shortens the prefix to /8.

### Q7

Answer: A, B, C

A /22 fixes the first 22 bits. The third octet’s block size is \(2^{32-22} = 1024\) addresses, which is four values of the third octet. 192.168.4.0/22 runs from 192.168.4.0 through 192.168.7.255. Addresses .4.1, .5.10, and .7.255 are inside, including the broadcast .7.255. The next address, 192.168.8.1, starts the following /22 and is outside.

### Q8

Answer: 16382

Host bits: \(32 - 18 = 14\).

\[
2^{14} - 2 = 16384 - 2 = 16382
\]

The total address count is 16384. Subtracting only one reserved address gives 16383. Both of those count at least one address that is not assigned to a host.

### Q9

Answer: A

The third octets 8, 9, 10, and 11 are four contiguous /24s, and 8 is divisible by 4, so they form the aligned block 172.20.8.0/22. A /23 would cover only 8 and 9. A /21 would also swallow 12 through 15, which were not in the set. 172.20.10.0/22 is not aligned: a /22 cannot start at 10.

### Q10

Answer: A

198.51.100.170 matches all of these:

- /0, everything
- /24, 198.51.100.0 through .255
- /25, 198.51.100.128 through .255
- /28, 198.51.100.160 through .175, because 170 is between 160 and 175

The longest match is /28, which points at eth3. eth2 and eth1 also match but lose on prefix length. eth0 is only the default.

### Q11

Answer: 8192

\[
2^{32-19} = 2^{13} = 8192
\]

This question asks for every address in the block. The usable-host count would be \(8192 - 2 = 8190\). That subtraction is the trap when the question includes the network and broadcast addresses.

### Q12

Answer: A, B, C

Aggregation needs a contiguous, aligned, power-of-two collection of equal prefixes. Four /24s are one /22 only when they sit on a /22 boundary. D drops contiguity, equal length, and alignment, so it is not a valid aggregation rule.

### Q13

Answer: A

A /20 mask in the third octet is 240, and the block size in that octet is 16. Then \(45 \mathbin{\&} 240 = 32\), so the network is 172.16.32.0. The broadcast is the last address of that 16-octet span, 172.16.47.255. B is the enclosing /24. C is the next /20, which starts at 48. D is the enclosing /16.

### Q14

Answer: 14

\[
2^{32-28} - 2 = 16 - 2 = 14
\]

The block contains 16 addresses. Two of them are the network address and the broadcast address, so 14 remain for hosts. Answering 16 includes both reserved ends.

### Q15

Answer: A

\[
2^6 - 2 = 62
\]

B counts every address in the /26, including the two that cannot be assigned to interfaces. C drops only one of them. D uses 5 host bits, which would be a /27.

### Q16

Answer: A, B, D

10.20.0.0/18 runs from 10.20.0.0 through 10.20.63.255. The all-zero host part is the network address. The all-ones host part, 10.20.63.255, is the directed broadcast. Neither is a host address. The usable range is therefore 10.20.0.1 through 10.20.63.254. C calls the broadcast the first host, which reverses the ends of the block.

### Q17

Answer: A

Check each prefix against the third octet 67:

- 200.15.64.0/19 covers 64 through 95, so it matches. Length 19.
- 200.15.64.0/20 covers 64 through 79, so it matches. Length 20.
- 200.15.68.0/22 covers 68 through 71, so 67 does not match.
- 200.15.66.0/23 covers 66 and 67, so it matches. Length 23.

The longest matching prefix is /23, on I4. I3 is a tempting nearby block, but 67 is just before it. I2 and I1 match and are shorter.

### Q18

Answer: A, B, D

172.16.45.70 is inside 172.16.0.0/16. It is inside 172.16.32.0/20, which runs through 172.16.47.255. It is inside 172.16.45.0/24. It is not inside 172.16.48.0/20, which starts at 48, after this address. Containing is not the same as longest match: several of these prefixes contain the address at the same time.

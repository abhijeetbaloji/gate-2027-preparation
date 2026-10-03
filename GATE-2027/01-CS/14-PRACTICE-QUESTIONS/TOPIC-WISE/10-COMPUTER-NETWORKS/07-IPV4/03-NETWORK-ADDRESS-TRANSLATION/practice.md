# Network Address Translation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Network address translation lets hosts that use private addresses talk to the public Internet by

A. rewriting addresses as packets cross the NAT boundary
B. assigning every private host a distinct public address that never changes and is never shared
C. encrypting the IPv4 header so routers ignore the source address
D. replacing TCP with a new transport protocol

---

## Q2 — MSQ

Select all that apply. Which addresses lie in the private IPv4 ranges commonly used behind a NAT?

A. 10.8.8.8
B. 172.20.1.1
C. 192.169.1.1
D. 172.15.1.1

---

## Q3 — NAT

One public address may use source ports 1024 through 65535 inclusive for translated connections. Enter how many distinct source ports that is.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A private host opens a TCP connection to a public server. The NAT

A. creates a mapping when the outbound packet arrives, and later uses that mapping to forward the server’s replies
B. refuses the outbound packet until the server has first connected inward
C. publishes the private address in DNS and does not rewrite anything
D. rewrites only the payload and leaves the IP header unchanged

---

## Q5 — MCQ

A packet arrives from the Internet addressed to the NAT’s public address and to a port that has no mapping. The NAT

A. forwards it to every private host
B. drops it, because there is no translation to apply
C. answers it using the private address 10.0.0.1
D. creates a mapping to a randomly chosen private host

---

## Q6 — MSQ

Select all that apply. Port-address translation of an outbound TCP segment typically rewrites

A. the source IPv4 address, from private to public
B. the source port, when several private hosts must share one public address
C. the destination IPv4 address of the public server, replacing it with the NAT’s address
D. the checksums that cover the fields it changed

---

## Level 3 — Multi-Step

## Q7 — MCQ

Several private hosts share one public IPv4 address at the same time. This is possible because

A. each host’s connections are distinguished by the translated port numbers
B. IPv4 addresses are 128 bits, so one address contains many hosts
C. the server uses the private addresses, which remain visible end to end
D. NAT forbids more than one private host from sending in the same second

---

## Q8 — NAT

A NAT table contains the mapping 10.0.0.7:4000 ↔ 203.0.113.5:52000. A packet arrives from the Internet addressed to 203.0.113.5 on port 52000. Enter the private port to which the NAT delivers it.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Which address is not a private IPv4 address?

A. 10.1.2.3
B. 172.31.5.5
C. 192.168.50.2
D. 172.32.1.5

---

## Q10 — MSQ

Select all that apply. Which statements about NAT are true?

A. Rewriting the source address means the public server does not see the private source address.
B. A protocol that writes the host’s own IP address inside the payload can break unless the NAT also rewrites that payload.
C. An unsolicited inbound connection to a private host succeeds with no mapping and no port forward.
D. The private ranges include 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16.

---

## Level 5 — Challenge

## Q11 — NAT

A NAT table has two rows:

- 10.1.1.5:3340 ↔ 198.51.100.20:40001
- 10.1.1.9:3340 ↔ 198.51.100.20:40002

Both private hosts used source port 3340. A reply arrives at 198.51.100.20 on port 40002. Enter the last octet of the private host that receives it.

---

## Q12 — MCQ

Static one-to-one NAT and port-address translation differ because

A. static one-to-one NAT uses a distinct public address per private host, while port-address translation shares one public address by using ports
B. port-address translation never rewrites the source address
C. static NAT allows many hosts to share one public address in the same way ports do
D. only static NAT can carry TCP, and port-address translation is limited to UDP

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B |
| 3 | NAT | 64512 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 4000 |
| 9 | MCQ | D |
| 10 | MSQ | A, B, D |
| 11 | NAT | 9 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

The NAT rewrites the private source address (and usually the source port) to a public address as the packet leaves, and it reverses that rewrite on the way back. B describes a public address per host, which is what NAT is used to avoid. C and D are not what NAT does.

### Q2

Answer: A, B

10.8.8.8 is inside 10.0.0.0/8. 172.20.1.1 is inside 172.16.0.0/12, which runs from 172.16.0.0 through 172.31.255.255. 192.169.1.1 is outside 192.168.0.0/16. 172.15.1.1 is just before the 172.16.0.0/12 block. The traps are the near misses 192.169 and 172.15.

### Q3

Answer: 64512

Inclusive count:

\[
65535 - 1024 + 1 = 64512
\]

Subtracting without the +1 gives 64511 and drops port 65535 or port 1024. Ports below 1024 are outside the range this question allows.

### Q4

Answer: A

The first outbound packet installs the mapping that return traffic must match. The server does not open the mapping by connecting inward first. The private address is not left visible as the source, and the rewrite is in the headers, not only in an untouched payload.

### Q5

Answer: B

With no table row, the NAT does not know which private host should receive the packet, so it drops it. It does not broadcast the packet to every host, invent a private source, or attach the packet to a random host.

### Q6

Answer: A, B, D

The source address becomes the public address, and the source port is changed when that is how several hosts share the address. Checksums that include those fields have to be updated. The destination is still the public server; replacing it with the NAT’s own address would send the packet to the NAT instead of to the server, so C is the wrong direction.

### Q7

Answer: A

The public side sees one address and many ports. The mapping from each public port leads back to a different private host and port. IPv4 addresses are 32 bits, not 128. The server does not see the private addresses. Hosts are not serialised one per second.

### Q8

Answer: 4000

The inbound packet matches the public side 203.0.113.5:52000. The table sends it to 10.0.0.7 port 4000. Delivering it to port 52000 would leave the translated port in place. The private port is the number stored on the inside of the mapping.

### Q9

Answer: D

10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 are the private blocks. 172.31.5.5 is the last /8 inside 172.16.0.0/12, so it is private. 172.32.1.5 is the next address block and is not private. The trap is to treat every 172 address as private.

### Q10

Answer: A, B, D

The rewritten source is what the server answers, so the private address stays on the private side. A payload that repeats the private address still shows the old address unless an application-level rewrite fixes it. An inbound packet with no mapping is dropped, so C is false. The three ranges in D are the standard private blocks.

### Q11

Answer: 9

Both hosts picked private port 3340, so the private port alone does not identify the host. The public ports do: 40002 maps to 10.1.1.9, whose last octet is 9. Choosing 5 uses the other row. Choosing 3340 reports a port instead of the octet the question asks for.

### Q12

Answer: A

Static one-to-one NAT binds one public address to one private host and does not need a port to tell hosts apart. Port-address translation multiplexes one public address by source port. B is false because the source address is rewritten in both designs. C gives static NAT the sharing behaviour it does not have. D invents a transport restriction; both forms can carry TCP.

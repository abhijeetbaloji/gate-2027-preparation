# GATE PYQs

## 2025

### Q.51

**Paper:** GATE 2025 CS-1

**Question:**

A disk of size 512M bytes is divided into blocks of 64K bytes. A file is stored in
the disk using linked allocation. In linked allocation, each data block reserves 4
bytes to store the pointer to the next data block. The link part of the last data block
contains a NULL pointer (also of 4 bytes). Suppose a file of 1M bytes needs to be
stored in the disk. Assume, 1K = 2^{10} and 1M = 2^{20}. The amount of space in bytes
that will be wasted due to internal fragmentation is ______. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.57

**Paper:** GATE 2025 CS-1

**Question:**

Suppose a message of size 15000 bytes is transmitted from a source to a destination
using IPv4 protocol via two routers as shown in the figure. Each router has a defined
maximum transmission unit (MTU) as shown in the figure, including IP header.
The number of fragments that will be delivered to the destination is ________ .
(Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.23

**Paper:** GATE 2025 CS-2

**Question:**

Consider a network that uses Ethernet and IPv4. Assume that IPv4 headers do not
use any options field. Each Ethernet frame can carry a maximum of 1500 bytes in
its data field. A UDP segment is transmitted. The payload (data) in the UDP
segment is 7488 bytes.
Which ONE of the following choices has the CORRECT total number of fragments
transmitted and the size of the last fragment including IPv4 header?

**Options:**

A. 5 fragments, 1488 bytes
B. 6 fragments, 88 bytes
C. 6 fragments, 108 bytes
D. 6 fragments, 116 bytes

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.36

**Paper:** GATE 2024 CS1

**Question:**

Consider a network path P—Q—R between nodes P and R via router Q. Node P
sends a file of size 10^{6} bytes to R via this path by splitting the file into chunks of
10^{3} bytes each. Node P sends these chunks one after the other without any wait time
between the successive chunk transmissions. Assume that the size of extra headers
added to these chunks is negligible, and that the chunk size is less than the MTU.
Each of the links P—Q and Q—R has a bandwidth of 10^{6}bits/sec, and negligible
propagation latency. Router Q immediately transmits every packet it receives from
P to R, with negligible processing and queueing delays. Router Q can
simultaneously receive on link P—Q and transmit on link Q—R.
Assume P starts transmitting the chunks at time 𝑡= 0.
Which one of the following options gives the time (in seconds,  rounded off to 3
decimal places) at which R receives all the chunks of the file?

**Options:**

A. 8.000
B. 8.008
C. 15.992
D. 16.000

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2024 CS1

**Question:**

Consider sending an IP datagram of size 1420 bytes (including 20 bytes of IP
header) from a sender to a receiver over a path of two links with a router between
them. The first link (sender to router) has an MTU (Maximum Transmission Unit)
size of 542 bytes, while the second link (router to receiver) has an MTU size of 360
bytes. The number of fragments that would be delivered at the receiver is ________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2024 CS2

**Question:**

Which of the following statements about IPv4 fragmentation is/are TRUE?
The fragmentation of an IP datagram is performed only at the source of the

**Options:**

A. datagram The fragmentation of an IP datagram is performed at any IP router which finds
B. that the size of the datagram to be transmitted exceeds the MTU
C. The reassembly of fragments is performed only at the destination of the datagram The reassembly of fragments is performed at all intermediate routers along the
D. path from the source to the destination

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2021

### Q.45

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider two hosts P and Q connected through a router R. The maximum transfer
unit (MTU) value of the link between P and R is 1500 bytes, and between R and
Q is 820 bytes.
A TCP segment of size 1400 bytes was transferred from P to Q through R, with IP
identification value as 0x1234. Assume that the IP header size is 20 bytes. Further,
the packet is allowed to be fragmented, i.e., Don't Fragment (DF) flag in the IP
header is not set by P.
Which of the following statements is/are correct?

**Options:**

A. Two fragments are created at R and the IP datagram size carrying the second fragment is 620 bytes.
B. If the second fragment is lost, R will resend the fragment with the IP identification value 0x1234.
C. If the second fragment is lost, P is required to resend the whole TCP segment.
D. TCP destination port can be determined by analysing only the second fragment. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2018

### Q.54

**Paper:** GATE 2018 CS

**Question:**

Consider an IP packet with a length of 4,500 bytes that includes a 20-byte IPv4 header and
a 40-byte TCP header. The packet is forwarded to an IPv4 router that supports a Maximum
Transmission Unit (MTU) of 600 bytes. Assume that the length of the IP header in all the
outgoing fragments of this packet is 20 bytes. Assume that the fragmentation offset value
stored in the first fragment is 0.
The fragmentation offset value stored in the third fragment is _______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.8

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 1 Wrong: -0.33
In a file allocation system, which of the following allocation scheme(s) can be used if no external
fragmentation is allowed?
I. Contiguous
II. Linked
III. Indexed

**Options:**

A. Iand III only
B. II only
C. III only
D. II and III only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.53

**Paper:** GATE 2016 CS-1

**Question:**

An IP datagram of size 1000 bytes arrives at a router. The router has to forward this packet on
a link whose MTU (maximum transmission unit) is 100 bytes. Assume that the size of the IP
header is 20 bytes.
The number of fragments that the IP datagram will be divided into for transmission is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2015

### Q.37

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Host A sends a UDP datagram containing 8880 bytes of user data to host B over an Ethernet LAN.
Ethernet frames may carry data up to 1500 bytes (1.e. MTU=1500 bytes). Size of UDP header is 8
bytes and size of IP header is 20 bytes. There is no option field in IP header. How many total
number of IP fragments will be transmitted and what will be the contents of offset field in the last
fragment?

**Options:**

A. 6 and 925
B. 6 and 7400
C. 7 and 1110
D. 7 and 8880

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

## 2014

### Q.25

**Paper:** GATE 2014 CS SET-3

**Question:**

Host A (on TCP/IP v4 network A) sends an IP datagram D to host B (also on TCP/IP v4 network
B). Assume that no error occurred during the transmission of D. When D reaches B, which of the
following IP header field(s) may be different from that of the original datagram D?
(i) TTL  (ii) Checksum  (iii) Fragment Offset

**Options:**

A. (i) only
B. (i) and (ii) only
C. (ii) and (iii) only
D. (i), (ii) and (iii)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2014 CS SET-3

**Question:**

An IP router with a Maximum Transmission Unit (MTU) of 1500 bytes has received an IP packet
of size 4404 bytes with an IP header of length 20 bytes. The values of the  relevant fields in the
CS03 (GATE 2014)header of the third IP fragment  generated by the router for this packet are

**Options:**

A. MF bit: 0, Datagram Length: 1444; Offset: 370
B. MF bit: 1, Datagram Length: 1424; Offset: 185
C. MF bit: 1, Datagram Length: 1500; Offset: 370
D. MF bit: 0, Datagram Length: 1424; Offset: 2960

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-3, `12-PYQ/2014/set-03/question-paper.pdf`

---

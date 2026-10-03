# GATE PYQs

## 2026

### Q.45

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the implementation of sliding window protocol over a lossless link, with a
window size of 𝑊 frames, where each frame is of size 1000 bits (including header).
The bandwidth of the link is 100 kbps (1k = 10^{3}) and the one-way propagation delay
is 100 milliseconds. Assume that processing times at the sender and receiver are zero
and the transmission time of acknowledgements is also zero. Which one of the
following options gives the minimum size of 𝑊 (in number of frames) required to
achieve 100% link utilization?

**Options:**

A. 10
B. 21
C. 20
D. 11

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.65

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

It is necessary to design a link-layer protocol between two hosts that are directly
connected over a lossless link of length 3000 kilometers. Assume that the link
bandwidth is  10^{8} bits per second and that the propagation delay in the link is 5
nanoseconds per meter. Every transmitted data byte is assigned a unique sequence
number.
Let 𝑁 be the minimum number of bits needed for the sequence number field in the
protocol header such that
i.  the sequence numbers do not wrap around before 60 seconds, and
ii.  the maximum utilization of the link is achieved.
The value of 𝑁 is ______. (answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.16

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following statements:
(i)  Address Resolution Protocol (ARP) provides a mapping from an IP
address to the corresponding hardware (link-layer) address.
(ii)  A single TCP segment from a sender S to a receiver R cannot carry both
data from S to R and acknowledgement for a segment from R to S.
Which ONE of the following is CORRECT?

**Options:**

A. Both (i) and (ii) are TRUE
B. (i) is TRUE and (ii) is FALSE
C. (i) is FALSE and (ii) is TRUE
D. Both (i) and (ii) are FALSE

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2025 CS-2

**Question:**

Suppose we are transmitting frames between two nodes using Stop-and-Wait
protocol. The frame size is 3000 bits. The transmission rate of the channel is 2000
bps (bits/second) and the propagation delay between the two nodes is 100
milliseconds. Assume that the processing times at the source and destination are
negligible. Also, assume that the size of the acknowledgement packet is negligible.
Which ONE of the following most accurately gives the channel utilization for the
above scenario in percentage?

**Options:**

A. 88.23
B. 93.75
C. 85.44
D. 66.67

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.29

**Paper:** GATE 2024 CS1

**Question:**

TCP client P successfully establishes a connection to TCP server Q. Let 𝑁_{𝑃} denote
the sequence number in the SYN sent from P to Q. Let  𝑁_{𝑄} denote the
acknowledgement number in the SYN ACK from Q to P. Which of the following
statements is/are CORRECT?

**Options:**

A. The sequence number 𝑁_{𝑃} is chosen randomly by P
B. The sequence number 𝑁_{𝑃} is always 0 for a new connection
C. The acknowledgement number 𝑁_{𝑄} is equal to 𝑁_{𝑃}
D. The acknowledgement number 𝑁_{𝑄} is equal to 𝑁_{𝑃} + 1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

## 2023

### Q.50

**Paper:** GATE 2023 CS

**Question:**

Suppose you are asked to design a new reliable byte-stream transport protocol
like TCP. This protocol, named myTCP, runs over a 100 Mbps network with Round
Trip Time of 150 milliseconds and the maximum segment lifetime of 2 minutes.
Which of the following is/are valid lengths of the Sequence Number field in the
myTCP header?

**Options:**

A. 30 bits
B. 32 bits
C. 34 bits
D. 36 bits

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.60

**Paper:** GATE 2022 CS

**Question:**

Consider the data transfer using TCP over a 1 Gbps link. Assuming that the
maximum segment lifetime (MSL) is set to 60 seconds, the minimum number of
bits required for the sequence number field of the TCP header, to prevent the
sequence number space from wrapping around during the MSL  is____________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.49

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the sliding window flow-control protocol operating between a sender and
a receiver over a full-duplex error-free link. Assume the following: |
• The time taken for processing the data frame by the receiver is negligible.
• The time taken for processing the acknowledgement frame by the sender is neg-
ligible.
• The sender has infinite number of frames available for transmission.|
• The size of the data frame is 2,000 bits and the size of the acknowledgement
frame is 10 bits.
• The link data rate in each direction is 1 Mbps (= 106 bits per second).
• One way propagation delay of the link is 100 milliseconds. |
The minimum value of the sender's window size in terms of the number of frames,
(rounded to the nearest integer) needed to achieve a link utilization of 50% is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2018

### Q.13

**Paper:** GATE 2018 CS

**Question:**

Match the following:
Field  Length in bits
P.  UDP Header’s Port Number  I.  48
Q.  Ethernet MAC Address  II.  8
R.  IPv6 Next Header  III. 32
S.  TCP Header’s Sequence Number  IV. 16

**Options:**

A. P-III, Q-IV, R-II, S-I
B. P-II, Q-I, R-IV, S-III
C. P-IV, Q-I, R-II, S-III
D. P-IV, Q-I, R-III, S-II

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2018 CS

**Question:**

Consider a long-lived TCP session with an end-to-end bandwidth of 1 Gbps (= 10^{9} bits-per-
second). The session starts with a sequence number of 1234. The minimum time (in seconds,
rounded to the closest integer) before this sequence number can be used again is _______.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2016

### Q.55

**Paper:** GATE 2016 CS-1

**Question:**

A sender uses the Stop-and-Wait ARQ protocol for reliable transmission of frames. Frames
are of size 1000 bytes and the transmission rate at the sender is 80 Kbps (1Kbps = 1000
bits/second). Size of an acknowledgement is 100 bytes and the transmission rate at the receiver
is 8 Kbps. The one-way propagation delay is 100 milliseconds.
Assuming no frame is lost, the sender throughput is  bytes/second.
CS(Set A)  17/17

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2016 CS-2

**Question:**

Consider a 128×10^{3} bits/second satellite communication link with one way propagation delay
of 150 milliseconds. Selective retransmission (repeat) protocol is used on this link to send
data with a frame size of 1 kilobyte. Neglect the transmission time of acknowledgement. The
minimum number of bits required for the sequence number field to achieve 100% utilization
is  .
CS(Set B)  18/18

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.23

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Suppose two hosts use a TCP connection to transfer a large file. Which of the following statements
1s/are FALSE with respect to the TCP connection?
I. If the sequence number of a segment is m, then the sequence number of the subsequent
segment is always m+1.
II. If the estimated round trip time at any given point of time is t sec, the value of the
retransmission timeout is always set to greater than or equal to t sec.
II. The size of the advertised window never changes during the course of the TCP connection.
IV. The number of unacknowledged bytes at the sender is always less than or equal to the
advertised window.
(А) III only (B) I and III only (C) Iand IV only (D) II and TV only

**Options:**

The options could not be read from the local paper. The PDF listed in Source is the authoritative copy.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Suppose that the stop-and-wait protocol is used on a link with a bit rate of 64 kilobits per second
and 20 milliseconds propagation delay. Assume that the transmission time for the
acknowledgement and the processing time at nodes are negligible. Then the minimum frame size in
bytes to achieve a link utilization of at least 50% is_
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

A link has a transmission speed of 10° bits/sec. It uses data packets of size 1000 bytes each.
Assume that the acknowledgment has negligible transmission delay, and that its propagation delay
is the same as the data propagation delay. Also assume that the processing delays at nodes are
negligible. The efficiency of the stop-and-wait protocol in this setup is exactly 25%. The value of
the one-way propagation delay (in milliseconds) 1s_
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following statements.
I. TCP connections are full duplex
II. TCP has no option for selective acknowledgement
IIl. TCP connections are message streams

**Options:**

A. Only I 1s correct
B. Only I and II are correct
C. Only II and III are correct
D. All of I, II and III are correct

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

158

network is 500x10° bits per second. The propagation speed of the media is 4x10° meters per Consıder a network connecting two systems located 8000 kılometers apart. The bandwidth of the
second. It is needed to design a Go-Back-N sliding window protocol for this network. The average
packet size is 10' bits. The network is to be used to its full capacity. Assume that processing delays
at nodes are negligible. Then, the minimum size in bits of the sequence number field has to be
Correct Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.28

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider a selective repeat sliding window protocol that uses a frame size of 1 KB to send data on a
1.5 Mbps link with a one-way latency of 50 msec. To achieve a link utilization of 60%, the
minimum number of bits required to represent the sequence number field is ________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

## 2013

### Q.37

**Paper:** GATE 2013 CS Booklet A

**Question:**

In an IPv4 datagram, the M bit is 0, the value of HLEN is 10, the value of total length is 400 and
the fragment offset value is 300. The position of the datagram, the sequence numbers of the first
and the last bytes of the payload, respectively are

**Options:**

A. Last fragment, 2400 and 2789
B. First fragment, 2400 and 2759
C. Last fragment, 2400 and 2759
D. Middle fragment, 300 and 689

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2013 CS Booklet B

**Question:**

In an IPv4 datagram, the M bit is 0, the value of HLEN is 10, the value of total length is 400 and
the fragment offset value is 300. The position of the datagram, the sequence numbers of the first
and the last bytes of the payload, respectively are

**Options:**

A. Last fragment, 2400 and 2789
B. First fragment, 2400 and 2759
C. Last fragment, 2400 and 2759
D. Middle fragment, 300 and 689

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.46

**Paper:** GATE 2013 CS Booklet C

**Question:**

In an IPv4 datagram, the M bit is 0, the value of HLEN is 10, the value of total length is 400 and
the fragment offset value is 300. The position of the datagram, the sequence numbers of the first
and the last bytes of the payload, respectively are

**Options:**

A. Last fragment, 2400 and 2789
B. First fragment, 2400 and 2759
C. Last fragment, 2400 and 2759
D. Middle fragment, 300 and 689

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.26

**Paper:** GATE 2013 CS Booklet D

**Question:**

In an IPv4 datagram, the M bit is 0, the value of HLEN is 10, the value of total length is 400 and
the fragment offset value is 300. The position of the datagram, the sequence numbers of the first
and the last bytes of the payload, respectively are

**Options:**

A. Last fragment, 2400 and 2789
B. First fragment, 2400 and 2759
C. Last fragment, 2400 and 2759
D. Middle fragment, 300 and 689

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2009

### Q.57

**Paper:** GATE 2009 CS

**Question:**

What is the minimum number of bits (I) that will be required to represent the sequence numbers
distinctly ? Assume that no time gap needs to be given between transmission of two frames.

**Options:**

A. / = 2
B. [= 3
C. |= 4
D. l = 5

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2007

### Q.69

**Paper:** GATE 2007 CS

**Question:**

The distance between two stations M and N is L kilometres. All frames are K bits
long. The propagation delay per kilometre is t seconds. Let R bits/second be the
channel capacity. Assuming that processing delay is negligible, the minimum
number of bits for the sequence number field in a frame for maximum utilization,
when the sliding window protocol is used, is:

**Options:**

A. | 2LIR+2K K 2LtR K
C. logz 2LtR + K
D. 10g2 2LtR+K 2K

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

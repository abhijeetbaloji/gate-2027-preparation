# GATE PYQs

## 2026

### Q.44

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

A TCP sender successfully establishes a connection with a TCP receiver and starts
the transmission of segments. The TCP congestion control mechanism’s slow-start
threshold is set to 10000 segments. Assume that the round-trip time is fixed at
1 millisecond. Assume that the sender always has data to send, the segments are
numbered from 1, and no segment is lost. Let 𝑡 denote the time (in milliseconds) at
which the transmission of segment number 2000 starts.
Which one of the following options is correct?

**Options:**

A. 9 ≤ 𝑡 < 10
B. 10 ≤ 𝑡 < 11
C. 11 ≤ 𝑡 < 12
D. 12 ≤ 𝑡 < 13

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider a new TCP connection between a sender and a receiver. The receiver
advertised window is constant at 48 KB, the maximum segment size (MSS) is
2 KB, and the slow start threshold for TCP congestion control is 16 KB. Assume
that there are no timeouts or duplicate acknowledgements. The number of rounds
of transmission required for the congestion control algorithm of the TCP connection
to reach the congestion avoidance phase is ___________. (answer in integer)
Note: 1K=2^{10}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2024

### Q.54

**Paper:** GATE 2024 CS2

**Question:**

Consider a TCP connection operating at a point of time with the congestion window
of size 12 MSS (Maximum Segment Size), when a timeout occurs due to packet
loss. Assuming that all the segments transmitted in the next two RTTs (Round Trip
Time) are acknowledged correctly, the congestion window size (in MSS) during the
third RTT will be _________

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2020

### Q.55

**Paper:** GATE 2020 CS

**Question:**

Consider a TCP connection between a client and a server with the following
specifications: the round trip time is 6 ms, the size of the receiver advertised
window is 50 KB, slow-start threshold at the client is 32 KB, and the maximum
segment size is 2 KB. The connection is established at time t = 0. Assume that
there are no timeouts and errors during transmission. Then the size of the
congestion window (in KB) at time t + 60 ms after all acknowledgements are
processed is
Copyright : GATE 2020, IIT Delhi

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2018

### Q.14

**Paper:** GATE 2018 CS

**Question:**

Consider the following statements regarding the slow start phase of the TCP congestion
control algorithm.  Note that cwnd stands for the TCP congestion window and MSS denotes
the Maximum Segment Size.
(i)  The cwnd increases by 2 MSS on every successful acknowledgment.
(ii)  The cwnd approximately doubles on every successful acknowledgement.
(iii) The cwnd increases by 1 MSS every round trip time.
(iv) The cwnd approximately doubles every round trip time.
Which one of the following is correct?

**Options:**

A. Only (ii) and (iii) are true
B. Only (i) and (iii) are true
C. Only (iv) is true
D. Only (i) and (iv) are true

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2014

### Q.27

**Paper:** GATE 2014 CS SET-1

**Question:**

Let the size of congestion window of a TCP connection be 32 KB when a timeout occurs. The round
trip time of the connection is 100 msec and the maximum segment size used is 2 KB. The time taken
(in msec) by the TCP connection to get back to 32 KB congestion window is _________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

## 2012

### Q.45

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider an instance of TCP’s Additive Increase Multiplicative Decrease (AIMD) algorithm where
the window size at the start of the slow start phase is 2 MSS and the threshold at the start of the first
transmission is 8 MSS. Assume that a timeout occurs during the fifth transmission. Find the
congestion window size at the end of the tenth transmission.

**Options:**

A. 8 MSS
B. 14 MSS
C. 7 MSS
D. 12 MSS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2008

### Q.56

**Paper:** GATE 2008 CS

**Question:**

In the slow start phase of the TCP congestion control algorithm, the size of the congestion window

**Options:**

A. does not increase
B. increases linearly
C. increases quadratically
D. increases exponentially

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

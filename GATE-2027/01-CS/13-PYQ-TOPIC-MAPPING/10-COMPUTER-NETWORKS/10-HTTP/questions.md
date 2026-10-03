# GATE PYQs

## 2026

### Q.19

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Which of the following statements is/are true with respect to the interaction of a
web browser with a web server using HTTP 1.1?

**Options:**

A. HTTP 1.1 facilitates downloading multiple objects of the same webpage over the same TCP connection, if the objects are stored in the same server
B. HTTP 1.1 facilitates downloading multiple objects of the same webpage over the same TCP connection, even if they are stored in different servers
C. HTTP 1.1 facilitates sending a request for downloading one object without waiting for a previously requested object to be downloaded completely
D. HTTP 1.1 facilitates downloading multiple webpages on the same server to be downloaded over a single TCP connection

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.22

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Which one of the following protocols may need to broadcast some of its messages?

**Options:**

A. SMTP
B. FTP
C. DHCP
D. HTTP

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2016

### Q.25

**Paper:** GATE 2016 CS-1

**Question:**

Which of the following is/are example(s) of stateful application layer protocols?
(i) HTTP
(ii) FTP
(iii) TCP
(iv) POP3

**Options:**

A. (i) and (ii) only
B. (ii) and (iii) only
C. (ii) and (iv) only
D. (iv) only CS(Set A) 8/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.25

**Paper:** GATE 2016 CS-2

**Question:**

Identify the correct sequence in which the following packets are transmitted on the network
by a host when a browser requests a webpage from a remote server, assuming that the host has
just been restarted.

**Options:**

A. HTTP GET request, DNS query, TCP SYN
B. DNS query, HTTP GET request, TCP SYN
C. DNS query, TCP SYN, HTTP GET request
D. TCP SYN, DNS query, HTTP GET request

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.27

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

In one of the pairs of protocols given below, both the protocols can use multiple TCP connections
between the same client and the server. Which one is that?
(А) НТТР, FТP (B) HTTP, TELNET (C) FTP, SMTP (D) HTTP, SMTP

**Options:**

The options could not be read from the local paper. The PDF listed in Source is the authoritative copy.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

12

Which one of the following statements is NOT correct about HTTP cookies?

**Options:**

A. A cookie is a piece of code that has the potential to compromise the security of an Internet user
B. A cookie gains entry to the user's work area through an HTTP header
C. A cookie has an expiry date and time
D. Cookies can be used to track the browsing pattern of a user at a particular site

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

In a web server, ten WebPages are stored with the URLs of the form
http://www.yourname.com/var.html; where, var is a different number from 1 to 10 for each
Webpage. Suppose, the client stores the Webpage with var = 1 (say W1) in local machine, edits
and then tests. Rest of the WebPages remains on the web server. W1 contains several relative URLs
of the form "var.html" referring to the other WebPages. Which one of the following statements
needs to be added in W1, so that all the relative URLs in W1 refer to the appropriate WebPages on
the web server?

**Options:**

A. <a href: "http://www.yourname.com/", href "..var.html">
B. <base href: «http://www.yourname.com/">
C. <a href: "http://www.yourname.com/">
D. < base href: "http://www.yourname.com/", range:".var.html"> 4 * D

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.25

**Paper:** GATE 2014 CS SET-1

**Question:**

Identify the correct order in which the following actions take place in an interaction between a web
browser and a web server.
1.  The web browser requests a webpage using HTTP.
2.  The web browser establishes a TCP connection with the web server.
3.  The web server sends the requested webpage using HTTP.
4.  The web browser resolves the domain name using DNS.

**Options:**

A. 4,2,1,3
B. 1,2,3,4
C. 4,1,2,3
D. 2,4,1,3

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2014 CS SET-2

**Question:**

An IP machine Q has a path to another IP machine H via three IP routers R1, R2, and R3.
Q—R1—R2—R3—H
H acts as an HTTP server, and Q connects to H via HTTP and downloads a file.  Session layer
encryption is used, with DES as the shared key encryption protocol.  Consider the following four
pieces of information:
[I1] The URL of the file downloaded by Q
[I2] The TCP port numbers at Q and H
[I3] The IP addresses of Q and H
[I4] The link layer addresses of Q and H
Which of I1, I2, I3, and I4 can an intruder learn through sniffing at R2 alone?

**Options:**

A. Only I1 and I2
B. Only I1
C. Only I2 and I3
D. Only I3 and I4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.28

**Paper:** GATE 2014 CS SET-2

**Question:**

A graphical HTML browser resident at a network client machine  Q accesses a static HTML
webpage from a HTTP server S.  The static HTML page has exactly one static embedded image
which is also at S.  Assuming no caching, which one of the following is correct about the HTML
webpage loading (including the embedded image)?

**Options:**

A. Q needs to send at least 2 HTTP requests to S, each necessarily in a separate TCP connection to server S
B. Q needs to send at least 2 HTTP requests to S, but a single TCP connection to server S is CS02 (GATE 2014)sufficient
C. A single HTTP request from Q to S is sufficient, and a single TCP connection between Q and S is necessary for this
D. A single HTTP request from Q to S is sufficient, and this is possible without any TCP connection between Q and S

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2011

### Q.2

**Paper:** GATE 2011 CS Booklet A

**Question:**

A layer-4 firewall (a device that can look at all protocol headers up to the transport layer) CANNOT

**Options:**

A. block entire HTTP traffic during 9:00PM and 5:00AM
B. block all ICMP traffic
C. stop incoming traffic from a specific IP address but allow outgoing traffic to the same IP address
D. block TCP traffic from a specific user on a multi-user system during 9:00PM and 5:00AM

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

### Q.4

**Paper:** GATE 2011 CS Booklet A

**Question:**

Consider different activities related to email.
ml: Send an email from a mail client to a mail server
m2: Download an email from mailbox server to a mail client
m3: Checking email in a web browser
Which is the application level protocol used in each activity?

**Options:**

A. ml: HTTP m2: SMTP m3: POP
B. ml: SMTP m2: FTP m3: HTTP
C. ml: SMTP m2: POP m3: HTTP
D. ml: POP m2: SMTP m3: IMAP

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

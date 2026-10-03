# HTTP — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Round-trip counting in this set uses one convention. The TCP handshake counts as 1 RTT. Each HTTP request and its response count as 1 further RTT. A non-persistent transfer uses a new TCP connection for every object, so one object costs 2 RTTs. On a persistent connection the handshake is paid once. Without pipelining, each object then costs one more RTT, and the next request waits for the previous response. With pipelining, several already-known requests can share one RTT.

## Level 1 — Conceptual

## Q1 — MCQ

Which HTTP method retrieves a representation of a resource without saying that it will change the resource?

A. GET
B. POST
C. A method that always deletes the resource
D. A method that exists only to open a TCP connection

---

## Q2 — MSQ

Select all that apply. Which status codes match the meanings?

A. 200 means the request succeeded.
B. 404 means the server did not find the target resource.
C. 301 means the resource has moved permanently.
D. 500 means the DNS name has no A record.

---

## Q3 — NAT

A browser fetches one HTML page and then two images. It uses non-persistent HTTP, opens no parallel connections, and learns the image URLs from the HTML. Using the RTT convention above, enter the number of RTTs.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A persistent HTTP connection

A. carries more than one object on the same TCP connection
B. opens a new TCP connection for every object and closes it immediately
C. removes the need for a request line
D. replaces status codes with Ethernet addresses

---

## Q5 — MCQ

An HTTP cookie is used so that

A. a server can recognise a client across otherwise stateless requests
B. the TCP handshake can be omitted on every new connection
C. IP fragmentation is disabled
D. the DNS hierarchy is flattened into one server

---

## Q6 — MSQ

Select all that apply. Which statements about persistent and non-persistent HTTP are correct under the convention in the introduction?

A. Non-persistent HTTP pays a handshake for every object.
B. Persistent HTTP pays the handshake once for the objects sent on that connection.
C. Non-persistent HTTP cannot carry a GET request.
D. Persistent HTTP can still send one request at a time when pipelining is not used.

---

## Q7 — NAT

A browser fetches one HTML page and four embedded objects. It uses one persistent connection, does not pipeline, and discovers the four objects only after the HTML arrives. Enter the number of RTTs.

---

## Level 3 — Multi-Step

## Q8 — MCQ

The HEAD method

A. returns headers for the resource and does not return the message body
B. stores a new copy of the resource on the server
C. deletes the resource
D. is the DNS query for the host in the URL

---

## Q9 — MSQ

Select all that apply. Which statements about cookies and HTTP are correct?

A. HTTP requests can be understood without the server keeping per-client state, and a cookie is an explicit token that puts state back in when the application wants it.
B. A cookie is set by the server and sent back by the client on later requests to that server.
C. A cookie replaces the TCP port numbers of the connection.
D. A cookie is not the same object as an A record.

---

## Q10 — NAT

Five objects are fetched with non-persistent HTTP and no parallel connections. Each object uses its own TCP connection. Enter the number of RTTs.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

One HTML page refers to four objects. The browser uses one persistent connection and pipelining, but it does not know the four object URLs until the HTML has arrived. After the HTML response, it pipelines the four object requests in one RTT. The number of RTTs is

A. 2
B. 3
C. 6
D. 10

---

## Q12 — MSQ

Select all that apply. Which statements are true?

A. 404 reports a missing resource. 500 reports a server-side failure, not a missing name in DNS.
B. GET is a retrieval. POST submits a body that the server may treat as a change.
C. A persistent pipelined fetch of HTML plus later objects always takes 2 RTTs, even when the object URLs are discovered only from the HTML.
D. Counting a non-persistent object as 1 RTT forgets the handshake that this set counts separately from the request.

---

## Level 5 — Challenge

## Q13 — MCQ

The browser uses non-persistent HTTP. It fetches HTML first, then four objects, with at most two connections in parallel. It does not know the object URLs until the HTML arrives. Each object, including the HTML, needs its own connection. The number of RTTs is

A. 6
B. 10
C. 4
D. 8

---

## Q14 — MCQ

Before connecting, the browser already knows the HTML URL and three object URLs. It uses one persistent connection and pipelines every request. The number of RTTs is

A. 2
B. 3
C. 4
D. 8

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 6 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B, D |
| 7 | NAT | 6 |
| 8 | MCQ | A |
| 9 | MSQ | A, B, D |
| 10 | NAT | 10 |
| 11 | MCQ | B |
| 12 | MSQ | A, B, D |
| 13 | MCQ | A |
| 14 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

GET retrieves a resource. POST is the method that commonly submits data the server may store or otherwise process. Deleting the resource is DELETE, not GET. Opening a TCP connection is not an HTTP method.

### Q2

Answer: A, B, C

200 is success, 404 is not found, and 301 is a permanent redirect. 500 means the server failed while handling the request. A missing DNS record prevents the HTTP connection from being addressed in the usual way; it is not what status 500 means. D is false.

### Q3

Answer: 6

There are three objects, and non-persistent HTTP with no parallelism costs 2 RTTs each:

\[
3 \times 2 = 6
\]

The HTML must come before the images are known, but each image still pays its own handshake, so knowing that order does not reduce the 2 RTTs per object. Counting 1 RTT per object gives 3 and drops every handshake. Counting one extra RTT for “parsing” gives 7, which this convention does not add.

### Q4

Answer: A

Persistence keeps the TCP connection open and sends later objects on it. B is non-persistent HTTP. The request line and the status codes remain, so C and D are false.

### Q5

Answer: A

A cookie is an application token the server gives the client and the client returns later, so the server can link requests. It does not remove the TCP handshake, it does not change IP fragmentation, and it does not restructure DNS.

### Q6

Answer: A, B, D

Non-persistent mode repeats the handshake. Persistent mode pays it once. Without pipelining, persistent mode still waits for one response before the next request. GET is the ordinary retrieval method in both modes, so C is false.

### Q7

Answer: 6

The handshake is 1 RTT. The HTML is 1 RTT. Each of the four objects is then 1 RTT, because there is no pipelining:

\[
1 + 1 + 4 = 6
\]

Non-persistent transfer of the same five objects would be \(5 \times 2 = 10\). Pipelining the four objects after the HTML would be \(1 + 1 + 1 = 3\). This question does neither of those.

### Q8

Answer: A

HEAD is GET without the body: headers and status, so a client can check metadata. PUT stores a representation. DELETE removes a resource. DNS is a different protocol.

### Q9

Answer: A, B, D

HTTP itself does not require the server to remember clients; a cookie is the usual way to pass an identifier back. The server sets it, and the client echoes it. It does not replace TCP ports. It is not a DNS A record, so D is a true distinction and belongs in the answer.

### Q10

Answer: 10

Five objects, two RTTs each, no overlap:

\[
5 \times 2 = 10
\]

A persistent non-pipelined count would be \(1 + 5 = 6\). A pipelined count would be smaller still. The factor of 2 is the handshake plus the request for each object.

### Q11

Answer: B

The handshake is 1 RTT. The HTML request is the second RTT, and only then are the four URLs known. The four pipelined object requests share a third RTT.

\[
1 + 1 + 1 = 3
\]

A answers 2, which would be right only if the HTML and the four objects had all been requested in the single RTT after the handshake. They could not be: the object URLs were still unknown. C is the persistent non-pipelined count, \(1+5 = 6\). D is the non-persistent count, \(5 \times 2 = 10\).

### Q12

Answer: A, B, D

404 and 500 are different failures: missing resource versus server error. GET retrieves and POST submits. C is the pipelining trap from the previous question: when the URLs come from the HTML, the fetch takes 3 RTTs under this convention, not 2. D is the other trap: a non-persistent object is handshake plus request, which this set counts as 2 RTTs, not 1.

### Q13

Answer: A

The HTML connection costs 2 RTTs, and the four URLs are known only after that. The four objects are fetched two at a time. Each object costs 2 RTTs, and a pair runs together, so each pair costs 2 RTTs of wall-clock time. Two pairs cost 4 RTTs.

\[
2 + 4 = 6
\]

B is the same four objects plus HTML with no parallelism: \(5 \times 2 = 10\). C counts 2 RTTs for the HTML and then 1 RTT per pair, dropping the handshake on the object connections. D counts 2 RTTs per pair and forgets that the two pairs are sequential, or adds an extra pair: \(2 + 2 + 2 + 2\) would be 8 if the HTML were also paired incorrectly. The serial pairs after the HTML are two, not three.

### Q14

Answer: A

All four URLs are known before the handshake. Persistence pays 1 RTT for the handshake. Pipelining puts the HTML request and the three object requests in the next RTT.

\[
1 + 1 = 2
\]

B is the count from the previous trap, where the objects were discovered only after the HTML. C pays a separate RTT per object after the handshake on a non-pipelined persistent connection: \(1 + 4 = 5\), which is not an option, or \(1 + 3\) if the HTML is forgotten. D is non-persistent: \(4 \times 2 = 8\). The change from Q11 is the assumption that every URL is known up front, and that assumption is what cuts the cost from 3 RTTs to 2.

# DNS — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

A hostname is resolved by walking a hierarchy. The server that holds the final address record for a name inside its zone is

A. the authoritative server for that zone
B. always the root server, and no other server stores addresses
C. the client’s application, with no query required
D. the default gateway

---

## Q2 — MSQ

Select all that apply. Which DNS record types match the descriptions?

A. An A record maps a name to an IPv4 address.
B. An NS record names a server that is authoritative for a zone.
C. A CNAME record is an alias for another name.
D. An MX record stores the Ethernet MAC address of a mail server.

---

## Q3 — NAT

A local resolver’s cache is empty. It resolves a name by iterative queries: one to a root server, one to a TLD server, and one to the authoritative server. There is no further delegation. Enter the number of iterative queries the local resolver sends.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

In iterative resolution, a server that is not authoritative for the name

A. returns a referral to another server, and the resolver asks that server itself
B. queries all later servers and returns only the final address to the resolver
C. returns the address of the client to the root
D. refuses every query, including referrals

---

## Q5 — MCQ

A CNAME record for `www.example.com` points at `web.example.com`. The IPv4 address is obtained from

A. an A record for the canonical name `web.example.com`
B. the CNAME record itself, which stores the address in place of the alias
C. an MX record, because every web name is a mail exchanger
D. an NS record, which stores host addresses rather than server names

---

## Q6 — MSQ

Select all that apply. Which statements about DNS caching are correct?

A. A resolver may reuse a record until its TTL expires.
B. After the TTL expires, the cached record should not be treated as still valid.
C. A cache can avoid repeating a query to the root for a name whose relevant records are still fresh.
D. A cached A record is permanent and has no TTL.

---

## Level 3 — Multi-Step

## Q7 — MCQ

The stub on the host sends one query to its local resolver. The local resolver then does the iterative work. In that split, the local resolver is

A. the agent that walks the hierarchy on behalf of the stub
B. the authoritative server for every name on the Internet
C. the root server
D. a router that rewrites DNS into NAT mappings

---

## Q8 — NAT

A lookup finds one CNAME record and then one A record for the canonical name. Enter the number of those DNS records that must be used to turn the original alias into an IPv4 address.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

The cache is empty and there is no extra delegation. The stub sends one query to the local resolver. The local resolver then queries a root server, a TLD server, and an authoritative server. How many iterative queries does the local resolver send to other servers?

A. 3
B. 4
C. 1
D. 2

---

## Q10 — MSQ

Select all that apply. Which statements are true?

A. An MX record directs mail to a mail exchanger. It is not the record that maps a web hostname to an IPv4 address.
B. An NS record names an authoritative server. It is not itself the IPv4 address of a web page.
C. An A record maps a name to an IPv4 address.
D. A CNAME record stores a 48-bit MAC address.

---

## Level 5 — Challenge

## Q11 — NAT

The name is `www.lab.example.com`. The cache is empty. The root refers the resolver to the `.com` servers. Those refer it to the `example.com` servers. The `example.com` servers delegate `lab.example.com` to a different nameserver. That nameserver returns the A record. Enter the number of iterative queries the local resolver sends.

---

## Q12 — MCQ

The local resolver already has a fresh NS record and the matching address for the `example.com` nameservers. It is looking up `host.example.com`, which is answered by those same servers with no further delegation. The number of iterative queries it sends is

A. 1
B. 2
C. 3
D. 4

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 3 |
| 4 | MCQ | A |
| 5 | MCQ | A |
| 6 | MSQ | A, B, C |
| 7 | MCQ | A |
| 8 | NAT | 2 |
| 9 | MCQ | A |
| 10 | MSQ | A, B, C |
| 11 | NAT | 4 |
| 12 | MCQ | A |

## Detailed Solutions

### Q1

Answer: A

The authoritative server is the one that holds the zone data and can answer for names in that zone. The root only knows the tops of the tree. The application does not store the global namespace, and the default gateway is not a DNS authority.

### Q2

Answer: A, B, C

A, NS, and CNAME match the descriptions in A, B, and C. An MX record names a mail exchanger. It does not store an Ethernet MAC address, so D is false.

### Q3

Answer: 3

The three iterative queries are root, TLD, and authoritative server. The final answer is a response, not a fourth query. Adding the stub’s query to the local resolver counts a query that this question does not include; it asks only for the resolver’s iterative queries, and it states that there is no further delegation.

### Q4

Answer: A

Iteration means the server that was asked returns a referral, and the resolver continues. B describes recursive resolution, where the server does the remaining work. The root is not given the client’s address as the answer, and a non-authoritative server can still return a referral.

### Q5

Answer: A

A CNAME is an alias, a pointer to another name. The address is on the A record of the canonical name. The CNAME does not contain the IPv4 address. MX is for mail. NS names a nameserver; the address of that nameserver, when needed, is a separate A record.

### Q6

Answer: A, B, C

TTL is the lifetime of a cached record. A fresh cache entry can answer without walking back to the root. When the TTL hits zero, the entry is stale. D denies the TTL that DNS records carry.

### Q7

Answer: A

The stub asks one recursive question of the local resolver. The resolver is the agent that issues the iterative queries. It is not authoritative for the whole Internet, it is not the root, and NAT is unrelated to this lookup role.

### Q8

Answer: 2

The alias is one CNAME. The canonical name’s address is one A record. Both are required. Stopping at the CNAME yields a name, not an address. An extra NS or MX is not required by this question.

### Q9

Answer: A

The stub’s single query is not one of the iterative queries the local resolver sends onward. Those are the three queries to the root, the TLD, and the authoritative server. B counts the stub query in the iterative total. C and D drop part of the cold-cache walk. This is the same three-query walk as the earlier numeric question, with the extra stub query placed in the stem as the trap.

### Q10

Answer: A, B, C

MX is for mail delivery, not for the A-record job of naming a web server’s IPv4 address. NS identifies a nameserver. A stores an IPv4 address. A CNAME stores another domain name, not a MAC address, so D is false.

### Q11

Answer: 4

The resolver queries four servers:

1. a root server
2. a `.com` server
3. an `example.com` server, which returns the delegation of `lab.example.com`
4. the `lab.example.com` nameserver, which returns the A record

Stopping at 3 misses the delegation. The delegation adds a query that the empty-cache three-server story does not have.

### Q12

Answer: A

The cached NS and address let the resolver skip the root and the TLD. It sends one query to the `example.com` nameserver and gets the A record. There is no further delegation, so it does not send a fourth query, and it does not repeat the two queries the cache has already made unnecessary.

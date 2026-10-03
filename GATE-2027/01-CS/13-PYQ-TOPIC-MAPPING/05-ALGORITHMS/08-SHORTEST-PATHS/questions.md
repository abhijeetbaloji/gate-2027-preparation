# GATE PYQs

## 2026

### Q.41

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Let 𝐺(𝑉, 𝐸) be an undirected, edge-weighted graph with integer weights. The weight
of a path is the sum of the weights of the edges in that path. The length of a path is
the number of edges in that path.
Let 𝑠∈𝑉 be a vertex in 𝐺. For every 𝑢∈𝑉 and for every 𝑘 ≥0, let 𝑑_{𝑘}(𝑢) denote
the weight of a shortest path (in terms of weight) from 𝑠 to 𝑢 of length at most 𝑘. If
there is no path from 𝑠 to 𝑢 of length at most 𝑘, then 𝑑_{𝑘}(𝑢) = ∞.
Consider the statements:
S1:  For every 𝑘 ≥0 and 𝑢 ∈𝑉,  𝑑_{𝑘+1}(𝑢) ≤𝑑_{𝑘}(𝑢).
S2:  For every (𝑢, 𝑣) ∈𝐸, if (𝑢, 𝑣) is part of a shortest path (in terms of
weight) from 𝑠 to 𝑣, then for every 𝑘≥ 0, 𝑑_{𝑘}(𝑢) ≤𝑑_{𝑘}(𝑣).
Which one of the following options is correct?

**Options:**

A. Only S1 is true
B. Only S2 is true
C. Both S1 and S2 are true
D. Neither S1 nor S2 is true

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.37

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Let 𝐺 be a weighted directed acyclic graph with 𝑚 edges and 𝑛 vertices. Given 𝐺
and a source vertex 𝑠 in 𝐺, which one of the following options gives the worst case
time complexity of the fastest algorithm to find the lengths of shortest paths from 𝑠
to all vertices that are reachable from 𝑠 in 𝐺?

**Options:**

A. Θ(𝑚+ 𝑛)
B. Θ(𝑚+ 𝑛log(𝑛))
C. Θ(𝑛𝑚)
D. Θ(𝑛^{3})

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.17

**Paper:** GATE 2025 CS-2

**Question:**

Consider the routing protocols given in List I and the names given in List II:
List I  List II
(i)  Distance vector routing  (a)  Bellman-Ford
(ii)  Link state routing  (b)  Dijkstra
For matching of items in List I with those in List II, which ONE of the following
options is CORRECT?

**Options:**

A. (i) – (a) and (ii) – (b)
B. (i) – (a) and (ii) – (a)
C. (i) – (b) and (ii) – (a)
D. (i) – (b) and (ii) – (b)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2025 CS-2

**Question:**

A machine receives an IPv4 datagram. The protocol field of the IPv4 header has the
protocol number of a protocol X.
Which ONE of the following is NOT a possible candidate for X?

**Options:**

A. Internet Control Message Protocol (ICMP)
B. Internet Group Management Protocol (IGMP)
C. Open Shortest Path First (OSPF)
D. Routing Information Protocol (RIP)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2025 CS-2

**Question:**

Which of the following statements regarding Breadth First Search (BFS) and
Depth First Search (DFS) on an undirected simple graph G is/are TRUE?

**Options:**

A. A DFS tree of 𝐺 is a Shortest Path tree of 𝐺.
B. Every non-tree edge of G with respect to a DFS tree is a forward/back edge.
C. If (𝑢, 𝑣) is a non-tree edge of G with respect to a BFS tree, then the distances from the source vertex 𝑠 to 𝑢 and 𝑣 in the BFS tree are within ±1 of each other.
D. Both BFS and DFS can be used to find the connected components of G.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2023

### Q.25

**Paper:** GATE 2023 CS

**Question:**

Which of the following statements is/are INCORRECT about
the OSPF (Open Shortest Path First) routing protocol used in the Internet?

**Options:**

A. OSPF implements Bellman-Ford algorithm to find shortest paths.
B. OSPF uses Dijkstra’s shortest path algorithm to implement least-cost path routing.
C. OSPF is used as an inter-domain routing protocol.
D. OSPF implements hierarchical routing.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2021

### Q.36

**Paper:** GATE 2021 CS Set-1

**Question:**

Let G = (V, E) be an undirected unweighted connected graph. The diameter of G
is defined as:
diam(G) = wucx {the length of shortest path between z and v}
Let M be the adjacency matrix of G.
Define graph G2 on the same set of vertices with adjacency matrix N, where
Nij = J1 if Mij > 0 or Pij > 0, where P = M2
1° otherwise
Which one of the following statements is true?

**Options:**

A. diam(G2) ≤ |diam(G)/2|
B. [diam(G)/2] < diam(G2) < diam(G)
C. diam(G,) = diam(G)
D. diam(G) < diam(Gz) ≤ 2 diam(G) GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

## 2020

### Q.40

**Paper:** GATE 2020 CS

**Question:**

Let G=(V,E) be a directed, weighted graph with weight functionw: E→R.
For some function f:V →R, for each edge (u,v) e E, define w'(u,v) as
w(u,v)+ f (u) - f(v).
Which one of the options completes the following sentence so that it is TRUE?
"The shortest paths in G under w are shortest paths under w' too, ".

**Options:**

A. for every f:V → R
B. if and only if VueV, f(u) is positive
C. if and only if Vu eV, f(u) is negative
D. if and only if f (u) is the distance from s to u in the graph obtained by adding a new vertex s to G and edges of zero weight from s to every vertex of G

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2017

### Q.9

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong:-0.33
Consider the following statements about the routing protocols, Routing Information Protocol (RIP)
and Open Shortest Path First (OSPF) in an IPv4 network.
I: RIP uses distance vector routing
II: RIP packets are sent using UDP
III: OSPF packets are sent using TCP
IV: OSPF operation is based on link-state routing
Which of the statements above are CORRECT?

**Options:**

A. I and IV only
B. I, II and III only
C. I, II and IV only
D. II, III and IV only

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.38

**Paper:** GATE 2016 CS-1

**Question:**

Consider the weighted undirected graph with 4 vertices, where the weight of edge {i, j} is
given by the entry W_{i j} in the matrix W .
 0 2 8 5 
W =  2 0 5 8 
8 5 0 x
5 8 x 0
The largest possible integer value of x, for which at least one shortest path between some pair
of vertices will contain the edge with weight x is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

## 2014

### Q.14

**Paper:** GATE 2014 CS SET-2

**Question:**

Consider the tree arcs of a BFS traversal from a source node  W in an unweighted, connected,
undirected graph.  The tree T formed by the tree arcs is a data structure for computing

**Options:**

A. the shortest path between every pair of vertices.
B. the shortest path from W to every vertex in the graph.
C. the shortest paths from W to only those nodes that are leaves of T.
D. the longest path in the graph.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2013

### Q.19

**Paper:** GATE 2013 CS Booklet A

**Question:**

What is the time complexity of Bellman-Ford single-source shortest path algorithm on a complete
graph of n vertices?

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet A, `12-PYQ/2013/set-01/question-paper.pdf`

---

### Q.7

**Paper:** GATE 2013 CS Booklet B

**Question:**

What is the time complexity of Bellman-Ford single-source shortest path algorithm on a complete
graph of n vertices?

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}log n) CS-B 2/20 2013COMPUTER SCIENCE & INFORMATION TECH. - CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet B, `12-PYQ/2013/set-02/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2013 CS Booklet C

**Question:**

What is the time complexity of Bellman-Ford single-source shortest path algorithm on a complete
graph of n vertices?

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet C, `12-PYQ/2013/set-03/question-paper.pdf`

---

### Q.7

**Paper:** GATE 2013 CS Booklet D

**Question:**

What is the time complexity of Bellman-Ford single-source shortest path algorithm on a complete
graph of n vertices?

**Options:**

A. Θ(n^{2})
B. Θ(n^{2}log n)
C. Θ(n^{3})
D. Θ(n^{3}log n)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2013 CS Booklet D, `12-PYQ/2013/set-04/question-paper.pdf`

---

## 2012

### Q.40

**Paper:** GATE 2012 CS Booklet A

**Question:**

Consider the directed graph shown in the figure below. There are multiple shortest paths between
vertices S and T. Which one will be reported by Dijkstra’s shortest path algorithm? Assume that, in
any iteration, the shortest path to a vertex  v is updated only when a strictly shorter path to  v is
discovered.
2
E
C  1  2
G
1
A  1
3
4  3
4
7  3
S  D
4
3  5
5  T
3
B  F

**Options:**

A. SDT
B. SBDT
C. SACDT
D. SACET

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2009

### Q.13

**Paper:** GATE 2009 CS

**Question:**

Which of the following statement(s) is/are correct regarding Bellman-Ford shortest path algorithm?
P. Always finds a negative weighted cycle, if one exists.
Q. Finds whether any negative weighted cycle is reachable from the source.

**Options:**

A. P only
B. Q only
C. both P and Q
D. neither P nor Q

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.45

**Paper:** GATE 2008 CS

**Question:**

-3
-5
2
Dijkstra's single source shortest path algorithm when run from vertex a in the above graph,
computes the correct shortest path distance to

**Options:**

A. only vertex a
B. only vertices a, e, f. g, h
C. only vertices a, b, c, d
D. all the vertices

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

## 2007

### Q.41

**Paper:** GATE 2007 CS

**Question:**

In an unweighted, undirected connected graph, the shortest path from a node S to
every other node is computed most efficiently, in terms of time complexity, by

**Options:**

A. Dijkstra's algorithm starting from S.
B. Warshall's algorithm.
C. performing a DFS starting from S.
D. performing a BFS starting from S.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2007 CS, `12-PYQ/2007/question-paper.pdf`

---

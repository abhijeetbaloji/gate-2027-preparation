# GATE PYQs

## 2026

### Q.34

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the following program in C:
#include <stdio.h>
void func(int i, int j) {
if(i < j) {
int i = 0;
while (i < 10) {
j += 2;
i++;
}
}
printf("%d", i);
}
int main() {
int i = 9, j = 10;
func(i, j);
return 0;
}
The output of the program is _________. (answer in integer)
Note: Assume that the program compiles and runs successfully.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.63

**Paper:** GATE 2026 CS-1 (forenoon)

**Question:**

Consider the following program snippet. Assume that the program compiles and runs
successfully. Further, assume that the fork() system call is always successful in
creating a process.
int main () {
int i;
for (i = 0; i < 3; i++){
if (fork() == 0){
continue;
}
break;
}
printf("Hello!");
return 0;
}
The total number of times that the printf statement gets executed is ________.
(answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-1 (forenoon), `12-PYQ/2026/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following three ANSI-C programs, P1, P2, and P3.
P1  P2  P3
#include <stdio.h>  #include <stdio.h>  #include <stdio.h>
int a=5;  int main(){  int main(){
int main(){  int a=5;  int a=5;
int a=7;  int a=7;  float a=7;
return(0);  return(0);  return(0);
}  }  }
Which one of the following statements is true?

**Options:**

A. Only P1 will compile without any error
B. Only P2 will compile without any error
C. Only P3 will compile without any error
D. All three programs P1, P2, and P3 will compile without any error

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.60

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following ANSI-C program.
#include <stdio.h>
int main(){
int *ptr, a, b, c;
a=5; b=11; c=20;
ptr=&a; *ptr=c; ptr=&c;
a=*(&b); c=*ptr-a;
printf("%d",c);
return(0);
}
The output of this program is ____________. (answer in integer)
Note: Assume that the program compiles and runs successfully.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2026 CS-2 (afternoon)

**Question:**

Consider the following ANSI-C function.
int func(int start, int end){
int length=end+1-start;
if((length<1)||(start<0)||(end<0)){ return(0); }
if(length%3==0){
return(func(start+1, end));
} else if(length%3==1){
return(1+func(start, end-1));
} else {
return(func(start+2, end));
}
}
The maximum possible value that can be returned from this function is
____________. (answer in integer)
Note: Ignore syntax errors (if any) in the function.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2026 CS-2 (afternoon), `12-PYQ/2026/set-02/question-paper.pdf`

---

## 2025

### Q.29

**Paper:** GATE 2025 CS-1

**Question:**

Suppose in a multiprogramming environment, the following C program segment is
executed. A process goes into I/O queue whenever an I/O related operation is
performed. Assume that there will always be a context switch whenever a process
requests for an I/O, and also whenever the process returns from an I/O. The number
of times the process will enter the ready queue during its lifetime (not counting the
time the process enters the ready queue when it is run initially) is _______. (Answer
in integer)
int main()
{
int x=0,i=0;
scanf("%d",&x);
for(i=0; i<20; i++)
{
x = x+20;
printf("%d\n",x);
}
return 0;
}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2025 CS-1

**Question:**

#include <stdio.h>
void foo(int *p, int x){
*p=x;
}
int main(){
int *z;
int a = 20, b = 25;
z = &a;
foo(z,b);
printf("%d",a);
return 0;
}
The output of the given C program is __________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2025 CS-1

**Question:**

#include <stdio.h>
int foo(int S[],int size){
if(size == 0) return 0;
if(size == 1) return 1;
if(S[0] != S[1]) return 1+foo(S+1,size-1);
return foo(S+1,size-1);
}
int main(){
int A[]={0,1,2,2,2,0,0,1,1};
printf("%d",foo(A,9));
return 0;
}
The value printed by the given C program is _______ . (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.63

**Paper:** GATE 2025 CS-1

**Question:**

Consider the following C program:
#include <stdio.h>
int gate (int n) {
int d, t, newnum, turn;
newnum = turn = 0; t=1;
while (n>=t) t *= 10;
t /=10;
while (t>0) {
d = n/t;
n = n%t;
t /= 10;
if (turn) newnum = 10*newnum + d;
turn = (turn + 1) % 2;
}
return newnum;
}
int main () {
printf ("%d", gate(14362));
return 0;
}
The value printed by the given C program is _______ . (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-1, `12-PYQ/2025/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following C program:
#include <stdio.h>
void stringcopy(char *, char *);
int main(){
char a[30] = "@#Hello World!";
stringcopy(a, a + 2);
printf("%s\n", a);
return 0;
}
void stringcopy(char *s, char *t) {
while(*t)
*s++ = *t++;
}
Which ONE of the following will be the output of the program?

**Options:**

A. @#Hello World!
B. Hello World!
C. ello World!
D. Hello World!d!

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.33

**Paper:** GATE 2025 CS-2

**Question:**

int x=126,y=105;
do {
if(x>y) x=x-y;
else y=y-x;
} while(x!=y);
printf("%d",x);
The output of the given C code segment is ________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.62

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following C program:
#include <stdio.h>
int main(){
int a;
int arr[5] = {30,50,10};
int *ptr;
ptr = &arr[0] + 1;
a = *ptr;
(*ptr)++;
ptr++;
printf("%d", a + (*ptr) + arr[1]);
return 0;
}
The output of the above program is ___________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

### Q.63

**Paper:** GATE 2025 CS-2

**Question:**

Consider the following C program:
#include <stdio.h>
int g(int n) {
return (n+10);
}
int f(int n) {
return g(n*2);
}
int main() {
int sum, n;
sum=0;
for (n=1; n<3; n++)
sum += g(f(n));
printf ("%d", sum);
return 0;
}
The output of the given C program is ________. (Answer in integer)

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2025 CS-2, `12-PYQ/2025/set-02/question-paper.pdf`

---

## 2024

### Q.18

**Paper:** GATE 2024 CS1

**Question:**

Consider the following C program:
#include <stdio.h>
int main(){
int a = 6;
int b = 0;
while(a < 10) {
a = a / 12 + 1;
a += b;}
printf(”%d”, a);
return 0;}
Which one of the following statements is CORRECT?

**Options:**

A. The program prints 9 as output
B. The program prints 10 as output
C. The program gets stuck in an infinite loop
D. The program prints 6 as output

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.19

**Paper:** GATE 2024 CS1

**Question:**

Consider the following C program:
#include <stdio.h>  void fX(){
void fX();  char a;
int main(){  if((a=getchar()) != ’\n’)
fX();  fX();
return 0;}  if(a != ’\n’)
putchar(a);}
Assume that the input to the program from the command line is 1234 followed by
a newline character. Which one of the following statements is CORRECT?

**Options:**

A. The program will not terminate
B. The program will terminate with no output
C. The program will terminate with 4321 as output
D. The program will terminate with 1234 as output

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.57

**Paper:** GATE 2024 CS1

**Question:**

Consider the following code snippet using the fork() and wait() system calls.
Assume that the code compiles and runs correctly, and that the system calls run
successfully without any errors.
int x = 3;
while(x > 0) {
fork();
printf("hello");
wait(NULL);
x--;
}
The total number of times the printf statement is executed is _______

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS1, `12-PYQ/2024/set-01/question-paper.pdf`

---

### Q.13

**Paper:** GATE 2024 CS2

**Question:**

Consider the following C program. Assume parameters to a function are evaluated
from right to left.
#include <stdio.h>
int g(int p) { printf("%d", p); return p; }
int h(int q) { printf("%d", q); return q; }
void f(int x, int y) {
g(x);
h(y);
}
int main() {
f(g(10),h(20));
}
Which one of the following options is the CORRECT output of the above
C program?

**Options:**

A. 20101020
B. 10202010
C. 20102010
D. 10201020

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2024 CS2

**Question:**

What is the output of the following C program?
#include <stdio.h>
int main() {
double a[2]={20.0, 25.0}, *p, *q;
p = a;
q = p + 1;
printf(”%d,%d”, (int)(q – p), (int)(*q – *p));
return 0;}

**Options:**

A. 4,8
B. 1,5
C. 8,5
D. 1,8

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2024 CS2, `12-PYQ/2024/set-02/question-paper.pdf`

---

## 2023

### Q.35

**Paper:** GATE 2023 CS

**Question:**

The integer value printed by the ANSI-C program given below is  .
#include<stdio.h>
int funcp(){
static int x = 1;
x++;
return x;
}
int main(){
int x,y;
x = funcp();
y = funcp()+x;
printf("%d\n", (x+y));
return 0;
}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.36

**Paper:** GATE 2023 CS

**Question:**

Consider the following program:
int main()  int f1()  int f2(int X)  int f3()
{  {  {  {
f1();  return(1);  f3();  return(5);
f2(2);  }  if (X==1)  }
f3();  return f1();
return(0);  else
}  return (X*f2(X-1));
}
Which one of the following options represents the activation tree corresponding to
the main function?
main
f1 f2 f3
f3 f2

**Options:**

A. f3 f1 main f1 f2 f3
B. f3 f1 main f1 f2
C. f3 f1 main f1 f2 f3
D. f3 f2 f1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

### Q.57

**Paper:** GATE 2023 CS

**Question:**

Consider the following two-dimensional array D in the C programming language,
which is stored in row-major order:
int D[128][128];
Demand paging is used for allocating memory and each physical page frame holds
512 elements of the array D. The Least Recently Used (LRU) page-replacement
policy is used by the operating system. A total of 30 physical page frames are
allocated to a process which executes the following code snippet:
for (int i = 0; i < 128; i++)
for (int j = 0; j < 128; j++)
D[j][i] *= 10;
The number of page faults generated during the execution of this code snippet is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2023 CS, `12-PYQ/2023/question-paper.pdf`

---

## 2022

### Q.21

**Paper:** GATE 2022 CS

**Question:**

What is printed by the following ANSI C program?
#include<stdio.h>
int main(int argc, char *argv[])
{
int x = 1, z[2] = {10, 11};
int *p = NULL;
p = &x;
*p = 10;
p = &z[1];
*(&z[0] + 1) += 3;
printf("%d, %d, %d\n", x, z[0], z[1]);
return 0;
}

**Options:**

A. 1, 10, 11
B. 1, 10, 14
C. 10, 14, 11
D. 10, 10, 14

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2022 CS

**Question:**

What is printed by the following ANSI C program?
#include<stdio.h>
int main(int argc, char *argv[])
{
int a[3][3][3] =
{{1, 2, 3, 4, 5, 6, 7, 8, 9},
{10, 11, 12, 13, 14, 15, 16, 17, 18},
{19, 20, 21, 22, 23, 24, 25, 26, 27}};
int i = 0, j = 0, k = 0;
for( i = 0; i < 3; i++ ){
for(k = 0; k < 3; k++ )
printf("%d ", a[i][j][k]);
printf("\n");
}
return 0;
}

**Options:**

A. 1 2 3 10 11 12 19 20 21
B. 1 4 7 10 13 16 19 22 25
C. 1 2 3 4 5 6 7 8 9
D. 1 2 3 13 14 15

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

### Q.44

**Paper:** GATE 2022 CS

**Question:**

25 26 27
What is printed by the following ANSI C program?
#include<stdio.h>
int main(int argc, char *argv[]){
char a = 'P';
char b = 'x';
char c = (a & b) + '*';
char d = (a | b) - '-';
char e = (a ^ b) + '+';
printf("%c %c %c\n", c, d, e);
return 0;
}
ASCII encoding for relevant characters is given below

**Options:**

A. z K S
B. 122 75 83
C. * - +
D. P x +

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2022 CS, `12-PYQ/2022/question-paper.pdf`

---

## 2021

### Q.37

**Paper:** GATE 2021 CS Set-1

**Question:**

Consider the following ANSI C program.
#include <stdio.h>
int main()
int i, j, count;
count = 0;
1 = 0;
for (j = -3; j <= 3; j++)
if ((j >= 0) && (itt))
count = count + j;
}
count = count + i;
printf ("%d", count);
return 0;
}
Which one of the following options is correct?

**Options:**

A. The program will not compile successfully.
B. The program will compile successfully and output 10 when executed.
C. The program will compile successfully and output 8 when executed.
D. The program will compile successfully and output 13 when executed. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-1, `12-PYQ/2021/set-01/question-paper.pdf`

---

### Q.3

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following ANSI C program:
int main() {
Integer x;
return 0;
}
Which one of the following phases in a seven-phase C compiler will throw an error?

**Options:**

A. Lexical analyzer
B. Syntax analyzer
C. Semantic analyzer
D. Machine dependent optimizer

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.10

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following ANSI C program.
#include <stdio.h>
int main(){
int arr[4] [5];
int i, j;
for (i=0; i<4; i++){
for (j=0; j<5; j++) {
arr[i][j] = 10*i + j;
}
}
printf ("%d", *(arr[1] + 9));
return 0;
}
What is the output of the above program?

**Options:**

A. 14
B. 20
C. 24
D. 30 GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following ANSI C program:
#include <stdio.h>
#include <stdlib.h>
struct Nodel
int value;
struct Node *next;};
int main(){
struct Node *boxE, *head, *boxN; int index = 0;
boxE = head = (struct Node *) malloc(sizeof(struct Node));
head→>value = index;
for (index = 1; index <= 3; indext+){
boxN = (struct Node *) malloc(sizeof(struct Node));
boxE->next = boxN;
boxN->value = index;
boxE = boxN; }
for (index = O; index <= 3; index++) {
printf("Value at index %d is %d\n", index, head->value);
head = head->next;
printf("Value at index %d is %d\n", index+1, head->value) ; } }
Which one of the statements below is correct about the program?

**Options:**

A. Upon execution, the program creates a linked-list of five nodes.
B. Upon execution, the program goes into an infinite loop.
C. It has a missing return which will be reported as an error by the compiler.
D. It dereferences an uninitialized pointer that may result in a run-time error. GATE Graduate Aptitude Test in Engineering 2021 2021 Organising Institute - IIT Bombay

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

### Q.49

**Paper:** GATE 2021 CS Set-2

**Question:**

Consider the following ANSI C' program.
#include <stdio.h>
int foo(int x, int y, int q)
if ((x <= 0) && (y <= 0))
return q;
if (x <= 0)
return foo (x, y-q, q);
if (y <= 0)
return foo(x, y-q, q) + foo (x-q, У, q); return foo (x-q, y, q);
}
int main()
int r = foo (15,15,10);
printf("%a", I);
return 0;
}
The output of the program upon execution is
GATE Graduate Aptitude Test in Engineering 2021
2021 Organising Institute - IIT Bombay

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2021 CS Set-2, `12-PYQ/2021/set-02/question-paper.pdf`

---

## 2020

### Q.22

**Paper:** GATE 2020 CS

**Question:**

Consider the following C program.
#include <stdio.h>
int main ()
int a[4][5]=((1, 2, 3, 4, 5),
16, 7, 8, 9, 10},
{11, 12, 13, 14, 15),
{16, 17, 18 , 19, 20));
printf("%d\n", * (*(a+**a+2)+3));
return (0);
}
The output of the program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2020 CS, `12-PYQ/2020/question-paper.pdf`

---

## 2019

### Q.17

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

The following C program is executed on a Unix/Linux system:
#include <unistd.h>
int mainl)
int i;
for (i=0; i<10; i++)
return 0; if (182 == 0) fork();
}
The total number of child processes created is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.18

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C program:
#include <stdio.h>
int jumble(int x, int y) {
x=2*x+y;
return x;
}
int main(){
int x=2, y=5;
y=jumble(y,x);
x=jumble(y,x); printf ("¿d \n", x);
return 0;
}
The value printed by the program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.24

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C program:
#include <stdio.h>
int main(){
int arr[]=(1,2,3,4,5,6,7,8,9,0,1,2,5), *ip=arr+4;
printf("¿d\n", ip[1]);
return 0;
}
The number that will be displayed on execution of the program is_
5/15

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.26

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C function.
void convert(int n){
if(n<0)
printf("8d",n) ;
else {
printf("¿d",n%2); convert (n/2);
}
Which one of the following will happen when the function convert is called with any
positive integer n as argument?

**Options:**

A. It will print the binary representation of n and terminate
B. It will print the binary representation of n in the reverse order and terminate
C. It will print the binary representation of n but will not terminate
D. It will not print anything and will not terminate

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.27

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C program:
#include <stdio.h>
int r(){
static int num=7;
return num--;
int main(){
Eor ("rintt("gd"
,r.())/
return 0;
}
Which one of the following values will be displayed on execution of the programs?

**Options:**

A. 41
B. 52
C. 63
D. 630 cs 6/15

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following sets:
S1. Sct of all rccursivcly cnumerable languages over the alphabet {0,1}
S2. Set of all syntactically valid C programs
S3. Set of all languages over the alphabet {0,1}
S4. Set of all non-regular languages over the alphabet {0,1}
Which of the above sets are uncountable?

**Options:**

A. S1 and S2
B. S3 and S4
C. S2 and S3
D. S1 and S4

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.52

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C program:
#include <stdio.h>
int main(){
float sum = 0.0, j = 1.0, i = 2.0;
while (i/j > 0.0625)1
j = j ÷ j¡
sum + i/ j;
printf("8f \n", sum) ;
return 0;
}
The number of times the variable sum will be printed, when the above program is executed,
12/15

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2019 CS (printed header Set-2)

**Question:**

Consider the following C program:
#include <stdio.h>
int main()
int al] = 12, 4, 6, 8, 10);
int i, sum = 0, *b = a + 4;
for (i = 0; i < 5; it+)
sum = sum t (*b-i) - *(b-i);
printf ("&d)n", sum);
return 0;
}
The output of the above C program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2019 CS (printed header Set-2), `12-PYQ/2019/question-paper.pdf`

---

## 2018

### Q.2

**Paper:** GATE 2018 CS

**Question:**

Consider the following C program.
#include<stdio.h>
struct Ournode{
char x,y,z;
};
int main(){
struct Ournode p = {'1', '0', 'a'+2};
struct Ournode *q = &p;
printf ("%c, %c", *((char*)q+1), *((char*)q+2));
return 0;
}
The output of this program is:

**Options:**

A. 0, c
B. 0, a+2
C. '0', 'a+2'
D. '0', 'c'

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

### Q.29

**Paper:** GATE 2018 CS

**Question:**

Consider the following C program:
#include<stdio.h>
void fun1(char *s1, char *s2){
char *tmp;
tmp = s1;
s1 = s2;
s2 = tmp;
}
void fun2(char **s1, char **s2){
char *tmp;
tmp = *s1;
*s1 = *s2;
*s2 = tmp;
}
int main(){
char *str1 = "Hi", *str2 = "Bye";
fun1(str1, str2);  printf("%s %s ", str1, str2);
fun2(&str1, &str2); printf("%s %s", str1, str2);
return 0;
}
The output of the program above is

**Options:**

A. Hi Bye Bye Hi
B. Hi Bye Hi Bye
C. Bye Hi Hi Bye
D. Bye Hi Bye Hi

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2018 CS, `12-PYQ/2018/question-paper.pdf`

---

## 2017

### Q.14

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 1 Wrong: -0.33
Consider the following function implemented in C:
void printxy(int x, int y) ı
int *ptr;
x = 0;
ptr = &x;
y = *ptr;
*ptr = 1;
printf ("gd, &d",x, y) ;
The output of invoking printxy (1,1) is

**Options:**

A. 0,0
B. 0,1
C. 1,0
D. 1.1

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.37

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong: -0.66
Consider the C program fragment below which is meant to divide x by y using repeated
subtractions. The variables x, y. g and r are all unsigned int.
while (I >=y) {
I = I - Y;
9 = g + 1;
Which of the following conditions on the variables x, y, q and r before the execution of the
fragment will ensure that the loop terminates in a state satisfying the conditionx == (y*q +
I)?

**Options:**

A. (9== I) &á (I == 0)
B. (x > 0) && (r == x) && (y >°0)
C. (g ==0) &a (I == x) && (y > 0)
D. (g == 0) && (y > 0)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.38

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong : -0.66
Consider the following C function.
int fun (int n) {
int i, j;
for (i = 1; i <= n; it+) {
for (j = 1; j < n; j += i) {
printf(" od sd", i,j);
Time complexity of fun in terms of O notation is

**Options:**

A. 0(n/n)
B. 0(n2)
C. e(nlogn)
D. e(n2logn)

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.54

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct : 2 Wrong : 0
Consider the following C Program.
#include<stdio.h>
int main () {
int m = 10;
int n, n_;
n = ++m;
ni = m++;
n--;
--nỉ;
n -= nl;
printf("öd", n);
return 0;
The output of the program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

### Q.55

**Paper:** GATE 2017 CS Session 2

**Question:**

Correct: 2 Wrong : 0
Consider the following C Program.
#include<stdio.h>
#include<string.h>
int main () {
char* c = "GATECSIT2017";
char* p = ci
printf("8d" , (int)strlen (ct2[p]-6[p]-1));
return 0;
The output of the program is

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2017 CS Session 2, `12-PYQ/2017/set-02/question-paper.pdf`

---

## 2016

### Q.12

**Paper:** GATE 2016 CS-1

**Question:**

Consider the following C program.
void f(int, short);
void main()
{
int i = 100;
short s = 12;
short *p = &s;
__________ ;  // call to f()
}
Which one of the following expressions, when placed in the blank above, will NOT result in
a type checking error?

**Options:**

A. f(s,*s)
B. i = f(i,s)
C. f(i,*s)
D. f(i,*p) CS(Set A) 3/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.15

**Paper:** GATE 2016 CS-1

**Question:**

Consider the following C program.
#include<stdio.h>
void mystery(int *ptra, int *ptrb) {
int *temp;
temp = ptrb;
ptrb = ptra;
ptra = temp;
}
int main() {
int a=2016, b=0, c=4, d=42;
mystery(&a, &b);
if (a < c)
mystery(&c, &a);
mystery(&a, &d);
printf("%d\n", a);
}
The output of the program is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.35

**Paper:** GATE 2016 CS-1

**Question:**

What will be the output of the following C program?
void count(int n){
static int d=1;
printf("%d ", n);
printf("%d ", d);
d++;
if(n>1) count(n-1);
printf("%d ", d);
}
void main(){
count(3);
}

**Options:**

A. 3 1 2 2 1 3 4 4 4
B. 3 1 2 1 1 1 2 2 2
C. 3 1 2 2 1 3 4
D. 3 1 2 1 1 1 2 CS(Set A) 11/17

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-1, `12-PYQ/2016/set-01/question-paper.pdf`

---

### Q.12

**Paper:** GATE 2016 CS-2

**Question:**

The value printed by the following program is  .
void f(int* p, int m){
m = m + 5;
*p = *p + m;
return;
}
void main(){
int i=5, j=10;
f(&i, j);
printf("%d", i+j);
}

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.14

**Paper:** GATE 2016 CS-2

**Question:**

The Floyd-Warshall algorithm for all-pair shortest paths computation is based on

**Options:**

A. Greedy paradigm.
B. Divide-and-Conquer paradigm.
C. Dynamic Programming paradigm.
D. neither Greedy nor Divide-and-Conquer nor Dynamic Programming paradigm.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

### Q.37

**Paper:** GATE 2016 CS-2

**Question:**

Consider the following program:
int f(int *p, int n)
{
if (n <= 1) return 0;
else return max(f(p+1,n-1),p[0]-p[1]);
}
int main()
{
int a[] = {3,5,2,6,4};
printf("%d", f(a,5));
}
Note: max(x,y) returns the maximum of x and y.
The value printed by this program is  .

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2016 CS-2, `12-PYQ/2016/set-02/question-paper.pdf`

---

## 2015

### Q.13

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

Match the following:
(P) Prim's algorithm for minimum spanning tree (1) Backtracking
(Q) Floyd-Warshall algonithm for all pairs shortest paths (11) Greedy method
(R) Mergesort (111) Dynamic programming
(S) Hamiltonian circuit (iv) Divide and conquer

**Options:**

A. P-111, Q-11, R-iv, S-1
B. P-1, Q-11, R-iv, S-111
C. P-11, Q-111, R-iv, S-1
D. P-11, Q-1, R-111, S-Iv

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

The output of the following C program is
void fl (int a, int b) {
int c;
c=a; a=b; b=c;
void f2 (int *a, int *b) {
int c;
c=*a; *a=*b; *b=c;
}
int main () {
int a=4, b=5, c=6;
f1 (a,b);
£2 (&b, &c);
printf ("¿d", c-a-b) ;
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.62

**Paper:** GATE 2015 CS, 7 February Shift 1

**Question:**

What is the output of the following C code? Assume that the address of x is 2000 (in decimal) and
an integer requires four bytes of memory.
int main () {
unsigned int x[4][3] =
{{1,2,3), (4,5,6}, (7,8,9), (10, 11,12));
printf("¿u, ¿u, §u", x+3, *(x+3), *(x+2)+3);

**Options:**

A. 2036, 2036, 2036
B. 2012, 4, 2204
C. 2036, 10, 10
D. 2012, 4, 6 B 3. 3 C

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 1, `12-PYQ/2015/set-01/question-paper.pdf`

---

### Q.21

**Paper:** GATE 2015 CS, 7 February Shift 2

**Question:**

Consider the following function written in the C programming language.
void foo (char *a) {
if ( *a && *a != " "){
foo (atl);
putchar (*a) ;
The output of the above function on input "ABCD EFGH" is

**Options:**

A. ABCD EFGH
B. ABCD
C. HGFE DCBA
D. DCBA 2 $ B 3.% C 4.VD

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 7 February Shift 2, `12-PYQ/2015/set-02/question-paper.pdf`

---

### Q.11

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following C program segment.
#include <stdio.h>
int main ()
char s1[7] = "1234", *p;
p = s1 + 2;
*p = '0';
printf("%s" , s1);
}
What will be printed by the program?

**Options:**

A. 12
B. 120400
C. 1204
D. 1034

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.42

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following C program.
#include<stdio.h>
int f1 (void);
int f2 (void);
int f3 (void);
int x = 10;
int main()
int x = 1;
x += f1( ) + f2( ) + f3( ) + f2( );
printf("&d", x);
return 0;
int f1() { int x = 25; xt+; return x;}
int 12() static int x = 50; xtt; return x;}
int f3() { x *= 10; return x};
The output of the program is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.43

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

230

Consider the following C program.
#include<stdio.h>
int main()
tinttpddat3, at4, atl, at2); static int al ] = 110, 20, 30, 40, 50);
int **ptr = pi
ptrtt;
printf("sd%d", ptr-p, **ptr) ;
The output of the program is
Correct Answer :

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.53

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider the following C program:
#include<stdio.h>
int main ()
int i, j, k = 0;
] = 2 * 3 / 4 + 2.0 / 5 + 8 / 5;
k == --i;
for (i = 0; 1 < 5; it+)
switch(i + k)
case 1:
case 2: printf("\nöd", i+k);
default: printf("|n%a" itk);. case 3: printf("\n%d"
, itk);
}
return 0;
The number of times printf statement is executed is_
Correct Answer:

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

### Q.58

**Paper:** GATE 2015 CS, 8 February Shift 1

**Question:**

Consider three software items: Program-X, Control Flow Diagram of Program-Y and Control Flow
Dıagram of Program-Z as shown below
Program-X: Control Flow Diagram of Program-Y:
sumcal (int maxint, int value)
int result=0, i=0;
if (value <0)
value = -value;
while((i<value) AND (result
<= maxint))
i=1+1;
result = result + 1;
if (result <= maxint)
printf (result);
}
else
printf("large");
printf ("end of program");
Control Flow Diagram of Program-Z:
Control Flow Diagram of
Program-X
Control Flow Diagram of
Program-y
The values of McCabe's Cyclomatic complexity of Program-X, Program-Y, and Program-Z
respectively are

**Options:**

A. 4, 4, 7
B. 3, 4, 7
C. 4, 4, 8
D. 4,3, 8

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2015 CS, 8 February Shift 1, `12-PYQ/2015/set-03/question-paper.pdf`

---

## 2014

### Q.10

**Paper:** GATE 2014 CS SET-1

**Question:**

Consider the following program in C language:
#include <stdio.h>
main()
{
int i;
int *pi = &i;
scanf(“%d”,pi);
printf(“%d\n”, i+5);
}
Which one of the following statements is TRUE?

**Options:**

A. Compilation fails.
B. Execution results in a run-time error.
C. On execution, the value printed is 5 more than the address of variable i.
D. On execution, the value printed is 5 more than the integer value entered.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-1, `12-PYQ/2014/set-01/question-paper.pdf`

---

### Q.10

**Paper:** GATE 2014 CS SET-2

**Question:**

Consider the function func shown below:
int func(int num) {
int count = 0;
while (num) {
count++;
num>>= 1;
}
return (count);
}
The value returned by func(435)is __________.

**Options:**

The paper does not print options for this numerical-answer question.

**Type:** NAT

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.11

**Paper:** GATE 2014 CS SET-2

**Question:**

Suppose n and p are unsigned int variables in a C program. We wish to set p to ^{n}C_{3}.
If n is large, which one of the following statements is most likely to set p correctly?

**Options:**

A. p = n * (n-1) * (n-2) / 6;
B. p = n * (n-1) / 2 * (n-2) / 3;
C. p = n * (n-1) / 3 * (n-2) / 2;
D. p = n * (n-1) * (n-2) / 6.0;

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

### Q.34

**Paper:** GATE 2014 CS SET-2

**Question:**

For a C program accessing  X[i][j][k],  the following intermediate code is generated by a
compiler. Assume that the size of an integer is 32 bits and the size of a character is 8 bits.
t0 = i ∗ 1024
t1 = j ∗ 32
t2 = k ∗ 4
t3 = t1 + t0
t4 = t3 + t2
t5 = X[t4]
Which one of the following statements about the source code for the C program is CORRECT?

**Options:**

A. X is declared as “int X[32][32][8]”.
B. X is declared as “int X[4][1024][32]”.
C. X is declared as “char X[4][32][8]”.
D. X is declared as “char X[32][16][2]”.

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2014 CS SET-2, `12-PYQ/2014/set-02/question-paper.pdf`

---

## 2012

### Q.3

**Paper:** GATE 2012 CS Booklet A

**Question:**

What will be the output of the following C program segment?
char inChar = ‘A’ ;
switch ( inChar ) {
case ‘A’ : printf (“Choice A\ n”) ;
case ‘B’ :
case ‘C’ : printf (“Choice B”) ;
case ‘D’ :
case ‘E’ :
default  : printf ( “ No Choice” ) ; }

**Options:**

A. No Choice
B. Choice A
C. Choice A Choice B No Choice
D. Program gives no output as it is erroneous

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

### Q.47

**Paper:** GATE 2012 CS Booklet A

**Question:**

The height of a tree is defined as the number of edges on the longest path in the tree. The function
shown in the pseudocode below is invoked as  height(root) to compute the height of a binary
tree rooted at the tree pointer root.
int height (treeptr n)
{ if (n == NULL) return -1;
if (n  left == NULL)
if (n  right == NULL) return 0;
else return  ;  // Box 1 B1
else { h1 = height (n  left);
if (n  right == NULL) return (1+h1);
else { h2 = height (n  right);
return  ;  // Box 2 B2
}
}
}
The appropriate expressions for the two boxes B1 and B2 are

**Options:**

A. B1: (1+height(n  right))
B. B1: (height(n  right)) B2: (1+max(h1, h2)) B2: (1+max(h1,h2))
C. B1: height(n  right)
D. B1: (1+ height(n  right)) B2: max(h1, h2) B2: max(h1, h2) CS-A 12/20 2012 COMPUTER SCIENCE & INFORMATION TECH. – CS Common Data Questions Common Data for Questions 48 and 49: Consider the following C code segment. int a, b, c = 0; void prtFun(void); main( ) { static int a = 1; /* Line 1 */ prtFun( ); a += 1; prtFun( ); printf(“ \n %d %d ”, a, b); } void prtFun(void) { static int a = 2; /* Line 2 */ int b = 1; a += ++b; printf(“ \n %d %d ”, a, b); }

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2012 CS Booklet A, `12-PYQ/2012/question-paper.pdf`

---

## 2011

### Q.22

**Paper:** GATE 2011 CS Booklet A

**Question:**

What does the following fragment of C program print?
Char c[] = "GATE2011";
char *p = C;
printf("8s" , P + p[3] - p[1]);

**Options:**

A. GATE2011
B. E2011
C. 2011
D. 011 CS-A 5/20 2011 CS

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2011 CS Booklet A, `12-PYQ/2011/question-paper.pdf`

---

## 2009

### Q.18

**Paper:** GATE 2009 CS

**Question:**

Consider the program below:
#include ‹stdio.h>
int fun(int n, int *f_p) {
int t, f;
if (n ‹= 1) {
*f_P = 1;
return 1 ;
}
t = fun (n-1, f_p) ;
f= t + *E_P ;
*fp =t ;
return f ;
}
int main() {
int x = 15; Vino B ma) 2do9x6)
printf ("%d\n", fun (5, &x)) ;
return 0;
}
The value printed is :

**Options:**

A. 6
B. 8
C. 14
D. 15

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2009 CS, `12-PYQ/2009/question-paper.pdf`

---

## 2008

### Q.60

**Paper:** GATE 2008 CS

**Question:**

What is printed by the following Cprogram?
int f (int x, int *py, int **ppz) void main()
int y,z; int c, *b, **a;
**ppz += 1; z = *ppz; c = 4; b = &c; a = &b;
*py += 2; y = *py; printf("%d", f (c,b,a)) ;
x += 3; }
return x+y+z;
}

**Options:**

A. 18
B. 19
C. 21
D. 22

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

### Q.61

**Paper:** GATE 2008 CS

**Question:**

Choose the correct option to fill ?1 and ?2 so that the program below prints an input string in
reverse order. Assume that the input string is terminated by a newline character.
void reverse(void) [|
int c;
if (?1) reverse();
?2
}
main () {
printf("Enter Text"); printf("\n");
reverse(); printf("\n");

**Options:**

A. ?1 is (getchar () != "\n') ?2 is getchar (c);
B. ?1 is (c = getchar()) != "\n') ?2 is getchar (c);
C. ?1 is (c != '\n') ?2 is putchar (c) ;
D. ?1 is ((c = getchar()) != '\n') ?2 is putchar (c);

**Type:** MCQ

**Answer:** VERIFICATION REQUIRED

**Source:** GATE 2008 CS, `12-PYQ/2008/question-paper.pdf`

---

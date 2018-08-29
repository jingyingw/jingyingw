---
title: Coding Theory 101
layout: post
author: Jingying
permalink: /coding-theory-intro/
published: true
date:   2018-08-04 20:18:30
tags:
- coding theory
description: ‘a summer’s worth of coding theory’
categories:
- Coding
---

**Coding theory**

Coding theory is the study of methods for efficient and accurate transfer of information from one place to another. From 1948 by Claude Shannon til now. Hamming codes are golay codes are both perfect.

# Terminology

Digit: 0 or 1

Word: sequence of digits

Length: number of digits in word

Binary channel: channel over which words are transmitted mechanically or otherwise

binary code: A set of words. E.g. a set of length 2 is *C* = {00, 10, 01, 11}.

*block code: *A code having all its words being the same length, 

Code: A binary block code (in the context of this textbook)

Codewords: words that belong to a given code C0, number of codewords in C denoted by |*C*|

Symmetric binary channel(BSC): receives 0 and 1 with equal accuracy; percentage of error does not depend on which digit is transported. Its reliability is a real number p where 0 \<= p \<= 1.

Zero word: a word in Kn with zero as all of its characters.

weight: the number of times the digit 1 occurs in v. denoted wt(v)

# 1 Basics of Coding Theory

**1.1 Transferring information**

Channel is the physical medium over which data travels. E.g. T.V. cables

Noise is undesirable disturbances that cause received information to differ to sent information. E.g. poor typing, using good channels and noise filters can minimize it.

A generic information transfer system is as follows:

 

Encoders and decoders are constructed such that: 

1. Information is fast to encrypt and decrypt

2. Ciphertext is easy to transmit

3. Errors due to noise can be corrected (primary goal, but also a trade-off for other goals)

4. Transfer of information per unit time is maximized

Information is usually sent in binary. 

**1.2 Assumptions regarding the channel**

1.Channel always receives a binary word of the same length as code word, despite it not necessarily being the same as original.

2.The channels always know the beginning of the first word received as per its knowledge of length n.

3.Probability of any digit being wrong in the transmission is independent. Noise is scattered randomly and not in clumps (terminology: bursts) 

4.No channel is perfect - noise is always present, albeit at different intensity.

It is always assumed that a channel of p 1/2 \<= p \<= 1 is used.

**1.3 Correcting and detecting error patterns**

One cannot detect any error if a codeword is received as the original word is not known.

Assuming that no digits are created or lost during transmission, the following simple schemes are used as error detection patterns:

Repetition code: repeating code words of length 2 three times to form: C2 = {000000, 010101, 101010, 111111}. If an erroneous code is received, the closest code word - the code word formed with the least number of digits altered - can be found. In this scheme, it is unique and hence will always correct to the code word intended.

**1.4 Information rate**

Adding digits to code words can improve error correction and detection capabilities. However, this may influence the time.

Information rate is a measurement of the proportion of message in each codeword.

Information rate of code C with length n is:

 

Assuming that 1 ≤ |C| ≤ 2n, information rate ranges between 0(if length is 1) and 1(every word is a codeword).

**1.5 The effects of error correction and detection**

In order to confirm that errors actually occured, retransmission of message might be requested - either:

1. Transmission must be held up until confirmation is received or

2. Messages are stored temporarily until retransmission is requested

Both might be costly and impractical. Incorporating error-correction capabilities into the code will make it more efficient but more difficult to encrypt and decrypt.

It is important to design codes with reasonable information rates, low encoding and decoding costs and some error-correcting or error-detecting capabilities that make the need for retransmission unlikely.

**1.6 Maximum Likelihood Principle**

Given that codeword v is transmitted and word w is received,  is the probability that v sent over BSC with *reliability *p that the word w is received. 

Noise is random.

Hence transmission of every single digit is an independent event. 

If v and w differs in d positions, then n-d is incorrect and d is incorrect. 

 

**Example: **

C is codeword and has length 5. For any v in C, probability that v is w is

  

Let 10101 be in C. Hence

  

If p = 0.9 then

  

Theorem 1.6.3: if bsc ½ \< p \< 1, if v1 and w disagree in d1 positions and v2 and w disagree in d2 positions then

  

**Example:**

If w = 00110 and p = 0.98, which is most likely the one sent - just find smallest d.

**1.7 Algebra**

When K = {0,1} and Kn a set of all binary words of length n, it is a vector space. Its elements are scalar, and it is closed under addition and multiplication. 

If v is sent over BSC and w is received, then v+w is the error pattern of the code as 0 will indicate correct transmission and 1 will indicate correct transmission.

**1.8 Weight and distance**

Hamming weight/weight: the number of times the digit 1 occurs in v. Denoted by wt(v).

Distance is the number of positions in which v and w disagree - will be an integer value. Denoted by d(v,w). 

Distance of v and w is the same as weight of the error pattern u=v+w:

 

Hence we can plug in to reexpress equation for probability of error:

 

where\*\* \*\*\* \* is the *probability of the error pattern u=v+w forming.*

**1.9 Maximum likelihood decoding**

1. Designing a transmitter

One cannot control the quantities:

1. Probability p that digits are transmitted correctly

2. Number of messages that can be transmitted

From this, |Kn| is denoted as 2n.

2. Encoding

A scheme must be found over which to transmit the message. 

1. A length *k* of every word is determined and message must have different binary words satisfying

2. A length *n* of every\*\* code\*\*word is found by determining the numbers of redundancy digits are added to ensure maximum error detection and correction

Transmitter finds the length k of word and then transmits codeword of length n.

3. Decoding

A word w in Kn is received and ran through **maximum likelihood decoding (MLD)** to decide which word v in C was sent. Two types of MLD exist:

1. **Complete maximum likelihood decoding(CMLD):** 

	1. w is decoded as v if there is one and **only** one word v closer to w than any other in C.

	2. **if multiple v closest to w:** arbitrarily select one and decode

2. **Incomplete maximum likelihood decoding(IMLD):** 

	3. w is decoded as v if there is one and **only** one word v closer to w than any other in C.

	4. **if multiple v closest to w:** request a retransmission

	5. Retransmission also requested if w is farther from any in the code

**Example: using IMLD**

For w to be closest to v, d is **minimum**,   is greatest.

Restating theorem for arbitrary v1 and v2:

  

The most likely codeword sent is the one with error pattern with smallest weight.

Supposing |M| = 2, n=3 and C={000,111}, if v = 000, when will IMLD conclude that 000 is sent and incorrectly conclude that 111 was sent:

IMLD will select error of smallest weight of the two error patterns. Will correct incorrectly if the last four are sent.

<table>
  <tr>
    <td>Received w</td>
    <td>Error pattern - 000+w</td>
    <td>Error pattern - 111+w</td>
    <td>Decode v</td>
  </tr>
  <tr>
    <td>000</td>
    <td>000</td>
    <td>111</td>
    <td>000</td>
  </tr>
  <tr>
    <td>100</td>
    <td>100</td>
    <td>011</td>
    <td>000</td>
  </tr>
  <tr>
    <td>010</td>
    <td>010</td>
    <td>101</td>
    <td>000</td>
  </tr>
  <tr>
    <td>001</td>
    <td>001</td>
    <td>110</td>
    <td>000</td>
  </tr>
  <tr>
    <td>110</td>
    <td>110</td>
    <td>001</td>
    <td>111</td>
  </tr>
  <tr>
    <td>101</td>
    <td>101</td>
    <td>010</td>
    <td>111</td>
  </tr>
  <tr>
    <td>011</td>
    <td>011</td>
    <td>100 </td>
    <td>111</td>
  </tr>
  <tr>
    <td>111</td>
    <td>111</td>
    <td>000</td>
    <td>111</td>
  </tr>
</table>


**Criterion for choosing ****_n_**\*\* and C\*\*

1. N should be kept small so information rate is closer to one as longer information take more time to transmit and decode

2. |C| should be small as the IMLD table would be too troublesome to construct if it's too large

3. C should be chosen that probability of MLD functioning is high as many errors in transmission will cause MLD to not work.

**1.10 Reliability of MLD**

For a chosen *n* and *C*, a procedure is used to determine the probability (thetap C,v).

The probability of the IMLD concluding v when it is sent over BSC of probability p.

1. Set L(v) of all *w *in K^n for which v is closest to - the only set of words for which IMLD will conclude correctly that v is sent, found in first row of IMLD tables.

2. thetap C,v) equals the sum of all the probabilities (phip v, w) through w range over L(v). This is the sum of probabilities that v+w occur as an error pattern for a w in K(v)

Advantages of theta

1. Can be used to compare two codes (see criterion for choosing n and C)

Disadvantages of theta

1. Ignores possibility of retransmission if received word has equal distance for two v, leading to anomalies (when thetap(Kn, v)\>thetap(C,u) for any v in Kn and u in C if C is a parity check code formed from Kn,)

2. Lower bound for probability that decoding v correctly.

**Example:** supposing p = 0.9, |M| = 2, n = 3, and C = {000,111}

If v = 000 is sent, what's the probability that IMLD will correctly conclude this after one transmission?

Set L(000) for words closest to v=000 is follows: L(000)={000,100,010,001}

Hence theta = 0.972 (see python function REL)

**1.11 Error-detecting codes**

If v in C is sent and w in Kn is received, error pattern u = v+w.

Any word u in Kn can be an error pattern.

Methodologies

1. C detects the error pattern u to be an error pattern iff v+u is not a codeword v in C.

2. Alternatively, find all error patterns that C does not detect and compare v+w to all words that can be written as a sum of 2 codewords(they cannot be detected)

3. Without manual checking:

	1. Distance of code C is minimum of d(v,w) throughout C which is also smallest wt(v+w). (Euclidian distance)

	2. **Theorem:** A code C of d will detect at least all non-zero error patterns that has weight less than or equal to d-1. There is at least one error pattern of d which C will not detect. (It may still detect error patterns of d or more.

	3. **Proof**: given that u is nonzero error pattern with wt(u)\<= d-1, d(v, v+u) = wt(v+v+u) = wt(u) \< d, as C has distance d v+u will not be in C, hence u is detected. However, d(v,w) = d for some codewords and the same error pattern will not be detected.

	4. This is a d-1 error-detecting code.

T error-detecting code: a code that detects all error patterns of weight maximum t and doesn't detect at least one error pattern of weight t+1.

**1.12 Error-correcting codes**

For v in code C over BSC having u=v+w, IMLD  will correctly conclude that v is sent.

If this occurs for every u regardlesss of codeword transmitted, then C corrects error pattern u.

Code C corrects error pattern u if for all v in C v+u is closest to v.

T-error correcting code: a code that corrects all error patterns of weight maximum t and doesn't correct at least one error pattern of weight t+1. 

**Example: **let C = {000,111}

1. Take error pattern u = 010. For v=000, d(000,v+u)=d(000,010)=1 and d(111,v+u)=d(111,010)=2. Since d is closest in both cases, it corrects.

IMLD table can be used to find. Asterisk means its the unique word - u is corrected if an asterisk is placed beside u in every column of the IMLD table.

A test for error-correcting using distance:

1. Floor function of x is greatest integer less than or equal to x.

2. **Theorem:** A code of distance d will correct all error patterns of weight less than or equal to the floor function of (d-1)/2. There is at least one error pattern of weight 1+ the floor function of (d-1)/2 that C will not correct.

Correcting error patterns of small weight is important.

lecture 1 binary, redundancy and likelihoods

Binary codes rely on modular arithmetic.

**Redundancy**

Too much information space taken to express the meaning intended. Comes with cost of time or more bandwidth.

**Maximum Likelihood Principle**

The word most similar to the erroneous word. 

**Basic Strategy - adding redundancy explicitly and smartly**

Encoding schemes in coding theory try to add redundant bits to help detect errors.

**Scheme 1: do nothing**.\*\* \*\*If p is infinitesmally small and n is large enough, the error range will be small within acceptable ranges.

**Scheme 2: duplicate every letter** Every single error will be uniquely detected in the scheme however not all double errors. If number of errors is odd, they will all be detected. Cost: double the itime and bandwidth. Cannot correct error 1/2

**Scheme 3: add parity checking bit** Cannot corrcet error - achieves same effect but with greater information rate; n/(n+1)

**Scheme 4: repeat three times** can correct single error, only 3+ error can escape.

**Scheme 5: hamming binary code **as follows:

 

 

 

 

Can detect and correct any mistake. Information rate 4/7.

Major problem in coding theory: finding best possible codes for all lengths and information rates.

# 2 linear codes

**2.1 Linear codes**

Linear code:\*\* \*\*a code for which v+w is a word in C whenever v and w are in C. A code which is closed under addition of words. Must contain the zero word. (Zero word being in a code does not guarantee the code is linear)

Advantage of linear code

1. Easy to find distance.

Distance of a linear code = the minimum weight of any non-zero codeword.

1. MLD procedure is simple

1. Encoding is faster and less storage space

2. Probability theta v is fast to calculate

3. East to describe the set of error patterns that it will detect and correct.

The vector space over K consists of scalars K and set of vectors/words Kn. 

A nonempty subset U of vector space V is a subspace if U is closed under vector addition and scalar multiplication. v+w and av are in U for any a = 0 and 1. - since a is binary U is subspace of Kn **iff** U is closed under addition.

**C is a linear code iff C is a subspace of Kn.**

**2.2 Two subspaces**

**Theorem: **For any subset S of Jn, code C = <S>(linear span of S - set of all linear combinations) generated by S consists precisely: the zero word, all words in S, and all sums of two or more words in S.

If v = (a1, a2, an) and w = (b1, b2, …bn) are vectors in Kn, then the **scalar product/dot product** v·w is 

v·w=a1b1+a2b2+…+anbn.

It is a scalar. If dot product is zero, then vectors v and w are orthogonal.

Orthogonal to the set S if v·w=0 for all w in S.

S_|_ is the orthogonal complement of S,\*\* \*\*set of all vectors orthogonal to S.

Any S_|_ is a subspace of its vector space. 

If C = <S>, C_|_=\*\* \*\*S_|_ .

Dual code of C: C_|_

**2.3 Independence, basis, dimension**

A set S={v1,v2…vk} is linearly dependent if:

1. There are scalars a1 a2…ak not all zero such that a1v1 + a2v2… = 0.

Else is independent. Testing involves forming equation using arbitrary scalars. If question forces all scalars to be **zero** then it's independent. If at least an ai is nonzero then S is independent.

**Any set of vectors S =/ 0 contains a largest linearly independent subset.**

Finding the subset:

Given that S = {110, 011, 101, 111} it's linearly dependent.

1(110)+1(011)+1(101)+0(111)=000.

So 101 = 1(110)+1(011)+0(111)

If words are taken in the order given, 101 is the first word that S is dependent on - the first linear combination of the preceding words 110 and 011 in S. If 101 is discarded, then new set S' {110, 011, 111} can be tested for independence and discarding the word that forms a linear combination to reach S’’ until a set is linearly independent. (s’ in this example is linearly independent)

**Any set of vectors containing zero vector is linearly dependent.**

A nonempty subset B of vectors from vspace V is a basis\*\* \*\*for V if both:

1. B spans V / <B> = V

2. B is linearly independent.

Any linearly independent set B is a basis for <B>/V.

A basis can be extracted from S for <S> from any set, if S = 0 then the basis is the empty set.

A vector space can have many bases but all bases has the **same number of elements**. The number of elements in any basis for a vector space is the **dimension** of the space and dimension for Kn is n.

For any vector space V, if {v1, v2,…vk} is a basis then every vector w in V can be expressed as a unique linear combination of the basis vectors with unique scalars a1, a2, ak.

**Any linearly independent subset of a vector space is contained in a basis for the space.**

**Application to linear codes**

If a code C has dimension k and basis {v1, v2, vk}. A word w in C is:

w=a1v1+a2v2…+akvk

For unique ak. Since a could be either 0 or 1, there are 2^k choices for a and hence 2^k words in c.

**Theorem: A linear code of dimension k contains precisely 2k codewords.**

**Theorem: For the linear code generated by a subset S of K^n C=<S>, (dimension of C) +(dimension of C_|_) = n.**

**Theorem: A linear code of dimension k has precisely 1/k!( WTAF???? RETURN AND CHECK!**

**Theorem**

**2.4 Matrices**

An m\*n matrix is is an array of scalars with m rows and n columns.

Two types of elementary row operations on matrix over K:

1. Interchanging two rows

2. Replacing a row by itself plus another row.

Row equivalence: one matrix can be obtained from the other by a sequence of elementary row operators.

A 1 in Matrix M over K is called a leading 1 if there are no 1s to its left in the same row.

A column of M is called a leading column\*\* \*\*if it contains a leading 1.

Row echelon form(REF): zero rows of M are all at the bottom and each leading 1 is to the right of the leading ones in the row above.

Reduced row echelon form(RREF): if each leading column contains exactly one 1 plus def of REF

**Any matrix over K can be put in REF or RREF** - any matrix is row equivalent to a matrix in REF or RREF.

For any given matrix, RREF\*\* is unique\*\* but REFs may be many. 

**2.5 Bases for C=<S> and C_|_**

Algorithmic methods for finding bases for a linear code and its dual.

Let S be a non-empty subset of K^n.

Algorithm 1: 

1. form matrix A whose rows are words in S.

2. Use elementary row operations to find a REF of A.

3. Nonzero rows of the REF forms a basis for C=<S>

Algorithm 2(basis for dual C):

1. Form matrix A whose rows are words in S.

2. Use elementary row operations to find a **RREF** of A.

3. Let G be the k\*n matrix consisting of all nonzero rows of RREF.

4. Let X be the k\*(n-k) matrix obtained from G by deleting leading columns of G

5. Form an N\*(n-k) matrix H by

	1. Place the rows of X in order in rows of H corresponding to the leading columns of G

	2. Place the rows of the (n-k)^2 identity matrix I in the remaining n-k rows of H

1. The columns of H forms a basis for C dual.

Since n-k columns of H are linearly independent, dimensions of Cdual = n-dimensions of C = n-k, and GH = X+X = 0.

**2.6. Generating matrices and encoding**

The rank of matrix over K is number of nonzero rows in any REF of matrix. 

Dimension k of code C is the dimension of C as subspace of Kn.

If C has length n and distance d, then C is an (n,k,d) linear code.

C has length n and dimension k, then any matrix whose rows form a **basis** for C is a generator matrix for C. Must have k rows and n columns and hence rank k.

**Theorem:** A matrix G is a generator matrix for C iff rows of G are linearly independent - iff rank of G is equal to number of rows in G.

Since row equivalent matrices have same rank…

Row equivalence: if one matrix can be changed to the other by a sequence of elementary row operations

**Theorem: **If G is generator matrix for C, then any matrix row equivalent to G is also g.m. for C - any linear code has g.m. in RREF.

**Example: **finding generator matrix for C={0000,1110,0111,1001}

Finding REF/Basis:

0000

1110

0111

1001

1110

0111

1001

0000

1110

0111

0111

1110

0111

0000

0000

Hence G is a generator matrix:

1110

0111 

Finding RREF:

1110

0111

0000

0000

1001

0111

0000

0000

Then G1 is also generator matrix for C.

1001

0111

**Theorem: **Let C be linear code of length n and dimension k. If G is g.m. for C and if u is a word of length k written as a row vector, then v = uG is a work in C since v is linear combination of rows of G - a basis for c.

Since every v in C is a linear combination of basis words(rows of G), then v = uG for some u in K^k.

If u1G = u2G then u1 = u2 since each word is a unique linear combination of words in a basis.

**Theorem: If G is a generator matrix for linear code C of length n and dimension k, then v=uG ranges over all 2^k words in C as u ranges over all 2%k words of length k. C is set of all words uG, for u in K^k. u1G = u2G iff u1 = u2.**

Information of such an nkd code is **k/n**.

**2.7 Parity check matrices**

Parity-check matrix H (X/I)for C: if columns of this matrix forms basis for the dual code. If C has length n and dimension k then since sum of dimensions of C and C dual is n, any parity check matrix will have n rows, n-k columns and rank.

**Theorem:** A matrix H is a parity check matrix for C iff columns of H are linearly independent.

**Theorem: **If H is a parity check matrix for C of length n, then C consists precisely all the words in K^n such that vH = 0.

Theorem: Matrices G and H are generating and parity check matrices respectively for C iff 

1. Rows of G and columns of H are linearly independent,

2. Number of rows of G + number of columns of H = number of columns of G = number of rows of H.

3. GH = 0.

Theorem: H is a parity check matrix of C iff H^T is a generator matrix for C dual.

**2.8 Equivalent codes**

Any k*n matrix G with k\<n whose first k columns form the k*k identity matrix Ik so that G = [Ik, X] automatically has linearly independent rows and also is an RREF.

Hence G is a generator matrix in standard form which generates code C as a systematic code.

Not all linear codes have a generator in standard form. 

Each codeword v in linear code C is equal to uG for one unique word u in K^k. The word u is the message to be sent but rather than transmitting u, it's transmitted as codeword v=uG. If MLD concludes u from uG, then recipient of transmission must recover the original message. If G is in standard form, then:

v = uG = u[IX] = uIuX = [u uX] 

**Theorem: **If C has n and dimension k with g.m. G in standard form, then the first k digits in the codeword v=uG form the word u in K^k.

These k digits are information digits as they contain u, while last n-k digits are redundancy/parity check digits. 

**What if code has no generator matrix in standard form?**

Transform order of codewords in C and obtain a similar code that has many same properties although they are different codes.

If C is any block code of length n, a new block code C' can be obtained by choosing a permutation of n digits then consistently rearranging every word in C in the chosen way. This resultant code C’ is equivalent to C.

**Theorem:** Any linear code C is equivalent to a linear code C' having a generator matrix in standard form.

**2.9 Distance of a linear code**

Distance of linear code is the minimum weight of any nonzero codeword. Distance can also be determined from a parity checking matrix for the code

**Theorem: **Let H be a parity check matrix for a linear code C. C has distane d iff any set of d-1 rows of H is linearly independent and at least one set of d rows of H is linearly dependent.

If v is a word, then vH is a linear combination of exactly wt(V) rows of H. So if v is in C and wt(v)=d, then vH will =0, some d rows will be dependent and wt(v)\>=d.

**Test for linear independence: no two rows of H sum to 000**. If 3 rows sum to 000 they're linearly dependent.

**2.10 Cosets**

If C is a linear code of length n and u is any word of length n, the coset of C determined by u to be the set of all words of the form v+u as u ranges over all words in C. This coset is denoted by C+u.

C+u = {v+u|vEC}

**Example: **Let C = {000,111} and u=101. Then

C+101 = {000+101, 111+101} = {101,010} = C+u

C+010 =C+101.

**Theorem: **Let C be l.c. of length n and u and v be words of length n.

1. If u is in coset C+v. Then C+u = C+v. Each word in a coset determines the coset.

2. The word u is in the coset C+u.

3. If u+v is in C, then u and v are in the same coset.

4. If u +v is not in C, then u and v are in different cosets.

5. Every word in K^n is contained in one and only one coset of c. Either C+u = C+v or they have no words in common.

6. |C+u| = |C| number of words in coset of C is equal to number of words in code C.

7. If C has dimension k, then there are exactly 2^(n-k) different cosets of C and each contains exactly 2^k words.

8. The code C itself is one of its cosets.

**2.11 MLD for linear codes**

Let C be a linear code. If v in C is transmitted and w is received and u =v+w error pattern, then w+u = v is in C so the error pattern u and received word w are in the same coset of C.

Since error patterns for a small weight, the MLD works as follows:

1. Word w is received.

2. Choose word u of least weight in coset C+w

3. Conclude v=w+u was sent.

**Using parity check matrix to find the word of least weight in C**

Let C be linear code of n and k, with H as p.c. matrix for C. For any word w in K^n, the syndrome of w is the word wH in K^(n-k).

 

**Theorem: **Let C be linear code of length n, with H as p.c. matrix for C. Let w and u be words in K^n.

1. wH = 0 iff w is a codeword in C.

2. uH = wH iff w and u are in the same coset of C.

3. If u is the error pattern in w, then uH is the sum of the rows of H that correspond to the positions in which errors occured in transmission.

If no error occurs, then wH = 0 however wH = 0 does not imply no errors occurred since w need not be the codeword sent.

Words in the same coset have the same syndromes, a coset can be identified by its syndrome - the syndrome of any word in that coset.

The 2^(n-k) words of length n-k each in a code of n,k occurs as the syndrome of exactly one of the 2^(n-k) cosets.

**Calculating syndrome of a coset**

Any word w in the coset will give syndrome as wH. The word of least weight is desired to be used as the error pattern. A coset leader is any word of least weight. If there was more than one candidate, one is arbitrarily selected when doing CMLD.

A table that matches the coset leader with the syndrome is a standard decoding array(SDA). A quick way to find SDA given H and d for C generates all error patterns e with wt(e)\<= floor function of (d-1)/2 and computes the syndrome s=eH respectively.

MLD Procedure after finding SDA

1. Receive w and calculate syndrome wH

2. Calculate u from wH = uH to find coset leader.

3. v=w+u is the most likely codeword sent.

# 3 Perfect and Related Codes

**3.1 Some bounds for codes**

Problem: determining how many words a linear code of length n and distance d can have. (Not solved in general)

**nCr(n, t) = **Number of words of length n and weight t.

**Theorem:** If 0 \<= t \<= n and if v is a word of length n, then the number of words of length n of distance at most t from v is precisely

 

If t = n, then it's 2^n.

To find all words of a distance t from fixed word v, add all words of weight t to v as there are nCr(n,t) such words. 

If C is a code of length n and distance 2t+1, then no word w at distance at most t from two different codewords v1 and v2. If d(w, v1)\<= t and d(w, v2)\<=t with v1 /= v2, then 

Which is impossible since minimum distance of C is d. Hence the list of words in K^n  at a distance at most t from a codeword v1 has no codewords in common with the list of words at a distance at most t from a codeword v2.

**Theorem of Hamming Bound:** If C is a code of length n and distance d=2t+1 or 2t+1 then 

|C| ≤ 2^n/(sum(nCr(n,x))) 

This is the Hamming Bound, an upper bound for the # of words in a code. t = Floor[(d-1)/2]

This code will correct all error patterns of weight ≤ t.

**Theorem Singleton bound**: For any nkd linear code, d-1 ≤ n-k.

It is a weaker upper bound than Hamming bound (overestimates more). Mainly used to define maximum distance separable codes

Maximum Distance Seperable Code(MDS):  For C that satisfies

1. a linear nkd code

2. d = n-k+1.

3. Every n-k rows of H are linearly independent

4. Every k columns of G are linearly independent.

The dual of an (n,k,n-k+1) MDS code is an (n,n-k,k+1)MDS code.

**Theorem Gilbert Varshamov Bound:** There exists a linear code of length n dimension k and distance d if  

If n =/ one and d =/ one, then there exists a linear code C of length N and distance at least d  with 

This is a lower bound for the most number of codewords such a code C will have.

**3.2 Perfect codes**

A code C of length n and odd distance d=2t+1 is a perfect code if C attains the Hamming bound of Theorem 3.1.3 exactly (equals). The sum in the Hamming bound must be a power of 2. If it's a perfect code, then each word will decode to a unique codeword.

Any perfect code of length and distance 2t+1 has exactly 2 codewords. Among linear codes there is only 1 such code: repetition code consisting of zero word and the word in which all digits are 1.

If codes are perfect but not very useful, they are trivial perfect codes.

**Theorem1:** IF C is a non-trivial perfect code of length n distance d=2t+1, then either n=23 d=7 or n=2^r-1 for some 2≤r and d=3.

If a linear code of length n has distance d=2t+1, C will correct all error patterns of weight less than or equal to t=(d-1)/2. Every word of length n and weight ≤ t is a coset leader. There are precisely nCr(n,0) + nCr(n,1)…+\*\* \*\*nCr(n,t) such words - precisely the number of cosets if the code is perfect.

**Theorem2: **If C is a perfect code of length n and distance d = 2t+1, then C will correct all error patterns of weight ≤ t and no other error patterns.

Each of the 2^n words in K^n lies within distance t of exactly 1 codeword. 

Perfect t-error correcting code: a perfect code which corrects all error patterns of weight less than or equal to t. The only possible values are t=1 and t=3 by Theorem 1.

**3.3 Hamming codes**

Hamming code of length 2^r-1 (because -1 since minus the zero vector.): A code of length n=2^r-1, 2≤r, having parity check matrix H whose rows consist of all nonzero vectors of length r. Has distance d=3. They are perfect single error-correcting codes.

Since H for a Hamming code C contains all r rows of weight 1, the r columns of H are linearly independent - a Hamming code has dimension 2^r-1-r and contains 2^(2^r-1-r) codewords.

Permuting rows = permuting columns of the generator matrix = gets an equivalent code.

No two rows of H are equal, so no two rows of H are linearly independent - C has distance at least 3. 

**SDA for a Hamming code:**

<table>
  <tr>
    <td>Coset leader u</td>
    <td>Syndrome uH</td>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>I of order (2^r-1)</td>
    <td>H</td>
  </tr>
</table>


**3.4 Extended codes**

Increasing length of a code by one or more digits result in a new code with improved error detection/correction capabilities despite lower information rate.

Let C be a linear code with length n. The code C\* of length n+1 obtained by adding one extra digit in order for each word in new code to have even weight is called the extended code of C.

If the original code C has a k*n G matrix, then C* has k\*(n+1) G matrix

G\* = [G,b]

Where b is the appended column so each row has even weight.

H for C\* is:

	      [H j

H\* =     0 1]

Where j is the n*1 column of all 1s. H* is (n+1)*(n+1-k) matrix. H has rank n-k, last row of H* ensure that H\* has rank n-k+1.

G*H* = [G,b][(H,j)(0,1)] = [GH, Gj+b] = 0

GH =1 and Gj sums the 1s in each row of G. Gj+b = 0, and G*H* = 0.

An extended code is useful only when d is odd for the original.

**3.5 The extended Golay code**

Let B be the 12\*12 matrix

110111000101

101110001011

011100010111

111000101101

110001011011

100010110111

000101101111

001011011101

010110111001

101101110001

011011100011

111111111110

Let G be the 12*24 Matrix G=[I,B] where I is the 12*12 identity matrix. The linear code C with generator matrix G is the extended Golay code\*\* C24\*\*.

1. C24 has length n=24, dimension k=12 and 2^12 = 4096 codewords.

2. H for C24 is [B/I] matrix.

3. Another H for C is [I/B] matrix.

4. Another G for C is [B,I]

5. C24 is self dual. Cdual=C24.

6. Distance of C is 8

7. C24 is a three-error-correcting code.

Why is distance of C =8?

Rows of G are orthogonal, v= ri + rj. ri \* rj = 0.

If dot product is zero, they have an even number of given number of positions in which they equal.

wt(v) = wt(ri) + wt(rj) -2(2x)

The last term is to correct overcounting. 

Since most rows are weight 8, 8+8-4x = 4(4-x)we must show there doesn't exist word of 4, proving minimum weight to be 8.

Proof by contradiction: suppose there exist word of weight 4, but looking it as half, each must have weight greater than 2. But this is a contradiction since wt(u) ≤3.

**3.6 Decoding the extended Golay code.**

wt(u)**≤3**. A comma is used to separa\`te first 12 and last 12 digits, and error pattern is [u1, u2.]

wt(u1)**≤1 **Let s1 be the syndrome of w=v+u using H=[I/B].

S1 = wH = [u1,u2]H = u1+u2 B.

Syndrome for wt(u2)**≤1.**

S2 = wH = [u1,u2]H = u1B+u2

B^2 = I.

S2 = s1B.

**Algorithm for decoding:**

1. Compute syndrome s=wH.

2. If wt(s) ≤3 then u=[s,0]

3. If wt(s+bi) ≤2 for some row bi of B then u = [s+bi, ei]

4. Compute the second syndrome sB.

5. If wt(sB) ≤3 then u=[0,sB]

6. If wt(sB+bi) ≤2 for some row bi of B then u = [ei, sB+bi]

7. If u is not yet determined, then request retransmission.

This algorithm requires at most 26 weight calculations.

The first 12 digits of decoded v contains the message.

**3.7 The Golay code**

Punturing:\*\* \*\*Removing a digit from every word

Golay code is obtained by removing a digit from every word in C24 - the last digit. 

Let Bx be the 12\*11 matrix obtained fro matrix B from deleting the last column.

Let G be the 12\*23 matrix G=[I12, Bx]

Linear code with generator matrix G is the Golay code C23. Has length n=12, k=12, and has 2^12 4096 codewords, distance 7.

1. It's a perfect code

2. Corrects all error patterns of weight 3 or less and no others

3. If a digit is appended to w forming w0 or w1 respectively so that resulting word has odd weight, then resulting word is distance at most 3 from a codeword in C24. Decoding to C using the last algorithm and removing last digit from C gives closest codeword to w in C23

**Algorithm for decoding the Golay code**

1. Form w0 or w1 whichever has the odd weight.

2. Decode wi using algorithm for decoding the e.G. code

3. Remove the last digit from c.

W is a codeword but wi in step 1 is never a codeword(because it has odd weight and a codeword in C24 has even weight) If w is a codeword then syndrome of wi is the last row of H.

4 CYCLIC LINEAR CODES

**4.1 Polynomials and words**

A polynomial of degree n over K is a polynomial a0 + a1x….anx^n where coefficients ai are elements of K. 

The set of all polynomials over K is denoted by K[x]. Elements of K[x] will be denoted by f(x), g(x), p(x) and the degree of f(x) is denoted by deg(f(x)).

**How are they added and multiplied?**

Polynomials over k are added and multiplied usually except

x^k + x^k = 0

Degree of f(x) + g(x) is not necessarily max[deg(f(x)), deg(g(x))}.

**Division algorithm**

Let f(x) and f(x) be in K[x] with h(x) =/ 0. There exist unique polynomials q(x) and r(x) in K[x] such that 

f(x) = q(x)h(x) + r(x)

With r(x) = 0 or deg(r(x)) \< deg(h(x)).

q(x) is the quotient and r(x) is the remainder. 

**Seeing it as a word**

The polynomial f(x) of degree at most n-1 over K can be regarded as the word v=a0a1a2…a(n-1) of length n in K^n.

**A code C of length n can be represented as a set of polynomials over K of degree at most n-1.**

Digits should be numbered from 0 to n-1 for word of length n.

f(x) and p(x) are equivalent modulo H(x) iff:

f(x) mod h(x) = r(x) = p(x) mod h(x)

f(x) = p(x) (modh(x))

**Lemma:** If f(x) **= **g(x)(mod h(x)), then f(x) + p(x) **= **g(x) + p(x) (mod h(x)) and f(x)p(x) **= **g(x)p(x) (mod h(x))

**4.2 Introduction to cyclic codes**

Let v be a word of length n. The cyclic shift pi(v) of v is the word of length n obtained from v by taking the last digit of v and moving it to the beginning, all other digits moving one position to the right.

**A code C is a cyclic code if the cyclic shift of each codeword is also a codeword and also if C is linear.**

**Lemma: **

1. pi(v+w) = pi(v)+pi(w)

2. pi(av) = api(v), a in K={0,1}

Hence, to show that a linear code C is cyclic, it is enough to show that pi(v) is in C for each word v in a basis for C.

**Constructing a cyclic linear code**

We can pick a word v to form a set S consisting of v and all its cyclic shifts, S={v, pi(v), pi^2(v)… pi^(n-1)(v).} and define C to be the linaer span of S, C=<S>. Since C contains basis for C, C must be cyclic.

If a word v and its cyclic shifts form a set S which spans the code C, then v is a generator of the linear cyclic code C. Since every linear cyclic code that contains v must contain S as well, C is the smallest linear cyclic code containing v. A lc code can have many generators.

**Representation of cyclic codes as polynomials**

pi(v) = xv(x) mod 1+x^n.

1 = x^n (mod 1+x^n)

**Lemma:** Let C be a cyclic code and let v be in C. For any polynomial a(x), c(x) = a(x)v(x) mod (1+x^n) is a codeword in C.

Among all non-zero codewords in a linear cyclic code C, there is a unique word g in C such that g(x) has minimum degree. This is the generator polynomial. 

For any codeword c(x) in C, there exists a(x) such that c(x) = a(x)g(x) mod (1+x^n).

There will be no remainder and g(X) is a divisor of every codeword c(x) in C.

**Theorem:** Let C be a cyclic code of length n and let g(x) be the generator polynomial. If n-k = degree(g(x)) then:

1. C has dimension k

2. The codewords corresponding to g(x), xg(x), x^(k-1)g(x) are a basis for C

3. c(x) is in C iff c(x) = a(x)g(x) with degree a(x) \< k. (e,g, g(x) divides every codeword in C(x))

**Theorem: **g(x) is the generator polynomial for a linear cyclic code of length n iff g(x) divides 1+x^n.

The generator polynomial g(x) for the smallest cyclic code of length n containing the word v is the gcd of v(x) and 1+x^n. g(x) = gcd(v(X), 1+x^n)

The standard generator is monic(irrelevant in binary), and has the smallest degree in all the generator polynomials and divides x^n+1

**Finding gcd of two polynomials**

1. Use Euclidean Algorithm.

2. Simple row reduction for cyclic code of length n and dimension n-k:

	1. Takes G and puts it into RREF with last k column as leading columns

	2. The row of minimum degree will be the generator polynomial.

**4.3 Generating and parity check matrices for cyclic codes**

The simplest G is the rows for codewords for the generator polynomial and its first k-1 cyclic shifts:

G=[g(x), xg(x),… x^(k-1) g(x)]

**Message polynomial**

Let C be a linear cyclic code of length n and dimension k (g(x) has degree n-k), The k information digits (a…a(k-1)) can be represented as a polynomial a(x) = a0+a1x+a(k-1)x^(k-1)

Encoding: a(x)g(x) = c(x). Instead of storing the entire k\*n generator matrix, I can only store the generator polynomial.

Decoding: c(x)/g(x).

**Finding parity check matrix**

wH = 0 iff w is a codeword. w(x) = c(x) + e(x) with e(x) being the error polynomial.

Syndrome polynomial is s(x) = w(x) mod g(x) assuming g(x) has degree n-k, s(x) will have degree less than n-k and will correspond to binary word s of length n-k.

s(x) = e(x) mod g(x) - dependent only on the error.\*\* \*\*

H is the matrix for which the ith row ri is the word of length n-k corresponding to ri(x) = x^i mod g(x).

**4.4 Finding cyclic codes**

A factor of 1+x^n with degree n-k must be found in order to construct n and k lcc.

Finding all factors of 1+x^n will allow one to find all linear cyclic codes of a given length n. - all the generators. This means finding all irreducible factors.

A polynomial f(x) in K[x] of degree at least 1 is irreducible If its not the product of 2 polynomials in K[x] both of degree at least 1. Finding the irreducible factors is finding all the factors of 1+x^n.

Factor 1 of 1+x^n has degree 0, generates a cyclic code of dimension n - K^n, proving that K^n is cyclic. 

{0} is also cyclic and its generator is 0.

K^n and {0} are improper cyclic codes. Everything else is a proper cyclic code.

**Theorem:** If n=s2^r then 1+x^n = (1+x^s)^(2^r)

Let n=s2^r. If s is odd and 1+x^s be the product of z irreducible polynomials, then there are (2^r+1)^z -1 proper linear cyclic codes of length n.

**Finding all cyclic codes**

One can find all cyclic codes or equivalently factor 1+x^n by the following algorithm assuming n is odd.

1. Generate all polynomials I(x) mod(1+x^n) such that I(x) = I(x)^2mod(1+x^n) - they are idempotent polynomials. If u(x) and v(x) are idempotent, their sum and product are also idempotent.

2. Partitioning Zn = {0,1, … n-1} into classes as follows: Ci = [s = 2^j\*imodn | j = 0,1,…r] where 1 = 2^r mod n.

**Theorem: **Every cyclic code contains a unique idempotent polynomial which generates the code. G(x) = gcd(t(x)g(x), 1+x^n)

**4.5 Dual cyclic codes**

Dual codes are also cyclic.

\**Lemma: \*\* Let a \<-\> a(x), b\<-\> b(x) and b' \<-\> b’(x) = x^n*b(x^-1) mod 1+x^n, then a(x)b(x)mod1+x^n = 0 iff pi^k(a)\* b’ = 0 for k = 0,1,n-1. B’ being the dual of the code generated by K.

**Theorem:** If C is a linear cyclic code of length n and dimension k with generator g(x) and if 1+x^n = g(x)h(x) then C dual is a cyclic code of dimension n-k with generator x^k\*h(x^-1).

If any codeword is given, how would you find the standard generator polynomial?

C = p(x) g(x) mod x^n+1.

The degree of C is smaller than n.

x^n+1 / 

**Given n, can you tell how many cyclic codes there are?**

Factor into irreducible polynomials and then summing nCr(r,i) i=0.

nCr(r,i) = 2^r.

Or…

1.Think that each irreducible factor will either appear or not appear in the generator.

2. Then there are total of 2^r choices.

Cyclic codes are fundamental in Algebraic Coding Theory.

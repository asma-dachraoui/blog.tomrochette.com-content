à---
title: Thomas Cover - Elements of Information Theory - 2006
created: 2017-05-26
taxonomy:
  category: [Artificial General Intelligence]
  status: in progress
---

## Context

## Learned in this study

## Things to explore

# Overview

# Pre-requisites
* Mathematics
	* Statistics
		* Random variables
		* Conditional probabilities
		* Mass function
	* Functions
	* Intervals
	* Derivatives
	* Series
		* Taylor series

# Notes
## Chapter 1 - Introduction and Preview
* Information theory answers two fundamental questions in communication theory:
	* What is the ultimate data compression (answer: the entropy $H$)
	* What is the ultimate transmission rate of communication (answer: the channel capacity $C$)
* The complexity of a string of data can be defined by the length of the shortest binary computer program for computing the string
* We consider Kolmogorov complexity to be more fundamental than Shannon entropy
* One can think about computational complexity (time complexity) and Kolmogorov complexity (program length or descriptive complexity) as two axes corresponding to program running time and program length. Kolmogorov complexity focuses on minimizing along the second axis, and computational complexity focuses on minimizing along the first axis

### 1.1 Preview of the Book
* The entropy of a random variable X with a probability mass function p(x) is defined by
$$
H(X) = - \sum_x p(x)\log_2 p(x)
$$
* Logarithm base 2, measures the entropy in bits
* The entropy is a measure of the average uncertainty in the random variable
* It is the number of bits on average required to describe the random variable
* We can define conditional entropy $H(X|Y)$, which is the entropy of a random variable conditional on the knowledge of another random variable. The reduction in uncertainty due to another random variable is called the mutual information
* For two random variables X and Y this reduction the mutual information
$$
I(X; Y) = H(X) - H(X|Y) = \sum_{x,y} p(x, y)\log \frac{p(x, y)}{p(x)p(y)}
$$
* A communication channel is a system in which the output depends probabilistically on its input. It is characterized by a probability transition matrix $p(y|x)$ that determines the conditional distribution of the output given the input. For a communication channel with input $X$ and output $Y$, we can define the capacity $C$ by
$$
C = \max_{p(x)} I(X; Y)
$$

## Chapter 2 - Entropy, Relative Entropy and Mutual Information
### 2.1 Entropy
* Let $X$ be a discrete random variable with alphabet $\mathcal{X}$ and probability mass function $p(x) = \text{Pr}\{X = x\}, x \in \mathcal{X}$
* The entropy $H(X)$ of a discrete random variable $X$ is defined by
$$
H(X) = - \sum_{x \in \mathcal{X}} p(x) \log p(x)
$$
* Some of the basic properties of entropy
	* It is a concave function of the distribution
	* Equals 0 when p = 0 or 1

### 2.2 Joint Entropy and Conditional Entropy
* The joint entropy $H(X, Y)$ of a pair of discrete random variable $(X, Y)$ with a joint distribution $p(x, y)$ is defined as
$$
H(X, Y) = - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(x, y)
$$
which can also be expressed as
$$
H(X, Y) = -E \log p(X, Y)
$$
* If $(X, Y) \sim p(x, y)$, the conditional entropy $H(Y|X) is
$$
H(Y|X) = -E \log p(Y|X)
$$
$$
H(X, Y) = H(X) + H(Y|X)
$$
$$
\log p(X, Y) = \log p(X) + \log p(Y|X)
$$
$$
H(X, Y|Z) = H(X|Z) + H(Y|X, Z)
$$

### 2.3 Relative Entropy and Mutual Information
* The relative entropy is a measure of the distance between two distributions
* The relative entropy or Kullback-Leibler distance between two probability mass functions $p(x)$ and $q(x)$ is defined as
$$
\begin{split}
D(p||q) &= \sum_{x \in \mathcal{X}} p(x) \log \frac{p(x)}{q(x)} \\
&= E_p \log \frac{p(X)}{q(X)}
\end{split}
$$
* Mutual information is a measure of the amount of information that one random variable contains about another random variable
* It is the reduction in the uncertainty of one random variable due to the knowledge of the other
* Consider two random variables $X$ and $Y$ with a joint probability mass function $p(x, y)$ and marginal probability mass function $p(x)$ and $p(y)$. The mutual information $I(X; Y)$ is the relative entropy between the joint distribution and the production distribution $p(x)p(y)$
$$
\begin{split}
I(X; Y) &= \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log \frac{p(x, y)}{p(x)p(y)} \\
&= D(p(x, y)||p(x)p(y)) \\
&= E_{p(x, y)} \log \frac{p(X, Y)}{p(X)p(Y)}
\end{split}
$$

### 2.4 Relationship Between Entropy and Mutual Information
* We can rewrite the definition of mutual information $I(X; Y)$ as
$$
I(X; Y) = H(X) - H(X|Y)
$$
* Thus, the mutual information $I(X; Y)$ is the reduction in the uncertainty of $X$ due to the knowledge of $Y$
* By symmetry, it also follows that
$$
I(X; Y) = H(Y) - H(Y|X)
$$
$$
I(X; Y) = I(Y; X)
$$
* Since $H(X, Y) = H(X) + H(Y|X)$
$$
I(X; Y) = H(X) + H(Y) - H(X, Y)
$$
$$
I(X; X) = H(X) - H(X|X) = H(X)
$$
* Thus, the mutual information of a random variable with itself is the entropy of the random variable

### 2.5 Chain Rules For Entropy, Relative Entropy, and Mutual Information
* Let $X_1, X_2, \dots, X_n$ be drawn according to $p(x_1, x_2, \dots, x_n)$. Then
$$
H(X_1, X_2, \dots, X_n) = \sum_{i=1}^n H(X_i|X_{i-1}, \dots, X_1)
$$
* The conditional mutual information of random variables $X$ and $Y$ given $Z$ is defined by
$$
\begin{split}
I(X; Y|Z) &= H(X|Z) - H(X|Y, Z) \\
&= E_{p(x, y, z)} \log \frac{p(X, Y|Z)}{p(X|Z)p(Y|Z)}
\end{split}
$$
$$
I(X_1, X_2, \dots, X_n; Y) = \sum_{i=1}^n I(X_i; Y|X_{i-1}, X_{i-2}, \dots, X_1)
$$
$$
D(p(x, y)||q(x, y)) = D(p(x)||q(x)) + D(p(y|x)||q(y|x))
$$

### 2.6 Jensen's Inequality and its Consequences
* A function $f(x)$ is said to be convex over an interval $(a, b)$ if for every $x_1, x_2 \in (a, b)$ and $0 \le \lambda \le 1$
$$
f(\lambda x_1 + (1 - \lambda)x_2) \le \lambda f(x_1) + (1 - \lambda) f(x_2)
$$
* A function is said to be strictly convex if equality holds only if $\lambda = 0$ or $\lambda = 1$
* A function $f$ is concave if $-f$ is convex
* If the function $f$ has a second derivative that is non-negative (positive) over an interval, the function is convex (stricly convex) over that interval
* (Jensen's inequality) If $f$ is a convex function and $X$ is a random variable
$$
Ef(X) \ge f(EX)
$$
* Moreover, if $f$ is strictly convex, the equality implies that $X = EX$ with probability 1
* (Information inequality) Let $p(x)$, $q(x)$, $x \in \mathcal{X}$, be two probability mass functions. Then
$$
D(p||q) \ge 0
$$
with equality if and only if $p(x) = q(x)$ for all $x$
* (Nonnegativity of mutual information) For any two random variables, $X$, $Y$,
$$
I(X; Y) \ge 0
$$
with equality if and only if $X$ and $Y$ are independent
$$
D(p(y|x)||q(y|x)) \ge 0
$$
with equality if and only if $p(y|x) = q(y|x)$ for all $y$ and $x$ such that $p(x) > 0$
$$
I(X; Y|Z) \ge 0
$$
with equality if and only if $X$ and $Y$ are conditionally independent given Z
* (Conditioning reduces entropy)(Information can't hurt)
$$
H(X|Y) \le H(X)
$$
with equality if and only if $X$ and $Y$ are independent

### 2.8 Data-Processing Inequality
* The data processing inequality can be used to show that no clever manipulation of the data can improve the inferences that can be made from the data
* Random variables $X$, $Y$, $Z$ are said to form a Markov chain in that order (denoted $X \rightarrow Y \rightarrow Z$) if the conditional distribution of $Z$ depends only on $Y$ and is conditionally independent of $X$. Specifically, $X$, $Y$, $Z$ form a Markov chain $X \rightarrow Y \rightarrow Z$ if the joint probability mass function can be written as
$$
p(x, y, z) = p(x)p(y|x)p(z|y)
$$
* Some simple consequences are as follows:
	* $X \rightarrow Y \rightarrow Z$ if and only if $X$ and $Z$ are conditionally independent given $Y$
	* $X \rightarrow Y \rightarrow Z$ implies that $Z \rightarrow Y \rightarrow X$
	* If $Z = f(Y)$, then $X \rightarrow Y \rightarrow Z$
* If $X \rightarrow Y \rightarrow Z$, then $I(X; Y) \ge I(X; Z)$
* If $Z = g(Y)$, we have $I(X; Y) \ge I(X; g(Y))$
	* Thus functions of the data Y cannot increase the information about X

### 2.9 Sufficient Statistics
* A function $T(X)$ is said to be a sufficient statistic relative to the family $\{f_\theta(x)\}$ if $X$ is independent of $\theta$ given $T(X)$ for any distribution on $\theta$
* A statistic $T(X)$ is a minimal sufficient statistic relative to $\{f_\theta(x)\}$ if it is a function of every other sufficient statistic $U$
	* A minimal sufficient statistic maximally compresses the information about $\theta$ in the sample
	* Other sufficient statistics may contain additional irrelevant information

### 2.10 Fano's Inequality
* Let $P_e = \text{Pr}\{\hat{X}(Y) \ne X\}$. Then
$$
H(P_e) + P_e \log |\mathcal{X}| \ge H(X|Y)
$$
* If $X$ and $X'$ are independent and identically distributed, then
$$
\text{Pr}(X = X') \ge 2^{-H(X)}
$$

## Chapter 3 - Asymptotic Equipartition Property
-

## Chapter 4 - Entropy Rates of a Stochastic Process
### 4.1 Markov Chains
* A stochastic process is said to be stationary if the joint distribution of any subset of the sequence of random variables is invariant with respect to shifts in the time index; that is
$$
\text{Pr}\{X_1 = x_1, X_2 = x_2, \dots, X_n = x_n\} = \text{Pr}\{X_{1+l} = x_1, X_{2+l} = x_2, \dots X_{n+l} = x_n\}
$$
for every $n$ and every shift $l$ and for all $x_1, x_2, \dots, x_n \in \mathcal{X}$
* A discrete stochastic process $X_1, X_2, \dots$ is said to be a Markov chain or a Markov process if for $n = 1, 2, \dots$
$$
\text{Pr}(X_{n+1} = x_{n+1} | X_n = x_n, X_{n-1} = x_{n-1}, \dots, X_1 = x_1) = \text{Pr}(X_{n+1} = x_{n+1} | X_n = x_n)
$$
for all $x_1, x_2, \dots, x_n, x_{n+1} \in \mathcal{X}$
* The Markov chain is said to be time invariant if the conditional probability $p(x_{n+1}|x_n)$ does not depend on $n$; that is, for $n = 1, 2, \dots$
$$
\text{Pr}\{X_{n+1} = b | X_n = a\} = \text{Pr}\{X_2 = b | X_1 = a\}
$$
for all $a, b \in \mathcal{X}$

### 4.2 Entropy Rate
* The entropy of a stochastic process $\{X_i\}$ is defined by
$$
H(\mathcal{X}) = \lim_{n \rightarrow \infty} \frac{1}{n} H(X_1, X_2, \dots, X_n)
$$
when the limit exists
$$
H'(\mathcal{X}) = \lim_{n \rightarrow \infty} H(X_n | X_{n-1}, X_{n-2}, \dots, X_1)
$$
* For a stationary stochastic process, the limits exists and are equal:
$$
H(\mathcal{X}) = H'(\mathcal{X})
$$
$H'(\mathcal{X})$ is the conditional entropy on the last random variable given the past

### 4.3 Example: Entropy Rate of a Random Walk on a Weighted Graph
* It is easy to see that a stationary random walk on a graph is time-reversible; that is, the probability of any sequence of states is the same forward or backward
$$
\text{Pr}(X_1 = x_1, X_2 = x_2, \dots, X_n = x_n) = \text{Pr}(X_n = x_1, X_{n-1} = x_2, \dots, X_1 = x_n)
$$
* Any time-reversible Markov chain can be represented as a random walk on an undirected weighted graph

## Chapter 5 - Data Compression
### 5.1 Examples of Codes
* A source code $C$ for a random variable $X$ is a mapping from $\mathcal{X}$, the range of $X$, to $\mathcal{D}^*$, the set of finite-length strings of symbols from a $D$-ary alphabet. Let $C(x)$ denote the codeword corresponding to $x$ and let $l(x)$ denote the length of $C(x)$
* The expected length $L(C)$ of a source code $C(x)$ for a random variable $X$ with probability mass function $p(x)$ is given by
$$
L(C) = \sum_{x \in \mathcal{X}} p(x)l(x)
$$
* A code is said to be nonsingular if every element of the range of $X$ maps into a different string in $\mathcal{D}^*$; that is
$$
x \ne x' \Rightarrow C(x) \ne C(x')
$$
* The extension $C^*$ of a code $C$ is the mapping from finite-length strings of $\mathcal{X}$ to finite-length strings of $\mathcal{D}$, defined by
$$
C(x_1x_2x\cdots x_n) = C(x_1)C(x_2)\cdots C(x_n)
$$
where $C(x_1)C(x_2)\cdots C(x_n)$ indicates concatenation of the corresponding codewords
* A code is called uniquely decodable if its extension is non-singular
* A code is called a prefix code or an instantaneous code if no codeword is a prefix of any other codeword
	* An instantaneous code is a self-punctuating code

### 5.2 Kraft Inequality
* For any instantaneous code (prefix code) over an alphabet of size D, the codeword lengths $l_1, l_2, \dots, l_m$ must satisfy the inequality
$$
\sum_i D^{-l_i} \le 1
$$
Conversely, given a set of codeword lengths that satisfy this inequality, there exists an instantaneous code with these word lengths
* (Extended Kraft Inequality) For any countably infinite set of codewords that form a prefix code, the codeword lengths satisfy the extended Kraft inequality
$$
\sum_{i=1}^\infty D^{-l_i} \le 1
$$
Conversely, given any $l_1, l_2, \dots$ satisfying the extended Kraft inequality, we can construct a prefix code with these codeword lengths

### 5.3 Optimal Codes
* The expected length L of any instantaneous D-ary code for a random variable X si greater than or equal to the entropy $H_D(X)$; that is
$$
L \ge H_D(X)
$$
with equality if and only if $D^{-l_i} = p_i$
* A probability distribution is called $D$-adic if each of the probabilities is equal to $D^{-n}$ for some $n$, thus we have equality in the (previous) theorem if and only if the distribution of $X$ is $D$-adic

### 5.4 Bounds on the Optimal Code Length
* Let $l_1^*, l_2^*, \dots, l_m^*$ be optimal codeword lengths for a source distribution $p$ and a $D$-ary alphabet, and let $L^*$ be the associated expected length of an optimal code ($L^* = \sum p_i l_i^*$). Then
$$
H_D(X) \le L^* < H_D(X) + 1
$$
* The minimum expected codeword length per symbol satisfies
$$
\frac{H(X_1, X_2, \dots, X_n)}{n} \le L_n^* < \frac{H(X_1, X_2, \dots, X_n)}{n} + \frac{1}{n}
$$
Moreover, if X_1, X_2, \dots, X_n is a stationary stochastic process,
$$
L_n^* \rightarrow H(\mathcal{X})
$$
where $H(\mathcal{X})$ is the entropy rate of the process
* (Wrong code) The expected length under $p(x)$ of the code assignment $l(x) = \left\lceil \log \frac{1}{q(x)} \right\rceil$ satifies
$$
H(p) + D(p || q) \le E_pl(X) < H(p) + D(p || q) + 1
$$

### 5.5 Kraft Inequality for Uniquely Decodable Codes
* (McMillan) The codeword lengths of any uniquely decodable $D$-ary code must satisfy the Kraft inequality
$$
\sum D^{-l_i} \le 1
$$
Conversely, given a set of codeword lengths that satisfy this inequality, it is possible to construct a uniquely decodable code with these codeword lengths

### 5.8 Optimality of Huffman Codes
* It is important to remember that there are many optimal codes: inverting all the bits or exchanging two codewords of the same length will give another optimal code
* For any distribution, there exists an optimal instantaneous code (with minimum expected length) that satisfies the following properties
	* The length are ordered inversely with the probabilities (i.e., if $p_j > p_k$, then $l_j \le l_k$)
	* The two longest codewords have the same length
	* Two of the longest codewords differ only in the last bit and correspond to the two least likely symbols
* Shannon code
$$
l_i = \left\lceil \log_D \frac{1}{p_i} \right\rceil
$$
$$
H_D(X) \le L < H_D(X) + 1
$$
* Huffmann code
$$
L^* = \min_{\sum D^{-l_i} \le 1} \sum p_i l_i
$$
$$
H_D(X) \le L^* < H_D(X) + 1
$$
* Wrong code: $X \sym p(x), l(x) = \left\lceil \log \frac{1}{q(x)} \right\rceil, L = \sum p(x)l(x)
$$
H(p) + D(p||q) \le L < H(p) + D(p||q) + 1
$$

## Chapter 6 - Gambling and Data Compression
### 6.4 The Entropy of English
* The entropy of the zeroth-order model is log 27 = 4.76 bits (27 => 26 letters + space)
* The first-order model gives an estimate of the entropy of 4.03 bits per letter, while the fourth-order model gives an estimate of 2.8 bits per letter

* Doubling rate
$$
W(\textbf{b}, \textbf{p}) = E(\log S(X)) = \sum_{k=1}^m p_k \log b_k o_k
$$
* Optimal doubling rate
$$
W^*(\textbf{p}) = \max_{\textbf{b}} W(\textbf{b}, \textbf{p})
$$
* Proportional gambling is log-optimal
$$
W^*(\textbf{p}) = \max_{\textbf{b}} W(\textbf{b}, \textbf{p}) = \sum p_i \log o_i - H(\textbf{p})
$$
is achieved by $\textbf{b}^* = \textbf{p}$
* Growth rate: Wealth grows as $S_n \doteq 2^{nW^*(\textbf{p})}$
* Conservation law: For uniform fair odds,
$$
H(\textbf{p}) + W^*(\textbf{p}) = \log m
$$
* Side information: In a horse race $X$, the increase $\Delta W$ in doubling rate due to side information $Y$ is
$$
\Delta W = I(X; Y)
$$

## Chapter 7 - Channel Capacity
* We define a discrete channel to be a system consisting of an input alphabet $\mathcal{X}$ and output alphabet $\mathcal{Y}$ and a probability transition matrix $p(y|x)$ that expresses the probability of observing the output symbol $y$ given that we send the symbol $x$
* The channel is said to be memoryless if the probability distribution of the output depends only on the input at that time and is conditionally independent of previous channel inputs or outputs
* We define "information" channel capacity of a discrete memoryless channel as
$$
C = \max_{p(x)} I(X; Y)
$$

### 7.2 Symmetric Channels
* A channel is said to be symmetric if the rows of the channel transition matrix $p(y|x)$ are permutations of each other and the columns are permutations of each other
* A channel is said to be weakly symmetric if every row of the transition matrix $p(\cdot|x)$ is a permutation of every other row and all the column sums $\sum_x p(y|x)$ are equal
* For a weakly symmetric channel,
$$
C = \log|\mathcal{Y}| - H(\text{row of the transition matrix})
$$
and this is achieved by a uniform distribution on the input alphabet

### 7.3 Properties of Channel Capacity
* $C \ge 0$ since $I(X; Y) \ge 0$
* $C \le \log|\mathcal{X}|$ since $C = \max I(X; Y) \le \max H(X) = \log|\mathcal{X}|$
* $C \le \log|\mathcal{Y}|$ for the same reason
* $I(X; Y)$ is a continuous function of $p(x)$
* $I(X; Y)$ is a concave function of $p(x)$

### 7.5 Definitions
* A discrete channel, denoted by $(\mathcal{X}, p(y|x), \mathcal{Y})$, consists of two finite sets $\mathcal{X}$ and $\mathcal{Y}$ and a collection of probability mass functions $(y|x)$, one for each $x \in \mathcal{X}$, such that for every $x$ and $y$, $p(y|x) \ge 0$, and for every $x$, $\sum_y p(y|x) = 1$, with the interpretation that $X$ is the input and $Y$ is the output of the channel
* The n-th extension of the discrete memoryless channel (DMC) is the channel $(\mathcal{X}^n, p(y^n|x^n), \mathcal{Y}^n)$ where
$$
p(y_k|x^k, y^{k-1}) = p(y_k|x_k), k = 1, 2, \dots, n
$$
* An $(M, n)$ code for the channel $(\mathcal{X}, p(y|x), \mathcal{Y})$ consists of the following:
	* An index set $\{1, 2, \dots, M\}$
	* An encoding function $X^n$: $\{1, 2, \dots, M\} \rightarrow \mathcal{X}$, yielding codewords $x^n(1), x^n(2), \dots, x^n(M)$. The set of codewords is called the codebook
	* A decoding function
$$
g: \mathcal{Y}^n \rightarrow \{1, 2, \dots, M\}
$$
which is a deterministic rule that assigns a guess to each possible received vector
* The rate $R$ of an $(M, n)$ code is
$$
R = \frac{\log M}{n} \text{bits per transmission}
$$
* A rate $R$ is said to be achievable if there exists a sequence of $(\left\lceil 2^{nR} \right\rceil, n)$ codes such that the maximal probability of error $\lambda^{(n)}$ tends to 0 as $n \rightarrow \infty$
* The capacity of a channel is the supremum of all achievable rates

### 7.6 Jointly Typical Sequences
* The set $A_\epsilon^{(n)}$ of jointly typical sequences $\{x^n, y^n\}$ with respect to the distribution $p(x, y)$ is the set of $n$-sequences with empirical entropies $\epsilon$-close to the true entropies
$$
A_\epsilon^{(n)} = \left\{(x^n, y^n) \in \mathcal{X}^n \times \mathcal{Y}^n : \\
\left|\frac{1}{n}\log p(x^n) - H(x)\right| < \epsilon, \\
\left|\frac{1}{n}\log p(y^n) - H(Y)\right| < \epsilon, \\
\left|\frac{1}{n}\log p(x^n, y^n) - H(X, Y)\right| < \epsilon\right\} \\
$$
where
$$
p(x^n, y^n) = \prod_{i=1}^n p(x_i, y_i)
$$

### 7.7 Channel Coding Theorem
* Channel coding theorem: For a discrete memoryless channel, all rates below capacity $C$ are achievable. Specifically, for every rate $R < C$, there exists a sequence of $(2^{nR}, n)$ codes with maximum probability of error $\lambda^{(n)} \rightarrow 0$.
	* Conversely, any sequences of $(2^{nR}, n)$ codes with $\lambda^{(n)} \rightarrow 0$ must have $R \le C$

### 7.9 Fano's Inequality and the Converse to the Coding Theorem
* Strong converse: for rates above capacity, the probability of error goes exponentially to 1
* At rates below capacity $P_e^{(n)} \rightarrow 0$ exponentially, and at rates above capacity $P_e^{(n)} \rightarrow 1$ exponentially

### 7.10 Equality in the Converse to the Channel Coding Theorem
* A capacity-achieving zero-error code has distinct codewords and the distribution of the $Y_i$'s must be i.i.d. with
$$
p^*(y) = \sum_x p*(x)p(y|x)
$$
the distribution on $Y$ induced by the optimum distribution on $X$

### 7.11 Hamming Codes
* The object of coding is to introduce redundancy so that even if some of the information is lost or corrupted, it will still be possible to recover the message at the receiver
* Obvious coding scheme: repeat information (0 -> 00000, 1 -> 11111), 3 bits out of 5 implies the predicted bit
* Parity check code: With a block of $n-1$ information bits, we choose the $n$th bit so that the parity of the entire block is 0 (the number of 1's in the block is even)

# See also

# References
* Thomas, Joy A., and Thomas M. Cover. Elements of information theory. John Wiley & Sons, 2006.
#From_321 #From_342
# The Analysis Framework 
## Measuring an Input's Size
- Wow, input size effects the time of an algorithm. We use $n$ and others to denote the size of an input.
- If possible, measure size by the number of bits in the $n$’s binary representation: $b=\lfloor(log_{2}n)\rfloor+1$.
## Units for Measuring Running Time
- Measuring by actual time (i.e. seconds) depends on external factors.
- A way is to count the amount of time the **basic operation** has run.
	- i.e. comparing keys is the basic operation for sorting algorithm
- A reasonable estimate: $T(n)\approx c_{op}*C(n)$
	- The running time of a program with this algorithm $\approx$ the time of a basic operation on a particular computer * the number of times the basic operation is executed.
	- $c_{op}$ is making it an estimate. Removing it to focus on $C(n)$'s **order of growth**
## Order of Growth
- $logn$, $n^{1/2}$, $n$, $nlogn$, $n^2$, $n^3$, $2^n$, $n!$
- ![[Pasted image 20221002182814.png | 250]]
## Worst-Case, Best-Case, and Average-Case Efﬁciencies
- [[372 - Computer Architecture/Week 01 - Machine-Level Representation of Programs/Class#Sequential Search|Class Notes]]
- Sequential Search (input size $n$)
	- $C_{\text{worst}}(n) = n$ (no match)
	- $C_{\text{best}}(n) = 1$ (first try)
	- $C_{\text{avg}}(n) = \frac{p(n+1)}{2}+n(1-p)$ (390 probability, where $(0\leq{q}\leq1)$)
		- Not trivial to find
- Amortized Algorithms [Lecture 18: Amortized Algorithms (cornell.edu)](http://www.cs.cornell.edu/courses/cs312/2006sp/lectures/lec18.html)
	- "amortized analysis is a worst case analysis, but for a sequence of operations, rather than for individual operations."
	- (more in Chapter 9)
# Asymptotic Notations and Basic Efﬁciency Classes 
- [[372 - Computer Architecture/Week 01 - Machine-Level Representation of Programs/Class#Asymptotic Notation|Class Notes]]
- Let $t(n)$ & $g(n)$ be nonnegative functions defined on the set of natural numbers.
## $O$-Notation
- A function $t(n)$ is said to be in $O(g(n))$, denoted $t(n) \in O(g(n))$, if $t(n)$ is bounded **above** by some constant multiple of $g(n)$ for all large $n$, i.e., if there exist some positive constant $c$ and some non-negative integer $n_0$ such that $t(n) \leq cg(n) \text{ for all } n \geq n_0$.
	- Chinny 321 was $c$ & $k$
## $\Omega$-Notation
- A function $t(n)$ is said to be in $\Omega(g(n))$, denoted $t(n) \in \Omega(g(n))$, if $t(n)$ is bounded **below** by some constant multiple of $g(n)$ for all large $n$, i.e., if there exist some positive constant $c$ and some non-negative integer $n_0$ such that $t(n) \geq cg(n) \text{ for all } n \geq n_0$.
## $\Theta$-Notation
- A function $t(n)$ is said to be in $\Omega(g(n))$, denoted $t(n) \in \Omega(g(n))$, if $t(n)$ is bounded **above & below** by some constant multiple of $g(n)$ for all large $n$, i.e., if there exist some positive constant $c_1$ & $c_2$ and some non-negative integer $n_0$ such that $c_{2}g(n) \leq t(n) \leq c_{1}g(n) \text{ for all } n \geq n_0$.
## A Theorem
- If $t_{1}(n) \in O(g_{1}(n))$ & $t_{2}(n) \in O(g_{2}(n))$ then $t_{1(n)}+ t_{2(n)}\in O(\max\{{g_{1}(n),g_{2}(n)}\})$
	- $O$, $\Omega$, and $\Theta$
	- Proof: ![[Pasted image 20221002175655.png | 20]]
	- implies that the algorithm’s overall efﬁciency is determined by the part with a higher order of growth, i.e., its least efﬁcient part
## Comparing Orders of Growth with Limits 
- ![[Pasted image 20221002181836.png | 450]]
	- use L'Hopital Rule: $\lim_{n\to\infty}\frac{t(n)}{g(n)}=\lim_{n\to\infty}\frac{t'(n)}{g'(n)}$
	- use Stirling's formula for !: $n!\approx \sqrt{2\pi n}(\frac{n}{e})^n$
	- 3 Ex: ![[Pasted image 20221002182046.png | 10]]  ![[Pasted image 20221002182646.png | 20]]
# Mathematical Analysis of Nonrecursive Algorithms
## General Plan for Analyzing the Time Efﬁciency of Nonrecursive Algorithms
1. Decide on a parameter (or parameters) indicating an input’s size.
2. Identify the algorithm’s basic operation. (As a rule, it is located in the inner-most loop.)
3. Check whether the number of times the basic operation is executed depends only on the size of an input. If it also depends on some additional property, the worst-case, average-case, and, if necessary, best-case efﬁciencies have to be investigated separately.
4. **Set up a sum** expressing the number of times the algorithm’s basic operation is executed.
5. Using standard formulas and rules of sum manipulation, either ﬁnd a closed-form formula for the count or, at the very least, establish its order of growth.
 - #TODO examples
### Summation Identities
- [Summation Identities - CSE 373, Spring 2019 (washington.edu)](https://courses.cs.washington.edu/courses/cse373/19sp/resources/math/summation/)
- [useful_summations.pdf (uh.edu)](https://www.math.uh.edu/~ilya/class/useful_summations.pdf)
	![[Pasted image 20221002183742.png | 250]]![[Pasted image 20221002183718.png | 100]]![[Pasted image 20221002183852.png | 150]]   ![[Pasted image 20221005131218.png|170]]    ![[Pasted image 20221005131311.png|100]]
- Change of Index
	![[Pasted image 20221002184029.png | 200]] Ex: ![[Pasted image 20221002184053.png | 100]]
# Mathematical Analysis of Recursive Algorithms
## General Plan for Analyzing the Time Efﬁciency of Recursive Algorithms
1. Decide on a parameter (or parameters) indicating an input’s size.
2. Identify the algorithm’s basic operation.
3. Check whether the number of times the basic operation is executed can vary on different inputs of the same size; if it can, the worst-case, average-case, and best-case efﬁciencies must be investigated separately.
4. **Set up a recurrence relation**, with an appropriate initial condition, for the number of times the basic operation is executed.
5. Solve the recurrence or, at least, ascertain the order of growth of its solution.
## Solving Recurrence Relations by Substitution
- Backward (the cooler method)
	- ![[Pasted image 20221002191833.png |350]]
- Forward
	- Assume initial condition if not given
	- then plug in $n, n+1, n+2, ...$ to find the pattern
# Empirical Analysis of Algorithms
## General Plan for the Empirical Analysis of Algorithm Time Efﬁciency
1. Understand the experiment’s purpose.
2. Decide on the efﬁciency metric $M$ to be measured and the measurement unit (an operation count vs. a time unit).
3. Decide on characteristics of the input sample (its range, size, and so on).
4. Prepare a program implementing the algorithm (or algorithms) for the experimentation.
5. Generate a sample of inputs.
6. Run the algorithm (or algorithms) on the sample’s inputs and record the data observed.
7. Analyze the data obtained.
- Could be comparing to different algorithms, using a counter at basic operation, actually time the program (usually needs avg of multiple runs, use profiling)
- Change the sample size in a pattern
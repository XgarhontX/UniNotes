# Pseudocode
- **Ex: High Level**
	**Algorithm**: SequentialSearch (A\[1 .. n], key)  
	**Input**: An array A of n integers and an integer key  
	**Output**: A position of the key in the array (-1 if not found) `
	For each element in the array A,
		if that element equals key then  
			return the index of the element  
	return -1
- **Ex: Low Level**
	(Same Input & Output)
	for i ← 1 to n do  
		if (data\[i] = key) then  
			return i
	return –1
- Ex: Fake Two Sum from 390
	- Input: $A$ Ordered array of ints, int $x$
	- Output: An array of size 2 that has 2 values from $A$ that adds up closest to $x$.
	TwoSum(A\[1...n], x)
		beg ← 1, end ← A ;indexes
# Correctness of an Algorithm
- Correct algorithm solves the problem, i.e.  
	1. gives the required output
	2. for any legitimate input
	3. in a finite amount of time
- Verifying correctness
	1. no verification algorithm available (the field young)
	2. tests only shows presence of bugs
	3. mathematical proof (discrete math be like)
# Efficiency of an Algorithm
- How do you find out how efficient?
	1. Empirical Analysis (after implementation)
		- Implement and run on a wide range of well chose input
		- Measure time in physical units
	2. Analytical Analysis (before implementation)
		- Reason about the algorithm expressed in pseudocode
		- Theoretical Model
		- Asymptotic Notation
	- Each has pros and cons, like how you won't see the physical time from. Empirical is way more labor intensive because you have to implement it, Analytical is just math 4head.
# Theoretical Model
- To start analysis, we assume
	1. random-access machine (RAM) model
	2. abstraction of real computer
	3. sequential execution of instructions
	4. standard operations of a real computer (assignment, +, -, *, /, comparison operators, boolean operators, etc.)
		- If needed, clarify if result of int / int operation.
	5. each operation takes one time unit
	6. infinite number of memory locations  
	7. each memory location contains a constant amount of memory (e.g. 32 bit integer)
# Analytical Analysis
- time efficiency is expressed in terms of **input size**
	- almost all algorithms run longer on larger inputs
- time efficiency is expressed as the number of times the **basic operation** is performed
	- the operation that contributes most to the running time
- Ex:
	- ![[Pasted image 20221004141039.png | 250]]
- in analytical analysis we often concentrate on the **worst-case** efficiency
	- $C_{\text{worst}}(n)$ Largest number of instructions needed to process any input of size $n$
- **average-case** (and **best-case**) efficiency are interesting too!
	- $C_{\text{best}}(n)$ Smallest number of instructions needed to process any input of size $n$
	- $C_{\text{avg}}(n)$ Average number of instructions needed to process a random input of size $n$
## Sequential Search 
- [[Book Chapter 2 - Fundamentals#Worst-Case Best-Case and Average-Case Efﬁciencies |Textbook Notes]]
- Input size ($n$) is the list's size $A[n]$ & the basic operation is comparing $\text{key}$s.
- $C_{\text{best}}(n) = 1$ when $A[1] = \text{key}$
- $C_{\text{worst}}(n) = n$ when  $A[n] = \text{key}$, or $\text{key}$ is not $A$
- $\begin{align} C_{\text{avg}}(n) &= \frac{p}{n}1+ \frac{p}{n}2 + \frac{p}{n}3+...+ \frac{p}{n}n+ (1-p)n \\ &= \frac{p}{n}(1+2+3+..+n)+ (1+p)n \\ &= \frac{p}{n} \frac{n(n+1)}{2}+ (1-p)n \end{align}$
# Order of Growth
- Let $C(n)$ be the number of times the basic operation is performed on an input of size $n$, e.g. in the worst-case.
- In efficiency analysis, we concentrate on the order of growth of $C(n)$, i.e. what happens to $C(n)$ when n grows larger?
- We ignore multiplicative constants.
	- e.g. $2n$ grows at the same rate as $n$
	- e.g. $n^2$ grows faster than $2022n$
- Asymptotic notation
	- $2n \in \Omega(n)$, $n \in \Omega(2n)$, $n^{2}\in \Theta(2022n)$, $2022n \in O(n^2)$
# Asymptotic Notation
- [[Book Chapter 2 - Fundamentals#Asymptotic Notations and Basic Efﬁciency Classes |Textbook Notes]]
- ![[Pasted image 20221004143928.png |500]]
	- $\lim_{n-\infty} \frac{t(n)}{g(n)} =$ ![[Pasted image 20221004144232.png | 260]]
	- 4Head simplification (not mathematically right)
		- O(n) means "t(n) grows no faster than g(n)" $\approx$ t(n)$\leq$g(n)
		- $\Omega$(n) means "t(n) grows at least as fast as g(n)" $\approx$ t(n)$\geq$g(n)
		- $\Theta$(n) means" t(n) grows at the same rate as g(n)" $\approx$ t(n)=g(n)
		- o(n) means "t(n) grows slower than g(n)" $\approx$ t(n)<g(n)
		- $\omega$(n) means "t(n) grows faster as g(n)" $\approx$ t(n)>g(n)
	- Relationship
		- 
# Ex: Big O-Notation
- We have an algorithm that has
	- $C_{best}(n)= n$
		- 
	-  $C_{avg}(n)=n^2$, $C_{worst}(n)=n^3$
# Algorithm Analysis Summary
- Set up sums for nonrecursive algorithms
	- Eww sum maths
- Set up recurrence relation for recursive algorithms
	- Backwards substitution
	- Master Theorem
		- ![[Pasted image 20221006151628.png|450]]
			- In this class, unspecified log is base 2, so it's $\Theta(n^{d}log_{2}{n})$
# Binary Search Analysis
- Treat comparison as a 3-way comparison operator for simplicity.
- $C(n)=1+C(\lfloor \frac{n}{2} \rfloor), n>1$ (1 comparison + again with 1/2 the length)
	- flooring is annoying, so assume n is a power of 2.
	- $C(n)=1+C(\frac{n}{2}), n>1$
- $C(1)=1$ (one element list, one comparison)
## Solve using Substitution method
- ![[Pasted image 20221009194533.png|350]]
## Solve using Master Theorem
- a=1 ,b=2, d=0 so wow it's the $\Theta(n^{d}log{n})$ case, $n^d=n^0=1$, so $\Theta(log{n})$
# Practice Problems for Recursive algorithms
- ![[Pasted image 20221009194603.png|200]]  ![[Pasted image 20221009194621.png|200]]  ![[Pasted image 20221009194636.png|250]]
	- "n-k=1" is like Chinn saying "let n=k", but this explains it using iff and gives you the correct offset to get to the initial condition.
	- The 3rd question, when done with the master theorem (a=1,b=3,d=0), you get $\Theta(log_2{n})$. This is the same efficiency as $\Theta(log_3{n})$ because $log_{3}{n}=log_3{2}*log_2{n}$.

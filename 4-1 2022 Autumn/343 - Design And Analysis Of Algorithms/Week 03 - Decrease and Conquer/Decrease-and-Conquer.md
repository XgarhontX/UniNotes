- General Plan
	- reduce the problem instance to a smaller instance of the same problem
	- solve the smaller instance
	- extend the solution of the smaller instance to obtain a solution to the original instance
- Can be recursive or not
- Subtle difference between decrease-and-conquer and divide-and-conquer
	- divide-and-conquer by dividing into multiple smaller problems
	- decrease-and-conquer is still one problem, just find way to skip
## Types of decrease-and-conquer
- By a constant (usually 1)
	- Insertion sort
	- Source removal topological sorting
- By constant factor (usually 1/2)
	- Binary search
- Variable
	- Euclid's gcd
	- quickselect
## Insertion sort
- Start growing a sorted partition in array, and insert the unsorted 
- To sort array A\[0..n-\1]:
	- sort array A\[0..n-2\] recursively
	- insert A\[n-1\] in its proper place among the sorted A\[0..n-2\]
- usually implemented bottom-up (nonrecursively)
- 2 common approaches to insertion sort:
	- linear insertion sort ($O(n^{2})$ comparison & $O(n^2)$ swaps/movements)
	- binary insertion sort (because you have a sorted part) ($O(n^{2})$ comparison & $O(logn)$ swaps/movements)
- Shellsort
	- generalization of insertion sort, reducing data movements (way better compared to )
	- Do multiple passes of linear insertion sort on different sets of elems (e.g. 1st elem for every 10 elems #TODO can be more specific)
### Linear Insertion Sort
- ![[Pasted image 20221018141005.png|350]]
#### Analysis
- $C_{\text{worst}}(n) = \sum_{i=1}^{n-1}\sum_{j=0}^{i-1}1 = \frac{n(n-1)}{n} \in \Theta(n^2)$ when list is backwards
- $C_{\text{best}}(n) = \sum_{i=1}^{n-1}1 = n-1 \in \Theta(n)$ when list is sorted
- $C_\text{avg} = \sum_{i=1}^{n-1}(\frac{1}{i+1}\left(\sum\limits_{j=1}^{i}{j} + i\right)) \approx \frac{n^2}{4}$ $\in \Theta(n^2)$
	- If we have finding a place to insert the 6th elem (index=5), there is 6 possible places to insert & 5 comparison needed
		- Avg to find a place for the 6th elem = $(1/6)(1+2+3+4+5+5)$
		- Generalize it: $\frac{1}{i+1}\left(\sum\limits_{j=1}^{i}{j} + i\right)$
- Stable & In Place
- Best elementary sorting algorithm, especially when the list is nearly sorted.
	- Can be paired with Quicksort when to insertion when the list becomes close to being sorted. 
### Binary Insertion Sort
- Uses binary search to find an appropriate position to insert A[i] among the previously sorted
#### Analysis
- Comparison = $\sum_{i=1}^{n-1} log(i)\approx (n-1)log(n-1)\in \Theta(nlogn)$
- Key Moves/Swaps $\in\Theta(n^2)$
### Shellshort
- Instead of comparing neighbors, compare elements that are k steps away from each other (k-sort)
	- in this way, elements move faster to their final position, elems move much multiple index
- Ex: Gap sequence 5, 3, 1
	- ![[Pasted image 20221018150444.png|400]]
- Still not as practical as normal insertion sort 
#### Analysis
- $O(n(logn)^2)$
	- very much dependent on the gap sequence
		- Like 32, 16, 8, 4, 1 is $O(n^2)$ because the only odd is 1
	- “Analysis of Shellshort and Related Algorithms” R. Sedgewick (1996)
		- Still not $O(nlogn)$, they have a long gap sequence
	- Research still ongoing to see if $O(nlogn)$ is possible
## Quickselect
- How do we find the $k^\text{th}$ smallest elem in a list $A[1...n]$?
- Brute Force passes $O(n^n)$
- Sort first then find $O(nlogn)$ via Mergesort
- Quickselect is $O(n)$
### Quickselect w/ Hoare
- Have a pivot and partition the list with 
- Ex:
	- <u>18</u> 40 10 32 12 17 37 06 02 35
	- <u>18</u> **02** 10 32 12 17 37 06 **40** 35
	- <u>18</u> 02 10 **06** 12 17 37 **32** 40 35
	- <u>18</u> 02 10 06 12 **37** **17** 32 40 35
	- <u>18</u> 02 10 06 12 17 37 32 40 35 (undo last swap)
	- **17** 02 10 06 12 <u>18</u> 37 32 40 35
		- We found the 6th smallest elem
		- We can continue dividing recursively to find the correct k
- Ex: k=11
	- <u>10</u> 03 02 08 23 11 18 22 17 01 06 05 20 19 09
	- <u>10</u> 03 02 08 **09** 11 18 22 17 01 06 05 20 19 **23
	- <u>10</u> 03 02 08 **09** **05** 18 22 17 01 06 **11** 20 19 **23
	- <u>10</u> 03 02 08 **09** **05** **06** 22 17 01 **18** **11** 20 19 **23
	- <u>10</u> 03 02 08 **09** **05** **06** **01** 17 **22** **18** **11** 20 19 **23
	- <u>10</u> 03 02 08 **09** **05** **06** **17** **01** **22** **18** **11** 20 19 **23
	- <u>10</u> 03 02 08 **09** **05** **06** **01** **17** **22** **18** **11** 20 19 **23** (undo after l & r crossed, right pointer is 01, will swap with pivot
	- **01** 03 02 08 **09** **05** **06** <u>10</u> **17** **22** **18** **11** 20 19 **23** (found k=8, do again on right list)
	- <u>17</u> 22 18 11 20 19 23
	- <u>17</u> **11** 18 **22** 20 19 23
	- <u>17</u> **18** **11** **22** 20 19 23
	- <u>17</u> **11** 18 **22** 20 19 23 (undo)
	- **11** <u>17</u> 18 **22** 20 19 23 (k=10)
	- <u>18</u> 22 20 19 23
	- <u>18</u> 22 20 19 23 (swap & undo) (k=11)
- Quicksort is basically doing this, but you have to keep doing Hoare's for both partitioned lists
#### Analysis
- 1 pass of Hoare's partitioning needs n+1 comparison, n+1 being for the extra swap that gets reverted when the pointers cross.
- Best case is doing only one pass of Hoare's. The first pivot is in rank k.
	- $C_\text{best} = n+1 \in \Theta(n)$
- Worst case is 
	- $C_\text{worst} = C(n-1)+(n+1)$ (We pivot only by 1 each pass, this happens when array is sorted)
		- $C(1)=0$ (At the end, there is nothing to compare with just 1)
	- #TODO scratch math solving recurrence
	- $C_\text{worst} \in \Theta(n^2)$
- Avg
	- The best pivot ending position is in the middle, like binary search. We want to cut up >1/4 of n.
		- So with 1/2 chance, your pivot will cut up >1/4 ($\frac{n}{\frac{4}{3}}$)
	- $C(n) \leq C(\frac{3}{4}n)+2\Theta(n)$
		- a=1, b=4/3, 1
		- $\therefore C(n) \in \Theta(n)$

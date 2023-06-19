# An algorithm is...
<u>Algorithm</u>: a sequence of unambiguous instructions
- for solving a problem, i.e.
- for obtaining a required output
- for any legitimate input  
- in a finite amount of time
- Not all computer programs are an algorithm
	- Ex: An OS because it doesn't end.

# Historical Perspective
- From algebra guy, **Muhammad ibn Musa al-Khwarizmi** – 9th century Persian mathematician.
	- ~600 B.C., there were 2 big number system, Roman Numerals & Decimal Positional System.
		- Man introduced the then Western world to decimal system which are easier to do math with.
- **Euclid’s algorithm** (300 B.C.) for finding the greatest common divisor of two nonnegative, not-both-zero integers a and b based on gcd(a,b) = gcd(b, a mod b).
	- gcd(60,24) = gcd(24,12) = gcd(12,0) = 12
	- Pseudocode (Recursive): 
		- ![[Pasted image 20220929143848.png | 300]] 
			- "gcd(a,b)" means "the greatest common divisor of a & b"
- **sieve of Eratosthenes** (ca. 200 B.C.) for generating all prime numbers less than or equal to a given integer n. #TODO(Read more in book)

# Problem & Algorithm
- <u>Problem</u>: What the input is like and the desired output.
- <u>Algorithm</u>: The sequence of instructions to solve the problem.

# Example of a Problem: Sorting
- **Statement of the problem**:  
	- input: a sequence A of n numbers.
	- output: the sequence A sorted in *ascending order*.
- Algorithms to solve the problem (from 342):
	- ![[Pasted image 20220929150316.png | 400]]
		- Besides Bucket and Radix, these are **Comparison Based Sorting Algorithms**
		- Bubble, Selection, & Bogo are Brute Force
		- Insertion is Decrease-and-Conquer
		- Merge & Quick is Divide-and-Conquer
		- Heap is Transform-and-Conquer
## Selection Sort

# Important/Common Problem Classes
- Sorting
- Searching
- String Processing
- Graph Problems
	- Shortest Path (Greedy)
		- Statement:
			- Input: Weighted Connected Graph, $G(V,E)$.
			- Output: Shortest path between A and every node in $V$.
		- Dijkstra Algorithm $O(|V|^2)$ or $O(|E|log|V|)$
	- Min Spanning Tree (Greedy) #From_342
		- Statement:
			- Input: Weighted Connected Graph, $G(V,E)$.
			- Output: Graph/Tree that includes all vertices connected by edges with the smallest sum of edges.
			- ![[Pasted image 20220929151652.png | 200]]
		- Kruskal's & Prim's Algorithm $O(|E|log|V|)$ #From_342
		- Ex: Park that connects 
	- Traveling Salesman Problem (NP)
		- Statement:
			- Input: Weighted Connected Graph, $G(V,E)$.
			- Output: Lightest path/cycle that goes through all nodes.
		- No known algorithm to solve in polynomial time
		- Ex: Amazon delivery be like
	- Graph Coloring Problem
- Numerical Problems
- Selection
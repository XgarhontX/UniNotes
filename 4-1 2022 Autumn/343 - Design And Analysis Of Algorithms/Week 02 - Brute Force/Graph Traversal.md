# Graph Traversal
## Graph Representations
![[Pasted image 20221011150411.png|150]]
- Adjacency Matrix
	- ![[Pasted image 20221011150434.png|200]]![[Pasted image 20221011151813.png|300]]
		- Space: $O(|V|^2)$ (not dependent on edges)
			- Better for dense graph
			- $O(1)$ edge check.
			- Slower to grab all neighbor of a node because it needs to check 0s.
- Adjacency Lists
	- ![[Pasted image 20221011150446.png|150]]![[Pasted image 20221011151850.png|300]]
		- In the book & here, the list is sorted, but it doesn't mean anything.
		- Space: $O(|V| + 2|E|)$
			- $|V|-1 \leq |E| \leq |V|^2$
			- Better for sparse graph
			- $O(n)$ to check for node.
			- Faster to grab all neighbor of a node.
-  
- Directed (only 1 way to travel) & Undirected (both way)
	- Ex: Webpages as nodes, links as directed edges.
## Breadth-First Search (BFS)
- Steps
	1. Choose start
	2. Visit all neighbors, adding them to the queue
	3. Use the queue to visit their unvisited neighbors and repeat 2 adding them to queue.
- Ex:
	- ![[Pasted image 20221013135534.png|200]]        ![[Pasted image 20221013140236.png|100]]![[Pasted image 20221013140418.png|75]]
	- discovered[] = [0,0,0,0,0,0,0,0,0,0] (1 elem corresponding to each vertices noting the order. 342 was adding them to a list, but then you can't )
	- And a queue to know which to go to next
		- \[1,0,0,0,0,0,0,0,0,0\] & [a]
		- \[1,0,2,3,4,0,0,0,0,0\] & \[c,d,e\]
		- \[1,0,2,3,4,5,0,0,0,0\] & \[d,e,f\]
		- \[1,0,2,3,4,5,0,0,0,0\] & \[e,f\]
		- \[1,6,2,3,4,5,0,0,0,0\] & \[f,b\]
		- \[1,6,2,3,4,5,0,0,0,0\] & \[b\]
		- \[1,6,2,3,4,5,0,0,0,0\] & \[\]
		- \[1,6,2,3,4,5,7,0,0,0\] & \[g\]
		- \[1,6,2,3,4,5,7,8,0,9\] & \[j,i\]
		- \[1,6,2,3,4,5,7,8,10,9\] & \[i\]
		- \[1,6,2,3,4,5,7,8,10,9\] & \[\]
- Pseudocode & Analysis
	- ![[Pasted image 20221013141924.png|400]]
	- So it's with a queue
		- $\Theta(|V|+|E|)$ for adjacency list 
		- $\Theta(|V|^2)$ for adjacency matrix (Because checking 0s again waste time)
		- considered linear time because it's based on input ($\Theta(|V|^4$ would be quadratic)
		- Same as DFS
## Depth-First Search (DFS)
- Steps
	1. Choose start
	2. Add unvisited neighbors to the stack, then visit 1 neighbor.
	3. Continue visit the next 
- Ex:
	- ![[Pasted image 20221013135534.png|200]]     ![[Pasted image 20221013142728.png|100]]
	- discovered[] = [0,0,0,0,0,0,0,0,0,0]
	- And a queue to know which to go to next
		- \[1,0,0,0,0,0,0,0,0,0\] & [a,]
		- \[1,0,2,0,0,0,0,0,0,0\] & [a,c]
		- \[1,0,2,3,0,0,0,0,0,0\] & [a,c,d]
		- \[1,0,2,3,0,0,0,0,0,0\] & [a,c]
		- \[1,0,2,3,0,4,0,0,0,0\] & [a,c,f]
		- \[1,b,2,3,0,4,0,0,0,0\] & [a,c,f,b]
		- \[1,5,2,3,6,4,0,0,0,0\] & [a,c,f,b,e]
		- \[1,5,2,3,6,4,0,0,0,0\] & []
		- \[1,5,2,3,6,4,7,0,0,0\] & [g]
		- \[1,5,2,3,6,4,7,8,0,0\] & [g,h]
		- \[1,5,2,3,6,4,7,8,9,0\] & [g,h,i]
		- \[1,5,2,3,6,4,7,8,9,10\] & [g,h,i,j]
		- \[1,5,2,3,6,4,7,8,9,10\] & []
- Pseudocode & Analysis
	- ![[Pasted image 20221013145652.png|400]] (don't know if 100% correct)
		-  $\Theta(|V|+|E|)$ for adjacency list
		- $\Theta(|V|^2)$ for adjacency matrix (Because checking 0s again waste time)
		- considered linear time because it's based on input ($\Theta(|V|^4$ would be quadratic)
		- Same as BFS
## Binary Tree w/ BFS & DFS
![[Pasted image 20221013143319.png|350]]
## Connectivity and Acyclicity
- Explain how one can identify connected components of a graph by using:
	- a depth-first search
		- cross edges
		- Instead of count++ every new node, only count++ when you complete reach dead end
- Explain how one can check a graph’s acyclicity by using:
	#TODO
# Topological sorting
## Directed Acyclic Graphs (dag)
- Direct and no cycles
- ![[Pasted image 20221013150516.png|250]]
## Topological Sorting
- Order the vertices such that for every edge, its starting vertex comes before its ending vertex
	- is possible iff the graph is a dag
	- 2 algorithms: DFS-based and source removal
	- Ex: Classes and prereqs
		- ![[Pasted image 20221013150605.png|250]]
### DFS Based
1. perform a DFS traversal of the graph
2. **keep track of the order in which vertices are popped off the traversal stack**
3. the **reverse order** solves topological sorting problem
4. back edges encountered? --> NOT a dag!
- Ex:
	- ![[Pasted image 20221013150913.png|400]]![[Pasted image 20221013150948.png|200]]
### Source Removal Algorithm
- A source: a vertex with no incoming edges
- outline of the source removal algorithm:
	1. **find a source**
	2. **remove this source** and all its outgoing edges
	3. **repeat** until either:
		- there is no vertex left (problem is solved)
		- there is no source among the remaining vertices (graph is not a dag)
- Implementation: keep track of in-degree
- Ex:
	- ![[Pasted image 20221013151117.png|400]]
## Practice
- ![[Pasted image 20221013152628.png|200]]
	- DFS Based (start @ a): d,c,a,b,g,f,e
	- Source Remove (start @ d): d,a,b,c,g,e,f
- ![[Pasted image 20221013152908.png|250]]
	- DFS Based: CYCLIC/Not DAG! a,b,c,d,g,e and back to a.
	- Source Remove: Pop of f, but then you find a cyclic graph.
# String Matching
- You got a a text with n characters, and a pattern with m characters.
	- ![[Pasted image 20221108152726.png|240]]
- Sweep through the text and check if the pattern exist for each character spot (except when there's not enough chars left).
## Pseudocode
- ![[Pasted image 20221108152632.png|400]]
### Analysis
- $C_{worst}(n) = \sum_{i=0}^{n-m}m = m(n-m+1) \in \Theta(m-n)$
- $C_{avg}(n)=n$ (need probabilistic model) (usually, you move one after 1 check)
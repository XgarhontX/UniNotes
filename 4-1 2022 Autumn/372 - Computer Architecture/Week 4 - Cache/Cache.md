# Cache Memories
- ![[Pasted image 20221025175148.png|300]]
## General Cache Organization (S, E, B)
- ![[Pasted image 20221025175303.png|350]]
	- set x line (row x column), S x E
	- valid bit: if the line is used
		- Useful in concurrency, when a thread updates memory but doesn't need cache, it sets the valid bit to 0 to signal the future that the cache is outdated.
## Cache Read
- ![[Pasted image 20221025175719.png|350]]
	- Block Offset determines the linear offset to start reading from the line.
		- Useful because a cache line can store multiple data from multiple addresses
		- Doesn't effect hit/miss
	- Set Index is just the index 4head to determine which set.
	- Tag determines is kinda like a hash type beat, the memory address must match with what is stored in the cache to make sure it's the correct data for a hit.
### Direct Mapped Cache (Line or E = 1) Example
- ![[Pasted image 20221025180628.png|350]]
- Example of a cache hit
	- ![[Pasted image 20221025181136.png|300]]
### Direct-Mapped Cache Simulation
-  ![[Pasted image 20221025181501.png|350]]
### E-way Set Associative Cache (e.g. E = 2)
- ![[Pasted image 20221025183546.png|400]]  ![[Pasted image 20221025183751.png|300]]
- There is no line index, the tag is used brute force check for the correct line. 
### 2-Way Set Associative Cache Simulation
- ![[Pasted image 20221025183941.png|300]]
## Cache Write
- ![[Pasted image 20221025190152.png|300]]
	- What to do when we hit/miss and want to write? 2-ways each, and situationally selected.
		- Write to cache and memory, memory only, cache only, disk too? Writing to slower memory slows down time.
### Intel i7 Cache Hierarchy
- ![[Pasted image 20221025191116.png|300]]
# System I/O
- Application-> Standard I/O -> OS -> UNIX IO -> Hardware
## Unix Files
- ![[Pasted image 20221027175216.png|300]]
## Unix File Types
- ![[Pasted image 20221027175523.png|300]]
## Unix I/O
- ![[Pasted image 20221027175720.png|300]]
	- OS doesn't know lower hardware operations. OS is abstracted to read() and write()
		- There is more abstraction between UNIX operations a programming language
### Opening Files
 - ![[Pasted image 20221027180332.png|300]]
### Closing Files
- ![[Pasted image 20221027180528.png|300]]
### Reading Files
- ![[Pasted image 20221027180615.png|300]]
### Writing Files
- ![[Pasted image 20221027180658.png|300]]
## Simple Unix I/O example
- ![[Pasted image 20221027180730.png|300]]
## Dealing with Short Counts
- ![[Pasted image 20221027180853.png|300]]
# Standard I/O Functions
- ![[Pasted image 20221027181129.png|300]]
## Standard I/O Streams
- ![[Pasted image 20221027181323.png|300]]
# Unix I/O vs. Standard I/O
- ![[Pasted image 20221027181429.png|300]]
# FAT!
![[Pasted image 20221103190744.png|500]]

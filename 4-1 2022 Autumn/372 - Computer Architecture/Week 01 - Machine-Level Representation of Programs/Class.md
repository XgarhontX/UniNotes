# Ints and Floats
- Signed Integer 32-bit
	- bit 31 is the sign bit. 0:+, 1:-
	- bit 30 to 0, $2^{31}$ possible magnitude value (2,147,483,647)
		- So watch out for overflow
- Signed Float 32-bit
	- Values closer to 0 are more accurate. Using too large reduces accuracy, will start rounding.
	- Adding to different values can cause underflow
		- (1e20 + -1e20) + 3.14 = 3.14
		- 1e20 + (-1e20 + 3.14) = 0
# Code Security Ex
- Real code from UNIX kernel
	- ![[Pasted image 20221004181728.png | 400]]
		- Only lets memcpy copy a maximum of KSIZE worth of bytes from kernel to user data.
	- ![[Pasted image 20221004182047.png | 450]]
		- Malicious usage has -MSIZE as an argument, copying way more than intended as the first bit (for sign) is 1.
# Memory System Performance Ex
- Copies a matrix to another (row first vs column first)
	- ![[Pasted image 20221004183255.png | 450]]
		- The green (column first copy) is considerably slower (then row first copy) because of how these data structures are stored in memory.
	- Play to the size of cache to maximize usage of faster memory.
# Intel x86 Processors
- Evolutionary design
	- Backwards compatible up until 8086 (1978)
- Complex instruction set computer (CISC)
	- Many different instructions with many different formats
		- But, only small subset encountered with Linux programs
- Milestones
	- ![[Pasted image 20221004185527.png | 350]]![[Pasted image 20221004185552.png|250]]
		- 128-bit is limited by RAM development. ($2^{128}$B of RAM is 16MTB)
	- 2008 i7 layout
		- ![[Pasted image 20221004190645.png | 200]]
			- Each core has Registers, L1, & L2 caches.
			- Each cores has multiple units, tracking and sharing these usage is creating logical cores/threads.
	- Itanium
		- ![[Pasted image 20221004191356.png|300]]
			- IA32 was slow and considered legacy mode, so it failed.
	- AMD
		- Historically
			- AMD has followed just behind Intel  
			- A little bit slower, a lot cheaper
		- Then
			- Recruited top circuit designers from Digital Equipment Corp. and other downward trending companies
			- Built Opteron: tough competitor to Pentium 4
			- Developed x86-64, their own extension to 64 bits
	- 64-bit
		- Itanium failed to shift usage to IA64
		- AMD's x86-64 (aka AMD64) succeeded by capitalizing on low end and 32-bit compatibility.
		- 2004: Intel Announces EM64T extension to IA32
			- Almost identical to x86-64.
------------------------------------------------------------------------------
# Architecture
- Architecture: (also Instruction Set Architecture: ISA) The parts of a processor design that one needs to understand to write assembly code.
	- i.e. ISA & Registers
- Microarchitecture: Implementation of the architecture
	- i.e. Cache Size & CPU Freq
# Assembly Programmer's View
- ![[Pasted image 20221004192339.png|450]]
# Turning C into Object Code
- ![[Pasted image 20221004192448.png|450]]
	- For Java: Java Program → C Program → Assembly → Object Program → Executable Program
# Compiling Into Assembly
- ![[Pasted image 20221004192825.png|450]]
	- Ex: "movl" move a double word/integer/4 bytes between register and memory.
# Assembly Characteristics: Data Types
- “Integer” data of 1, 2, or 4 bytes
	- Data values
	- Addresses (untyped pointers)
- Floating point data of 4, 8, or 10 bytes
- No aggregate types such as arrays or structures
	- Just contiguously allocated bytes in memory
# Assembly Characteristics: Operations
- Perform arithmetic function on register or memory data
- Transfer data between memory and register  
	- Load data from memory into register
	- Store register data into memory
	- 
# Object Code
- ![[Pasted image 20221004193320.png | 400]]
# Machine Instruction Example
- ![[Pasted image 20221004193730.png|400]]
# Disassembling Object Code
- ![[Pasted image 20221004194118.png|400]]
# What Can be Disassembled?
![[Pasted image 20221004194154.png|450]]
------------------------------------------------------------------------------
# Integer Registers (IA32)
- ![[Pasted image 20221004194324.png|400]]
	- %e__ is 32-bit
	- %r__ is 64-bit
	- %__ is 16-bit
	- There is also %eip / %rip, the program counter, which pointes at the next instruction going to be executed.
# Moving Data (IA32)
- ![[Pasted image 20221004194612.png|400]]
	- (btw, a full example: "movl $0x400, $-533")
	- Operand Combinations
		- ![[Pasted image 20221004194957.png|400]]
			- Can't do memory to memory transfer with 1 instruction. (Why use CPU since Memory Controllers can do it instead)
			- Brackets (i.e. "(%eax)"), is just like accessing memory through a pointer ("\*p")
			- Each memory can hold a byte, so a data type need more, it will extend to subsequent addresses.
# Simple Memory Addressing Modes (mov)
- ![[Pasted image 20221006181050.png|300]]
	- 8(%ebp) = 8 addresses ahead of %ebp. (aka offset)
## Using Simple Addressing Modes: Swap
- ![[Pasted image 20221006182004.png|300]]   ![[Pasted image 20221006182445.png|150]] 
	- Set up & Finish is for Call Stack crap, don't worry about it now.
	1. First, we move/copy the addresses store in each pointer to the register. (Line1&2)
		- ![[Pasted image 20221006182809.png|80]]![[Pasted image 20221006183155.png|300]]
	2. Then, using those addresses in register, move/copy the ints to the registers. (Line3&4)
		- ![[Pasted image 20221006182908.png|80]]![[Pasted image 20221006183213.png|300]]
	3. Finally, we move/copy the values in our registers to override the values in memory using the addresses we stored in the registers. (Line5&6)
		- ![[Pasted image 20221006182958.png|100]]![[Pasted image 20221006183226.png|300]]
# Complete Memory Addressing Modes
- ![[Pasted image 20221006183334.png|400]]
	- Like accessing array index, but you can also multiply the offset by a scale
## Practice Calculate Address
- Registers
	- %edx: 0xf000
	- %ecx: 0x0100
- Practice
	- 0x8(%edx) = 0xf000 + 8 = 0xf008
	- (%edx, %ecx) = 0xf000 + 0x0100 = 0xf100
	- (%edx, %ecx, 4) = 0xf000 + (0x0100 \* 4) = 0xf400
	- 0x80( , %edx, 2) = 0x0 + (0xf000 \* 2) + 80 = 0x1E080
# Data Representations: IA32 + x86-64 #fat
- ![[Pasted image 20221006190647.png|500]]
	- Pointer's size is same as processor's word size
# x86-64 Integer Registers
- ![[Pasted image 20221006190801.png|400]]
	- x86-64 can still run x86 because of the
	- i9 and above has more than %r15
# Instruction Changes
- ![[Pasted image 20221006191020.png|400]]
	- l (4-bytes) becomes q (8-bytes)
# 64-bit code
- ![[Pasted image 20221006191310.png|400]]
- To move longs, we replace movl with movq & use 64-bit registers.
	- ![[Pasted image 20221006191533.png|400]]![[Pasted image 20221006191352.png|225]]
# Address Computation Instruction (lea)
- ![[Pasted image 20221006191714.png|400]]
	- The example is of multiplication
		- Much slower than add and bit shift operations
		- So the compiler does x + x \* 2 
			- Where \* 2 is done by bit shift

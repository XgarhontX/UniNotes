# Some Arithmetic Operations
- ![[Pasted image 20221006192720.png|350]]![[Pasted image 20221006192839.png|300]]
	- sarl is logical (copying the leading bit), while shrl is arithmetic (inserts 0)
	- Of course, this is examples for l/int/double word.
## Arithmetic Expression Example
- ![[Pasted image 20221011175718.png|400]]![[Pasted image 20221011181317.png|150]]
	- Assembly code can run in different order than C code.
	- Assembly code will optimize math operations with bit shift and lea, as well as combining lines of C code to reduce assembly instructions.
		- Therefore, simple code should be written as comprehensible as possible.
## Another Example
- ![[Pasted image 20221011181918.png|200]]![[Pasted image 20221011182047.png|400]]
# Condition Code
## Processor State
- ![[Pasted image 20221011182654.png|500]]
	- CF (carry), ZF (zero), SF (sign), OF (overflow) are 1 bit flags/condition codes
## Implicit Setting
- ![[Pasted image 20221011182800.png|400]]
	- Automatically set by arith & logic instructions. lea does the calculation, but doesn't change any condition code
## Explicit Setting: Compare
- ![[Pasted image 20221011183134.png|400]]
## Explicit Setting: Test
- ![[Pasted image 20221011183410.png|375]]
## Reading Condition Codes
- ![[Pasted image 20221011183729.png|500]]
## Example
- ![[Pasted image 20221011185449.png|250]]
	- ![[Pasted image 20221011185502.png|320]]
		1. Save y into %eax (because only up to 1 is )
		2. Compare "x-y"
		3. setg checks if that last compare was "x>y" & set %al bit the result. (memory layout: ![[Pasted image 20221011185923.png|4]])
		4. movzb copies the 1 bit in %al to %eax, ready for the return.
		- Ex: x=2, y=1
			- cmpl is x-y = 2-1 = 1 (true)
				- ZF=0, SF=0, CF=0, OF=0
			- setg %al is putting ~(SF^OF)&~ZF = 1 into %al.
### 2 More Examples
- ![[Pasted image 20221011190719.png|300]]
# Jumping
- Like setX, but we jump if the condition codes matched (or unconditionally)
	- ![[Pasted image 20221011190824.png|400]]
	- Similar to C's goto
## Example
- ![[Pasted image 20221011191040.png|400]]
	- The if branches are done by the jumps.
	- goto version
		- ![[Pasted image 20221011191553.png|400]]
			- Bad coding style, but it generates the same assembly code
			- This is why C is considered close to machine-level. Jumps and pointers.
## Ternary into Assembly
- ![[Pasted image 20221011191705.png|300]]
## Using Conditional Moves
- ![[Pasted image 20221011191754.png|350]]![[Pasted image 20221011191811.png|350]]
## Bad Cases of Conditional Move
- ![[Pasted image 20221011191853.png|250]]
# Loops
## Do While
- ![[Pasted image 20221011191941.png|300]]   ![[Pasted image 20221011192010.png|300]]
- 
- #TODO other loops
# IA32 Stack Structure
## IA32 Stack
- ![[Pasted image 20221013175507.png|400]](Kinda makes sense if you flip the pic, but ok.)
	- %esp or %rsp is the stack pointer
	- When we push something into the stack, the stack top then moves down (decreasing addresses)
### IA32 Stack: Push
- ![[Pasted image 20221013175842.png|400]]
	- l is double word or int, 4 bytes of data. So %esp decreases by 4.
### IA32 Stack: Pop
- ![[Pasted image 20221013180322.png|300]]
	- Move stack top back (increase address)
## Procedure Control Flow
- Let's focus on the Setup & Clean Up of a method in assembly code
- ![[Pasted image 20221013180603.png|400]]![[Pasted image 20221013181117.png|300]]
	- %eip/%rip is the program counter
	- When call execs, the stack top (%esp) changes to grow the stack and to add in the current program counter (so it can resume).
	- Then 0x8048591 ret (aka return) executes
		- ![[Pasted image 20221013182045.png|300]]
## Stack-Based Languages
- ![[Pasted image 20221013183608.png|300]]
	- C, Java, probably most all modern languages
	- Arguments, Local Variable, Return Pointer goes into the stack.
### Stack Frame
- ![[Pasted image 20221013184435.png|400]]
#### Call Chain Ex
- ![[Pasted image 20221013184202.png|300]] ![[Pasted image 20221013184213.png|75]]

	- ![[Pasted image 20221013184601.png|300]]
	- %ebp & %esp surrounds the latest frame
## IA32/Linux Stack Frame
- ![[Pasted image 20221013190319.png|400]]
	- Conventions for what is saved in caller's and callie's frames.
## Revisit Swap
### Call
- ![[Pasted image 20221013190525.png|400]]
	- subl decrease %esp by 8 spaces.
### Set up
1. Save %ebp
	- ![[Pasted image 20221013190945.png|300]]
2. Move %ebp to %esp, tracking the stack frame bottom
	- ![[Pasted image 20221013191256.png|100]]
3. Push %ebx (register with argument data)
	- ![[Pasted image 20221013191318.png|100]]
### Body
- ![[Pasted image 20221013191403.png|350]]
### Finish
- ![[Pasted image 20221013191421.png|350]]
 ### Another Example
- ![[Pasted image 20221013194225.png|200]]
	- caller:
		1. decrease %rsp (stack pointer) by 48
		2. move 10 (argument for array size) to a register to prepare callie
		3. move %rsp (pointer to sum variable) to register to prepare for callie
		4. calls the callie to do work
		5. increase %rsp by 48, free memory
# Arrays
## Array Allocation
- ![[Pasted image 20221013191737.png|400]]
	- arrays have a pointer to the start, and then linear offset + data size is how you index.
- 2D Array
	- If we have A\[3\]\[2\], the stack:
		- A(0,0)
		- A(0,1)
		- A(1,0)
		- A(1,1)
		- A(2,0)
		- A(2,1)
	- So it's row first order. That's why access is faster with row first.
		- We can load row first into the cache easier, than exchanging out rows to find column first.
- 3D Array
	- Same as 2D. 1st dimension, then 2nd, then 3rd.
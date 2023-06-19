# Instruction Set Architecture
- ![[Pasted image 20221108175102.png|350]]
	- The bridge between HW & SW
# CISC (Complex Instruction Set Computer) Instruction Sets
- ![[Pasted image 20221108175242.png|300]]
	- e.g. AMD & Intel CPUs, majority
	- Uses stacks for control
	- Arithmetic Instructions to access memory (unlike LC3 with load and crap)
	- Uses Condition Codes
	- We may want to expand the instruction set for new tasks
# RISC (Reduced Instruction Set Computer) Instruction Sets
- ![[Pasted image 20221108175600.png|350]]
	- Simpler, easier to implement.
		- So people like to put more cores
	- Less instructions
	- No Condition Codes
	- Load & Store, no arithmetic access to memory
		- Most instructions manipulate the registers
		- So more register count than CISC
	- Speed gap between CISC & RISC has closed
## MIPS Registers
- ![[Pasted image 20221108180021.png|300]]
	- 32 registers, 13 years ago
	- Lots of register to save variables that would be on the stack.
## MIPS Instruction Examples
- ![[Pasted image 20221108180259.png|300]]
	- Instructions are all the same size unlike CISC
# CISC vs. RISC
- ![[Pasted image 20221108180439.png|350]]
	- Before Apple and M1, RISC seemed worse.
	- But as most programs become easier to run as HW got more powerful, RISC can 
# Sequential Implementation
- We will use Y86, a bruh moment and a subset of x86.
# Y86
- 6 bytes for instructions
- ![[Pasted image 20221108181253.png|450]]
	-  move (mov), operation (OPl & OPq), jump (jxx)
		- ![[Pasted image 20221108181320.png|100]]   ![[Pasted image 20221108181421.png|90]]  ![[Pasted image 20221108181452.png|89]]
## Instruction Decoding
- ![[Pasted image 20221108181647.png|250]]   ![[Pasted image 20221108181704.png|250]]
	- ifun must be valid for the icode, else it will error.
	- Since instructions vary in size, a chunk of memory can have a variable amount of instructions.
		- So the PC must be incremented by the size of the instruction
	- Ex: 001021AB40341FFBCEDF
		- (halt: 00) (nop: 10) (cmovle: 21AB) (etc.)
## SEQ Stages
- ![[Pasted image 20221108183637.png|220]] ![[Pasted image 20221108183426.png|150]]
	- Before all of that, you have a Program Counter value to start from.
## Computed Values
- ![[Pasted image 20221108183139.png|400]]   
## SEQ Hardware Structure
- ![[Pasted image 20221108183451.png|200]]
### Executing Arithmetic/Logical Operation (OPl)
- ![[Pasted image 20221108185235.png|300]]  ![[Pasted image 20221108185340.png|300]]
### Executing Register to Memory Move (rmmovl)
- ![[Pasted image 20221108185832.png|300]]  ![[Pasted image 20221108185845.png|300]]
### Executing Pop (4 Bytes of Data) from Stack to Register (popl)
- ![[Pasted image 20221110180339.png|300]]![[Pasted image 20221110180401.png|300]]
### Executing Jumps (jxx)
- ![[Pasted image 20221110182407.png|300]]![[Pasted image 20221110182423.png|300]]
### Executing Call (call)
- Save next PC on stack, Jumps to memory address, when done: Return to saved PC
	- Paired with ret
- ![[Pasted image 20221110183503.png|300]]![[Pasted image 20221110183516.png|300]]
### Executing Return (ret)
- Pop off the Return address that was stored by call & Jump to it
	- Paired with call
- ![[Pasted image 20221110190817.png|300]]![[Pasted image 20221110190828.png|300]]
### FAT Execution of Operations List
- [y86-isa.pdf (jmu.edu)](https://w3.cs.jmu.edu/lam2mo/cs261_2018_08/files/y86-isa.pdf)
- ![[Pasted image 20221108185439.png]]
# Endianness
- Big Endian System
	- stores the **most significant byte** of a word **at the smallest memory address** and the least significant byte at the largest
- Little Endian System
	- stores the **least-significant byte at the smallest address**. the weird aids garbage
	- 0x10c = 0x010c is reversed and stored as 0c01
# C & Y86-64
- The first argument to a function is always passed in the %rdi register, the second argument is passed in the %rsi register.
- When exiting a loop, an index register is usually incremented one _object_ beyond the last object accessed.
# SEQ Hardware
- What happens & when during the instructions?
	- Clock cycle
		- ![[Pasted image 20221115180042.png|150]]
		- 1 instruction takes 1 cycle
- ![[Pasted image 20221115175455.png|500]]  ![[Pasted image 20221115175513.png|200]]
## SEQ Operation
- ![[Pasted image 20221115175635.png|400]]
### Ex
- Executing addl
- ![[Pasted image 20221115175806.png|300]]  ![[Pasted image 20221115180158.png|300]] ![[Pasted image 20221115180212.png|300]] ![[Pasted image 20221115180225.png|300]]
- 
## SEQ Summary
- ![[Pasted image 20221115181114.png|350]]
	- A single pipeline is now too slow by modern standards. We need concurrent pipelines.
## SEQ Calculations Ex
- f (frequency) = 1 GHz
- c (cycle time) =1/f
	- f = 1/c
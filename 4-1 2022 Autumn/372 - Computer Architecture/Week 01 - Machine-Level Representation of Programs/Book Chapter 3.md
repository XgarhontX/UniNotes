# History
- Intel with 8086 with the x86 ISA (aka IA32).
- To better handle more data types ditching x87 & companion CPU: SSE (float) & SSE2 (double) 
- 64-bit extension of x86 ISA from AMD: x86-64 (aka IA64)
- Hyperthreading, then Multicore
- AVX & AVX2 (256-bit vectors) improving on SSE (128-bit)
# Program Encoding
## Machine Level Code
- Determined by the ISA
- Concurrency is safeguarded to match ISA sequentially.
- Stored in virtual addresses (x86-64 has $\approx$ 64-bit worth of addresses, which the OS uses the memory management unit (MMU) to map to RAM & virtual/paging memory)
- Abstraction of C hides
	- the program counter (PC)
	- the integer register file holding ints, pointers, temp local variables
	- the condition code registers holding info of recent executed instructions, required for condition statements
	- set of vector registers holding ints and floats
### Ex:
- ![[Pasted image 20221003170024.png | 225]] ![[Pasted image 20221003170126.png | 250]] ![[Pasted image 20221003171247.png|250]]
	- x84-64 instructions are 1-15 bytes long, designed to have common one use less bytes.
- Same code but now is used in a main()
	- ![[Pasted image 20221003170909.png | 250]]
		- Addressed shifted by linker because of main()
			- callq points to the new corresponding address
		- nop is to fill empty, growing function to 16 bytes, optimizing placement of memory
- Intel assembly-code format (above is ATT)
	- ![[Pasted image 20221003171553.png | 175]]
## Data Format #fat
- ![[Pasted image 20221003171738.png | 450]]
# Giga
- K = 2^10 (kilo), M = 2^20 (mega), G = 2^30 (giga), T = 2^40 (tera), P = 2^50 (peta), E = 2^60 (exa)
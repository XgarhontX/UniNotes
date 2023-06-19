# 2 Types of Processor
 - <u>CISC</u> (**Complex** Instruction Set Computing)
	 - Intel
	 - AMD
 - <u>RISC</u> (**Reduced** Instruction Set Computing)
	 - ARM
	 - GPUs
	 - M1

# Structure of Computer System
1. Application
2. OS
3. ISA
4. Hardware
- How does the each layer communicate with the next?
- We (CSS Major) are focusing on ISA and up.

# Computer System
## Hardware Assembly
- pcpartpicker be like
## Computer Organization Abstraction
- ![[Pasted Image 20220929192900_896.png | 350]]
	- The Motherboard is the I/O bridge, I/O bus, System bus, and Memory bus.
	- Register file is the fastest & most expansive memory
		- i7 has like 64 registers.
	- Increasing cores doesn't mean linear increase in performance
		- A major reason why is Data Dependency (subsequent instructions require data to be processed by earlier instructions)
		- Another is Control Dependency (waiting on earlier instructions to know which instruction to execute next, i.e. IF branch)
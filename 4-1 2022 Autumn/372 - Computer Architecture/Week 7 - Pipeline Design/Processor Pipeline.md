# Types of Processing
- ![[Pasted image 20221115182036.png|300]]
	- Sequential is the slowest.
	- Pipelined design is limited by the slowest stage.
		- An additional object increases the total time taken by the slowest stage's duration
	- Parallel is the fastest
		- However, it's not guaranteed to be applicable everywhere. Decencies between function units can slow it down.
- Multiple Pipelined is the chosen CPU design (ISA, not talking about threading/concurrency)
	- **A CPU can do one Fetch, Decode, Execute, Memory, & Write Back stage per clock cycle.**
# Computation Ex
- ![[Pasted image 20221115184028.png|400]]
	- ![[Pasted image 20221115184055.png|300]]
	- Sequential System
	- **Delay** is the total time it takes for the instruction
	- **Throughput** is the amount of instruction per sec = 1/Delay. (GIPS = Giga Instructions Per Sec)
		- Throughput(n) = Amount of Instructions / Delay for that Amount of Instructions
			- Take the limit to infinity, and you get how 
# 3-Way Pipelined Ex
- ![[Pasted image 20221115184416.png|400]]
	- ![[Pasted image 20221115190120.png|300]]
	- Delay here is the total delay.
	- This pipeline is limited by the slowest stage, 120ps.
		- So the throughput is $1/(120[ps]) * 10^{3}[ps/GIPS]=8.333$ GIPS
	- The amount of registers = how many stages you have.
		- e.g. 3-way needs 3 registers
# Unpipelined vs 3-way Pipelined
- ![[Pasted image 20221115191331.png|300]]
# Operating a Pipeline
- ![[Pasted image 20221115191543.png|300]]
# Nonuniform Delays
- ![[Pasted image 20221117175800.png|300]]
	- Total delay = 510ps
	- Clock cycle time = slowest stage =170 ps
	- To improve further on the clock cycle time, designers are dividing stages to smaller faster stages.
# Register Overhead
- ![[Pasted image 20221117180544.png|300]]
	- Further dividing the stages is limited by register access.
		- The throughput increases but not linearly.
# Data Dependencies
- ![[Pasted image 20221117181035.png|300]]
## Data Hazards
- ![[Pasted image 20221117181134.png|300]]
## Data Dependencies in Processors
- ![[Pasted image 20221117181200.png|350]]
	- Read after Write dependency
		- A register needs to wait for another register to write before using it to read.
	- Write after Write dependency
		- A register needs to wait for another register to write before using it to write.
# Control Dependency
- When the processor have to wait on the outcome of CC to determine what to execute next. 
## Predicting the PC
- ![[Pasted image 20221117183721.png|300]]
## Predicting Strategies
- ![[Pasted image 20221117184442.png|250]]
## Recovering from PC Misprediction
- ![[Pasted image 20221117184719.png|300]]
	- We need to remember the changes (memory, registers, PC, etc.) to 
		- Done by the HW
# Pipeline Demos
## No Dependency
- ![[Pasted image 20221117190417.png|300]]
	- EZ, no dependencies, we can easily pipeline it.
		- This scenario is extremely rare in real computing
	- The space on the bottom left of the graph is called the **fill up time**.
## Data Dependencies: 3 Nop’s
- Nop's is basically sleep. It's used to adding timing to the pipeline
	- Done by the compiler
- ![[Pasted image 20221117191138.png|300]]
	- The 3 nop's offset the addl to start it's decode phase when %edx & %eax's instructions finishes writing.
- If we have only 2 or less nop's
	- ![[Pasted image 20221117191558.png|300]]  ![[Pasted image 20221117191632.png|250]]
		- %edx or/and %eax is not ready and the program fails.
# Pipeline Summary
- ![[Pasted image 20221117191739.png|300]]
- ![[Pasted image 20221117191810.png|300]] ![[Pasted image 20221117191829.png|300]]

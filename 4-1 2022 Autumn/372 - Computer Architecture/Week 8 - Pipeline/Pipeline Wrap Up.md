# Exceptions
- ![[Pasted image 20221122175939.png|300]]
	- Bad instructions
		- We can
			- Stop the program completely
			- Skip the following instructions
			- Mitigate with exception handlers and other instructions.
## Exception Example
- ![[Pasted image 20221122180455.png|300]]
	- Bad instructions, bad memory address, etc.
## Exception Example Real 1
- ![[Pasted image 20221122180839.png|300]]
	- An instruction will only cause an exception in the stage that has a problem.
		- That's why ".byte" caused an exception first.
		- It'll still finish the current items in the pipeline before stopping.
## Exception Example Real 2
- ![[Pasted image 20221122181643.png|300]]
	- The exceptions doesn't affect the program, because it'll never jump into "t" logically
	- However, this example processor predicts that the jump will jump.
		- This is why "t" is the third into the pipeline, continuing until the jump finishing evaluating if it needs to jump or not.
		- The misprediction after the jump is done allows the program to continue normally, cancelling the bad instruction.
		- "I'm Lost" is basically a nop that is placed by the processor
# Maintaining Exception Ordering
- ![[Pasted image 20221122182258.png|300]]
	- stat is the special register that gets set during each stage to keep track of exceptions
# Side Effects in Pipeline Processor
- ![[Pasted image 20221122182557.png|300]]
	- Because rmmovl created an exception, addl should have gotten cancelled. That didn't happen & addl evaluated the CCs. We need to revert.
## Avoiding Side Effects
- ![[Pasted image 20221122182912.png|300]]  ![[Pasted image 20221122183509.png|300]]
# Performance Metrics
- ![[Pasted image 20221122183529.png|300]]
	- F = Frequency = 1/C (GHz)
	- C = Clock Rate = 1/F (GIPS)
	- CPI = Clock Cycle Time per Instruction
		- Ideal Cases
			- Single-Core: We expected to see an instruction completed every clock cycle, so 1 cycle / 1 instruction = 1 CPI.
			- Dual-Core: We expected to see 2 instruction completed every clock cycle, so 1 cycle / 2 instruction = 0.5 CPI
			- CPI for Quad-Core = 1/4 = 0.25
		- But we have exceptions and misprediction that increases the CPI.
## CPI w/ Penalty
- ![[Pasted image 20221122185048.png|300]]
- B/I is the penalty
	- ![[Pasted image 20221122185618.png|300]]
	- If we have multiple core, we have to penalize each core.
# Virtual Memory
## A System Using Physical Addressing
- ![[Pasted image 20221027181701.png|300]]
## A System Using Virtual Addressing
- ![[Pasted image 20221027181807.png|300]]
	- Even though it's slower than direct access to physical, we still use it.
## Address Spaces
- ![[Pasted image 20221027181958.png|400]]![[Pasted image 20221027182340.png|300]]
	- Virtual memory give a virtual memory space for each application.
## VM as a Tool for Caching
- ![[Pasted image 20221027183426.png|400]]
	- A page can be mapped to any continuous part of DRAM.
## DRAM Cache Organization
- ![[Pasted image 20221027183718.png|350]]
## Page Tables
- ![[Pasted image 20221027184041.png|350]]
### Page Hit
- ![[Pasted image 20221027184310.png|300]]
### Page Fault
- ![[Pasted image 20221027184328.png|300]]
#### Handling Page Fault
- The Disk sends the page to the Memory (evicting 1 if needed), then the memory can send it to the CPU.
- Ex: 
	- ![[Pasted image 20221027184636.png|200]]   ![[Pasted image 20221027184650.png|200]]
		- VP 4 in DRAM got evicted
### Locality to the Rescue Again!
- ![[Pasted image 20221027185730.png|300]]
## VM as a Tool for Memory Management
- ![[Pasted image 20221027190104.png|300]]   ![[Pasted image 20221027190258.png|300]]
## Simplifying Linking and Loading
- ![[Pasted image 20221027190400.png|350]]
## VM as a Tool for Memory Protection
- ![[Pasted image 20221027190659.png|300]]
- 
# VM Address Translation
- ![[Pasted image 20221101175255.png|300]]
## Address Translation: Page Hit
- ![[Pasted image 20221101175323.png|300]]
	- Basically, check if cache/memory has it from a virtual memory. A hit will return the actual physical address to access.
## Address Translation: Page Fault
- ![[Pasted image 20221101175506.png|300]]
	- Miss, time to read disk for page and evict. Then redo the process for a hit.
## Integrating VM and Cache
- ![[Pasted image 20221101175841.png|300]]
	- Best: If the PA is a cache hit, then you don't look at memory.
	- A PTE will always be turned into PA.
		- If you get a page table hit (from PTA), then you go to MMU to look up in memory.
	- There is:
		- VA
			- Page hit/miss (page from memory is in cache)
			- Page Table hit/fault (page from disk is in memory)
		- PA
			- Cache hit/miss (data from memory is in cache)
			- Data Page hit/fault (data from disk is in memory)
## Speeding up Translation with a TLB
- ![[Pasted image 20221101180322.png|325]]
## Summary of Address Translation Symbols
- ![[Pasted image 20221101182539.png|325]]
	- Addresses
		- N: n bits in VA (Virtual Address)
			- VPObits = n - p
			- VPNbits = n - VPObits (aka the rest)
		- M: m bits in PA (Physical Address)
			- PPO = n - p = VPO (yea, same offset because we cache pages)
			- PPNbits = n - PPObits (aka the rest)
	- Convert VA to PA
		- Look up page table
			- We need VPN to find corresponding PPN (Physical Page Number)
			- First though, we have multilayer paging TLB (caches page table)
		- TLB (Translation Lookaside Buffer) (aka Page Table Cache in the Cache)
			- Uses VPN bits, so same length as VPN too
			- Set up like cache C=SEB, but for storing PPNs
				- S = how many sets
				- B = Block size in bytes
				- E = "S-way associated" or how many lines
			- TLB set index (depends on how many sets) (TLB$_i$) (s = $log_2S$)
			- \# of bits = VPNbits - P+S
			- TLB hit, we can return the PPN found
			- else, we miss and must look up in the actual Page Table
		- Page Table (RAM via DMA)
			- Check the Page Table for the non-cached (not present in TLB) PPN
			- If we check here with the VPN and it misses, we have a Page Fault
		- Paging Files (Disk via DMA)
			- We actually find it in the Disk because the Page Fault
			- retrieve the page from the Disk
		- When PPN found, we have PA
			- PA is the "PPN" + "VPO" (Physical Page Number concatenated with the same Virtual Page Offset)
	- With the PA
		- Cache
			- C=SEB to find Block Offset ($log_2B$), Set Index ($log_2S)$, Tag (the rest of the bits)
		- RAM (via DMA)
			- Read actually data from RAM via PA
# Address Translation With a Page Table
- ![[Pasted image 20221101182902.png|300]]
	- VA gets looked up in the Page Table. The PA is that the PPN found in the table, and the offset is the same.
## Simple Memory System TLB
- c = 16 entries, E = 4-way associative
	- that means S = 4
	- ![[Pasted image 20221101183212.png|400]]
## TLB Hit
- ![[Pasted image 20221101183701.png|350]]
	- A TLB hit eliminates a memory access
## TLB Miss
- ![[Pasted image 20221101183755.png|350]]
- A TLB miss incurs an additional memory access (the PTE)
	- Fortunately, TLB misses are rare. Why?
# Multi-Level Page Tables
- A way to manage paging files being very big.
- ![[Pasted image 20221101184518.png|400]]
## A Two-Level Page Table Hierarchy
- ![[Pasted image 20221101184653.png|400]]
## Summary
- ![[Pasted image 20221101184717.png|400]]
# Actual In-Class Practice on VM
- Walkthrough
	- VA has \____ bits
	- Page Size (P) = $2^p$
		- VPO bits = VA bits - p
		- VPN bits = VA bits - VPO bits
		- PPN & PPO is same sizes
	- Finding PA
		1. Look up VPN in TLB
			- Splitting it to TLBT & TLBI
				- Multilayer TLB bits is just like finding CSEB of cache (Treat B as 1? C=entries, E=how many -way)
		1. If 1 fails, Look up VPN in PT
			- Using whole VPN normally
	- After finding out the PA 
		1. Use PA to check L1 cache (comprised of tag T, set index S, block offset BO)
		2. If miss, use PA again to check L2
		3. If still miss, check L3
		4. Out of caches and still miss, use PA and read from memory actually (which evicts and moves to cache crap).
# I7 Cache
- ![[Pasted image 20221103184948.png|400]]
	- TLB misses are rare, hopefully
# FAT!
![[Pasted image 20221103191013.png|500]]
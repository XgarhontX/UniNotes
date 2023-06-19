# Memory Hierarchy
## Example
- ![[Pasted image 20221018175019.png|450]]
	- Registers are as fast as CPU Hz
## RAM
- ![[Pasted image 20221018175203.png|400]]  ![[Pasted image 20221018180023.png|300]]
	- SRAM is cache, DRAM is what we call RAM
	- When DRAM has weird cell count (e.g. 9), it's for error correction. It can slow down speed a bit for the extra operations.
		- This is worth for servers, which benefits from stability.
	- The Pins provide I/O for CPU to give address, DRAM to send data, as well as power.
	- We have DDR, double speed because it operates on the up & down tick.
	- DRAM needs to refresh all cells (1-by-1) to keep maintaining the correct voltage.
		- SRAM is more sophisticated with more components, it only refreshes the needed cells.
### Conventional DRAM Organization
- ![[Pasted image 20221018181714.png|400]]
	- (Row, Column) matrix organization
	- The example:
		- 16 supercells
			- 2 bits for row, 2 bits for column
				- but we actually only use 2-bit input bus for address selection. Row & Column sent back to back.
		- Each supercell can hold 8 bits
			- So the output bus needs 8 bits.
#### Reading DRAM Supercell (2,1)
- ![[Pasted image 20221018182028.png|340]]
- ![[Pasted image 20221018182415.png|350]]
	- The row buffer improves performance, you don't have to send a row address every time if you don't need to.
### Memory Modules
- ![[Pasted image 20221018185247.png|400]]
	- We read 64 bits worth of data in parallel
	- Increasing # of chips doesn't mean better.
		- More heat
		- Supercells would hold less
### Enhanced DRAMs
- ![[Pasted image 20221018185628.png|400]]
## Nonvolatile Memories
- ![[Pasted image 20221018185956.png|400]]
	- No power needed to store data
## Traditional Bus Structure Connecting CPU and Memory
- ![[Pasted image 20221018190411.png|350]]
### Read Transaction
- ![[Pasted image 20221018190438.png|300]]
- ![[Pasted image 20221018190452.png|300]]
- ![[Pasted image 20221018190513.png|300]]
### Write Transaction
- ![[Pasted image 20221018190606.png|300]]
- ![[Pasted image 20221018190621.png|300]]
- ![[Pasted image 20221018190639.png|300]]
## Disk Drive
- ![[Pasted image 20221018191104.png|300]]
### Geometry
- ![[Pasted image 20221020175545.png|300]]  ![[Pasted image 20221020175637.png|250]]
### Capacity
- ![[Pasted image 20221020175714.png|300]]   ![[Pasted image 20221020180450.png|250]]
### Reading
- ![[Pasted image 20221020180854.png|400]]   ![[Pasted image 20221020181359.png|200]]
### Disk Access
- ![[Pasted image 20221020181632.png|350]]
	- Surface organized into tracks
	- Tracks divided into sectors
### Disk Access Time
- ![[Pasted image 20221020181828.png|350]]   ![[Pasted image 20221020182308.png|300]]
### Disk & I/O Bus
1. ![[Pasted image 20221020183327.png|350]]
2. ![[Pasted image 20221020183349.png|350]] 
	- direct memory access (DMA): components request disk to transfer data into main memory
3. ![[Pasted image 20221020183404.png|300]]
	- More data is sent than the requested, acts as buffer.
## Solid State Disk/Drive (SSD)
- ![[Pasted image 20221020185213.png|325]]
	- EEPROM as storage
### Ex Performance
- ![[Pasted image 20221020185620.png|400]]
	- Random read is slower because we need more DMAs
	- Random writing is even slower because SSD needs to write a whole block, shifting stuff around.\
### SSD VS HDD
- ![[Pasted image 20221020190459.png|400]]
## Storage Trends
- ![[Pasted image 20221020190639.png|400]]
## CPU Clock Rates
- ![[Pasted image 20221020190844.png|400]]
## The CPU-Memory Gap
- ![[Pasted image 20221020191208.png|400]]
# Locality
- ![[Pasted image 20221020191654.png|300]]
## Example
- ![[Pasted image 20221020192031.png|350]]
# Caches
- ![[Pasted image 20221020192643.png|400]]
## General Cache Concepts
- ![[Pasted image 20221020192706.png|400]]
	- Cache Hit: We request a block, and we find it. 
	- Cache Miss: We requested a block, but it's not in the cache. We need to read from memory.
		- Placement policy: determines where the requested block goes
		- Replacement policy: determines which block gets evicted (victim)
### Types of Cache Misses
- ![[Pasted image 20221020193331.png|350]]
- 
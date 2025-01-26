#computerengineering #sem5

![[Pasted image 20241110142607.png#invert]]
## Components
### Registers
![[Pasted image 20241110142700.png#invert]]
#### Register Usage
![[Pasted image 20241116080321.png#invert]]
### ALU
![[Pasted image 20241110142731.png#invert]]
### Flags
[[6 Arithmetic Operation]]
#### Location
![[Pasted image 20250116104236.png]]
### Control Unit
- Instruction Register (IR)
	- Machine code (opcode) of instruction that is currently being executed
- Controls execution flow based on instruction in IR
- Generates control signals for all other CPU components
### Bus Interface
Interface between internal CPU bus and external system-bus
- contains registers to store addresses
## Program Execution
![[Pasted image 20241110143412.png#invert]]
Assembler converts each Assembly instruction to 16-bit opcode

Be careful, Opcodes are **reversed** ([[Little Endian]]) compared to the addresses in Debugger:
**Program Counter in 2-Byte-steps**

Blue Numbers = machine code of instruction
![[Pasted image 20241110143622.png#invert]]
Furthermore, the Programm Counter (PC) is always one step **ahead** (at second MOVS [[5 Data Transfer]], even though 0x20A5 isn't in R0 yet). Jumps after Fetch Step (green).
![[Pasted image 20241110144226.png#invert]]
## Memory Map
- System Address Map
- Graphical layout of main memory
- Linear array of bytes
- What is located where (at which address) in memory?
	- Location of RAM (readable and writable)
	- Location of ROM (only readable)
	- Location of I/O registers
![[Pasted image 20241110143912.png#invert]]
### CT-Board (ZHAW specific)
#### I/O
![[Pasted image 20241110144457.png#invert]]
#### Integer Types
![[Pasted image 20241110144814.png#invert]]
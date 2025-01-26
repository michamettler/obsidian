#computerengineering #sem5

## Overview
### Type
- [[#Unconditional]]
	- Branch always
- [[#Conditional]]
	- Branch if condition is met
### Address hand-over
- Direct
	- Target addresses part of instruction
- Indirect
	- Target address in register
### Address of target
- Relative
	- Target address relative to PC
- Absolute
	- Absolute address
## Unconditional
- B (immediate)
	- `B <label>`
	- Direct
	- Relative
- BX (register)
	- `BX R0`
	- Branch and Exchange
	- `BX <Label>` funktioniert nicht!
	- Indirect (=> target from register)
	- Absolute
- BLX (register)
	- `BLX R0`
	- indirect
	- PC = register
![[Pasted image 20250122102555.png]]
![[Pasted image 20250122102649.png]]
## Conditional
Conditional Branches Flag-dependent and arithmetic branches.
- Direct
- **always** relative

Unsigned
- Higher and Lower
Signed
- Greater and Less

**ACHTUNG, oft zuerst [[#Compare and Test]] nötig**
### Flag-dependent
![[Pasted image 20241114205955.png#invert]]
### Arithmetic - unsigned
![[Pasted image 20241114210027.png#invert]]
### Arithmetic - signed
![[Pasted image 20241114210044.png#invert]]
### Opcodes
![[Pasted image 20241114210121.png#invert]]
## Compare and Test
### CMP
- Same as **SUBS** but without storing a result (only flags affected) [[6 Arithmetic Operation]]
- also high registers
- ![[Pasted image 20241114210227.png#invert]]
### TST
- Is a specific bit set
- **AND** (without storing result) [[7 Logic and Shift-Rotate]] 
- changes N and Z (C and V unchanged)
- ![[Pasted image 20241114210359.png#invert]]

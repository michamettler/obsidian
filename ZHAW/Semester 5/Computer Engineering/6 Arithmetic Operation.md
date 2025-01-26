#computerengineering #sem5 #instructions

https://moodle.zhaw.ch/pluginfile.php/1890591/mod_page/content/30/CT1_Quick_Reference%20%281%29.pdf
![[Pasted image 20241113214105.png#invert]]

## Flags
![[Pasted image 20241113214209.png#invert]]
![[Pasted image 20241113214537.png#invert]]
- [[5 Data Transfer]] Instructions ending with S allow modification of flags
- Processor does not know whether the user is working with unsigned (C) or signed (V) numbers
  => always calculates **both**
## Overview
![[Pasted image 20241113214708.png#invert]]
## Negative Numbers
![[Pasted image 20241113215810.png#invert]]
![[Pasted image 20241113220004.png#invert]]
### Carry and Overflow
![[Pasted image 20241113220235.png#invert]]
![[Pasted image 20241113220459.png#invert]]
#### unsigned
- Addition → C = 1 → **carry** result too large for available bits
- Subtraction → C = 0 → **borrow** result less than zero → no negative numbers
##### Subtraction Burrow
![[Pasted image 20250116153617.png#invert]]
#### signed
- Addition → potential **overflow** in case of operands with equal signs
- Subtraction → potential **overflow** in case of operands with opposite signs
### Zweier Komplement um Berechnen der Negativ Zahl
0101: 5
1011: -5
![[Pasted image 20241113220050.png#invert]]
#### In Assembly
- **RSBS** Instruction
![[Pasted image 20241113220347.png#invert]]
## Instructions
### Addieren
**Wieviel max. addieren bis 1111 1111**
![[Pasted image 20241115192146.png#invert]]
### Subtrahieren
**Wieviel max. subtrahieren bis 1000 0000 (im Rechner nachschauen)**
![[Pasted image 20250123173525.png#invert]]
### Addition
![[Pasted image 20250116151607.png#invert]]
#### ADDS
- update of flags
- result and two operands
- only low registers
- immediate values (0-7)
- immediate (0-255) if **same register** for result and operand
##### Example
```assembly
00000002 18D1   ADDS R1,R2,R3
00000004 1889   ADDS R1,R1,R2
00000006 1889   ADDS R1,R2      ; the same (dest = R1)
00000008 ;      ADDS R9,R2      ; not possible (high reg)
00000008 ;      ADDS R1,R10     ; not possible (high reg)

00000010 1D63   ADDS R3,R4,#5
00000012 ;      ADDS R3,R4,#8   ; out of range immediate
00000012 ;      ADDS R10,R11,#5 ; not possible (high reg

00000012 33F0   ADDS R3,R3,#240
00000014 33F0   ADDS R3,#240    ; the same (dest = R3)
00000016 ;      ADDS R8,R8,#240 ; not possible (high reg)
00000016 ;      ADDS R3,#260    ; out of range immediate
```
#### ADD
- **no** update of flags
- high or low register
- `<Rdn>` result and operand
```assembly
00000008 4411   ADD R1,R1,R2  ; low regs 0000000A 44D1 ADD R9,R9,R10 ; high regs 0000000C 44D1   ADD R9,R10    ; the same (dest = R9) 0000000E 4411 ADD R1,R1,R2 0000000E ;      ADD R1,R2,R3  ; not possible
```
### Subtraction
- there is no subtraction
- uses addition of 2 complement instead
- ![[Pasted image 20241113220938.png#invert]]
- with 64-bit values, try part by part
- ![[Pasted image 20241115192444.png#invert]]
#### SUBS
- updates flags
- result and 2 operands
- only low register
- immediate (0-7)
- immediate (0-255) if **same register** for result and operand
![[Pasted image 20241113221011.png#invert]]
### Multiplication
#### MULS
- Flags
	- N and Z are updated
	- C and V are unchanged
- Operands
	- Rn multiplicand
	- Rd multiplier
- only low registers
- result only contains lowest 32 bits of product
![[Pasted image 20241113221451.png#invert]]
![[Pasted image 20250123183232.png#invert]]
![[Pasted image 20250123183830.png#invert]]
## Multi-Word Arithmetic
### Multi-Word Addition with ADCS
![[Pasted image 20241113221232.png#invert]]
### Multi-Word Subtraction with SBCS
![[Pasted image 20241113221254.png#invert]]
## Integer Casting in C

![[Pasted image 20241113221627.png#invert]]
![[Pasted image 20241113221712.png#invert]]
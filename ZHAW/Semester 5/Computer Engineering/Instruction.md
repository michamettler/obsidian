#computerengineering #sem5 

https://moodle.zhaw.ch/pluginfile.php/1890591/mod_page/content/30/CT1_Quick_Reference%20%281%29.pdf
## Base Structure
![[Pasted image 20241110143104.png]]
## Data Transfer
![[Pasted image 20241110183257.png#invert]]
### Load
Load operands from memory to register.
![[Pasted image 20241110193724.png#invert]]
![[Pasted image 20241110183110.png#invert]]
#### Load Variations
##### LDR
- 32-Bit Literal `LDR R1, #0xA1B2C3D4`
- Literal + Offset `LDR R1, [PC, #12]`
- Constant `LDR R1, =MyConst`
- Reg Value `LDR R1, [R2]`
- only low registers
##### LDRB
- Load Register Byte
- Bits 31 to 8 set to zero
##### LDRH
- Load Register Half-word
- Bits 31 to 16 set to zero
LDRSB • Load Register Signed Byte • Sign extend - Register bits 31 to 8 set or reset depending on bit 7  LDRSH • Load Register Signed Half-word • Sign extend - Register bits 31 to 16 set or reset depending on bit 15
##### LDRSB
- Load Register Signed Byte
- Sign extend
	- Register bits 31 to 8 set or reset depending on bit 7
##### LDRSH
- Load Register Signed Half-word
- Sign extend
	- Register bits 31 to 16 set or reset depending on bit 15
#### Pseudo Instructions
- get address of literal
- allocates space in literal pool
- save address of `mylita` in R5 `LDR R5,=mylita`
- ![[Pasted image 20241110193316.png#invert]]
- after pseudo instruction, data has to be loaded again with `LDR R1, [R5]`
	- value stored at address of `mylita`
#### Array
- `my_array` = 3 * 4 Bytes
- Instructions = 5 * 2 Bytes
- Literals (0x08) = 1 * 4 Bytes
- work with offsets
### Store
Store result from register to memory.
![[Pasted image 20241110183530.png#invert]]
![[Pasted image 20241110195152.png#invert]]
#### STR
- Value from Register `STR R1, [R2]`
- Value from Reg + Offset `STR R1, [R2, #0x04]`
- only low registers
#### STRB
- Store Register Byte (Low 8 bits of register stored)
#### STRH
- Store Register Half-word (Low 15 bits of register stored)
#### Example
![[Pasted image 20241110195255.png#invert]]
### Move
Copy Register to Register or loading literals.
![[Pasted image 20241110183451.png#invert]]
![[Pasted image 20241110183434.png#invert]]

#### MOVS
- updates flags
- only low registers
- Reg to Reg `MOVS R1, R2`
- 8-Bit Literal Hex `MOVS R1, #0x1C`
- Literal dec `MOVS R1, #12`
- Constant `MOVS R1, #MyConst`
	- `MY_CONST8 EQU 0x12`
	  `MOVS R1,#MY_CONST8`
	- ![[Pasted image 20241110183752.png#invert]]
#### MOV
- low and high registers
- `MOV R1, R2`
## Arrays

```assembly
byte_array
	DCB 0xAA,0xBB,0xCC,0xDD
	DCB 0xEE,0xFF

halfword_array
	DCW 0x0011,0x2233
	DCW 0x4455,0x6677
	DCW 0x8899,0xAABB

word_array
	DCD 0xFFEEDDCC
	DCD 0xBBAA9988
	DCD 0x77665544
	DCD 0x33221100
```

![[Pasted image 20241110195407.png#invert]]
![[Pasted image 20241110195511.png#invert]]
### Accessing
![[Pasted image 20241110195533.png#invert]]
- element sizes in bytes
	- word 4
	- half-word 2
	- byte 1

![[Pasted image 20241110195623.png]]
#computerengineering #sem5 #instructions

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
![[Pasted image 20241114202844.png#invert]]
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
-  word 4
	- myArray DCD 0xAAAAAAAA, 0xBBBBBBBB, 0xCCCCCCCC, 0xDDDDDDDD, 0xEEEEEEEE, 0xFFFFFFFF
	- (0xDDDDDDDD zb. => 3 * 4 Bytes = 12 Bytes = 0xC)
- half-word 2
- byte 1
#### Offsets
##### Table for Half-Words (2 bytes each):

| Number of Elements | Total Length in Bytes | Total Length in Hexadecimal |
| ------------------ | --------------------- | --------------------------- |
| 1                  | 2                     | 0x2                         |
| 2                  | 4                     | 0x4                         |
| 3                  | 6                     | 0x6                         |
| 4                  | 8                     | 0x8                         |
| 5                  | 10                    | 0xA                         |
| 6                  | 12                    | 0xC                         |
| 7                  | 14                    | 0xE                         |
| 8                  | 16                    | 0x10                        |
| 9                  | 18                    | 0x12                        |
| 10                 | 20                    | 0x14                        |
| 11                 | 22                    | 0x16                        |
| 12                 | 24                    | 0x18                        |
| 13                 | 26                    | 0x1A                        |
| 14                 | 28                    | 0x1C                        |
| 15                 | 30                    | 0x1E                        |
| 16                 | 32                    | 0x20                        |
##### Table for Words (4 bytes each):

|Number of Elements|Total Length in Bytes|Total Length in Hexadecimal|
|---|---|---|
|1|4|0x4|
|2|8|0x8|
|3|12|0xC|
|4|16|0x10|
|5|20|0x14|
|6|24|0x18|
|7|28|0x1C|
|8|32|0x20|
|9|36|0x24|
|10|40|0x28|
|11|44|0x2C|
|12|48|0x30|
|13|52|0x34|
|14|56|0x38|
|15|60|0x3C|
|16|64|0x40|
##### Table for Bytes (1 byte each):

|Number of Elements|Total Length in Bytes|Total Length in Hexadecimal|
|---|---|---|
|1|1|0x1|
|2|2|0x2|
|3|3|0x3|
|4|4|0x4|
|5|5|0x5|
|6|6|0x6|
|7|7|0x7|
|8|8|0x8|
|9|9|0x9|
|10|10|0xA|
|11|11|0xB|
|12|12|0xC|
|13|13|0xD|
|14|14|0xE|
|15|15|0xF|
|16|16|0x10|
![[Pasted image 20241110195623.png]]
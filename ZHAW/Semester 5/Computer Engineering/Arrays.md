#computerengineering #sem5 
## Arrays
![[Pasted image 20250116150254.png#invert]]

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

### Array of Bytes
![[Pasted image 20241110195407.png#invert]]
### Array of Hal-Words
![[Pasted image 20250116150627.png#invert]]
### Array of Words
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
![[Pasted image 20250123152450.png]]
##### Table for Half-Words (2 bytes each):
**Achtung, STRH benutzen**

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
**Achtung, STR benutzen**

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
**Achtung, STRB benutzen**

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
![[Pasted image 20250116150403.png#invert]]
#computerengineering #sem5 #instructions

https://moodle.zhaw.ch/pluginfile.php/1890591/mod_page/content/30/CT1_Quick_Reference%20%281%29.pdf

## Logic Instructions
- Updates flags N and Z
- Only low registers
![[Pasted image 20241114201920.png#invert]]
![[Pasted image 20241114201939.png#invert]]
## Bit Manipulations
![[Pasted image 20241114202039.png#invert]]
## Shift / Rotate
![[Pasted image 20241114202137.png]]
![[Pasted image 20241114202121.png#invert]]
![[Pasted image 20241114202214.png#invert]]
### Multiplication
![[Pasted image 20241114202240.png#invert]]
![[Pasted image 20241114202255.png#invert]]
Example: https://github.com/michamettler/zhaw-ct1/blob/main/Lab06_ALUBranchInstructions/bcd/app/main.s

| Multiplikationsfaktor | Shift-Anweisung (LSL) |
| --------------------- | --------------------- |
| 2                     | LSLS #1               |
| 4                     | LSLS #2               |
| 8                     | LSLS #3               |
| 16                    | LSLS #4               |
| 32                    | LSLS #5               |
| 64                    | LSLS #6               |
| 128                   | LSLS #7               |
## Sign Extension
![[Pasted image 20241114211155.png#invert]]
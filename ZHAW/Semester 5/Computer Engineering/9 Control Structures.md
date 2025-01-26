#computerengineering #sem5
## Selection (If-Else)
![[Pasted image 20241114211442.png#invert]]
## Switch
![[Pasted image 20241114211502.png#invert]]
## Loops
### Do-While
![[Pasted image 20241114211527.png#invert]]
### While
![[Pasted image 20241114211549.png#invert]]
### For
![[Pasted image 20241114211603.png#invert]]
```assembly

main
    PROC
	EXPORT main
	
	LDR R6, =i
	LDR R0, [R6]
	LDR R7, =count
	LDR R1, [R7]
	B cond

loop
    ADDS R0, R0, #1
    ADDS R1, R1, #1

cond
    CMP R0, #10
    BLT loop     ; *signed* comparison
    STR R0, [R6] ; store final i
    STR R1, [R7] ; store final count

endless
    B endless
    ENDP

AREA progData, DATA, READWRITE
i       DCD 0
count   DCD 0
		END
```

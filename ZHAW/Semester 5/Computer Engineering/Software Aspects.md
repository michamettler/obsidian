#computerengineering #sem5 

![[Pasted image 20241110135725.png#invert]]
## Preprocessor
- Text processing
- Pasting of `#include` files
- Replacing macros (`#define`)
## Compiler
- Translate CPU-independent C-code into CPU-specific assembly code
## Assembler
- Translate to machine instructions
- Result: Relocatable object file
- Binary file => **not readable** with text editor, use Hex Dump
## Linker
- Merge object files
- Resolve dependencies and cross-references
- Create executable
- **not readable**
## Example
### Before
```c
#include "utils_ctboard.h"
#define LED_ADDR 0x60000100
#define LED_VALUE 0x12
int main(void)
{
 while (1) {
 write_byte(LED_ADDR, LED_VALUE);
 }
}
```
### After Preprocessor
```c
void write_byte(uint32_t address,
 uint8_t data);
int main(void)
{
 while (1) {
 write_byte(0x60000100, 0x12);
 }
}
```
### After Compiler
```assembly
AREA .text, CODE, READONLY

main PROC
	B endloop

mloop
	MOVS r1,#0x12
	LDR r0,L112
	BL write_byte

endloop
	B mloop
	ENDP

L112 DCD 0x60000100
```

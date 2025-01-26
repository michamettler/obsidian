#computerengineering #sem5
## File Sections
**Achtung**: Reihenfolge kann variieren.
![[Pasted image 20241110145148.png#invert]]
### Example
![[Pasted image 20250116111026.png#invert]]
![[Pasted image 20250122162719.png#invert]]
liegen 1 Byte auseinander
1 Byte entspriche 1 in Hexa
![[Pasted image 20250116111014.png#invert]]
### Ausrechnen

Tiefste Adresse = 0x20000700
**CODE**: 1024 Bytes= 0x400
**Endadresse**: 0x20000700 + 0x400 - 1 = 0x20000AFF

Neue tiefste Adresse = 0x20000B00
**STACK**: 256 Bytes = 0x100
**Endadresse**: 0x20000B00 + 0x100 - 1 =0x20000BFF

Neue tiefste Adresse = 0x20000BFF
**DATA**: 512 Bytes = 0x200
**Endadresse**: 0x20000B00 + 0x200 - 1 =0x20000DFF

*Tipp*: Windows Rechner benutzen (Programmierer)
*Ausserdem*: 
- Eine Konstante = 4 Bytes
- Eine Codezeile = 2 Byte * Anz. Zeile + 4 * Anz. verwendete Vars, Konstante nur falls auf Var verweist

| Bytes | Hexa |
| ----- | ---- |
| 1024  | 400  |
| 512   | 200  |
| 256   | 100  |
| 128   | 80   |
### Directives
Directives for uninitialized data
	- SPACE or % with number of bytes to be reserved - Reserves number of bytes without initialing them
- DCB: **B**ytes
- DCW: Half-**W**ords
- DCD: Words
![[Pasted image 20241110154504.png]]
![[Pasted image 20241110153740.png#invert]]
### In Code
![[Pasted image 20241110153644.png#invert]]
#### Example
![[Pasted image 20241110155432.png#invert]]
![[Pasted image 20250116111912.png#invert]]
### Object File Sections
![[Pasted image 20250116111817.png#invert]]

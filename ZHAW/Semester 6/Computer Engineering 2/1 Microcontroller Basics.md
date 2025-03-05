#sem6 #computerengineering 
## System Bus
![[Pasted image 20250222092853.png#invert]]
Memory Bus bidirektional

![[Pasted image 20250222092923.png#invert]]
### Multiple Devices
![[Pasted image 20250222092948.png#invert]]
Problem: Wenn nur digital führt Slave 1 und Slave 2 zu "Licht" => Board geht kaputt. Einer der beiden Slaves muss effektiv ausgeschaltet werden (NULL statt 0 oder 1).
#### Lösung
CMOS Inverter
![[Pasted image 20250222093059.png#invert]]
=> Zusätzlicher Inverter einbauen, damit beide auf Off (NULL)
![[Pasted image 20250222093126.png#invert]]
##### Timing Diagramm
![[Pasted image 20250222093154.png#invert]]
### Digital Basics
![[1 Microcontroller Basics-1740216576402.png#invert]]
## Synchronous Bus
![[1 Microcontroller Basics-1740813047399.webp#invert]]
### Timing Diagram
![[1 Microcontroller Basics-1740813394642.webp#invert]]
#### Wie wird in Speicher geschrieben
![[1 Microcontroller Basics-1740813423178.webp#invert]]
#### Write vs. Read
![[1 Microcontroller Basics-1740813767296.webp#invert]]
Erkennen anhand von NWE SIgnal und/oder ob fertig bei T4 bzw. T6
#### Control vs. Status Registers
![[1 Microcontroller Basics-1740814635417.webp#invert]]
### Address Decoding
![[1 Microcontroller Basics-1740814934306.webp#invert]]
=> **select is active for exactly one address in full decoding**
=> for partial, just use A8 - A31 for example instead of A0 - A31 (mask last two symbols)
![[1 Microcontroller Basics-1740815055863.webp#invert]]
### Slow Slaves
![[1 Microcontroller Basics-1740815901914.webp#invert]]
=> Zusätzliches Signal (Ready), damit der Slave sagen kann er braucht mehr Zeit
### Implementation with C

![[1 Microcontroller Basics-1740819503126.webp]]


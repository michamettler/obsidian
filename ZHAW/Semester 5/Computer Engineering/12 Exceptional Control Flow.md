#computerengineering #sem5 
## Interrupts
**wichtig Interrupt Bits clearen, bevor Business Logik vorgenommen wird**
![[Pasted image 20250123113637.png#invert]]
![[Pasted image 20250123113941.png#invert]]
![[Pasted image 20250122145905.png#invert]]
### Workflow
![[Pasted image 20250122145942.png#invert]]
### Interrupts
![[Pasted image 20250122150012.png#invert]]
### Context
![[Pasted image 20250122150229.png#invert]]
![[Pasted image 20250122150245.png#invert]]
![[Pasted image 20250122150352.png#invert]]
## Interrupt Control
![[Pasted image 20250122150452.png#invert]]
![[Pasted image 20250122150751.png#invert]]
### Types
- Interrupt Pending: Interrupt
- Interrupt Enable: Enabling and Disabling of specific Interrupt
- PRIMASK: Enable or Disable all Interrupts, PRIMASK = 0 => enabled
- Priority Level (**the lower the priority level the greater the priority)
- Interrupt Active
### Register View
![[Pasted image 20250122151339.png#invert]]
#### Details
![[Pasted image 20250122151441.png]]
![[Pasted image 20250122151452.png]]
#### Befehle
![[Pasted image 20250122151607.png]]
### Exception States
![[Pasted image 20250122150556.png#invert]]
### Nested Exceptions
![[Pasted image 20250122151736.png#invert]]
![[Pasted image 20250122151901.png#invert]]
## NVIC
![[Pasted image 20250123113802.png]]
### Example
![[Pasted image 20250122152126.png#invert]]
![[Pasted image 20250123182030.png#invert]]
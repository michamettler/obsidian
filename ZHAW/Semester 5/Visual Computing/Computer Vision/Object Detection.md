#sem5 #visualcomputing/computer-vision 

## Viola-Jones (VJ) Image Detection
![[Pasted image 20241202152617.png#invert]]
![[Pasted image 20250113202309.png]]
- schnelles Herausfiltern, falls nicht gewünschtes Objekt (sobald Faltung nicht mehr matched => drop)
### Simple Image Features
![[Pasted image 20250110115236.png]]
Machine Learning: [[ZHAW/Semester 5/Machine Learning/1 Introduction]]
![[Pasted image 20241202150409.png#invert]]
#### Classifier
Choosing a feature that generates a good threshold:
![[Pasted image 20241202150439.png]]
#### Bagging
Goal: Gather more Features => combine them for a powerful classifier.
![[Pasted image 20241202150610.png#invert]]
#### Boosting
Iterativer Ansatz von Classifier zu Classifier (nur mit denjenigen Samples die noch falsch sind).
![[Pasted image 20241202150628.png#invert]]
#### Algorithm
1. Initialization: Train first model on data
2. Repeat:
	- Compute error of the model on each training sample
	- Give higher importance to samples which the model makes mistakes
	- Train next model using “importance weighted” training samples

**Boosting before Feature Selection**
### Integral Image (Data Structure)
![[Pasted image 20241202151929.png#invert]]
$A - B - C + D$ = Summe von neuem Feld (links)

**A** 235
**B** 459
**C** 691
**D** 1444

Laufzeit O(1)

**Ziel**: Mit vier Zugriffen Summe von Pixelwerten berechnen (extrem schnell).

![[Pasted image 20250111155857.png]]
### Cascaded Classifier
Mehr Subwindows ohne Gesicht als mit Gesicht 
=> möglichst schnell reject-en
=> De-generated Decision Tree

---

=> Model-Tracking optional
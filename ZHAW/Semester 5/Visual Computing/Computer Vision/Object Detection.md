#sem5 #visualcomputing/computer-vision 

## Template Matching
![[Pasted image 20241202142805.png#invert]]
Muss normalisiert sein. Template ist nötig und muss mit Bild übereinstimmen (Overfitting). Wird deshalb nur selten verwendet. Sobald zu viel Helligkeit => Sobel [[Image Filtering]] (Ableitung) um Kanten zu erhalten.
## Viola-Jones (VJ) Image Detection
![[Pasted image 20241202152617.png#invert]]
### Simple Image Features
Machine Learning: [[1 Introduction]]
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
### Cascaded Classifier
Mehr Subwindows ohne Gesicht als mit Gesicht 
=> möglichst schnell reject-en
=> De-generated Decision Tree

---

=> Model-Tracking optional
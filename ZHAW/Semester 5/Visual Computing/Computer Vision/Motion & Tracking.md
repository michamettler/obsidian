#visualcomputing/computer-vision #sem5 

![[Pasted image 20241125140952.png#invert]]
## Optical Flow (Basic Tracking)
![[Pasted image 20241125141115.png#invert]]
### Assumptions
**Ableitung = filern nach x und y (Sobel Filter [[Image Filtering]])**
![[Pasted image 20241125142426.png]]
![[Pasted image 20250113201712.png]]
#### Brightness constancy
1. Zeile in Gleichung, Taylor Reihe
#### Small motion
Taylor-Reihe (ganz kleine Verschiebungen), letzte Zeile in Gleichung
![[Pasted image 20241125144058.png#invert]]
nach unten propagieren
![[Pasted image 20250110121031.png]]
#### Spatial coherence (Optical Flow und Motion Field don't correspond)
##### Aperture Problem
**wichtig** Gradient in eine Richtung, man weiss nicht welche. Homogene Wand geht gar nicht (nur eine Farbe). Am besten => Schneidung
![[Pasted image 20241125142633.png#invert]]
![[Pasted image 20250110121503.png]]
## Object Tracking
![[Pasted image 20241125150154.png#invert]]
### Bedeutung Formel
![[Pasted image 20250113201842.png]]
![[Pasted image 20250113201853.png]]
![[Pasted image 20241125150208.png#invert]]
![[Pasted image 20250113202001.png]]
### Predictions
![[Pasted image 20241125150614.png#invert]]
#### Drifting
Kann dazu führen, dass das erkannte Objekt ändert (Beispiel Gesicht zu Hand)
![[Pasted image 20241125151038.png#invert]]
### Tracking By Detection
- detect object(s) independently in each frame 
- associate detections over time into tracks
- cannot drift
- object has to be known (detector)
![[Pasted image 20241125151148.png#invert]]
#### Gaussian
![[Pasted image 20250110140546.png]]
#### Feature
Best Option (more resilient to objects in front of the area of interest).
![[Pasted image 20250110143442.png]]
#### Tempate
![[Pasted image 20241202142805.png#invert]]
Muss normalisiert sein. Template ist nötig und muss mit Bild übereinstimmen (Overfitting). Wird deshalb nur selten verwendet. Sobald zu viel Helligkeit => Sobel [[Image Filtering]] (Ableitung) um Kanten zu erhalten.

![[Pasted image 20250110142736.png]]
Kann dazu führen, dass die Area of Interest zu einem ähnlichen Objekt überspringt (Basketballspieler - [[#Drifting]]).
#### Background (Segmentation)
![[Pasted image 20250110145950.png#invert]]
### Combination: KLT
![[Pasted image 20241125151358.png#invert]]
![[Pasted image 20250113202152.png]]

Wenn man Object detektieren kann, kann man auch tracken.
#visualcomputing/computer-vision #sem5 

![[Pasted image 20241125140952.png#invert]]
## Optical Flow (Basic Tracking)
![[Pasted image 20241125141115.png#invert]]
### Assumptions
**Ableitung = filern nach x und y (Sobel Filter [[Image Filtering]])**
![[Pasted image 20241125142426.png]]
#### Brightness constancy
1. Zeile in Gleichung
#### Small motion
Taylor-Reihe (ganz kleine Verschiebungen), letzte Zeile in Gleichung
![[Pasted image 20241125144058.png#invert]]
nach unten propagieren
#### Spatial coherence
##### Aperture Problem
**wichtig** Gradient in eine Richtung, man weiss nicht welche. Homogene Wand geht gar nicht (nur eine Farbe). Am besten => Schneidung
![[Pasted image 20241125142633.png#invert]]
## Object Tracking
![[Pasted image 20241125150154.png#invert]]
![[Pasted image 20241125150208.png#invert]]
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
### Combination: KLT
![[Pasted image 20241125151358.png#invert]]
Wenn man Object detektieren kann, kann man auch tracken.
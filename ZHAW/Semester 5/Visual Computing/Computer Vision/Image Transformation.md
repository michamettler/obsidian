#visualcomputing/computer-vision #sem5
## Geometrische Transformation
Wird u.a. auch verwendet, um Daten in Machine Learning zu vermehren (Data Augmentation).
**Inverse von Nachbarschaft damit alle Pixel berücksichtigt werden (keine schwarze Löcher). Wenn transformierter Pixel ausserhalb von Bild, ignorieren (wichtig).**
![[Pasted image 20241118151320.png#invert]]
![[Pasted image 20250113201436.png]]
### Geometry
Pixel coordinate transformation
- Homogene Coordination
- Transformation Matrix (Affine, Perspective, etc.)  
### Radiometric
Gray/Color value interpolation
- Nearest neighbor
- Bilinear (4 neighbors, weights)
- Cubic
### Interpolation
![[Pasted image 20241118151624.png]]
### Transformation Matrix
#### Homogene Koordinaten
**Translation in gleiche Matrix bringen (Plus wegbringen bei M3x3 + (tx, ty)T)**. Reihenfolge spielt eine Rolle bei mehreren Freiheitsgraden (aneinandergehängten Translationen).
![[Pasted image 20241118152550.png]]
#### Projective
![[Pasted image 20241118152108.png#invert]]
#### Translation
![[Pasted image 20241118152132.png#invert]]
#### Rotation
![[Pasted image 20241118152200.png#invert]]
#### Euclidian
![[Pasted image 20241118152622.png#invert]]
#### Scale
![[Pasted image 20241118152639.png#invert]]
#### Reflection
![[Pasted image 20241118152659.png#invert]]
#### Invarianten
Die unterschiedlichen Operationen lassen sich kombinieren (Freiheitsgrade).
![[Pasted image 20241118152836.png#invert]]
#### Affine
![[Pasted image 20241118152854.png#invert]]
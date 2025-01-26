#visualcomputing/computer-vision #sem5

## Pixel Transformation
![[Pasted image 20241118142557.png#invert]]
## 2D Convolutions
![[Pasted image 20241118142632.png#invert]]
### Filter Kernels
Faltung ($*$ in Formel).
![[Pasted image 20241118152018.png]]
#### Average 7x7
![[Pasted image 20241118142722.png#invert]]
#### Gauss 7x7
![[Pasted image 20241118142748.png#invert]]
#### High Pass
![[Pasted image 20241118142816.png#invert]]
#### Sobel
##### Vertical
![[Pasted image 20241118142848.png#invert]]
##### Horizontal
![[Pasted image 20241118142908.png#invert]]
#### Laplace
![[Pasted image 20241118142928.png#invert]]
### In Gimp
![[Pasted image 20241118142953.png#invert]]
### Runtime
- Fast-Fourier-Transformation
## Hybrid Images
- Hochfrequenz und tief-Frequenz Filter überlagert
## Edge Detection
![[Pasted image 20241118143242.png]]
### Nachbarschaften
![[Pasted image 20241118143742.png#invert]]
## Hough Transformation
Gerade Linien in Bildern erkennen (oben rechts is Gerade in Bild):
1. Apply Sobel
2. Apply Hough to detect the edges
![[Pasted image 20241118150923.png#invert]]
(geht auch mit Kreisen => überlappend)
![[Pasted image 20250110113144.png]]
## CNN
[[Convolutional Neural Network (CNN)]] Neuronales Netz lernt [[#Filter Kernels]] (sowohl lineare als auch nicht linear).
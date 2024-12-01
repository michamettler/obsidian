#sem5 #visualcomputing 

mettlmi1
## Aufgabe 1 - zum Laufen bringen
Zuerst versuche ich, das Programm zum Laufen zu bringen. Obwohl ich die Integer-Castings umgesetzt habe, erhalte ich trotzdem noch folgende Fehlermeldung:
![[Pasted image 20241127204122.png]]
Nach etwas Recherche im Internet finde ich heraus, dass ich auf Float casten muss:

```python
patch_x = cv2.getRectSubPix(Ix, (15, 15), (float(xy[i, 0]), float(xy[i, 1]))) patch_y = cv2.getRectSubPix(Iy, (15, 15), (float(xy[i, 0]), float(xy[i, 1])))
```

Das Problem existiert allerdings immer noch bei patch_t, wo ich es somit ebenfalls anpasse:
![[Pasted image 20241127204245.png]]
Anschliessend lässt sich das Programm ausführen mit folgendem Resultat:
![[Pasted image 20241127204324.png]]
## Aufgabe 2 - Point Detection mit Harris Corners

Der Code zur Point Detection befindet sich in der Methode:

```python
# Keypoint detector using Harris-corner criteria
def keypoint_detector(input_img, k, window_size, threshold):
```

Als erstes werden die Kernel-Filter (Sobel) angewendet und anschliessend die Ableitungen (Taylor-Reihe) gebildet. Daraus entstehen die Gradienten, mit welchen sich die $I$'s herleiten lassen.

```python
    kernel_x = np.array([[-1, 0, 1],[-2, 0, 2],[-1, 0, 1]])
    kernel_y = np.array([[1, 2, 1], [0, 0, 0], [-1, -2, -1]])

    dx = linear_filter(input_img, kernel_x)
    dy = linear_filter(input_img, kernel_y)
    
    Ixx = dx**2
    Ixy = dy*dx
    Iyy = dy**2
```

Das entspricht diesen beiden Zeilen der Formel:
![[Pasted image 20241127205031.png]]
Anschliessend wird in einem For-Loop über das gesamte Bild iteriert, um die gesuchten Linien des Objekts zu erkennen.
Im letzten Abschnitt wird noch mit der Nachbarschaft abgeglichen.

```python
# NMS over a 5x5 neighborhood
    for i in range(len(corners)):
      for j in range(i+1,len(corners)):
        if((corners[i][0] +5) >= corners[j][0] and (corners[i][0] -5) < corners[j][0] and (corners[i][1] +5) >= corners[j][1] and (corners[i][1] -5) < corners[j][1]):
          corners[j][0] =0
          corners[j][1] =0      
    l = len(corners)
    i=0
    while(l):
      if(corners[i][0] == 0):
        corners.pop(i)        
      else:
        i=i+1
      l=l-1
    
    corners = np.asarray(corners)
```
## Aufgabe 3 - KLT

Die Hauptfunktion des KLT Trackings sehen wir hier:
```python
# The given KLT algorithm is implemented
  for i in range(len(xy)):
    patch_x = cv2.getRectSubPix(Ix, (15, 15), (float(xy[i, 0]), float(xy[i, 1])))
    patch_y = cv2.getRectSubPix(Iy, (15, 15), (float(xy[i, 0]), float(xy[i, 1])))
    A = np.array([[np.sum(patch_x * patch_x), np.sum(patch_x * patch_y)], [np.sum(patch_x * patch_y), np.sum(patch_y * patch_y)]])

    for j in range(25):
      patch_t = cv2.getRectSubPix(im2, (15, 15), (float(xy2[i, 0]), float(xy2[i, 1])))
      B = -1* np.array([[np.sum(patch_x*patch_t)],[np.sum(patch_y*patch_t)]])
      disp = np.matmul(np.linalg.pinv(A), B)

      u = disp[0].item()
      v = disp[1]

      xy2[i] = [xy2[i,0] + u, xy2[i,1] + v] 

      # Checking if the norm of (u, v) is leser than the threshold (from the textbook section - 9.1.3 Incremental refinement)
      if np.hypot(u, v) <= 0.01:
        break
```

Auch hier wird prinzipiell wieder über mehrere Pixelfenster (patches) iteriert. Insbesondere diese Zeile

```python
A = np.array([[np.sum(patch_x * patch_x), np.sum(patch_x * patch_y)], [np.sum(patch_x * patch_y), np.sum(patch_y * patch_y)]])
```

entspricht diesem Teil der Formel:
![[Pasted image 20241127210430.png]]
Diese Zeile hier

```python
disp = np.matmul(np.linalg.pinv(A), B)
```

berechnet die pseudo-Inverse von A multipliziert mit B, um die Verschiebung $(u,v)$ zu ermitteln.
Dies kann potenziell zu Problemen führen, da nicht jede Matrix immer eine Inverse hat.
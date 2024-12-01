#visualcomputing #sem5 
## Image Filtering

Wir haben folgendes Bild mit einem Salt and Pepper Effekt:
![[Pasted image 20241118155406.png]]
Um die entsprechenden Punkte zu entfernen, wählen wir einen Filter. Dies aus dem Grund, dass beim Anwenden eines Filters auch die Nachbarschaftspixel mit einbezogen werden und sich dadurch der lokale Noise minimiert bzw. die Ausreisser ausgeglichen werden. Der Filter selbst spielt dabei nicht so eine Rolle, optimal ist einer der das Bild nicht allzu sehr verändert wie bspw. Blur.
![[Pasted image 20241118155342.png]]
## Hybrid Images

Für unser Beispiel nehmen wir folgende zwei Bilder:
![[Pasted image 20241118160436.png]]
und
![[Pasted image 20241118160454.png]]
Als erstes wende ich den Gaussian Blur auf das Bild von Lena an:
![[Pasted image 20241118160653.png]]
Anschliessend nehme ich das Bild von Arnold, wende einen tieferen Gaussschen Weichzeichner an, invertiere die Farben und halbiere die Deckkraft (Hochpassfilter).
![[Pasted image 20241118161258.png]]
Anschliessend lege ich die beiden Ebenen übereinander. Das Endresultat sieht dann wie folgt aus:
![[Pasted image 20241118161818.png]]
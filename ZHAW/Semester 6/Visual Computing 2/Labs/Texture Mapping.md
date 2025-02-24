#sem6 #visualcomputing 

## Mesh textuieren

Für die erste Aufgabe möchte ich einen Affen mit einer Fell Textur einfärben.

Dafür erstelle ich als erstes einen neuen Monkey Mesh. Anschliessend verändere ich ihn ein wenig, indem ich einerseits die Ohren und den Hals extrude sowie das eine Auge mit S runter-scale, um ihn ein wenig zu individualisieren:
![[Pasted image 20250220193645.png]]
Anschliessend gehe ich in den Shading Modus und befolge die Schritte gem. Anleitung, um ein Fell-JPEG einzubinden:
![[Pasted image 20250220195214.png]]
Als letztes füge ich noch sowohl die Normal Map sowie Bump Map hinzu und verknüpfe diese
![[Pasted image 20250220201120.png]]
## Replacement Map
Für diese Aufgabe habe ich zuerst den die Sphere gem. Anleitung hinzugefügt und die entsprechenden Texturen hinterlegt.
![[Pasted image 20250220203052.png]]
Schritt 7. führt bei mir allerdings zu einem seltsamen Resultat:
![[Pasted image 20250220205835.png]]
Nach etwas Recherche habe ich allerdings herausgefunden, dass ich einfach die Scale des Replacements runter setzen muss:
![[Pasted image 20250221190117.png]]
Das Endresultat sieht somit wie folgt aus:
![[Pasted image 20250221190413.png]]
#visualcomputing #sem5 

mettlmi1
## Bilder
Als erstes suchte ich vier verschiedene Bilder aus dem Internet, die ich analysieren will. Dabei habe ich mich auf bekannte Schauspielerinnen und Schauspieler fokussiert, mit unterschiedlicher Hautfarbe und in verschiedenen Kontexten.
![[Pasted image 20241202170208.png]]
## Face Recognition
#### Viola Davis
Als erstes führen wir eine Face Recognition mit Viola Davis und Daniel Craig durch. Dafür orientiere ich mich am YouTube Tutorial von DeepFace und erstelle das entsprechende Jupyter Notebook:
![[Pasted image 20241202170325.png]]
Hier hatte ich kurz ein Problem, da im Tutorial angegeben war, man könne mit `result[0]` auf der Resultat zugreifen. Dies hat wohl aber mittlerweile geändert.

Beim ersten Anlauf mit einem Vergleich von Viola Davis und Daniel Craig erkennt das Modell korrekt, dass es sich nicht um dieselbe Person handelt (die Bilder sind aber auch sehr unterschiedlich):
![[Pasted image 20241202170441.png]]
Als zweiten Versuch probiere ich es mit Idris Elba, der ebenfalls dunkelhäutig ist:
![[Pasted image 20241202170530.png]]
Auch hier wird korrekt erkannt, dass es nicht dieselbe Person ist. Spannend ist aber, dass die Distanz weniger hoch ist, was an der Hautfarbe liegen könnte.

Probieren wir nun tatsächlich ein zweites Bild von Viola Davis.

Und tatsächlich, sie wird erkannt, obwohl sehr unterschiedliche Frisuren und Gesichtsausdrücke vorhanden sind:
![[Pasted image 20241202170901.png]]
![[Pasted image 20241202170914.png]]
## Attributes
Um die Attribute auszulesen, nehmen wir als erstes nochmals Daniel Craig. Die Attribute stimmen mehrheitlich, sogar das Alter kann trotz Sonnenbrille gut ausgelesen werden:
![[Pasted image 20241202171948.png]]
![[Pasted image 20241202171906.png]]
Probieren wir als nächstes etwas anspruchsvolleres, den diesjährigen Oscar Kandidaten Ralph Fiennes in Action:
![[Pasted image 20241202172114.png]]
Dieses Bild lässt sich leider nicht erkennen. Probieren wir es erneut:
![[Pasted image 20241202172343.png]]
Dieses mal hat das Auslesen zwar geklappt, bei den Emotionen ist sich das Modell jedoch etwas unsicher. Ob man ein Lächeln als Neutral oder Happy einstufen will, ist jedoch vermutlich auch Interpretationssache.
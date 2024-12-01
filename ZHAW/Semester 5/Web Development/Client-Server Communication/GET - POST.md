#sem5 #webdevelopment/client-server

![[Pasted image 20241129134842.png#invert]]
## GET
- Formulardaten an URL angehängt (Browser-Adressleiste)Genannt: Query String (Teil der URL)
- Vor allem für passive Anfragen (zum Beispiel eine Suche)
- Im Beispiel: %3F steht für ? (URL encoding)
- Funktionen: `encodeURIComponent`, `decodeURIComponent`
- Die GET-Methode ist ungeeignet für Anmeldedaten und andere sensitiven Informationen
## Post
- Im Formular wird method="post" gesetzt
- Formulardaten im Body des HTTP-Request gesendet
- Um Daten anzulegen oder zu aktualisieren
- Für sensitive Daten (Login): POST und HTTPS

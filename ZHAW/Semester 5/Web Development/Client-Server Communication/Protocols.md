#webdevelopment/client-server #sem5 
## HTTP
- GET : Ressource laden
- POST : Informationen senden
- PUT : Ressource anlegen, überschreiben
- PATCH : Ressource anpassen
- DELETE : Ressource löschen

```http
// request

GET /~bkrt/hallo.htmlHTTP/1.1
Host: dublin.zhaw.ch
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X...) Gecko/20100101 Firefox
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: de-de,de;q=0.8,en-us;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: keep-alive

// response

HTTP/1.1 200 OK
Date: Mon, 15 Jul 2013 17:10:56 GMT
Server: Apache/2.2.15 (CentOS)
Last-Modified: Wed, 17 Oct 2012 08:10:22 GMT
ETag: "5b018a-af-4cc3ccd575780"
Accept-Ranges: bytes
Content-Length: 175
Connection: close
Content-Type: text/html; charset=UTF-8

<!doctype html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>Hallo</title>
	</head>
	<body>
		<h1>Hallo</h1>
		<p>Ich bin eine Webseite</p>
	</body> 
</html>
```
### Status Codes
- 1XX : Information (z.B. 101 Switching Protocols)
- 2XX : Erfolg (z.B. 200 Ok, 204 No Content)
- 3XX : Weiterleitung (z.B. 301 Moved Permanently)
- 4XX : Fehler in Anfrage (z.B. 403 Forbidden, 404 Not Found)
- 5XX : Server-Fehler (z.B. 501 Not Implemented)
## Rest API
- REST: Representational State Transfer
- Programmierparadigma für verteilte Systeme
- Grundlage: Web-Architektur und [[#HTTP]]
- Leichtgewichtig (im Vergleich zu RPC oder SOAP/WSDL)
- Zugriff auf Ressourcen über ihre Adresse (URI)
- Kein Zustand: jede Anfrage komplett unabhängig
- Kein Bezug zu vorhergehenden Anfragen
- Alle nötigen Informationen in Anfrage enthalten
![[Pasted image 20241101203726.png#invert]]
## Express.js
- Minimales, flexibles Framework für Web-Apps
- Zahlreiche Utilities und Erweiterungen
- Grundlage: Node.js
- Grundlage für zahlreiche weitere Frameworks
![[Pasted image 20241101204524.png#invert]]
### Installation
```sh
$ mkdir myapp
$ cd myapp
$ npm init
$ npm install express --save

# Hilfetext ausgebennpx
$ express-generator -h
# Generator starten
$ npx express-generator
```
### Beispiel
```js 
const express = require('express')  
const app = express()  
const port = 3000

app.get('/', (req, res) => {
	res.send('Hello World!')
})

app.listen(port, () => {
	console.log(`Example app listening at http://localhost:${port}`)
})

// Routing
app.get('/', function (req, res) {
	res.send('Hello World!')
})
app.post('/', function (req, res) {
	res.send('Got a POST request')
})
app.put('/user', function (req, res) {
	res.send('Got a PUT request at /user')
})
app.delete('/user', function (req, res) {
	res.send('Got a DELETE request at /user')
})
```
### Reverse Proxy
- Express-App wird übers Internet nicht direkt angesprochen
- Zugang erfolgt über Reverse Proxy, z.B. ein nginx-Server
- Dieser leitet Anfragen an die Express-App weiter
- Zusätzliche Services: Fehlerseiten, Komprimierung, Cache
![[Pasted image 20241101204704.png#invert]]
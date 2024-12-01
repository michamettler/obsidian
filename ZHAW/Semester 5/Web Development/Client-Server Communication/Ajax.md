#sem5 #webdevelopment/client-server 

- standards-based presentation using XHTML and CSS
- dynamic display and interaction using the DOM
- data interchange and manipulation using XML and XSLT
- asynchronous data retrieval using [[#XMLHttpRequest]]
- and JavaScript binding everything together
![[Pasted image 20241129135422.png#invert]]
### XMLHttpRequest
- Low-level, umständlich einzusetzen
- Besser Abstraktionen wie Fetch oder Axios verwenden
```javascript
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
	if (xhr.readyState === 4) {
		xhr.status === 200 ? console.log(xhr.responseText)
			: console.error('error')
	}
}
xhr.open('GET', 'https://yoursite.com') xhr.send()
```
## Fetch API
- Interface for fetching resources
- Gibt Promise zurück
- Nach Server-Antwort erfüllt mit Response-Objekt

```js
cons url = 'https://...'
fetch(url).then(response => {
	console.log(response.status) // → 200
	console.log(response.headers.get("Content-Type")) // → text/plain
})  
```
### Response
- `headers` : Zugriff auf HTTP-Header-Daten Methoden `get`, `keys`, `forEach`, ...  
- `status` : Status-Code  
- `json()` : liefert Promise mit Resultat der JSON-Verarbeitung  
- `text()` : liefert Promise mit Inhalt der Server-Antwort
## Security (CORS)
- Browser blockieren normalerweise Zugriffe von Scripts auf andere Domains
- Genannt: same-origin Policy
- Grund: Angriffsmöglichkeiten reduzieren
- Manchmal ist der Zugriff auf andere Server erwünscht
- Cross-Origin Resource Sharing (CORS)
- Server kann Zugriff erlauben mit diesem Header:
  `Access-Control-Allow-Origin: *`
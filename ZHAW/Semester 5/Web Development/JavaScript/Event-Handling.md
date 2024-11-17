#webdevelopment #javascript #sem5 

## Event Listener
- im Browser können Event Handler registriert werden
- Methode: `addEventListener`
- Erstes Argument: Ereignistyp  
- Zweites Argument: Funktion, die beim Eintreten des Events aufgerufen werden soll

```html
<p>Click this document to activate the handler.</p>
<script>
	window.addEventListener("click", () => {
		console.log("You knocked?")
	})
</script>
```
### Event registrieren
- Events können auch an DOM-Elementen registriert werden
- Nur Ereignisse, die im Kontext dieses Elements auftreten, werden dann berücksichtigt

```html
<button>Click me</button>
<p>No handler here.</p>
<script>
	let button = document.querySelector("button")
	button.addEventListener("click", () => {
		console.log("Button clicked.")
	})
	/* oder: button.onclick = () => {...} */
</script>
```

### Handler entfernen
- Entfernen von Handlern mit `removeEventListener`

Beispiel – Ereignis nur einmal behandeln:
```html
<button>Act-once button</button>

<script>
	let button = document.querySelector("button")
	function once () {  
		console.log("Done.")
		button.removeEventListener("click", once)
	}
	button.addEventListener("click", once)
</script>
```
### Event weiterleiten
- Ereignisse werden für Knoten im DOM-Baum registriert
- Reagieren auch, wenn Ereignis an untergeordnetem Knoten auftritt  
- Alle Handler nach oben bis zur Wurzel des Dokuments ausgeführt
- Bis ein Handler `stopPropagation()` auf dem Event-Objekt aufruft

```html
<p>A paragraph with a <button>button</button>.</p>

<script>
	document.querySelector("p").addEventListener("mousedown", () => {
		console.log("Handler for paragraph.")
	})
	document.querySelector("button").addEventListener("mousedown", event => {
		console.log("Handler for button.")
		if (event.button == 2) event.stopPropagation()
	})
</script>
```
### Defaults
- Viele Ereignisse haben ein Default-Verhalten
- Beispiel: auf einen Link klicken
- Eigene Handler werden vorher ausgeführt
- Aufruf von `preventDefault()` auf Event-Objekt verhindert Default-Verhalten

```html
<a href="https://developer.mozilla.org/">MDN</a>
<script>
	let link = document.querySelector("a")
	link.addEventListener("click", event => {
		console.log("Nope.")
		event.preventDefault()
	})
</script>
```
### Keyboard Events
- Ereignisse `keydown` und `keyup`
- Modifier-Tasten als Attribute des Event-Objekts
- Achtung: `keydown` kann bei längerem Drücken mehrfach auslösen

```html
<p>Press Control-Space to continue.</p>  
<script>  
	window.addEventListener("keydown", event => {  
		if (event.key == " " && event.ctrlKey) {  
			console.log("Continuing!")  
		}  
	})  
</script>
```
### Mouse Events
- Mausklicks:
	- `mousedown`, `mouseup`, `click`, `dblclick` 
- Mausbewegung:
	- `mousemove`
- Berührung (Touch-Display):
	- `touchstart`, `touchmove`, `touchend`
### Scroll Events
- Ereignis-Typ: `scroll`
- Attribute des Event-Objekts: `pageYOffset`, `pageXOffset`
### Focus Events
- Fokus erhalten/verlieren: `focus`, `blur`
- Seite wurde geladen: `load`
	- Ausgelöst auf `window` und `document.body`
	- Elemente mit externen Ressourcen ( `img` ) unterstützen ebenfalls `load` -Events
	- Bevor Seite verlassen wird: `beforeunload`
- Diese Ereignisse werden nicht propagiert 
## Event Objekt
![[Pasted image 20241117163724.png#invert]]

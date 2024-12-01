#webdevelopment/javascript #sem5 #javascript 

## Baumstruktur
![[Pasted image 20241117161803.png#invert]]
- Diverse Attribute und Methoden zur Navigation im DOM-Baum
- Häufig: Array-ähnliche Objekte
- Jeder Knoten hat ein `nodeType` -Attribut
- Das Attribut `childNodes` liefert kein echtes Array (**Iteration nicht möglich**)
- ![[Pasted image 20241117161922.png#invert]]
## DOM-Operationen
### Allgemeines Beispiel
```js
/* scans a document for text nodes containing a given string and *//* returns true when it has found one */
function talksAbout (node, string) {
	if (node.nodeType == Node.ELEMENT_NODE) {
		for (let i = 0; i < node.childNodes.length; i++) {
			if (talksAbout(node.childNodes[i], string)) {
				return true
			}
		}
		return false
	} else if (node.nodeType == Node.TEXT_NODE) {
		return node.nodeValue.indexOf(string) > -1
	}
}

console.log(talksAbout(document.body, "book")) /* → true */
```
### Element auffinden
```js
let aboutus = document.getElementById("aboutus") 
let aboutlinks = aboutus.getElementsByTagName("a") 
let aboutimportant = aboutus.getElementsByClassName("important")  
let navlinks = document.querySelectorAll("nav a")
```
### Element verschieben
```html
<p>One</p>
<p>Two</p>
<p>Three</p> 

<script>
	let paragraphs = document.body.getElementsByTagName("p")
	document.body.insertBefore(paragraphs[2], paragraphs[0])
</script>
```
### Textknoten erzeugen
```html
<p>The <img src="img/cat.png" alt="Cat"> in the <img src="img/hat.png" alt="Hat">.</p>

<p><button onclick="replaceImages()">Replace</button></p>

<script>
	function replaceImages () {
		let images = document.body.getElementsByTagName("img")
		
		for (let i = images.length - 1; i >= 0; i--) {
			let image = images[i]
			if (image.alt) {
				let text = document.createTextNode(image.alt)
				image.parentNode.replaceChild(text, image)
			}
		}
	}
</script>
```
### Neues Element anlegen
- Element erzeugen: `document.createElement`
- Attribute erzeugen: `document.createAttribute`
- Und hinzufügen: `<element>.setAttributeNode`
- Element in Baum einfügen: `<element>.appendChild`
#### Abstraktion
Hilfsfunktion zum Erzeugen von Elementknoten:

```js
function elt (type, ...children) { 
	let node = document.createElement(type)
	
	for (let child of children) {
		if (typeof child != "string") node.appendChild(child)
		else node.appendChild(document.createTextNode(child))
	}
	return node
}
```
### Eigene Attribute
- Beginnen mit `"data-"`
- DOM-Attribut `dataset` liefert `DOMStringMap` mit allen `data` -Attributen
#webdevelopment/javascript #sem5 #javascript 
## Form
- Attribut action : Script das die Daten entgegen nimmt
- Attribut method : HTTP-Methode zum Senden der Daten [[GET - POST]]
	- GET : Formulardaten an URL angehängt (Default)
	- POST : Formulardaten im Body des HTTP-Request gesendet
- Gruppieren mit `<fieldset>` und `<legend>`
### Events
- Formularelement geändert: `change`
- Eingabe in Textfeld:  `input`
- Tastendrücke in aktivem Textfeld: `keydown`, `keypress`, `keyup`
- Formular absenden: `submit`
### Example
```html
<form>
	<label>Text field <input type="text" value="hi"></label>
	<label>Password <input type="password" value="hi"></label>
	<label>Textarea <textarea>hi</textarea></label>
	<label>Checkbox <input type="checkbox"></label>
	<label>Radio button <input type="radio" name="demo" checked></label>
	<label>Another one <input type="radio" name="demo"></label>
	<label>Button <button>Click me</button></label>
	<label>Select box
		<select name="cars">
			<option value="volvo">Volvo</option>
			<option value="saab">Saab</option>
			<option value="fiat">Fiat</option>
			<option value="audi">Audi</option>
		</select>
	</label>
	<input type="submit" value="Send">
</form>
```

oder 

```html
<form>
    <label>Name: <input type="text"></label>
    <label>Age: <input type="text"></label>
    <input type="submit" value="Send">
</form>

<form>
    <label for="nameid">Name: </label>
    <input type="text" id="nameid">
    <label for="ageid">Age: </label>
    <input type="text" id="ageid">
    <input type="submit" value="Send">
</form>
```
#### Varianten Vergleich
![[Pasted image 20250118160150.png]]
## Type-Attribute
- Spezielle Tastaturlayouts für Mobilgeräte möglich
- Werte: `email`, `url`, `range`, `date`, `search`, `color`
## Focus
- Aktives Element
- Bei Textfeldern: das welches Tastatureingaben aufnimmt
- Referenz in `document.activeElement`
- Anpassbar mit Methoden `focus` und `blur`
## Submit Form
![[Pasted image 20250118160740.png#invert]]
### GET-Methode
- über URL
- ungeeignet für sensitive Daten (Login)
- eher für passive Anfragen (wie Suche)
![[Pasted image 20250118160821.png#invert]]
### POST-Methode
- Formulardaten im Body senden
- für sensitive Daten (Login)
![[Pasted image 20250118160908.png#invert]]
### Example Express
#### GET
![[Pasted image 20250118160955.png#invert]]
#### POST
![[Pasted image 20250118161019.png#invert]]

#webdevelopment/javascript #sem5 #javascript 
## Form
- Attribut action : Script das die Daten entgegen nimmt
- Attribut method : HTTP-Methode zum Senden der Daten [[GET - POST]]
	- GET : Formulardaten an URL angehängt (Default)
	- POST : Formulardaten im Body des HTTP-Request gesendet
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
## Type-Attribute
- Spezielle Tastaturlayouts für Mobilgeräte möglich
- Werte: `email`, `url`, `range`, `date`, `search`, `color`
## Focus
- Aktives Element
- Bei Textfeldern: das welches Tastatureingaben aufnimmt
- Referenz in `document.activeElement`
- Anpassbar mit Methoden `focus` und `blur`
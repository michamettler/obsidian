#javascript #sem5 #webdevelopment 

## Basics

- Funktion kann zugewiesen werden
- Schlüsselwort `function`
- Parameterliste, Rückgabewert
- Die Parameterliste kann leer sein
- Die `return` -Anweisung kann fehlen: es wird `undefined` zurückgegeben
- Funktionen können an Variablen gebunden werden
- Diese Bindung kann jederzeit neu zugewiesen werden (ausser es ist eine Konstante)
- Funktionen auch als Parameter und Rückgabewert möglich: First Class Citizens

```js
const makeNoise = function () {
	console.log("Pling!")
}
makeNoise() // → Pling!

const power = function (base, exponent) {
	let result = 1
	for (let count = 0; count < exponent; count++) {
		result *= base
	}
	return result
}
console.log(power(2, 10)) // → 1024

let launchMissiles = function () {
	missileSystem.launch("now")
}
if (safeMode) {
	launchMissiles = function () {/* do nothing */}
}

// Alternative (Aufruf kann vor Deklaration stehen)
console.log(square(5))
function square (x) {
	return x * x 
}

/* mit Abstraktionen sum und range wenn verfügbar */
let result = sum(range(1, 10))
```
### Pfeilnotation
- Weitere Möglichkeit, [[Functions]] einzuführen
- Genau ein Parameter: Parameterliste muss nicht geklammert werden
- Nur ein [[Expressions]]: return und Block-Klammern können entfallen
- Möglichkeit, einfache Funktionen kompakt zu schreiben

```js
const square1 = (x) => { return x * x }
const square2 = x => x * x
```
### Rekursive Funktionen
```js
const factorial = function (n) {
	if (n <= 1) {
		return 1
	} else {
		return n * factorial(n-1)
	}
}

/* oder kurz: */
const factorial = n => (n<=1) ? 1 : n * factorial(n-1)
console.log(factorial(10)) // → 3628800
```
## Methods
- Attribute, deren Werte Funktionen [[Data Types]] sind, werden Methoden genannt
- Sie werden über das Objekt [[Objects]] aufgerufen

```sh
 let cat = { type: "cat", sayHello: () => "Meow" }
> cat.sayHello
#[Function: sayHello]
> cat.sayHello()
'Meow'
```

```js
let player = {
	sayHello: function () { return "Hello" }, /* ausführlich */
	sayHi() { return "Hi" }, /* abgekürzt */
	sayBye: () => "Bye", /* Pfeilnotation */
}

let cat = {
	type: "cat",
	say1() { return "Meow from " + this.type },
	say2: () => "Meow from " + this.type, // IMPORTANT, this referenziert nicht auf cat
}
console.log( cat.say1() ) /* → Meow from cat */
console.log( cat.say2() ) /* → Meow from undefined */

// this Objekt, über das Methode aufgerufen wird (nicht für Pfeilnotation)
```
- Man kann jederzeit Attribute oder Methoden hinzufügen
```sh
> const add = (x, y) => x + y
> add.doc =
"This function adds two values"
> add(3,4)
7
> [add.toString(), add.doc]
[ '(x, y) => x + y', 'This function adds two values' ]
```
## Scope
- Am besten: `const` , wenn veränderlich: `let` 
- Funktions-Scope ( `var` ) kann verwirren (function scope)
- wenn nichts angegeben, global
- Scope möglichst einschränken
- Die Menge der sichtbaren Variablenbindungen wird bestimmt durch den Ort im Programmtext
- Jeder lokale Gültigkeitsbereich sieht alle Gültigkeitsbereiche, die ihn enthalten
- Alle Gültigkeitsbereiche sehen den globalen Gültigkeitsbereich

```javascript
const demo = function () {
	let x = 10
	if (true) {
		let y = 20
		var z = 30
		console.log(x + y + z)
		/* → 60 */
	}
	/* y is not visible here */
	console.log(x + z)
	/* → 40 */
}
```
### Inner Functions
```js
const hummus = function (factor) {

	const ingredient = function (amount, unit, name) {
		let ingredientAmount = amount * factor
		if (ingredientAmount > 1) {
			unit += "s"
		}
		console.log(`${ingredientAmount} ${unit} ${name}`)
	}
	
	ingredient(1, "can", "chickpeas")
	ingredient(0.25, "cup", "tahini")
	// ...
}
```
## Parameter
- Anzahl Parameter muss nicht mit der Anzahl beim Aufruf übergebener Argumente übereinstimmen
- Fehlende Argumente: sind `undefined`
- Überzählige Argumente: werden ignoriert
- Überladen nicht möglich

```js
function minus (a, b) {
	if (b === undefined) return -a
	else return a - b
}
console.log(minus(10)) /* → -10 */
console.log(minus(10, 5)) /* → 5 */

// arguments
function f () {
	return arguments.length
}
function g (...args) {
	return args.length
}
console.log(f(1,2,3,4)) /* → 4 */
console.log(g("hello", "world")) /* → 2 */
```
### Default Parameters
- wenn Argument `undefined` => default Wert
- stehen am Ende der Parameter Liste

```js
function power (base, exponent=2) {
	let result = 1
	for (let count = 0; count < exponent; count++) {
		result *= base
	}
	return result
}
console.log(power(4)) /* → 16 */
console.log(power(2, 6)) /* → 64 */
```
### Rest-Parameters (Array)
- Übergebene Argumente in Array verfügbar
- Vorher können normale Parameter stehen

```js
function max (...numbers) {
	let result = -Infinity
	for (let number of numbers) {
		if (number > result) result = number
	}
	return result
}
console.log(max(4, 1, 9, -2)) /* → 9 */
```
### Spread-Syntax
- Spread-Operator `...`
- Fügt den Array-Inhalt in die Parameterliste ein
- Analog Spread-Syntax in Arrays

```js
let numbers = [5, 1, 7]
console.log(max(...numbers)) /* → 7 */
console.log(max(9, ...numbers, 2)) /* → 9 */

// zum Vergleich: Array
let more = ["a", "b"]
numbers = [5, 1, ...more, 7]
console.log(numbers) /* → [ 5, 1, 'a', 'b', 7 ] */
```
### Deconstruction
#### Arrays
- Wie bei der Zuweisung können Arrays auch bei der Parameterübergabe destrukturiert werden
- Vermeidet das spätere Zugreifen über den Array-Index

```js
const func = ( [a, b] ) => `${a}.${b}`
let result = func([5, 1]) /* → '5.1' */

// zum Vergleich: return-Wert destrukturieren
function gethttp (url) {
	if (...) return [400, "not found"]
}

let [code, message] = gethttp(url)
```
#### Objects
- Nur einzelne Attribute aus einem (möglicherweise sehr grossen) Objekt übernehmen
- Vermeidet das spätere Zugreifen über den Attributnamen

```js
let bar = 87
let obj = { foo: 12, bar, baz: 43 }

const selectFoo = ( {foo} ) => foo
console.log(selectFoo(obj)) /* → 12 */
```
## Functions of higher Orders
- Funktionen, welche Funktionen als Parameter oder Rückgabewert haben
- Sie bieten weitere Abstraktionsmöglichkeiten

```js
function repeat (n, action) {
	for (let i = 0; i < n; i++) {
		action(i)
	}
}

let labels = []

repeat(4, i => {
	labels.push(`Unit ${i + 1}`)
})
console.log(labels) // → ["Unit 1", "Unit 2", "Unit 3", "Unit 4"]
```
## Closures
```js
function wrapValue_v1(n) {
	let local = n
	let func = () => local
	return func
}

/* kürzer */
function wrapValue_v2(n) {
	return () => n
}

/* noch kürzer */
const wrapValue_v3 = (n) => () => n
```
### Decorate Functions
```js
function trace (func) {
	return (...args) => {
		console.log(args)
		return func(...args)
	}
}

/* Fakultätsfunktion */
let factorial = (n) => (n<=1) ? 1 : n * factorial(n-1)

/* Tracer an Funktion anbringen */
factorial = trace(factorial)

/* Aufruf */
console.log(factorial(3)) // → [ 3 ] → [ 2 ] → [ 1 ] → 6
```
## Functional Programming
- Funktionen sind in JavaScript ausserordentlich mächtig und sehr flexibel einsetzbar
- JavaScript unterstützt funktionales Programmieren, ist aber eine Multiparadigmensprache
### Pure Functions
- Rückgabewert der Funktion ist ausschliesslich abhängig von den übergebenen Argumenten
- Keine weiteren Abhängigkeiten
- Keine Seiteneffekte
- Wenn möglich verwenden
### Functional
- Variante von reduce , die eine Funktion zurückgibt
- Currying: Umwandeln in Funktionen mit einem Argument
- Nun lässt sich die Summe eines Arrays elegant definieren

```js
const reduce = f => init => array => array.reduce(f, init)
const add = (m, n) => m + n

reduce (add) (0) ([1,2,3,4]) /* → 10 */

/* Summe der Elemente eines Arrays */
const sum = reduce(add)(0)

sum([1,2,3,4]) /* → 10 */
```
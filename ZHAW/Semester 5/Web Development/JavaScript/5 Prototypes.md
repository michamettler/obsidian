#webdevelopment/javascript #sem5 #javascript 
## This
Bezieht sich auf das aktuelle [[2 Objects]]
Bedeutung ist abhängig davon, wo es vorkommt 
### Methodenaufruf (method invocation)
- `this` in einer Funktion ist abhängig von Art des Aufrufs
- Aufruf als Methode eines [[2 Objects]]: `this` ist das Objekt

```js
function speak (line) {
	console.log(`The ${this.type} rabbit says '${line}'`)
}

let whiteRabbit = {type: "white", speak}
let hungryRabbit = {type: "hungry", speak}

hungryRabbit.speak("I could use a carrot right now.")
// → The hungry rabbit says 'I could use a carrot right now.'
```
### Funktionsaufruf (function invocation)
- Hier ist this das globale Objekt (Node REPL: global)
- Es hat kein type -Attribut, daher wird undefined eingesetzt 
- **Dies ist praktisch immer ein Programmierfehler**
- bei `strict`-Mode undefined

```js
function speak (line) {
	console.log(`The ${this.type} rabbit says '${line}'`)
}

speak("I could use a carrot right now.")
// → The undefined rabbit says 'I could use a carrot right now.'
```
#### call, apply
- Methoden `call` und `apply` von [[3 Functions]]
- Erstes Argument: Wert von `this` in der [[3 Functions]]
- Weitere Argumente von `call` : Argumente der [[3 Functions]]
- Weiteres Argument von `apply` : Array mit den Argumenten

```js
function speak (line) {
	console.log(`The ${this.type} rabbit says '${line}'`)
}

let hungryRabbit = {type: "hungry"}
speak.call(hungryRabbit, "Burp!")
// → The hungry rabbit says 'Burp!'
```
#### bind
- Noch eine Methode von [[3 Functions]]: `bind`
- Erzeugt neue Funktion mit gebundenem `this`
- Auch weitere Argumente können gebunden werden
```js
function speak (line) {
	console.log(`The ${this.type} rabbit says '${line}'`)
}

let hungryRabbit = {type: "hungry"}  
let boundSpeak = speak.bind(hungryRabbit)
boundSpeak("Burp!")
// → The hungry rabbit says 'Burp!'
```
#### Pfeilnotation
- Arrow [[3 Functions]] verhalten sich hier anders
- Sie übernehmen this aus dem umgebenden Gültigkeitsbereich

```js
function normalize () {
	console.log(this.coords.map(n => n / this.length))
}

normalize.call({coords: [0, 2, 3], length: 5})
// → [0, 0.4, 0.6]
```
## Prototyp
![[Pasted image 20241021213051.png#invert]]
- Funktionen haben Function.prototype als Prototyp
- Arrays haben Array.prototype als Prototyp
- Diese Prototypen haben Object.prototype als Prototyp
- Mit Object.create kann ein Objekt mit vorgegebenemPrototyp angelegt werden
- Es kann dann mit weiteren Attributen versehen werden
![[Pasted image 20241021213117.png#invert]]
```sh
> Object.getPrototypeOf(Math.max) === Function.prototype
true
> Object.getPrototypeOf(Function.prototype) === Object.prototype
true
> Object.getPrototypeOf([]) === Array.prototype
true
> Object.getPrototypeOf(Array.prototype) === Object.prototype
true  
```

Example
```js
let protoRabbit = {
	speak (line) {
		console.log(`The ${this.type} rabbit says '${line}'`)
	}
}  
let killerRabbit = Object.create(protoRabbit)
killerRabbit.type = "killer"
killerRabbit.speak("SKREEEE!")
// → The killer rabbit says 'SKREEEE!'
```
## Konstruktor
![[Pasted image 20241021213449.png#invert]]
- Mit function definierte Funktionen können als Konstruktor interpretiert und mit new aufgerufen werden
- this ist dabei das neu angelegte Objekt
- Konvention: Konstruktoren mit grossen Anfangsbuchstaben
- Funktion hat prototype -Attribut: Referenz zu Prototyp
- Prototyp hat constructor -Attribut: zurück zur Funktion
- Objekte erben vom Prototyp, nicht vom Konstruktor

```sh
> Object.getPrototypeOf(p35) === Person.prototype
true
> Person.prototype.constructor === Person
true
> p35.toString()
Person with name'John'
> Object.getOwnPropertyNames(p35)
[ 'name' ]
> p35 instanceof Person
true
```

Example mit Function: (**nicht ideal**)
```js
function Person (name) {
	this.name = name
	this.toString = function () {return `Person with name '${this.name}'`}
}  
let p35 = new Person("John")
console.log(""+p35)
// → Person with name 'John'
```

Example mit Class (Syntactic Sugar):
```js
class Person {
	constructor (name) {
		this.name = name
	}
	toString () {
		return `Person with name '${this.name}'`
	}
}

let p35 = new Person("John")
console.log(p35.toString())
// → Person with name 'John'
```
### Vererbungshierarchie
- Möglich: Prototyp durch Objekt eines anderen Konstruktors ersetzen
![[Pasted image 20241021213823.png#invert]]
Example:
```js
class PartTimeEmployee extends Employee {
	constructor (name, salary, percentage) {
		super(name, salary)
		this.percentage = percentage
	}
	get salary100 () {
		return this.salary * 100 / this.percentage
	}
	set salary100 (amount) {
		this.salary = amount * this.percentage / 100
	}
}

let e18 = new PartTimeEmployee("Bob", 4000, 50)
console.log(e18.salary100) /* → 8000 */

e18.salary100 = 9000
console.log(e18.salary) /* → 4500 */
```
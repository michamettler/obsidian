#webdevelopment #javascript #sem5 
## Literals
```js
let person = {
	name: "John Baker",
	age: 23,
	"exam results": [5.5, 5.0, 5.0, 6.0, 4.5] // attribute name with space
}
```
### Optional Chaining
```js
const adventurer = {
	name: 'Alice',
	cat: { name: 'Dinah' }
}
console.log(adventurer.dog.name) /* → TypeError */
console.log(adventurer.dog && adventurer.dog.name) /* → undefined */
console.log(adventurer.dog?.name) /* → undefined */
```
## Attributes
- Attribute von Wertetypen sind unveränderlich [[Data Types]]
- Zuweisung neuer Attribute zu Wertetypen wird ignoriert [[Data Types]]
- [[Objects]] (auch Arrays, Funktionen) können aber jederzeit Attribute zugewiesen werden

```sh
> const square = n => n*n
> square.doc = "Quadratfunktion"
'Quadratfunktion'
> square(3)
9
> square.doc
'Quadratfunktion'
```

- Die (normalen) Attribute eines Arrays sind ganze Zahlen >=0
- Wird etwas anderes als Index angegeben, wird ein Attribut hinzugefügt

```sh
> let arr = [1, 2, 3]
> arr[-1] = 4
> arr['key'] = 'value'
> arr
[ 1, 2, 3 ]
> arr.key
'value'
```
#### Access Attributes
```js
let person = {
	name: "John Baker",
	age: 23,
	"exam results": [5.5, 5.0, 5.0, 6.0, 4.5]
}
console.log(person.name) /* → John Baker */
console.log(person["age"]) /* → 23 */
console.log(person["exam"]) /* → undefined */
```
#### Manipulate Attributes
```sh
# add
> let obj = { message: "not yet implemented" }
> obj.ready = false
> obj
{ message: 'not yet implemented'
, ready: false }
> obj.attr
undefined

# remove
> let obj = { message: "ready"
, ready: true, tasks: 3 }
> delete obj.message
> obj.tasks = undefined
> obj
{ ready: true, tasks: undefined }
> "message" in obj
false
> "tasks" in obj
true
```
## Object-Operations
### Analyze Objects
- Methode `keys` von Object
- Liefert Array aller Attributnamen
- Analog liefert `values` alle Werte
- Map

```sh
 let obj = {a: 1, b: 2}
> Object.keys(obj)
# [ 'a','b' ]
> Object.values(obj)
# [ 1, 2 ]
```
### Merge Objects
- Methode `assign` von Object
- Erstes Argument ist das Zielobjekt
- Attribute der weiteren Argumente ins Zielobjekt kopiert
- Referenz auf Ergebnis (erstes Arg.) zurückgegeben

```sh
> let objectA = {a: 1, b: 2}
> Object.assign(objectA, {b: 3, c: 4})
# { a: 1, b: 3, c: 4 }
> Object.assign(objectA, {m: 10}, {n: 11})
# { a: 1, b: 3, c: 4, m: 10, n: 11 }
```
### Spread
- Inhalte eines Objekts in ein anderes Objekt einfügen
- Spread-Operator `...`
```sh
> let objectA = { a: 1, b: 2 }
> let objectB = { c: 100, d: 200 }
> {...objectA, ...objectB, c: 3}
# { a: 1, b: 2, c: 3, d: 200 }
> {...objectA}
# { a: 1, b: 2 }
> {...objectA} == objectA
# false
```
### Deconstruct Objects
- Teile aus (möglicherweise grossen) Objekten extrahieren
- Auch in [[Functions]]-Parameter möglich (spätere Lektion)
```js
let bar = 87
let obj = { foo: 12, bar, baz: 43 }
let {foo, baz} = obj
console.log(foo) /* → 12 */
```
## Arrays
- Nicht jede Position muss besetzt sein
- Nicht besetzte Positionen liefern undefined
- Elemente können von beliebigem Typ [[Data Types]] sein
- Typen [[Data Types]] können gemischt werden
- gelten als `Object` mit speziellen Eigenschaften
- Test auf Array: `Array.isArray()`

```js
let a = [1, 2, 3]
a[10] = 99
console.log( a ) /* → [ 1, 2, 3, <7 empty items>, 99 ] */
console.log( a.length ) /* → 11 */
console.log( a[1000] ) /* → undefined */

let data = [41, 3.14, "pi" , [1, 2, 3], n => 2*n]
console.log(data[4](3)) // 6
```
### Array-Methods
- [[Functions]]
- `push`
- `pop`
- `shift`
- `unshift` : Einfügen und Entfernen am Array-Anfang
- `indexOf` , lastIndexOf : Element im Array finden
- `slice` : Bereich eines Arrays ausschneiden
- `concat` : Arrays zusammenhängen
- `at` : Zugriff auf Index (ECMAScript 2022)
![[Pasted image 20241011132607.png#invert]]
```sh
> let data = [ 1, 2, 3, 10, 11 ]

> data.slice(1, 3)
[ 2, 3 ]

> data.concat([100, 101])
[ 1, 2, 3, 10, 11, 100, 101 ]
let num = [5, 2, 9, -3, 15, 7, -5]

> num.filter(n => n>0) # Neues Array wird erstellt
[ 5, 2, 9, 15, 7 ]
> num.filter(n => n%3==0)
[ 9, -3, 15 ]

let num = [5, 2, 9, -3, 15, 7, -5]
> num.map(n => n*n) # Funktion für jedes Array (neues Array mit Ergebnissen wird gebildet)
[ 25, 4, 81, 9, 225, 49, 25 ]

let num = [5, 2, 9, -3, 15, 7, -5]
> num.reduce((curr, next) => curr+next)
30
> num.reduce((curr, next) => 'f('+curr+', '+next+')')
'f(f(f(f(f(f(5,2),9),-3),15),7),-5)'
```
### Array with For

```js
/* Standard for-Schleife */
for (let i = 0; i < myArray.length; i++) {
	doSomethingWith(myArray[i])
}
/* einfachere Variante für Arrays */
for (let entry of myArray) {
	doSomethingWith(entry)
}

/* forEach */
[1,2,3].forEach(item => console.log(item))
/* → 1 → 2 → 3 */
```
### Spread with Array
- Inhalte eines arrays in ein anderes Array einfügen

```sh
> let parts = ['shoulders', 'knees']
> ['head', ...parts, 'and', 'toes']
["head", "shoulders", "knees", "and", "toes"]
> [...parts]
['shoulders', 'knees']
> [...parts] == parts
false
```
### Deconstruct Arrays
- Mehrere Parameter oder Variablen [[Variables]] aus einem Array zuweisen
- Vermeidet das spätere Zugreifen über den Array-Index
```js
let numbers = [1, 2, 3]
let [a, b, c] = numbers
console.log(c) /* → 3 */
```
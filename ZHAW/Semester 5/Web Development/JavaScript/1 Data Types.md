#webdevelopment/javascript #sem5 #javascript 
## Zahlenliterale und Ausdrücke [[Expressions]]
```js
17 // Ganzzahlliteral
3.14 // Dezimalstellen
2.998e8 // Dezimalpunktverschiebung mal 10 hoch 8

0.1 // hexadezimal 3FB999999999999A, entspricht nicht exakt 0.1
0.25 // hexadezimal 3FD0000000000000, entspricht exakt 0.25

// Ausdrücke
100 + 4 * 11 // 144
(100 + 4) * 11 // 1144
314 % 100 // 14
1/0 // Infinity
Infinity + 1 // Infinity
0/0 // NaN

// BigInt
1n + 2n // 3n
2n ** 128n // 340282366920938463463374607431768211456n
BigInt(1) // 1n
Number(1n) // 1
1n + 1 // TypeError: Cannot mix BigInt and ...
```
## Typeof
```js
typeof 12 // 'number'
typeof(12) // 'number'
typeof 2n // 'bigint'
typeof Infinity // 'number'
typeof NaN // 'number' !!
typeof 'number' // 'string'
```
## Datentypen
### Verschiedene Datentypen
#### String
- `" "` und `' '` dasselbe
- Strings sind in JavaScript ein primitiver Datentyp
- String-Methoden [[3 Functions]] sind in String.prototype definiert (mehr zu Prototypen später)

```sh
> String.prototype.slice
[Function: slice]

> "Hello World".slice(0, 5)
'Hello'
```

```js
`Down on the sea` // für Multi-Line
"Lie on the ocean"
'Float on the ocean'

`half of 100 is ${100 / 2}` // 'half of 100 is 50'
`erste Zeile
zweite Zeile` // 'erste Zeile\nzweite Zeile'
```
##### String-Methoden 
- [[3 Functions]]
- `slice` : Ausschnitt aus einem String (vgl. Arrays)
- `indexOf` : Position eines Substrings (vgl. Arrays)
- `trim` : Whitespace am Anfang und Ende entfernen
- `padStart` : vorne Auffüllen bis zu bestimmter Länge
- `split` : Aufrennen, liefert Array von Strings [[2 Objects]]
- `join` : Array von Strings zusammenfügen [[2 Objects]]
- `repeat` : String mehrfach wiederholen
#### Number
- Methoden und Konstanten von `Number` [[3 Functions]]
- Methoden von `Number.prototype` können auf einzelne Zahlen angewendet werden [[3 Functions]]

```sh
> Number.MAX_VALUE
1.7976931348623157e+308
> Number.isInteger(1.5)
false
> 3500.75.toLocaleString('de-DE') '3.500,75'
```
#### Dynamisches Typenkonzept
```sh
> 8 * null
0
> "5" - 1
4
> "5" + 1
"51"
> null == undefined
true

> [!0, !0n, !"" , !false, !undefined, !null, !NaN ]
[ true, true, true, true, true, true, true ]
```
#### Math
- Methoden und Konstanten als Attribute des Math -Objekts [[3 Functions]]
- Objekt als Namensraum für Methoden und Konstanten [[3 Functions]]
- Gleich wie String und Number ist Math built-in

```sh
> Math.E
2.718281828459045
> Math.exp(1)
2.718281828459045
> Math.min(5, 2, 7, -4, 12)
-4
> Math.sin(0.5)
0.479425538604203
> Math.round(3.7)
4
> Math.random()
0.04802545627381716
```
#### Date
```js
let now = new Date()
console.log(now) /* → 2021-10 09T15:43:21.753Z */
console.log(now.getHours()) /* → 17 */
console.log(now.getUTCHours()) /* → 15 */
console.log(now.getTime()) /* → 1633794201753 */
now.setFullYear(now.getFullYear()+1)
console.log(now.toString())
// 'Sun Oct 09 2022 17:43:21 GMT+0200 (Mitteleuropäische Sommerzeit)'
```
### Werte vs. Referenz
- Objekt- und Array-Literale legen neue [[2 Objects]] an
- `==` und `===` vergleichen die Referenzen [[Expressions]]
- `const` heisst: Referenz kann nicht geändert werden

```sh
> const a = [1, 2, 3]
> const b = [1, 2, 3]
> const c = a
> a == b
false
> a == c
true
> c[0] = 99
> a
[ 99, 2, 3 ]
```

```sh
> const obj = { message: "loading..." }
> obj.message =
"ready"
'ready'
> obj = {}
# Uncaught TypeError: Assignment to constant variable.
```
#### Werte-Datentypen
- Zahlen, Strings und Wahrheitswerte sind Wertetypen
- Sie sind unveränderlich
- Zuweisung kann wie Kopieren behandelt werden
```js
let msg =
"Hello developers!"
let greeting = msg
greeting += "!!"

console.log(greeting) /* → 'Hello developers!!!' */
console.log(msg) /* → 'Hello developers!' */
```
#### Referenz-Datentypen
- Objekte und Arrays sind Referenz-Datentypen
- Sie sind jederzeit veränderbar
- Es werden Referenzen zugewiesen
- Objekte sind also Referenztypen
- Das gilt auch für Arrays und Funktionen
```js
let obj = { message: "loading..." }
let anotherObj = obj
anotherObj.message = "ready"
console.log(obj) /* → { message: 'ready' } */
```
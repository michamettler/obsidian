#webdevelopment/javascript #sem5 #javascript 

- Keine Typangabe, dynamische Typzuordnung [[1 Data Types]]
- Im gleichen Gültigkeitsbereich (s. später) kann eine Variable nicht erneut definiert werden
- Alternativen zur Variablenbindung: var und const (s. später)

```js
let width = 10
console.log(width * width) /* → 100 */
let answer = true, next = false
let novalue
console.log(novalue) /* → undefined */
```
### Kontrollstrukturen
- Vergleichbar mit C/Java
- Verzweigungen: if , switch
- Schleifen: while , do...while , for
- Spezielle Varianten der for -Schleife

```js
for (let i=1; i<50; i*=2) {
	console.log(i)
}
// → 1, → 2, → 4, → 8, → 16, → 32
```
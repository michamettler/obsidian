#webdevelopment #sem5 #nodejs
## Node.js
- Asynchrone, ereignisbasierte JavaScript-Laufzeitumgebung
- Grundlage für skalierbare Netzwerk-Anwendungen
- Basiert auf Googles V8 Engine
- Open-Source und plattformübergreifend
- Ryan Dahl 2009

```js
/* === hello-world.js === */
const http = require('http')
const hostname = '127.0.0.1'
const port = 3000

const server = http.createServer((req, res) => {
	res.statusCode = 200
	res.setHeader('Content-Type'
	,
	'text/plain')
	res.end('Hello, World!\n')
})

server.listen(port, hostname, () => {
	console.log(`Server running at http://${hostname}:${port}/`)
})
```

```sh
# Console
$ node hello-world.js
Server running at http://127.0.0.1:3000/
# Abbruch mit CTRL-C

$ node
Welcome to Node.js v22.7.0.
Type ".help" for more information.
```

## Console

### Commands
```js
let x = 30 console.log("the value of x is " , x) // → the value of x is 30
console.log('my %s has %d ears' , 'cat' , 2) // → my cat has 2 ears

console.clear() // Konsole löschen
console.trace() // Stack Trace ausgeben
console.time(); console.timeEnd() // Zeit messen
console.error() // auf stderr ausgeb
```

```js
null || 'user' // 'user'
'Agnes' || 'user' // 'Agnes'

'' || 'user' // 'user'
'' ?? 'user' // ''

1 > 2 ? 'A' : 'B' // 'B'

// ausserdem gilt:
a && b ≡ a ? b : a
a || b ≡ a ? a : b
!a ≡ a ? false : true
```
### Arguments
- Über `process.argv`zugreifbar
- Array von Kommandozeilenargumenten als Strings
```sh
/* args.js */
process.argv.forEach((val, index) => {
	console.log(`${index}: ${val}`)
})
```
### I/O
```js
const readline = require('readline').createInterface({
	input: process.stdin,
	output: process.stdout
})

readline.question(`What's your name?`, name => {
	console.log(`Hi ${name}!`)
	readline.close()
})
```
## Modules
- Einfachste Variante: alles in Funktion einpacken Immediately Invoked Function Expressions
- Globaler Namensraum nicht beeinflusst
- Diverse Varianten, z.B. Rückgabe globaler Elemente
```js
(function () {
	let foo = function () {...}
	let bar = 'Hello world' console.log(bar)
})()
```
### Module Systems
#### CommonJs
```js
/* car-lib.js */
const car = {
	brand: 'Ford',
	model: 'Fiesta'
}

module.exports = car

/* other js file */
const car = require('./car-lib')
```
#### ES6
```js
/* square.js */
const name ='square'

function draw (ctx, length, x, y, color) { ... }
function reportArea () { ... }

export { name, draw, reportArea }

/* other js file */
import { name, draw, reportArea } from './modules/square.js'
```

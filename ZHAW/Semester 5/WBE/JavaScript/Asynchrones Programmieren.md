#webdevelopment #sem5 
## Event Loop
Wenn Call Stack leer, d.h. (synchrone) Aufrufe abgearbeitet
![[Pasted image 20241101201023.png#invert]]
## Callback
Ein Callback ist eine Funktion, welche als Argument einer anderen Funktion übergeben wird und erst aufgerufen wird, wenn das Ereignis eingetreten ist.

```js
document.getElementById('button').addEventListener('click', () => {
	//item clicked
})
```
## Event Emitter
- Verwaltet Liste von Listeners zu bestimmten Events
- Listener für das Event können hinzugefügt oder entfernt werden
- Event kann ausgelöst werden → Listener werden informiert
- `emit` ruft synchron alle Listener auf

```js
const EventEmitter = require('events')  
const door = new EventEmitter()

const EventEmitter = require('events')  
const door = new EventEmitter()
door.on('open', () => {
	console.log('Door was opened')
})

oor.on('open', (speed) => {
	console.log(`Door was opened, speed: ${speed || 'unknown'}`)
})
door.emit('open')
door.emit('open', 'slow')

const myEmitter = new EventEmitter()
myEmitter.on('event', function (a, b) {
	console.log(a, b, this, this === myEmitter)
	// Prints: a b EventEmitter { domain: null, ... } true
})
myEmitter.emit('event', 'a', 'b')
// this referenziert dieEventEmitter-Instanz, an welche der Listener angehängt ist
```
## Promises
Platzhalter für einen Wert, der erst später voraussichtlich verfügbar sein wird.
Rückgabe einer Promise: potentieller Wert. Kann später erfüllt oder zurückgewiesen werden.

- `then` -Aufruf gibt selbst Promise zurück
- `catch` -Aufruf ebenfalls, per Default erfüllt
- So können diese Aufrufe verkettet werden
- Promise, welche unmittelbar resolved wird:
	- `Promise.resolve(...)`  
- Promise, welche unmittelbar rejected wird:
	- `Promise.reject(...)`
- `Promise.all()`: 
	- Erfüllt mit Array der Resultate, wenn alle erfüllt sind
	- Zurückgewiesen sobald eine Promise zurückgewiesen wird
- `Promise.race()`: Erste erfüllte oder zurückgewiesene Promise entscheidet  
- `Promise.any()`:
	- Erfüllt sobald eine davon erfüllt ist
	- Zurückgewiesene Promises werden ignoriert
	- `AggregateError`, wenn alle Promises zurückgewiesen  

```js

// Callback
const fs = require('fs')  

function readFileAsync (file, success, error) {
	fs.readFile(file, "utf8", (err, data) => {
		if (err) error(err)
		else success(data)
	})
}
/* Aufruf: */
readFileAsync(file, okCallback, failCallback)

// Promise
function readFilePromise (file) {
	let promise = new Promise(
		function resolver (resolve, reject) {
			fs.readFile(file, "utf8", (err, data) => {
				if (err) reject(err)
				else resolve(data)
			})
		})
	return promise
}

readFilePromise('/etc/hosts')
	.then(console.log)
	.catch(() => {
		console.error("Error reading file")
	})
```
### Zustände
![[Pasted image 20241101202112.png#invert]]
- `pending`: Ausgangszustand  
- `fulfilled`: erfolgreich abgeschlossen  
- `rejected`: ohne Erfolg abgeschlossen
- Nur ein Zustandsübergang möglich
- Zustand in Promise-Objekt gekapselt
## Async / Await
- Grund: Einsatz von [[#Promises]] immer noch kompliziert
- Nun: asynchroner Code ähnlich synchronem Code aufgebaut 

```js
/* Mit async/await */  
const readHosts = async () => {
	try {
		console.log(await readFilePromise('/etc/hosts'))
	} catch (err) { 
		console.error("Error reading file")
	}
}

function resolveAfter2Seconds (x) {
	return new Promise(resolve => {
		setTimeout(() => {
			resolve(x)
		}, 2000)
	})
}  
async function add1(x) { 
	var a = resolveAfter2Seconds(20)
	var b = resolveAfter2Seconds(30)
	return x + await a + await b
}
add1(10)
	.then(console.log)
```
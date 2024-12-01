#webdevelopment/javascript #sem5 #javascript 
## File API
### Synchrones Lesen aus Datei

```js
const fs = require('fs')  
let data = fs.readFileSync('/etc/hosts')console.log(data)
/* → <Buffer 23 23 0a 23 20 48 6f 73 74 20 44 61 74 61 62 61 ...> */
data = fs.readFileSync('/etc/hosts', 'utf8')console.log(data)
/* → ### Host Database#... */
```
### Asynchrones Lesen aus Datei [[6 Async]]

```js
const fs = require('fs')
fs.readFile('/etc/hosts', "utf8", (err, data) => {
	if (err) throw err
	console.log(data)
})

doSomethingElse()
```
### File öffnen (Deskriptor)

```js
const fs = require('fs')
fs.open('test.txt', 'r', (err, fd) => {
	// fd is our file descriptor
})

fs.stat('test.txt', (err, stats) => {
	if (err) {
		console.error(err)
		return  
	}
	stats.isFile() /* true */
	stats.isDirectory() /* false */
	stats.isSymbolicLink() /* false */
	stats.size /* 1024000 = ca 1MB */
})
```
### File schreiben
```js
const fs = require('fs')  
const content = 'Node was here!'

fs.writeFile('/Users/bkrt/test.txt', content, (err) => {
	if (err) {
		console.error(`Failed to write file: ${err}`)
		return  
	}
	/* file written successfully */
})
```
### Pfade

```js
const path = require('path')  
const notes = '/users/bkrt/notes.txt'
path.dirname(notes) /* /users/bkrt */
path.basename(notes) /* notes.txt */
path.extname(notes) /* .txt */
path.basename(notes, path.extname(notes)) /* notes */
```
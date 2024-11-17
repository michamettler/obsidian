#javascript #sem5 #webdevelopment 
## Overview
- Speichern von Daten clientseitig
- Einfache Variante: [[Cookies]]
- Einfache Alternative: [[#Local Storage]]
## Local Storage

- Bleibt nach Schliessen des Browsers erhalten
- Attributwerte als Strings gespeichert (mit Json codieren)
- Alternative: `sessionStorage`

```js
localStorage.setItem("username", "bkrt")  
console.log(localStorage.getItem("username")) // → bkrt  
localStorage.removeItem("username")
```
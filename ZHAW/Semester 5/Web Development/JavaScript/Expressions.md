#webdevelopment #javascript #sem5 
## Logische Ausdrücke

```js
typeof true // 'boolean'
3 > 4 // false
1 < 2 && 2 < 3 // true
4 >= 5 || !(1 == 2) // true
"ab"
==
"a" + "b" // true
```
## Vergleich

```sh
> 12 == "12"
true
> 12 === "12"
false
> 12 != "12"
false
> 12 !== "12"
true

> undefined == null
true
> undefined === null
false
> "" == false
true
> "" === false
false
```
### Vergleich Werte- und Referenzdatentypen [[Data Types]]

```sh
> [ []==[], {}=={}, (()=>{})==(()=>{}) ]
[ false, false, false ]
> [ 3.5==3.5, "abc"=="abc", false==false ]
[ true, true, true ]

### Logische Operatoren
- Wenn das Ergebnis feststeht, werden weitere Operanden nicht mehr ausgewertet (short-circuiting)
- Null coalescing operator ?? : liefert nur für null oder undefined den zweiten Operanden
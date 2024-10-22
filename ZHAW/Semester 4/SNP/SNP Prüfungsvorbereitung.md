#Prüfungsvorbereitung 
#sem4 
#snp
### Arrays

###### `sizeof`
- Grösse des Objekts in Bytes
- Bei Pointer Grösse des Pointer Objekts

##### Arrays
- wie initialisiert?
	- Kommt alles nacheinander im Speicher (vom gleichen Typ)
	- Bei `int` bspw.
		- 4 Bytes
		- nochmals unterteilt in vier (100-103 erstes Element, 104-107 zweites etc.)
- wie Zugriff auf Länge?
	- falls Zugriff auf Deklaration$$\dfrac{sizeof(array)}{sizeof(a[0])}$$
	- sonst
		- Länge übergeben (`define`)
- Strings
	- `"\0"` am Ende
	- array von `char`
- String Funktionen
	- strcopy
	- strlen (bis zum `"\0"`, kann auch über mehrere Arrays hinweg gehen falls nicht korrekt terminiert)
	- strcmp

##### Pointer
- Variable die Adresse für Memory Location beinhaltet (für Objekt)
- Mit `&a` (`a` ist der Pointer) bekommt man die Adresse
- dereferenzieren
	- `b = *p;`
	- `char* ch;`
- egal ob
	- `int *p`
	- `int* p`
- ==Achtung==
	- `int * p, q`
		- nur p ist ein Pointer
	- `char *d[20]
		- Array von 20 Pointern
	- `char (*d)[20]
		- Array von Pointers für einen Char Array (ein Pointer für jedes Element)
	- `char **ppd`
		- Pointer auf Pointer von `chars`
- Grössen der Pointer Variablen
	- `sizeof(int*) == 4`
		- obwohl `sizeof(int) == 4`
	- `sizeof(char*) == 4`
		- obwohl `sizeof(char) == 1`
	- `sizeof(double*) == 4
		- obwohl `sizeof(double) == 8`

##### Dynamische Allozierung
- dynamisch: `malloc()`, `free()`
- automatisch [10]
- Memory wird autom. in Stack, dynamisch in Heap alloziert (wenn Grösse nicht bekannt)
	- `malloc()` braucht Memory aus Heap
- Stack-, Heap-, BufferOverflow
	- Grössen beschränken für Stack und Heap
	- Buffer wenn Array überfüllt wird

##### Funktionen, Parameters-by-reference
- Parameter der Funktion als Adresse übergeben
- Bei konstanten Parametern Speicherbereich nur lesbar
- Bei Arrays
	- mit `malloc()` alloziert und als Pointer zurückgegeben (und übergeben)

##### Computer Systeme
- CPU, Memory, RAM, I/O, Bus
- Tasks
	- Aufgabem
- Schichtenmodell anschauen


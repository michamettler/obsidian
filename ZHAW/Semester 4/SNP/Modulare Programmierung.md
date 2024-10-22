#snp #sem4 
## Präprozessor, Compiler und Linker

1. Präprozessor führt Text-Ersetzungen durch (Makroanweisungen wir `#include, #define, #ifdef`)
	1. Befehle beginnen immer mit `#`
	2. Output mit `gcc -E`
	3. `#include <Datei>` extern, `#include "Datei"` intern
	4. Code kann auch selektiv ein-/ ausgeschlossen werden, bspw. bei Debugging uund Produktion
```c
#define DEBUG                /* esgeht auch #ifdef, 
								Konstante; ohne zugehörigen Wert */
#if defined DEBUG            /* ist eine Konstante DEBUG definiert? */
	printf("Program Version 1 (Debugging)\n");  /* ja */
#else
	printf("Program Version 1 (Production)\n"); /* nein */
#endif

```
1. Compiler wandelt Quellcode in Objektdateien um
	1. Objektdateien beinhalten
		1. Maschinencode
		2. Symbole, die gelinked werden müssen
		3. Daten wie debug-Infos
	2. Enthält noch offene Aufrufe
		1. auf Funktionen, die in anderer Quelldatei
		2. Variablen in anderer Quelldatei
2. Linker verbindet noch offene Aufrufe und generiert ausführbares Programm

![[Pasted image 20240611193657.png]]
## Modulare Programmierung
Beschreibt Aufteilung des Codes in mehrere Module (typischerweise pro Modul ein Headerfile, Schnittstelle).

### Headerfile
Beinhaltet Konstanten (`#define`), Funktionsdeklarationen, User definierte Types (struct, enum).

### Beispiel
header.h
```c
#define MAX 1000         /* Definition einer Konstante MAX mit dem Wert 1000 */
int doit(int b);         /* Funktionsdeklaration */
```
main.c
```c
#include "header.h"      /* alles, was in header.h steht, wird hier eingefügt */

int main(void) {
    return MAX + doit(10);
}
```
doit.c
```c
#include "header.h"      /* alles, was in header.h steht, wird hier eingefügt */

int doit(int b) {        /* Funktionsdefinition */
    return MAX + b;
}

```

Generieren des ausführbaren Programmes über
`gcc -o prog main.c doit.c`

Präprozessor macht folgendes:
neues doit.c
```c
int doit(int b);      /* Funktionsdeklaration, aus header.h */

int doit(int b) {     /* Funktionsdefinition */
    return 1000 + b;
}
```
neues main.c
```c
int doit(int b);      /* Funktionsdeklaration, aus header.h */

int main(void) {
    return 1000 + doit(b);
}
```

Anschliessend generieren Compiler und Linker ausführbares Programm.
Einbinden der Headerdateien, die nicht im aktuellen Verzeichnis sind:
`gcc -Idir -o prog main.c doit.c`
## Libraries
### C Standard Libray
Befindet sich unter /usr/lib/libc.a
Wird automatisch mit `#include <stdio.h>` eingebunden.

Weitere Bestandteile der Standardlibrary
- assert.h (Makro zur Diagnose von Programmen)
- ctype (Testen einzelner Character)
- errno (Globale Variable errno)
- float.h (Bestimmung von Eigenschaften von Gleitkommazahlen (grösste/kleinste Zahl)
- limits.h (Bestimmung Eigenschaften von ganzen Zahlen)
- locale.h (Auslesen von lokalen Eigenschaften)
- math.h (Mathematische Funktionen)
- setjmp.h (Umgehen von direktem Funktionsaufruf)
- signal.h (Ausnahmebedingungen (Division durch 0))
- starg.h (Variable Anzahl Parameter)
- stddef.h (Zusätzliche Typen (NULL))
- stdio.h (Input/Output)
- stdlib.h (Utility Funktion, malloc)
- string.h
- time.h
## Mehrfaches Include
Aufpassen, dass man nicht mehrfach etwas included. Am besten mit Konstante sicherstellen.

```c
/* Header list.h */
#ifndef LIST_H             /* Verhindert Mehrfacheinbindung */
#define LIST_H

#include "person.h"        /* Einbinden der Definitionen aus person.h */

struct List {
    struct Person inhalt;  /* Inhalt des Listenelements */
    struct List *next;     /* Zeiger auf das nächste Listenelement */
};

void insert(struct List l, struct Person p);  /* Deklaration der insert-Funktion */
void remove(struct List l, struct Person p);  /* Deklaration der remove-Funktion */

#endif /* LIST_H */
```

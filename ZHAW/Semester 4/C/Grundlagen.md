#c #sem4
### C vs. Java
- Java auf C aufgebaut
- Details weggelassen (Memory Management)
- C ist fehleranfälliger ([[Pointer]], Variablen auf Stack oder Heap, [[ZHAW/Semester 4/C/Arrays]] Grenzen)
- Java Compiler generiert Bytecode, C Maschinencode
- C nicht plattformunabhängig
- Java langsamer
### C Basics
- prozedual
- keine Klassen
- [[Funktionen]] statt Methoden
- Kompilieren:
- ![[Pasted image 20240611120803.png]]
### Sprachelemente
- Schlüsselwörter
  ![[Pasted image 20240611120910.png#invert]]
- Namen
- nummerische Literale
- String Literale
- Character Literale
- Operatoren
- Trenn- und Sonderzeichen
### Kommentare
- `/* */` Block
- `//` Linie
### Variablen
- `0-9`, `a-z, A-Z`., `_`
- Case Sensitive
- Erstes Zeichen Buchstabe oder `_`
- Keine reservierten Wörter
### Datentypen
![[Pasted image 20240611121206.png#invert]]
#### Integer
![[Pasted image 20240611121224.png#invert]]
#### Weitere wichtige Typ-Aliase
- `size_t`: aus `#include <stddef.h>` für [[ZHAW/Semester 4/C/Arrays]] Indizes
- `ptrdiff_t`: aus `#include <stddef.h>` für [[Pointer]] Subtraktion
### Literale
Im Code eingefügte, unveränderliche Werte
#### Ganzzahlen
- mit `1-9` beginnen => `dezimal`, `signed int` (wenn zu lange `long`)
- mit `0` beginnen => `oktal`, `unsigned int`
- mit `0x / 0X` beginnen => `hexa`, `unsigned int`
- mit `' '` beginne => ASCII
- explizit
	- `long 6l / 6L`
	- `long long 6ll / 6LL`
	- `unsigned 6ul / 6UL`
#### Gleitkommazahlen
- Dezimalpunkt => `double`
- Exponent (bspw. `1.6e4`) => `double`
- implizit immer `double`, kann auch explizit als `float 12f / 12F` oder `long double 15l / 15L` interpretiert werden
#### Zeichenliterale
Spezielle Zeichen mit `\` bilden:
![[Pasted image 20240611121709.png#invert]]
(kann auch durch ASCII ausgedrückt werden)
=> aus technischer Sicht Typ `int` (Hexa Code für ASCII)
#### Strings
- durch `" "` eingeschlossen
- Achtung, kein richtiger Datentyp, intern als `char` gehandhabt und mit `\0` abgeschlossen (Speicherplatz Anzahl Zeichen +1)
#### Symbolische Konstanten
Wenn Literal mehrfach gebracht wird
- mit `#define` am Anfang des Programms gesetzt
- `#define MAX_LENGTH 1000` (kein = und kein ;)
- Werte werden während Kompilieren ersetzt
### Definition vs. Deklaration
Deklaration bestimmt Name, Definition alloziert Speicher, Funktionsbody und ist immer auch eine Deklaration. Basis Typen implizit bekannt, `struct` und `enum` mit Body definieren Typen.
Typen ohne Body nur Deklaration.
`typedef` als Alias (kein neuer Typ).
#### Variablen
Meist innerhalb von [[Funktionen]] definiert.

```c
double hoehe;
int laenge, breite;
double r, radius = 15.0;
```
#### Konstanten
`const double pi = 3.14159`
#### Typ-Alias
`typedef int Index`
=> Index anderer Name für `int`
### Operatoren
Vorrang und Reihenfolge gleich wie Java (Punkt vor Strich, Klammer, etc.)

![[Pasted image 20240611145327.png#invert]]
![[Pasted image 20240611145341.png#invert]]
### Ausdrücke
- Verbindung von Operationen
- müssen nicht zugewiesen werden (kann auch allein stehen und nichts machen)

Übung:
```c
/* expression.c */
#include <stdio.h>

int main(void) {
    double x, y = 3.0;
    int i, j = 4;

    i = 2.5 + y;            /* i = 5 */
    x = 5 * i / 3;          /* x = 8.0 */
    x = 5.0 * i / 3;        /* x = 8.333333 */
    i += j;                 /* i = 9 */
    i = ++j;                /* i = 5, j = 5 */
    i = j++;                /* i = 5, j = 6 */
    x = 3 + (y = i + 5.0);  /* x = 13.0, y = 10.0 */

    printf("x = %f\n", x);
    printf("y = %f\n", y);
    printf("i = %d\n", i);
    printf("j = %d\n", j);

    return 0;
}
```
#### Type Casts

```c
double d; 
int i = 5; 
d = i / 3; 
/* d = 1.0 */

double d; 
int i = 5; 
d = (double) i / 3; 
/* d = 1.6667 */
```

### Kontrollstrukturen
#### If-Else
```c
if (n > 0) {
    result = 1;
} else if (n == 0) {
    result = 0;
} else {
    result = -1;
}
```
#### For
```c
int sum = 0;
int max = 5;
int i;

for (i = 1; i <= max; i++) {
    sum += i;    /* oder sum = sum + i */
}

/* Alternative */
for (int i = 1; i <= max; i++) { ... }

```
#### While / Do
```c
int sum = 0;
int max = 5;
int i = 1;

while (i <= max) {
    sum += i;
    i++;
}

/* oder */
do {
    sum += i;
    i++;
} while (i <= max);

```
#### Switch
```c
switch (n) {
    case 1:
        result = 1;
        break;
    case 2:
    case 3:
    case 4:
        result = 10;
        break;
    default:
        result = 0;
        break;
}
```
Achtung, break wichtig
### Input/Output
Standardlibrary, hizufügen mit
```c
#include <stdio.h>

a = puts("Hello"); 
/* Ausgabe des Strings Hello World auf Standard Output, a = EOF bei Fehler, sonst non-negative Zahl */

a = putchar('A'); 
/* Ausgabe des Zeichens A auf Standard Output, a = EOF oder non-negative */

c = getchar(void); 
/* Einlesen eines Zeichens von Standard Input */

printf(format-string, arg1, arg2,...);

(void)printf("Hello World\n"); 
/* Ohne weitere Argumente */

(void) printf("The sum of %d and %d is %d\n", a, b, a + b);
/* printf mit 3 Argumenten, wobei a + b innerhalb der Funktion ausgewertet wird; %d (Konvertierungsoperatoren) bedeutet, dass a, b und a + b*/

// Auslesen 3 Werte aus Standard Input
a = scanf("%d%d%d", &day, &month, &year);

// Overall Example
/* outformat.c */
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    const double pi = 3.1415926535;

    for (int r = 5; r <= 20; r += 5) {
        double area = pi * r * r;
        printf("Radius = %d -> Flaeche = %.2f\n", r, area);
    }
    
    return EXIT_SUCCESS;
}

```

![[Pasted image 20240611182019.png#invert]]
### Enum
```c
enum wochentage {Montag, Dienstag, Mittwoch, Donnerstag, Freitag, Samstag, Sonntag};

/* By default, the first value (`Montag`) is 0, and each subsequent value is incremented by 1. So, `Dienstag` is 1, `Mittwoch` is 2, and so on up to `Sonntag`, which is 6.*/

enum frucht {Apfel = 5, Birne = 10, Zitrone = 15};
enum frucht {Apfel = 5, Birne, Zitrone}; /* Birne = 6, Zitrone = 7 */
enum frucht {Apfel, Birne = -1, Zitrone}; /* Apfel = 0, Birne = -1, Zitrone = 0 */

/* Using Enum Values in Expressions */
enum frucht {Apfel, Birne, Zitrone};
int essen = Apfel;      /* essen = 0 */
essen = Birne + Zitrone; /* essen = 3 */

/* Als Variable */
enum wochentage {Montag, Dienstag, Mittwoch, Donnerstag, Freitag, Samstag, Sonntag};

int main(void) {
    enum wochentage w1 = Mittwoch;    /* w1 has the value 2 */
    enum wochentage w2 = 77;          /* Works as well, w2 has the value 77 */

    return EXIT_SUCCESS;
}

/* Variable mit typedef*/
enum wochentage {Montag, Dienstag, Mittwoch, Donnerstag, Freitag, Samstag, Sonntag};

int main(void) {
    enum wochentage w1 = Mittwoch;    /* w1 has the value 2 */
    enum wochentage w2 = 77;          /* Works as well, w2 has the value 77 */

    return EXIT_SUCCESS;
}
```
### Structs
Zusammenfassung von Elementen verschiedener Typen in einem Datentyp
```c
/* point3d.c */
#include <stdio.h>
#include <stdlib.h>

struct point3D {  /* Deklaration der Struktur */
    double x, y, z;
};

typedef struct { /* Alternative */
    double x;
    double y;
    double z;
} Point3D;



int main(void) {
    struct point3D ptA = {2.0, 4.0, 6.0}, ptB;

    ptB = ptA;        /* Kopiert die komplette Struktur */
    ptA.x = 5;        /* Zugriff auf einzelne Elemente */
    ptA.y += ptA.z;

    /* Output: A = (5, 10, 6), B = (2, 4, 6) */
    (void) printf("A = (%g, %g, %g)\n", ptA.x, ptA.y, ptA.z);
    (void) printf("B = (%g, %g, %g)\n", ptB.x, ptB.y, ptB.z);
    return EXIT_SUCCESS;
}
```

#c #sem4
## Funktionsdefinition

```c
int max(int a, int b) {
    if (a > b) return a;
    return b;
}

main {
	int v = max(1000, 50);
}
```

Definition muss durch Deklaration bereits bekannt sein.
Entweder durch `#include` oder explizite Deklaration im File.
Jeder Name darf auch nur eine Definition haben. Deklariert werden darf beliebig oft.

Empfohlen wird, globale Deklarationen in einem Header File unterzubringen (einbinden mit `#include`). Identische Typdefinitionen dürfen aber in verschiedenen Source-Files vorkommen.
Typischerweise am Anfang des Quellcodes nach dem `#include` nicht-öffentliche Typen definieren sowie globale Variablen:
```c
int max(int a, int b);
```

Beispiele Aufruf:
```c
int a = 5;
int b = 3;
int c;

c = max(a, b);            /* c = 5 */
c = max(7, 13);           /* c = 13 */
(void) max(15, 4);        /* OK, aber hier sinnlos */
c = 5 + max(8, a);        /* c = 13 */
c = max(max(5, 9), max(b, 12));  /* c = 12 */
```

Beispiel Definition, Deklaration
```c
/* max.c */
#include <stdio.h>

int max(int a, int b);      /* Deklaration */

int main(void) {
    int x, y, p;
    (void) printf("1. Zahl: ");
    (void) scanf("%d", &x);
    (void) printf("2. Zahl: ");
    (void) scanf("%d", &y);
    (void) printf("Maximum: %d\n", max(x, y));  /* Aufruf */
    return 0;
}

int max(int a, int b) {     /* Definition */
    if (a >= b) {
        return a;
    }
    return b;
}
```

## Parameter und Rückgabewert

### Formalitäten
Folgende Parameter sind zugelassen:
- Basis-Datentypen [[Grundlagen]]
- Structs und Enums [[Grundlagen]]
- [[ZHAW/Semester 4/C/Arrays]]
- [[Pointer]]

Folgende Rückgabewerte sind zugelassen:
- Basis-Datentypen [[Grundlagen]]
- Structs und Enums [[Grundlagen]]
- [[Pointer]]
=> [[ZHAW/Semester 4/C/Arrays]] können nicht returned werden, allerdings über [[Pointer]] (Achtung, keine Referenz auf lokale Variable aufgrund von Lifecycle).

Beispiel:
````c
int *create_copy(const int array[], int n) { // NICHT: int [] create_copy(...) { ... }
const int bytes = n * sizeof(int);
int *cp = malloc(bytes);
if (cp) memcpy(cp, array, bytes);
return cp;
}
int a[] = { 1, 2, 3, 4 };
int *copy = create_copy(a, 4);
````

### By Value
Parameter immer per Value übergeben (sprich Kopie des Werts, Veränderung der neuen lokalen Variable hat keinen Einfluss auf Original).

Beispiel 1
```c
/* increment1.c */
#include <stdio.h>

void increment(int a);

int main(void) {
    int a = 5;
    increment(a);
    (void) printf("%d\n", a);  // Ausgabe: 5
    return 0;
}

void increment(int a) {
    ++a;  // Erhöht nur das lokale 'a', nicht die Variable 'a' in main
}
```

Beispiel 2
```c
/* increment2.c */
#include <stdio.h>

int increment(int a);

int main(void) {
    int a = 5;
    a = increment(a);
    (void) printf("%d\n", a);  // Ausgabe: 6
    return 0;
}

int increment(int a) {
    return ++a;  // Erhöht 'a' und gibt den neuen Wert zurück
}

```
### By Reference
![[Pasted image 20240612155656.png#invert]]

Adresse wird auch per Value übergeben. Referenzierte Variable kann so aber in Methode modifiziert werden.

Beispiel
```c
void swap_int(int *a, int *b) {
int saved_a = *a; // den Wert der ersten referenzierten Variablen merken
*a = *b; // den Wert der ersten referenzierten Variablen überschreiben
*b = saved_a; // den Wert der zweiten referenzierten Variablen überschreiben
}
//...
int x = 10;
int y = 20;
swap_int(&x, &y);   // für diesen swap_int Call:
					// int *a = &x;
					// int *b = &y;
					// int saved_a = *a;
					// *a = *b;
					// *b = saved_a;
// nach dem Aufruf von swap_int(&x, &y) sind die Werte von x und y ausgetauscht
// x == 20
// y == 10
```

Wichtig für konstante Variablen. Somit kann sichergestellt werden, dass übergebene Referenz nur gelesen und nicht verändert werden darf (gleiches gilt für Arrays).

```c
int starts_with_capital_letter(const char *s) {
return s && isupper(*s);
}
int is_caps = starts_with_capital_letter("Hello");
// für diesen Call: const char *s = "Hello"; return s && isupper(*s);
```
#### Arrays als Parameter
Array kann auch übergeben werden, [[Pointer]] zeigt immer auf erstes Element.

![[Pasted image 20240612174724.png#invert]]

```c
// Beides äquivalent
void print_array(int a[], int n) { // identisch zu void print_array(int *a, int n)
for(int i = 0; i < n; i++) printf(" %d", a[i]);
printf("\n");
}

// innerhalb von Funktion nicht erkennbar wie übergeben.
void print_array(int a[], int n); // identisch zu void print_array(int *a, int n);
int array[] = { 1, 2, 3, 4 };
int v = 17;
print_array(array, 4); // Adresse auf das erste Element des Arrays
print_array(&v, 1); // Adresse auf die einfache Variable
```
#### Struct als Parameter
Kann auch by value übergeben werden.

```c
// by value
struct t { int v; };
void print_struct(struct t arg) {
	printf("arg.v = %d\n", arg.v);
	}
	struct t s = { 1 };
	print_struct(s); // für diesen Call:
	// struct t arg = s; printf("arg.v = %d\n", arg.v);


// by reference (effizienter)
struct t { int v; };
void print_struct(const struct t *p) {
	printf("p->v = %d\n", p->v);
	}
	struct t s = { 1 };
	print_struct(&s); // für diesen Call:
	// const struct t *p = &s; printf("p->v = %d\n", p->v);
```
### Return
- Methode wird sofort verlassen
	- `void` =>` return;`
	- nicht `void` => `return -1`
- Methode wird am Ende auch ohne `return` verlassen (geht nur bei `void`, sonst Exception)
- Erfolg By Value
- Spezialfall `main` => Compiler fügt automatisch `return 0` ein wenn kein Rückgabewert.
- Falls Adresse returned werden soll: 
### Parameter

```c
int generateRandomInt(void);
int generateRandomInt();

/* Beides korrekt, bei void wird geprüft, dass wirklich keine Parameter mitgegeben werden*/
```
### Variable Anzahl Parameter
Mittels Library `>stdarg.h>`:

```c
/* mittelwert */
#include <stdarg.h>
#include <stdio.h>
int mittelwert (unsigned anzahl, ...) {
va_list args;
```
### Funktions-[[Pointer]]
- Funktion und Funktions-Pointer-Variable müssen zusammenpassen
- Funktionsname ohne Klammern angeben
```c
void logger(char *msg); // Deklaration einer Logging Funktion
void (*out)(char *); // Definition der Variable out als Pointer auf eine Funktion
// mit einem char *s Parameter und void Return Typ
out = &logger; // out enthält die Adresse auf die logger Funktion
out = logger; // abgekürzte, übliche Schreibweise, ohne Address-of-Operator
//...
(*out)("Hello"); // Dereferenzieren von out (=logger) und die Funktion aufrufen
out ("Hello"); // abgekürzte, übliche Schreibweise, ohne Dereferenz-Operator

typedef void (*log_fp_t)(char *); // log_fp_t ist ein Alias auf void (*)(char *)
log_fp_t f = logger; // f ist vom Typ void (*)(char *)
f("Hello"); // Aufruf über die Funktionspointer Variable f

double trapez (double (*func)(double x), double start, double end, int n);
double trapez (double (*func)(double x), double start, double end, int n) {
	// ...
}

```

Beispiel:

![[Pasted image 20240612175445.png#invert]]
## Lokale Variablen
Funktionsparameter wie lokale Variable, nur innerhalb der Funktion sichtbar (keine Konflikte mit Variablen von aussen).

```c
void printLine(int n) {     /* n ist wie eine lokale Variable */
    int i;                  /* i ist lokale Variable */
    for (i = 0; i < n; i++) {
        (void) printf("_");
    }
    (void) printf("\n");
}
```
### Sichtbarkeit
![[Pasted image 20240611190459.png#invert]]

```c
#include <stdio.h>

/* vertausche1.c */
#include <stdio.h>

void vertausche(int a, int b);

int main(void) {
    int a, b;
    (void) printf("a = ");  /* Einlesen von a und b */
    (void) scanf("%d", &a);
    (void) printf("b = ");
    (void) scanf("%d", &b);
    vertausche(a, b);
    (void) printf("a = %d, b = %d\n", a, b);  // Ausgabe: a = 5, b = 10
    return 0;
}

void vertausche(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

```
## Variablen

### Globale Variablen
Können von allen Dateien des Programms aus zugegriffen werden. Mit Vorsicht verwenden. Initialwert implizit auf 0 wenn nichts anderes angegeben.

```c
/* updatemax_global.c */
#include <stdio.h>

int max = 0;  // Definition globale Variable

void updateMax(int a);

int main(void) {
    int a;
    while (1) {
        (void) printf("a = ");       /* Eingabeaufforderung */
        (void) scanf("%d", &a);      /* Einlesen von a */
        updateMax(a);                /* Aktualisierung von max */
        (void) printf("Maximum bis jetzt: %d\n", max);  /* Ausgabe des aktuellen Maximums */
    }
}

void updateMax(int a) {
    if (a > max) {
        max = a;                     /* Aktualisierung des globalen max, wenn a größer ist */
    }
}
```
### Global statische Variablen
Genau gleich wie globale, nur innerhalb gegebener Quelldatei sichtbar (private).

```c
/* updatemax_global_static.c */
#include <stdio.h>

static int max = 0;  // Definition globale statische Variable

void updateMax(int a);

int main(void) {
    int a;
    while (1) {
        (void) printf("a = ");       /* Eingabeaufforderung */
        (void) scanf("%d", &a);      /* Einlesen von a */
        updateMax(a);                /* Aktualisierung von max */
        (void) printf("Maximum bis jetzt: %d\n", max);  /* Ausgabe des aktuellen Maximums */
    }
}

void updateMax(int a) {
    if (a > max) {
        max = a;                     /* Aktualisierung des globalen max, wenn a größer ist */
    }
}
```
## Lokal statische Variablen
Innerhalb eines Blocks oder Fuunktionsbodies definiert. Nur im Block sichtbar. Wert überlebt somit und ist beim nächsten Aufruf wieder vorhanden.

```c
/* updatemax_local_static.c */
#include <stdio.h>

int updateMax(int a);

int main(void) {
    int a;
    while (1) {
        (void) printf("a = ");         /* Eingabeaufforderung */
        (void) scanf("%d", &a);        /* Einlesen von a */
        (void) printf("Maximum bis jetzt: %d\n", updateMax(a));  /* Ausgabe des aktuellen Maximums */
    }
}

int updateMax(int a) {
    static int max = 0;  /* Definition lokale statische Variable */

    if (a > max) {
        max = a;
    }
    return max;  /* max ist außerhalb dieser Funktion *nicht* sichtbar */
}
```
### Lokal automatische Variablen
Standard-Variablen, leben nur bis ans Ende des Blocks, Zugriff auch nur innerhalb von Block. Initialwert implizit undefiniert.
### Attribute
#### auto
- sehr selten in Gebrauch, kein Nutzen, einfach ohne `auto` definieren
#### register
- sehr selten in Gebrauch, Compiler sehr gut im Optimieren von Zugriffen
#### static
- ausserhalb von Funktionen wenn möglich immer brauchen, bei Funktionen eher mit Vorsicht
#### extern
- fast immer Code Smell, da es eine globale Variable definiert, die woanders definiert sein muss (unkontrollierte Zugriffe)
## Rekursive Funktionen
### Iterativ
```c
/* Iterativ */
int fakultae(int n) {
    int i = 1;
    int res = 1;
    for (i = 2; i <= n; i++) {
        res = res * i; // Multipliziert res mit i und speichert das Ergebnis wieder in res
    }
    return res; // Gibt das Ergebnis zurück
}
```
### Rekursiv
```c
/* Rekursiv */
int fakultae(int n) {
    if (n < 2) {
        return 1; // Basisfall: Wenn n kleiner als 2 ist, gib 1 zurück
    } else {
        return n * fakultae(n - 1); // Rekursiver Fall: n mal die Fakultät von (n - 1)
    }
}
```
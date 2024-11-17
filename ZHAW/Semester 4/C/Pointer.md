#c #sem4
## Motivation

![[Pasted image 20240611213841.png#invert]]

## Speicher Adressierung

- eindeutige Nummer eines Bytes ist seine Adresse
- Benötigt Element mehrere Bytes im Speicher, ist Adresse die niedrigste Adresse dieser Bytes![[Pasted image 20240611214150.png#invert]]
- mittels `sizeof` Grösse eines Elements abfragen
- mittels `&` Adresse abfragen
- Pointer ist Variable, die Speicheradresse enthält (zeigt auf ein anderes Element)

## Syntax

### Deklaration
```c
// Pointer auf eine einfache Variable
int *p;  // p ist ein Pointer auf ein Objekt vom Typ int
int* p;  // bedeutet dasselbe

// Array von Pointern
char *d[20];  // d ist ein Array von 20 Pointern auf Objekte vom Typ char

// Pointer auf ein Array
double (*d)[20];  // d ist ein Pointer auf einen Array mit 20 double Elementen

// Pointer auf Pointer
char **ppc;  // ppc ist ein Pointer auf ein Objekt vom Typ Pointer auf ein Objekt vom Typ char

// kombinierte Deklaration
int * p, q // q ist Variable von Typ int, Stern bindet stärker an Variable Namen als Typ
```

### sizeof einer Pointer Variable

Grösse einer Pointer-Variable auf System bleibt immer gleich.

```c
#include <stdio.h>

int main(void) {
    printf("sizeof(int*) == %zu\n", sizeof(int*));      // 4 (unabhängig davon dass sizeof(int) == 4)
    printf("sizeof(char*) == %zu\n", sizeof(char*));    // 4 (unabhängig davon dass sizeof(char) == 1)
    printf("sizeof(double*) == %zu\n", sizeof(double*)); // 4 (unabhängig davon dass sizeof(double) == 8)
    return 0;
}
```

### Pointer Operationen
![[Pasted image 20240611215047.png#invert]]

Adresse abfragen mittels `&`
```c
int i;       // eine Variable vom Typ int
int *ip;     // ein Pointer auf int
ip = &i;     // Abfrage der Adresse von i mittels &
```

Zugriff auf Objekt: Dereferenz-Operator mittels `*`
```c
*ip = 3;  // ip wird dereferenziert und so dem Objekt 3 zugewiesen
          // (die Variable i ist jetzt 3)
```

Fallstrick
![[Pasted image 20240611215544.png#invert]]

## void Pointer

Möglichkeit, nackte Adresse abzuspeichern (kein cast notwendig).

```c
double d       = 1.0;   // double Variable
double *dp1    = &d;    // Pointer auf double Variable
void *vp       = dp1;   // Pointer auf ein beliebiges Objekt

double *dp2 = vp;  // wird vom Compiler akzeptiert
```

## Pointer und const

Pointer Variable kann const sein, auf const Objekt zeigen oder beides.
### const-Pointer auf Variable

```c
int i = 15;
int * const ip = &i;  // der Pointer ist const, das Objekt ist variabel
*ip = 20;  // das Objekt ist variabel, Zuweisung erlaubt
int k = 17;
// ip = &k;  // der Pointer ist const, Zuweisung nicht erlaubt
```
### Pointer auf const-Objekt

```c
const int i = 15;
const int * ip = &i;  // der Pointer ist variabel, das Objekt ist const
*ip = 20;  // das Objekt ist const, Zuweisung nicht erlaubt
const int k = 17;
ip = &k;  // der Pointer ist variabel, Zuweisung erlaubt
```

### const-Pointer auf const-Objekt

```c
const int i = 15;
const int * const ip = &i;  // der Pointer ist const, das Objekt auch
*ip = 20;  // das Objekt ist const, Zuweisung nicht erlaubt
const int k = 17;
ip = &k;  // der Pointer ist const, Zuweisung nicht erlaubt
```

## Pointer und NULL

Speicheradresse 0 unzulässig. Für NULL wird `stdio.h` verwendet.

Beispiel

```c
/* null_pointer.c, gibt drei Zeilen aus */
#include <stdio.h>

int main(void) {
    int *p1 = 0;        /* das funktioniert */
    int *p2 = NULL;     /* das ist aber sauberer */

    if (p1 == NULL) printf("p1 ist NULL\n");
    if (p2 == 0) printf("p2 ist 0\n");
    if (p1 == p2) printf("p1 ist gleich p2\n");
    if (!p1) printf("p1 ist false\n");

    return 0;
}
```
## Pointer und struct

Schreibweise `->` da häufig verwendet.

Beispiel
```c
#include <stdio.h>
#include <string.h>

struct student {          /* Deklaration der struct student */
    int studNr;
    char name[30];
    char vorname[30];
};

struct student *sp, s;    /* sp ist Pointer auf eine Struktur student */
s.studNr = 999;           /* Initialisierung von s */
(void)strcpy(s.name, "Mueller");
(void)strcpy(s.vorname, "Max");
sp = &s;                  /* sp zeigt auf die Struktur s */

(void)printf("Student: %s %s, Nr. %d\n", (*sp).name, (*sp).vorname, (*sp).studNr);
/* oder besser (wegen Lesbarkeit) */
(void)printf("Student: %s %s, Nr. %d\n", sp->name, sp->vorname, sp->studNr);

int main(void) {
    struct student *sp, s;    /* sp ist Pointer auf eine Struktur student */
    s.studNr = 999;           /* Initialisierung von s */
    (void)strcpy(s.name, "Mueller");
    (void)strcpy(s.vorname, "Max");
    sp = &s;                  /* sp zeigt auf die Struktur s */

    (void)printf("Student: %s %s, Nr. %d\n", (*sp).name, (*sp).vorname, (*sp).studNr);
    /* oder besser (wegen Lesbarkeit) */
    (void)printf("Student: %s %s, Nr. %d\n", sp->name, sp->vorname, sp->studNr);

    return 0;
}
```
## Diverse Beispiele

```c
/* pointers.c */
int main(void) {
    int *ap, *bp;
    int c = 5, d;

    ap = &c;             // ap = Adresse von c,        *ap = 5
    c++;                 // c = 6,                     *ap = 6
    *ap = -10;           // c = -10,                   *ap = -10
    bp = &c;             // bp = Adresse von c,        *bp = -10
    c = 15;              // *ap = 15,                  *bp = 15
    *bp = *ap / 2;       // c = 7,                     *ap = 7,    *bp = 7

    ap = &d;             // ap = Adresse von d,        *bp = 7
    d = 3;               // *ap = 3,                   *bp = 7

    return 0;
}
```
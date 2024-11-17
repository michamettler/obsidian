#c #sem4
## sizeof
- gibt Grösse von Typen oder Variablen aus
- wird zu Kompilierzeit ausgewertet

Beispiele

sizeof(int)
![[Pasted image 20240611210757.png#invert]]
```c
int v = 1234;            // Wert von v in hexadezimaler Darstellung ist 0x000004D2
printf("size=%zd\n", sizeof(v));  // Ausgabe der Größe von v in Bytes, was 4 ist
```

sizeof(struct)
![[Pasted image 20240611210832.png#invert]]
```c
struct { 
    short s; 
    char a, b; 
} v = { 1234, 'a', 'b' };  

printf("size=%zd\n", sizeof(v));  // Ausgabe der Größe von v in Bytes, die jedoch mehr als 4 sein sollte
```
## Java vs. C Arrays
![[Pasted image 20240611210910.png#invert]]
## Aufbau
- Elemente direkt hintereinander im Speicher
- Array mit 100 int-Elemente belegt genau 400 Bytes (für 4-Byte ints)
- lokal kein default-Wert, global Wert 0

## Anordnung im Speicher
![[Pasted image 20240611211152.png#invert]]

Daraus resultiert, dass der Array seine Länge nicht kennt.

## Initialisierung und Zugriff

```c
int a[5] = {4, 7, 12, 77, 2};   /* Alle 5 Elemente werden initialisiert */
int b[] = {4, 7, 12, 77, 2};    /* Länge wird implizit auf 5 gesetzt */
int c[5] = {4, 3, 88, 5};       /* OK, letztes Element erhält Wert 0 */
int d[5] = {4, 3, 88, 5, 3, 6}; /* Kompilierfehler */

int a[5] = {4, 7, 12, 77, 2};
a[3] = 4;
a[8] = 222;  /* Kein Fehler zur Laufzeit!!! */
a[-3] = 36;  /* Kein Fehler zur Laufzeit!!! */
```
### Konstante Arrays

```c
int a[5] = {0, 1, 2, 3, 4};
const int b[5];                /* Funktioniert, macht aber kaum Sinn */
const int c[5] = {5, 6, 7, 8, 9};
const int d[] = {10, 11, 12, 13, 14};

a[0] = 4;                      /* OK */
b[1] = 55;                     /* Kompilierfehler */
c[2] = 666;                    /* Kompilierfehler */
d[3] = 6666;                   /* Kompilierfehler */
```

## Länge
- Grenze mitgeben
- speziellen Wert als End-Marke verwenden

Beispiel End-Marke
```c
#define DATA_SENTRY (-1)  // oder ein anderer Wert, der sonst nicht existieren kann
int array[] = { 1, 2, 3, DATA_SENTRY };
...
for (size_t i = 0; array[i] != DATA_SENTRY; i++) {
    ... array[i] ...;
}
```
Oder berechnen
$$\dfrac{sizeof(array)}{sizeof(a[0])}$$
=> dies allerdings nur ausserhalb der Funktion, wie folgendes Beispiel
```c
/// OK: Length as parameter ///
void access(int array[], size_t n) {
    for(size_t i = 0; i < n; i++) {
        ...
    }
}

int a[100] = { 0 };
size_t n = sizeof(a) / sizeof(a[0]);
access(a, n);

/// OK: same, but with #define ///
void access(int array[], size_t n) {
    for(size_t i = 0; i < n; i++) {
        ...
    }
}

#define N 100
int a[N] = { 0 };
access(a, N);
```
## Strings
![[Pasted image 20240611212520.png#invert]]

- kein Typ String in c, dafür ein char-Array
- letztes Element enthält `\0`
- String Literal in "" geschrieben
### Deklarationen
![[Pasted image 20240611212549.png#invert]]
#### Ohne Initialisierung

```c
char ca1[20];  /* char-Array für 20 chars, hat noch nichts mit einem String zu tun! */

char ca2[];    /* Kompilierfehler */
ca1 = "hello, world";  /* Kompilierfehler */

ca1[0] = 'h';
ca1[1] = 'e';
...
ca1[11] = 'd';
ca1[12] = '\0';  /* Jetzt kann man sagen, in ca1 ist ein String abgelegt! */
```

Beispiele
```c
/* string_printf.c */
#include <stdio.h>

int main(void) {
    char a[] = "Hans";
    char b[5];

    (void) printf("%s\n", a);  // String in a wird ausgegeben --> "Hans", printf erkennt \0 am Ende

    b[0] = 'H'; b[1] = 'a'; b[2] = 'n'; b[3] = 's';
    (void) printf("%s\n", b);  // String in b wird ausgegeben --> "Hans", kein \0 nach dem s --> printf gibt weiter Zeichen aus bis irgendwann \0 im Speicher gefunden wird

    b[4] = '\0';
    (void) printf("%s\n", b);  // \0 am Ende wird von printf erkannt

    return 0;
}
```

### Library string.h

Wichtige Funktionen
- strlen(): Länge des Strings (zählt Zeichen bis abschliessendes `\0` (ohne Terminator, sizeof() mit))
- strcmp(): Vergleichen zweier Strings
- strcopy(): Kopieren eines Strings von Source nach Destination (inkl. Return des [[Pointer]] nach Destination, Grösse beachten)
- strcat(): Zusammenhängen zweier Strings
Alle diese Funktionen sind auf `\0` angewiesen.

Beispiel
```c
/* strings.c */  
#include <stdio.h>  
#include <string.h>  
  
char a[4] = "Maus";  
char b[] = "Hund";  
char c[14] = "Katze";  
char d = 'x';  
  
int main(void) {  
    printf("strlen(a)=%d\n", strlen(a));  /* Ausgabe? */ // 8  
    printf("strlen(b)=%d\n", strlen(b));  /* Ausgabe? */ // 4  
    printf("strlen(c)=%d\n", strlen(c));  /* Ausgabe? */ // 5  
    strcat(c, b);  
    printf("%s\n", c);  /* Ausgabe? */ // KatzeHund  
    strcat(c, a);  
    printf("%s\n", c);  /* Ausgabe? */ // KatzeHundMausHund  
    printf("%c\n", d);  /* Ausgabe? */ // u  
  
    return 0;  
}
```

#### Initialisierung

Initialisierung geht auch über Pointer:
```c
char a[] = "hello, world";
char *pa = "hello, world";

char a[] = "hello Switzerland";
char *pa = "hello Switzerland";
// a = pa; // This line would cause a compilation error pa = a;
```

Beinahe identisch, aber
- a ist char-Array und stellt fixe Startadresse dar (kann nie auf anderen Speicherbereich zeigen)
- pa ist Pointer-Variable, kann auch später anderen Wert enthalten
![[Pasted image 20240612145034.png#invert]]
## Pointer von Arrays

Adresse des ersten Elements des Arrays ist identisch mit Startadresse des Arrays

![[Pasted image 20240612151205.png#invert]]
![[Pasted image 20240611221220.png#invert]]

```c
int a[3] = {2, 4, 6};
int b[3] = {2, 4, 6};
int *p;

p = a; // OK, p zeigt auf Array a, identisch mit p = &a[0];
p = b; // OK, p zeigt auf Array b, identisch mit p = &b[0];

// a = b; // Kompilierfehler, weil die Startadresse von a nicht veränderbar ist
```

Die Adressen der Elemente sind `sizeof(ElementTyp)` auseinander.
Die Startadresse ist nicht veränderbar.

### Gleichheit von Adressen
Operatoren (bspw. `==` ) können auch auf Pointer angewandt werden.
Somit wird bei Arrays die Startadresse, und nicht der Inhalt verglichen.

Beispiel

```c
int a[3] = {2, 4, 6};
int b[3] = {2, 4, 6};
int *p = a;

if (a == b) {
	// ist die Start-Adresse von a gleich der Start-Adresse von b?
}

if (a != p) { 
	// ist die Start-Adresse von a ungleich der Adresse in p? 
}
```

Für Inhaltsvergleich muss ein For-Loop erstellt werden.

```c
for (size_t i = 0; i < 3; i++) {
    if (a[i] == b[i]) {
        // Vergleich elementweise...
    }
}
```

### Adressen von Array Elementen
![[Pasted image 20240611221716.png#invert]]
### Mehrdimensionale Arrays Parameter
In Parameterliste alle Dimensionen ausser erste angeben
- Wenn Arrayschreibweise für erste Dimension => Grösse irrelevant
- Grösse bei mehrere Dimensionen angeben wegen [[Pointer]]-Arithmetik

Beispiel
```c
void print_matrix_2x3(double (*m)[3]) { // Syntax Sugar: ...(double m[][3])
	for(int row = 0; row < 2; row++) {
		for(int col = 0; col < 3; col++) printf(" %f", m[row][col]);
		printf("\n");
	}
}

double matrix[2][3] = { { 1, 2, 3 }, { 4, 5, 6 } };
print_matrix_2x3(matrix);   // für diesen Call:
							// double (*m)[3] = matrix; ... m[row][col]...
```
## Rechnen mit Adressen: Pointer-Arithmetik
![[Pasted image 20240611222023.png#invert]]

- ist p ein Pointer auf erstes Element von Array, so zeigt Ausdruck `(p + i)` auf der i-te Element des Arrays.
- Compiler wandelt um in $$p + (i * sizeof(Element) Bytes)$$
- Alle `x[n]` Zugriffe werden so umgewandelt in `*(x + n)`.

Beispiel
```c
int a[5] = {2, 4, 6, 8, 10};
int *p = a;
// alle folgenden Zeilen sind identisch
a[3] = 1;        // vom Compiler intern als *(a + 3) = 1 generiert
*(a + 3) = 1;    // a steht für die Startadresse von a
*(p + 3) = 1;    // p ist auf die Startadresse von a gesetzt
p[3] = 1;        // vom Compiler intern als *(p + 3) = 1 generiert
```

#### Addition und Subtraktion

```c
int a[5] = {2, 4, 6, 8, 10};
int *p;

p = a + 3;        // identisch zu p = &a[3];
*(p + 1) = 17;    // identisch zu p[1] = 17 oder a[4] = 17;
*(p - 1) = 13;    // identisch zu p[-1] = 13 oder a[2] = 13;
*(p++) = 19;      // identisch zu *p = 19; p++; oder a[3] = 19; p = &p[1];
p -= 2;           // identisch zu p = &p[-2] oder p = &a[2];
// a++;          // Kompilierfehler, da a = &a[1] nicht erlaubt ist
```
##### Mehrdimensionale Arrays
```c
// 1D
double values [10] = ( 0.0, 5.0 };
double (*Values) = values; // pointer to double (or: double *Values)

// 2D
int matrix[2](3] = ((1, 2, 3}, (4, 5, 6}) ;
int (*Matrix) [3] = matrix; // pointer to array 3 of int

// 3D
char board [8] [8] [3] = ( 0 };
char (*pBoard) [8][3] = board; // pointer to array 8 of array 3 of char

// etc

// Arithmetik
int p [10] = ( 0 };
// p[2]
ist identisch zu * (p + 2)
int 9[5] [8];
// q[2][3] ist identisch zu (q[2]) [3]
// ebenfalls identisch zu * (* (q + 2) + 3)
```

Beispiel
![[Pasted image 20240612180136.png#invert]]
##### Jacked Arrays
```c
char *jagged [] = {
"January", "February", "March", "April", "Mai", "June",
"July", "August", "September", "October", "November",
"December" } ;
//...
if (jagged [3] [2] == 'r') {
//...
}

// jagged [3] is "April"
// jagged [3][2] is the third character of April
```
##### Beispiele
```c
/* 2d.c */
#include <stdio.h>
int main(void) {
char days[7][10] = {"Monday", "Tuesday", "Wednesday",
"Thursday", "Friday", "Saturday", "Sunday"};
char *pdays[7] = {"Monday", "Tuesday", "Wednesday",
"Thursday", "Friday", "Saturday", "Sunday"};

(void) printf("%zd %zd\n", sizeof(days), sizeof(pdays)); // 70 56
(void) printf("%zd %zd\n", sizeof(days + 1), sizeof(pdays + 1)); // 8 8
(void) printf("%zd %zd\n", sizeof(days[1]), sizeof(pdays[1])); // 10 8
(void) printf("%s %s\n", days[4], pdays[4]); // Friday Friday
(void) printf("%zd\n", days[4] - days[1]); // 30 (4*10-1*10)
(void) printf("%zd\n", pdays[4] - pdays[1]); // 27 (aber beliebig)
(void) printf("%zd\n", &days[2][3] - &days[0][0]); // 23 (2*10+3-0*10+0)
(void) printf("%zd\n", &pdays[2][3] - &pdays[0][0]); // 18 (aber beliebig)
}```
#### Relationen

```c
int a[5] = {2, 4, 6, 8, 10};
int *p = a + 3;  // identisch zu p = &a[3]; oder p = &a[0] + 3;

if (a < a + 1) {
    // true, da &a[0] < &a[1]
}

if (a > p) {
    // false, da &a[0] < p, weil p = &a[3]
}
```
#### Sonstige Beispiele
![[Pasted image 20240611222416.png#invert]]

Übung
```c
/* arraypointer. c */
#include <stdio.h>
int main (void) {
double table [10];
double *pt, *gt;
pt = table;
*pt = 0;
*(pt + 2) = 3.14;
pt [5] = 2.5;
// Tabelle: 0. 0,?,3.14, ?,?, 2.5, ?,?,?,?
pt = table + 2;
gt = pt;
*qt = 2.718;
gt[4] = 3.5;

*(table + 8) = 6.7;
// Tabelle: 0. 0, 2, 2. 718,?, 2, 2. 5, 3. 5,?, 6. 7,?
pt = table;
qt = table + 10;
printf("8d\n", qt - pt) ;
printf("8d\n", (int)gt - (int)pt) ;
// Output 80 // bzw. 10 * sizeof (double)
for (; pt < qt; pt++) {
	*pt = 1.23;
}
// 1.23,... , 1.23
```
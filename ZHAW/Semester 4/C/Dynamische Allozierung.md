#c #sem4
## Speicherorte

Per Default wird Speicher automatisch auf dem Stack alloziert. Kann auch dynamisch auf Heap alloziert werden.
![[Pasted image 20240612152833.png#invert]]

## Stack
Mit jedem [[Funktionen]] passiert automatische Reservation auf Stack für lokale automatische Variablen. Besonders wichtig bei Rekursion. Verändert sich dauernd (Überlauf möglich).
- Grosse Datenmengen nicht auf Stack speichern
- Rekursive Aufrufe nicht zu tief und sicher terminieren
## Heap
Möglichkeit, dynamisch Speicher aus Heap anzufordern. Wird durch `<stdlib.h` angeboten.

Beispiel:
```c
// aus stdlib.h
// alloziert "size" Bytes vom Heap und gibt die Start Adresse zurück
void *malloc(size_t size);
// alloziert "nitems" mal "size" Bytes, setzt sie auf 0, und gibt die Adresse zurück
void *calloc(size_t nitems, size_t size);
// vergrössert (oder verkleinert) einen vorgängig angeforderten Speicherbereich
void *realloc(void *ptr, size_t size);
// gibt einen oben angeforderten Speicherbereich frei
void free(void *ptr);
```

free() sehr wichtig, sonst kommt es zu Memory Leak.

### Malloc()

![[Pasted image 20240612154241.png]]

Dynamisch allozierter Speicher wird zur Laufzeit auf Heap angefordert (Speicher Reservation + Pointer zurückgeben).
=> Brauchen, wenn Grösse unbekannt

Anwendung
```c
int *p = malloc(3 * sizeof(int));
if (p == NULL) { /* error handling falls kein Speicher mehr verfügbar */ }
p[1] = 5;
```

Beispiel anfordern:
```c
size_t number_of_bytes = get_file_size(my_file);
char *data = malloc(number_of_bytes);
if (!data || read_data(data, my_file) == -1) { /* error... */ }
process_data(data);
free(data);
```

Beispiel LinkedList:
```c
typedef struct node { struct node *next; void *payload; } node_t;

node_t linked_list_append(node_t *root, void *payload) {
	assert(root); // hard precondition of the function
	node_t *p = root; // start point of the linked list
	
	while(p->next) p = p->next; // seek for the end of the linked list
	
	p->next = malloc(sizeof(node_t)); // allocate a new node
	if (p->next) { // if allocation was successful...
		*(p->next) = (node_t){ NULL, payload }; // ... set the node’s content
	} // ... else do nothing
	
	return p->next; // returns NULL if failed, otherwise
} 
```
### free()

![[Pasted image 20240612154429.png]]

Gibt Speicher wieder frei, Achtung, nicht doppelt oder vergessen zu verwenden

```c
int *p = malloc(3 * sizeof(int));
if (p == NULL) { /* error handling */ }
p[0] = 5; p[1] = 10; p[2] = 15
// ...
free(p); // Speicher wird freigegeben
```

## Sicherheit
Auf Heap werden auch Verwaltungsinformationen gespeichert, somit Vorsicht geboten
### Stack-Overflow
kein Speicherplatz mehr, bspw. bei Rekursion oder DDoS

```c
int main(int argc, char *argv[])
{
char buffer[20];
strcpy(buffer, argv[1]); // argv[1] kann beliebig lang sein
return 0;
}
```
### Buffer-Overflow
Speicher wird überschrieben, bspw. durch Hackercode.
### Heap-Overflow
Heap ist zu klein oder fragmentiert.

Massnahmen:
- Ablauf anpassen
- Fragmentierung (Memory Pools)
- konsequentes Fehler Handling
- Anwender-Eingaben prüfen

Negativbeispiel
```c
int main(int argc, char *argv[]) {
char* a = malloc(strlen(argv[1]) * sizeof(char));
```
### Sichere Funktionen
![[Pasted image 20240612155358.png]]


#c #sem4 
## Make Utility
Dient zum inkrementellen Erzeugen von Programmen.
- inkrementell: nur diejenigen, die out-of-date

## Makefile
Regeln, wann was wie auszuführen ist.

Enthält
- Kommentare
- Variablendefinitionen
- Explizite regeln

Ausserdem
- nicht alle Targets repräsentieren File
- erstes Target wird ausgeführt, wenn nichts anderes angegeben. Defaults:
	- default
	- all
	- clean
	- test
- diese speziellen Targets mit `.PHONY` kennzeichnen, damit diese nicht als File interpretiert werden

Beispiel PHONY
```c
TARGET = ...                  # Definition der Zielvariablen

.PHONY: default all clean test # Definition der Phony-Ziele

default: $(TARGET)            # Das Standardziel verweist auf das Ziel, das in TARGET definiert ist

...

$(TARGET): ...                # Definition des Ziels, das in TARGET angegeben ist
```

### Aufbau Regel
![[Pasted image 20240611205306.png]]

Beispiel
```c
# rechner wird aus allen Objektdateien (.o) zusammengebaut; clean dient
# dazu, alle Objektdateien zu entfernen;
all: rechner

rechner: add.o sub.o mul.o div.o main.o
    gcc -o rechner add.o sub.o mul.o div.o main.o

clean:
    rm -f *.o rechner

# so entstehen die Objektdateien (def.h und Makefile werden angegeben, um
# auch bei Veränderungen dieser Dateien die Kompilierung neu zu starten)
add.o: add.c def.h Makefile
    gcc -c add.c

sub.o: sub.c def.h Makefile
    gcc -c sub.c

mul.o: mul.c def.h Makefile
    gcc -c mul.c

div.o: div.c def.h Makefile
    gcc -c div.c

main.o: main.c def.h Makefile
    gcc -c main.c
```

- zeilenorientiert, wenn auf mehrere Zeilen aufteilen mit \ arbeiten
### Variablen
Werden bei jeder Verwendung neu als Text expandiert.

Beispiel
```c
TARGET = my-program
OBJECTS = main.o persistency.o model.o view.o ctrl.o

$(TARGET): $(OBJECTS)
	gcc -o $(TARGET) $(OBJECTS)
	echo "#### $(TARGET) done ####"
```
### Erweiterungen
Suffix Regel, beschreibt basierend auf File Extension, welche Aktion ausgeführt werden soll.

![[Pasted image 20240611205949.png]]

Beispiel
```c
PNGFILES := $(DOTFILES:%.dot=%.png)  # Erzeugt die Liste der PNG-Dateien aus der Liste der DOT-Dateien

doc: $(PNGFILES)  # Das Ziel 'doc' hängt von den PNG-Dateien ab

...

# Regel, um eine PNG-Datei aus einer DOT-Datei zu erstellen, falls die PNG-Datei veraltet ist
%.png: %.dot
    dot -Tpng $< > $@
```
### Fehler ignorieren
![[Pasted image 20240611210116.png]]
### Sonstige Befehle
- dry Run: `make -n`
- Ausgabe nur in Hochkomma `@echo "Hello World"`
- Auflisten aller built-in Regeln `make -n -p | grep CFLAGS`
	- `grep` Zeigt wo überall CFLAGS gesetzt und verwendet wird
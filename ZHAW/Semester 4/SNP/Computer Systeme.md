#snp #sem4 
## Schichtentrennung

![[Pasted image 20240612181503.png]]
![[Pasted image 20240612181532.png]]
### Computer Hardware
![[Pasted image 20240612181554.png]]
#### CPU
- Programmausführung
- Datenverarbeitung
- Master am Systembus
#### Bus Interface
- Zugriff auf andere Elemente des Systems
- bidirektional (Read-Write)
#### Control Unit (Programmausführung)
- Wo im Memory nächste Maschineninstruktion leigt
#### Data Path
- ALU (Arithmetic-Logic-Unit)
- Register (schneller Zwischenspeicher)
### Memory
- über System Bus angesprochen
- Entgegennehmen von Daten
- Liefern von Daten
- RAM: Random-Access-Memory (behält Daten nur so lange wie Strom)
- ROM: Daten definiert zur Produktionszeit, behält Daten
### Input/Output
- Anbindung an Aussenwelt
- Lese-Schreibe Schnitttstellen
- wichtig: Everything is a File => die meisten Interaktionen geschehen durch Lesen und Schreiben von Files (gelesen wird mit File-Position, beim Lesen startet immer mit 0, leeres File Länge 0)
#### Directory
Inode (Verwaltungseinheit von Files mit i-Nummer) nicht anwenderfreundlich, deshalb Verzeichnisse mit Name-zu-ino-Paaren.
#### File Deskriptoren
Kernel verwaltet geöffnete Files mit Deskriptoren (int Wert).
#### Streams
- logische Sequenz von Daten
- Abstraktion von Files für auch nicht Unix ähnliche Systeme
- assoziiert mit einem File
##### Buffering
- unbuffered: direkt am Zielort ankommen
- fully-buffered: Daten können gesammelt werden und erst wenn Buffer voll wird Block ans Ziel übermittelt
- line-buffered: erst wenn Zeilenende erkannt als Block ans Ziel übermittelt
#### IO Attribuute
![[Pasted image 20240612190052.png]]
## Betriebssystem (OS)
- Verwalten der Hardware Ressourcen
- [[Task, Prozesse und Threads]], Memory, Filesystem
### [[Task, Prozesse und Threads]]
Aufgabe, wird von CPU abgearbeitet
- Single Task
- Multi Task
#### Prozess
Programm in Ausführung, ein Kontrollfluss/Stack, eigenes Memory
#### Thread
Separater Kontrollfluss/Stack innerhalb eines Prozesses
#### Multitasking
![[Pasted image 20240612182253.png]]
## System Calls
Auf geschützte HW zugreifen => Mode Switch (Kernel Mode, User Mode), insbesondere auch für Programme wichtig um auf CPU zuzugreifen. Gehen immer über syscall() Funktion.

Jede Kernel-Funktion hat eine eigene Nummer.
### man pages
Hilfestellungen
### System Library
vereinfacht Portierung von Programmen auf verschiedene Systeme (Wrapper-Funktionen für System Calls) und standardisierte Basisfunktionalitäten
#### Virtuelles Memory
Alle Prozesse haben selben virtuellen Memory Bereich.
- MMU: übersetzt logische Adresse in physische (jedes virtuelle Memory muss mit physikalischem hinterlegt sein)
- MPU: überwacht Adress-Bus auf unerlaubte Speicherzugriffe und löst Konflikte

### (Bash) Shell
- Anweisungen an Betriebssystem (unter Linux auf /etc/passwd)
- Kommandos werden in Tokens zerlegt
#### Pipe
Speist stdout von Kommando in stdin des nächsten.
## Filesystem
![[Pasted image 20240612183217.png]]
![[Pasted image 20240612183224.png]]


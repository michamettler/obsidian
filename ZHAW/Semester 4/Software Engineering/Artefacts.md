#softwareengineering #sem4

## Use Cases
### Grundlagen
- Akteure (externe Person, Zeit oder System, die/das mit System interagiert)
	- Primärakteur
		- initiiert Anwendungsfall
		- Hauptnutzen
	- Unterstützender Akteur
		- Hilft System zur Bearbeitung eines Anwendungsfalls
	- Offstage Akteur
		- Weitere Stakeholder, nicht direkt mit System interagiert
- Arten
	- Kurz (Brief UC)
		- Titel + 1 Absatz
		- Beschreibt Standardablauf (keine Varianten oder Problemfälle)
	- Informell (Casual UC)
		- Titel + informelle Beschreibung in ein bis mehreren Absätzen
		- Beschreibt auch Varianten
	- Vollständig ([[Fully Dressed Use-Case]])
		- Titel + alle Schritte und Varianten im Detail
		- weitere Infos zu Vorbedingung, Erfolgsgarantie, etc.
		- ![[Pasted image 20240606165434.png#invert]]
- Allgemein
	- mehr als eine Aktion
	- Aktiv formuliert (Verb + evtl. Objekt vorangestellt, "Kasse eröffnen")
	- beschreibt Ziel
	- enthält Trigger
	- beschreibt Logik, nicht konkrete Umsetzung (Implementierung offen lassen)
	- keine kann-Formulierungen
- UC-Diagramm
	- ![[Pasted image 20240606165320.png#invert]]
### Use Case Realisation
![[Pasted image 20240606202012.png#invert]]

> [!NOTE] Use Case Realisation
> Beschreibt, wie ein bestimmter Use Case innerhalb des Designs mit kollaborierenden Objekten realisiert wird

Es wird wie folgt unterschieden:
- statische Modelle
	- UML-Klassendiagramm
- dynamische Modelle
	- Interaktionsdiagramm
![[Pasted image 20240606193849.png#invert]]
#### Vorgehen
1. Controller Klasse bestimmen resp. identifizieren (vgl. GRASP Controller)
2. zu verändernde Klasse festlegen
3. Weg zu dieser Klasse festlegen
	1. mithilfe Parameter richtigen Weg wählen
	2. allenfalls notwendige Klassen erstellen
	3. Aufruf weiterleiten mit allen notwendigen Params
	4. Verantwortlichkeiten gem. GRASP Information Expert zuweisen
	5. In Varianten denken (Low Coupling / High Cohesion)
4. Veränderungen gem. Systemvertrag programmieren
5. Review bzgl. High Cohesion & Architekturkonformität
#### Fehlerbehandlung
- (Standard-) Exceptions verwenden
- Wo sinnvoll eigene Klasse definieren
- Entscheiden, welche Fehlermeldungen dem Benutzer angezeigt werden sollen
#### Coding Guidelines
- legt formale Verbindlichkeiten fest (Gross-/Kleinschreibung, Einrückung, Klammern)
- Linter
- Namensgebungen
#### Implementierungen
- Code-Driven Development
- TDD: Test-Driven Development
- BDD: Behavior-Driven Development
- Optimierungen (Performance-Monitor, Datenbankzugriffe)
#### Refactoring
- viele kleine Schritte
- trennen von eigentlicher Weiterentwicklung
- Tests (Unit-Tests und Testautomatisierung)
- Pull Up / Pull Down => Methode in Super-/ Subklasse verschieben
- Method Extract => Methode soll sich auf Hauptaufgabe beschränken
- vorher (schlecht) 
```java
public void takeTurn(){
    // roll dice
    int rollTotal = 0;
    for (int i = 0; i < dice.length; i++){
        dice[i].roll();
        rollTotal += dice[i].getFaceValue();
    }
    Square newLoc = board.getSquare(
        piece.getLocation(), rollTotal);
    piece.setLocation(newLoc);
}
```
- nachher (gut)
```java
public void takeTurn(){
    // the refactored helper method
    int rollTotal = rollDice();
    Square newLoc = board.getSquare(
        piece.getLocation(), rollTotal);
    piece.setLocation(newLoc);
}

private int rollDice(){
    int rollTotal = 0;
    for (int i = 0; i < dice.length; i++){
        dice[i].roll();
        rollTotal += dice[i].getFaceValue();
    }
    return rollTotal;
}
```
 Testing
- Integrationstest
- Systemtests
- Abnahmetests
- Regressionstests
## Klassendiagramm (DCD)
beschreibt die statische Struktur des Systems inkl. Klassen, Objekte, Attribute, Operationen und Beziehungen. Design-Klassendiagramm für Implementation = DCD.
![[Pasted image 20240606194012.png#invert]]
![[Pasted image 20240610181425.png#invert]]
=> Details siehe VL
## Interaktionsdiagramm

> [!NOTE] Title
> Spezifiziert, auf welche Weise Nachrichten und Daten zwischen Interaktionspartnern ausgetauscht werden.

Wird unterteilt in Sequenz- und Kommunikationsdiagramm 
### Sequenzdiagramm
Stellt zeitlichen Ablauf des Informationsaustausches zwischen Kommunikationspartnern dar. Schachtelungen und Flussteuerungen (If, Loop) möglich.
![[Pasted image 20240606194808.png#invert]]
![[Pasted image 20240606194848.png#invert]]
![[Pasted image 20240606194859.png#invert]]
### Kommunikationsdiagramm
Gleiches Ziel wie Sequenzdiagramm, Überblick steht im Vordergrund. Jedes Sequenzdiagramm kann in ein Kommunikationsdiagramm umgewandelt werden und umgekehrt.

![[Pasted image 20240606194948.png#invert]]
![[Pasted image 20240606195003.png#invert]]
## Systemsequenzdiagramm (SSD)
- formal ein UML Sequenzdiagramm
- zeigt Interaktion der Akteure mit System
- Ziel: wichtigste Systemoperationen identifizieren für Anwendungsfall identifizieren (APIs)
- Methodenaufrufe
	- treffender Name
	- Parameter
	- durchgezogener Pfeil: Methodenaufruf
	- gestrichelt: Rückgabewert (kann fehlen)
- kann auch zwischen mehreren Systemen sein
- keine Lebensbalken

![[Pasted image 20240606165904.png#invert]]
## Zustandsdiagramm
Welche Zustände kann ein Objekt, eine Schnittstelle, ein Use Case haben?
Wird vor allem in der Modellierung von Echtzeitsystemen, Steuerungen und Protokollen verwendet.
![[Pasted image 20240606195121.png#invert]]
![[Pasted image 20240606195141.png#invert]]
![[Pasted image 20240606195150.png#invert]]
## Aktivitätsdiagramm
Wie läuft ein bestimmter Prozess oder Algorithmus ab? Visualisierung von Abläufen. Parallelisierung und Synchronisation sind möglich.
![[Pasted image 20240606195533.png#invert]]
![[Pasted image 20240606195545.png#invert]]
## Domänenmodell
- zeigt fachliche Begriffe mit Attributen und setzte diese zueinander in Beziehung
- geht noch nicht um Software
- Datentypen nicht angeben
- ![[Pasted image 20240606175843.png#invert]]
- Spezialfälle
	- Komposition
		- wenn ein "Objekt" gelöscht wird auch anderes gelöscht
	- Aggregation
		- hat-Beziehung
	- tendenziell nicht benutzen
- Generalisierung / Spezialisierung
	- ![[Pasted image 20240606180131.png#invert]]
### Operation Contract
- System wird mit Vertrag genauer spezifiziert
- insb. bei komplizierten Operationen
- wird auch in Domain Model vermerkt
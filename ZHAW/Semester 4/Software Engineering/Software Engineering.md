#sem4 #softwareengineering 
## Usability
### UX
Kann auf drei unterschiedliche Dinge verstanden werden:
- Usability
	- Wie einfach ist es, Applikation zu benutzen (Gebrauchstauglichkeit)
- User Experience
	- Wie fühlt sich App an (Usability + Desirability)
- Customer Experience
	- Was ist der Gesamteindruck der App, der Marke, der Firma
	- Usability + Desirability + Brand Experience
	![[Pasted image 20240606152648.png]]

### Usability
![[Pasted image 20240606152820.png]]
#### Was ist Usability?
- Effektivität
	- Benutzer kann seine Aufgaben vollständig erfüllen
	- Inkl. gewünschter Genauigkeit
- Effizienz
	- Benutzer kann Aufgaben Aufgaben mit minimalem/angemessenem Aufwand erledigen (mental, physisch, Zeit)
- Zufriedenheit
	- Mit dem System
		- mindestens: nicht verärgert
		- normal: zufrieden
		- optimal: erfreut

#### 7 wichtige Anforderungsbereiche
- Aufgabenangemessenheit
	- Minimale Schritte für eine Aufgabe
	- Nur Infos, die wichtig sind für Aufgabe
	- Kontextabhängige Hilfe
	- min. Anzahl Benutzereingaben
- Selbstbeschreibungsfähigkeit
	- Benutzer ausreichend informieren (Wo ist er, was muss er tun, was macht System)
	- Begriffe des Benutzers verwenden (Labels, Fehlermeldungen)
- Kontrolle
	- Interaktion durch Benutzer gesteuert (Tempo, Dialogfluss, Darstellung, Modalität (Maus, Sprache))
	- Benutzeraktionen rückgängig machen
	- Aktionen abbrechen
- Erwartungskonformität
	- ![[Pasted image 20240606153419.png]]
	- Konsistenz in Terminologie, Verhalten, Darstellung
- Fehlertoleranz
	- Kommunikation welche Inputs erwartet sind
	- Benutzereingaben prüfen (nicht zwingend beim Tippen)
	- Benutzer helfen (Fehler verstehen)
	- Einfache Korrektur
	- Kein Datenverlust
- Individualisierbarkeit
	- Anpassungsfähigkeit (Sprache, Know-How, Kultur, Einschränkungen)
- Lernförderlichkeit
	- Informationen über grundliegende Konzepte anbieten
		- nur auf Verlangen des Users
		- meistes sollte ohne Vorkenntnisse erledigt werden können

---
## User-Centered-Design (UCD)

![[Pasted image 20240606153756.png]]
### User & Domain Research
- Was ist das?
	- Wer sind Benutzer
	- Was ist ihre Arbeit, Ziel
	- Wie sieht Arbeitsumgebung aus
	- Was brauchen sie, um Ziel zu erreichen (Hilfestellungen)
	- Welche Sprache
	- Welche Normen (organisatorisch, kulturell, sozial)
	- Pain Points
	- ebenso: Wo, wann, warum wird App genutzt
	- **Allgemein => Domäne verstehen**
- Methoden zur Erreichung
	- Beobachtung, Fokusgruppen, Umfragen
	- Contextual Inquiry
		- Experte beobachtet User, der seinen Job erledigt
	- Contextual Interview
		- strukturiert (geschlossene Fragen), vollständig vorbereitet
		- semi-strukturiert (geschlossene & offene Fragen), vieles vorbereitet
		- unstrukturiert (keine vorbereiteten Fragen), nur grobe Ziele
### Artefakte
- Personas
	- fiktive Person zur Repräsentation von Kundengruppen
	- ![[Pasted image 20240606154626.png]]
- Usage-Szenarien
	- kurze Geschichte (Einbezug von Persona)
	- Usage-Szenarien
		- aktuelle Situation
		- enthält
			- Motivation/Trigger
			- Persona & Ziele
			- Aktionen, Interaktionen
			- Kontext (wo, ändert etwas)
			- Probleme, Ablenkungen
	- Kontext-Szenarien
		- sprachliche Beschreibung zukünftig gewünschte Situation (wichtig für Anforderungsanalyse)
		- gleiches Formate wie Usage-Szenario
		- aus Benutzersicht (Interaktionsschritte, High Level)
- Stakeholder-Map
	- ![[Pasted image 20240606154946.png]]
- Blueprint / Geschäftsmodell
	- ![[Pasted image 20240606155134.png]]
- Sonstige
	- Skizzen, Wirefrimes (Prototypen), Designs (Mockups)
### Anforderungsanalyse
- Ziel ausgehend aus UCD Anforderungen ableiten
	- Funktionale Abläufe (Kontextszenarien, Storyboards, Use Cases)
	- Domänenmodell
	- FURPS-Modell (Performance, Support, etc.)
- Funktionale Anforderungen
	- von UC beschrieben
- Weitere funktionale und nicht-funktionale
	- als zusätzliche Anforderungsspezifikation / User Story
---
## Artefakte
### Use Cases
#### Grundlagen
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
		- ![[Pasted image 20240606165434.png]]
- Allgemein
	- mehr als eine Aktion
	- Aktiv formuliert (Verb + evtl. Objekt vorangestellt, "Kasse eröffnen")
	- beschreibt Ziel
	- enthält Trigger
	- beschreibt Logik, nicht konkrete Umsetzung (Implementierung offen lassen)
	- keine kann-Formulierungen
- UC-Diagramm
	- ![[Pasted image 20240606165320.png]]
#### Use Case Realisation
![[Pasted image 20240606202012.png]]

> [!NOTE] Use Case Realisation
> Beschreibt, wie ein bestimmter Use Case innerhalb des Designs mit kollaborierenden Objekten realisiert wird

Es wird wie folgt unterschieden:
- statische Modelle
	- UML-Klassendiagramm
- dynamische Modelle
	- Interaktionsdiagramm
![[Pasted image 20240606193849.png]]
##### Vorgehen
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
##### Fehlerbehandlung
- (Standard-) Exceptions verwenden
- Wo sinnvoll eigene Klasse definieren
- Entscheiden, welche Fehlermeldungen dem Benutzer angezeigt werden sollen
##### Coding Guidelines
- legt formale Verbindlichkeiten fest (Gross-/Kleinschreibung, Einrückung, Klammern)
- Linter
- Namensgebungen
##### Implementierungen
- Code-Driven Development
- TDD: Test-Driven Development
- BDD: Behavior-Driven Development
- Optimierungen (Performance-Monitor, Datenbankzugriffe)
##### Refactoring
- viele kleine Schritte
- trennen von eigentlicher Weiterentwicklung
- Tests (Unit-Tests und Testautomatisierung)
- Pull Up / Pull Down => Methode in Super-/ Subklasse verschieben
- Method Extract => Methode soll sich auf Hauptaufgabe beschränken
- vorher (schlecht) 
```
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
```
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
##### Testing
- Integrationstest
- Systemtests
- Abnahmetests
- Regressionstests
### Klassendiagramm (DCD)
beschreibt die statische Struktur des Systems inkl. Klassen, Objekte, Attribute, Operationen und Beziehungen. Design-Klassendiagramm für Implementation = DCD.
![[Pasted image 20240606194012.png]]
![[Pasted image 20240610181425.png]]
=> Details siehe VL
### Interaktionsdiagramm

> [!NOTE] Title
> Spezifiziert, auf welche Weise Nachrichten und Daten zwischen Interaktionspartnern ausgetauscht werden.

Wird unterteilt in Sequenz- und Kommunikationsdiagramm 
#### Sequenzdiagramm
Stellt zeitlichen Ablauf des Informationsaustausches zwischen Kommunikationspartnern dar. Schachtelungen und Flussteuerungen (If, Loop) möglich.
![[Pasted image 20240606194808.png]]
![[Pasted image 20240606194848.png]]
![[Pasted image 20240606194859.png]]
#### Kommunikationsdiagramm
Gleiches Ziel wie Sequenzdiagramm, Überblick steht im Vordergrund. Jedes Sequenzdiagramm kann in ein Kommunikationsdiagramm umgewandelt werden und umgekehrt.

![[Pasted image 20240606194948.png]]
![[Pasted image 20240606195003.png]]
### Systemsequenzdiagramm (SSD)
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

![[Pasted image 20240606165904.png]]
### Zustandsdiagramm
Welche Zustände kann ein Objekt, eine Schnittstelle, ein Use Case haben?
Wird vor allem in der Modellierung von Echtzeitsystemen, Steuerungen und Protokollen verwendet.
![[Pasted image 20240606195121.png]]
![[Pasted image 20240606195141.png]]
![[Pasted image 20240606195150.png]]
### Aktivitätsdiagramm
Wie läuft ein bestimmter Prozess oder Algorithmus ab? Visualisierung von Abläufen. Parallelisierung und Synchronisation sind möglich.

![[Pasted image 20240606195533.png]]
![[Pasted image 20240606195545.png]]
### Domänenmodell
- zeigt fachliche Begriffe mit Attributen und setzte diese zueinander in Beziehung
- geht noch nicht um Software
- Datentypen nicht angeben
- ![[Pasted image 20240606175843.png]]
- Spezialfälle
	- Komposition
		- wenn ein "Objekt" gelöscht wird auch anderes gelöscht
	- Aggregation
		- hat-Beziehung
	- tendenziell nicht benutzen
- Generalisierung / Spezialisierung
	- ![[Pasted image 20240606180131.png]]
#### Operation Contract
- System wird mit Vertrag genauer spezifiziert
- insb. bei komplizierten Operationen
- wird auch in Domain Model vermerkt
---

## Softwarearchitektur
- Analyse funktional und nicht-funktionaler Anforderung
- ![[Pasted image 20240606181449.png]]
- Modularität mit schwacher Kopplung
### Views
![[Pasted image 20240606181813.png]]
	- Logical View
		- Welche Funktionen
		- Schichten, Subsysteme, Pakete, Frameworks, Klassen
	- Process View
		- Welche Prozesse wo und wann im System
		- Prozesse, Threads, Performance, Stabilität
	- Development View
		- Wie wurde logische Struktur umgesetzt
		- Source Code, Executables, Artefakte
	- Physical View
		- Infrastruktur
		- Prozessknoten, Netzwerke, Protokolle
	- +1 View, Scenario View
		- UseCases und nicht-funktionale Anforderungen
### Paketdiagramm
- betrifft logische Stuktur
- ![[Pasted image 20240606182704.png]]
- Umgesetzt in java packages

### Architekturpatterns
![[Pasted image 20240606182957.png]]
#### Layered Pattern
- Zerlegung Applikation in Schichten
- je weiter unten, desto allgemeiner
- zuoberst das UI
- Kopplung nur von oben nach unten, nie umgekehrt
- ![[Pasted image 20240606183047.png]]
#### Client-Server
- ein Server und mehrere Clients
- Request/Response
- ![[Pasted image 20240606183107.png]]
#### Master-Slave
- Master verteilt Aufgaben auf Slaves
- Slaves senden Ergebnis zu Master
- ![[Pasted image 20240606183144.png]]
#### Pipe-Filter
- Datenströmen (RxJs, Observables)
- Jeder Prozessschritt durch Operator abstrahieren
- ![[Pasted image 20240606183158.png]]
#### Broker
- Verteilte Systeme koordinieren
- Broker für Kommunikation zwischen Client und Subsystemen zuständig
- ![[Pasted image 20240606183400.png]]
#### Event-Bus
- EventSource publizieren Meldungen für Kanal
- EventListeners Melden sich für Events an & werden informiert, sobald Meldungen auf Kanal
- ![[Pasted image 20240606183413.png]]
#### Model View Controller (MVC)
![[Pasted image 20240606183430.png]]
### Clean Architecture
![[Pasted image 20240606185144.png]]
- Unabhängigkeit von Framework
- Business Rules unabhängig von UI, DB und Web Server (Infra)
- Domänenlogik keine Abhängigkeit zu externen Code (Stored Procedures)
### Softwarepatterns (GRASP)
Allgemein, an Verantwortlichkeiten denken (RDD). Diese werden durch Attribute und Methoden implementiert. Kann auf jeder Ebene des Designs angewendet werden.

> [!NOTE] Title
> Ein Prinzip ist ein Grundsatz oder Postulat, das zu gutem OO-Design führen soll.

> [!NOTE] Title
> Pattern ist bekanntes Problem-Lösungspaar, das in neuen Kontexten angewendet werden kann.

#### Information Expert
Verantwortlichkeit einer Klasse zuweisen, die erforderliche Informationen verfügt um diese zu erfüllen.
![[Pasted image 20240606200606.png]]
#### Creator
Klasse A Verantwortlichkeit zuweisen, Klasse B zu erstellen.
![[Pasted image 20240606200805.png]]
#### Controller
Welches Objekt jenseits der UI-Schicht empfängt und koordiniert Systemoperation => Controller Klasse.
- Fassaden Controller
	- Root-Objekt, übergeordnetes System
- Use Case Controller
	- Pro Use Case Szenario künstliche Klasse, in der Systemoperation abläuft
![[Pasted image 20240606200950.png]]
#### Low Coupling / High Cohesion
Geringe Abhängigkeiten zwischen Objekten (Low Coupling) und wohldefinierte Aufgaben pro Objekt (High Cohesion)
#### Polymorphismus
Typabhängiges Verhalten mit polymorphen Operationen einer Klasse zuweisen mittels Abstraktion.
![[Pasted image 20240606201149.png]]
#### Pure Fabrication
Künstliche Hilfsklasse um bspw. bei Information Expert High Cohesion und/oder Low Coupling sicherzustellen.
![[Pasted image 20240606201307.png]]
#### Indirection
Verantwortlichkeiten zwischengestelltem Objekt zuweisen, das zwischen anderen Komponenten oder Diensten vermittelt.
![[Pasted image 20240606201451.png]]
#### Protected Variations
Instabilitäten mittels stabiler Interfaces entkapseln.
![[Pasted image 20240606201652.png]]
### Design Patterns
Bewährte Lösungsschablonen für wiederkehrende Entwurfsprobleme
#### Adapter
Adapter-Klasse zwischen zwei inkompatiblen Klassen zwischenschalten.

![[Pasted image 20240606214538.png]]
#### Simple Factory
Klasse für Erzeugen eines Objekts schreiben, das häufig genutzt wird.

![[Pasted image 20240606214726.png]]
#### Singleton
Klasse, von der nur eine Instanz benötigt wird, mittels einer statischen Methode (mit `return` des Objekts) erstellen.
Achtung, globale Sichtbarkeit wird heute als kritisch betrachtet.

```
public class Singleton {

    private static Singleton instance = new Singleton();

    // privater Konstruktor, verhindert direkte Instanziierung
    private Singleton() {
    }

    // Instanzvariablen ...

    public static Singleton getInstance() {
        return instance;
    }

    // Instanz-Methoden ...
}

```

#### Dependency Injecton
Referenz von Klasse auf anderes Objekt mit Interface wird von aussen (Injector) gesetzt.
Ersetzt das Factory Pattern. Wird bspw. in Java Spring eingesetzt und ist besonders hilfreich für das Schreiben von Unit Tests. ist Singleton und Factory vorzuziehen.

![[Pasted image 20240606214220.png]]
#### Proxy
Objekt, das nicht oder noch nicht im selben Adressraum verfügbar ist, wird mittels Stellvertreter-Objekts ersetzt. Proxy leitet alles an das richtige Objekt weiter. Wird oft für Caching verwendet.

Arten
- Remote Proxy: Stv. für Objekt in anderem Adressraum und übernimmt Kommunikation.
- Virtual Proxy: Verzögert Erzeugen des richtigen Objekts auf das erste Mal, dass dieses benutzt wird.
- Protection Proxy: kontrolliert Zugriff auf richtiges Objekt.

![[Pasted image 20240606214256.png]]
#### Chain of Responsibility
Um für ein Objekt mit mehreren Handlern herauszufinden, welches der richtige ist, werden Handler in verketteter Linie aneinander geschaltet. Jeder Handler entscheidet, ob er Anfrage bearbeiten will. Möglich, dass niemand die Anfrage behandelt.

![[Pasted image 20240606214332.png]]
#### Decorator
Um Objekt (nicht ganze Klasse) mit zusätzlichen Verantwortlichkeiten zu versehen, wird Decorater mit identischen Schnittstellen vorgeschaltet. Decorator kann Methodenaufrufe selber bearbeiten oder weiterleiten.

![[Pasted image 20240606214104.png]]
#### Observer
Interface informiert Objekt über Änderungen eines anderen Objekts.

![[Pasted image 20240606214832.png]]
#### Strategy
Algorithmus wird in eine eigene Klasse mit nur einer Methode verschoben, um ihn einfach auszutauschen. Interface stellt sicher, dass Algorithmus-Klassen implementiert und einheitlich aufgerufen werden.

![[Pasted image 20240606214958.png]]
#### Composite
Wenn eine Menge von Objekten dasselbe Interface haben, kann ein Composite definiert werden, welches dasselbe Interface definiert und Methoden an darin enthaltene Objekte weiterleitet (Hierarchie).

![[Pasted image 20240606215559.png]]
#### State
Um Zustände eines Objekts zu steuern, wird ein eigenes Zustandsobjekt generiert, in welchem die zustandsspezifischen Methoden enthalten sind. Zustandsobjekte implementieren wiederum ein Zustandsinterface.

![[Pasted image 20240606215653.png]]
#### Visitor
Klassenhierarchie wird mit einer Visitor-Infrastruktur erweitert, um zusätzliche Verantwortlichkeiten zu realisieren. Stellt allerdings Widerspruch zum Information Expert dar.

![[Pasted image 20240606215842.png]]
#### Facade
Um die Kom­pli­ziert­heit eines Systems zu minimieren, welches eine vereinfachte Schnittstelle zum Subsystem anbietet und die meisten Anwendungen abdeckt. Kapselt (im Gegensatz zu Facade) nicht komplett ab. Beispiel wäre ein Framework.

![[Pasted image 20240606220653.png]]
#### Abstract Factory
Erweiterung der Factory um abstrakte Produkte zu generieren. Hat für jedes Objekt eine eigene Create-Methode. Die konkrete Factory wird dann davon abgeleitet, um das konkrete Objekt zu erzeugen.

![[Pasted image 20240606220932.png]]
#### Factory Method
Creator eines abstrahierten Objekts mit abstrakter Methode erweitern, dass die Spezialisierung korrekt returned. Konkrete Creator Klasse erzeugt dass die konkrete Subklasse des abstrakten Objekts.

![[Pasted image 20240606221155.png]]
#### Command
Um Aktionen für späteren Gebrauch zu speichern (inkl. allfälliger Priorisierung und Protokollierung) wird Interface definiert, das nur Auslösung dieser Aktion erlaubt. Implementation des Interfaces überschreiben Methoden zur Auslösung der Aktion, was bedeutet, dass Methode auf einem anderen Objekt aufgerufen wird. Parameter dieser Methode werden in Aktion zwischengespeichert.

![[Pasted image 20240606221620.png]]
#### Template Method
Um Ablauf in gewissen Punkten anpassen zu können, wird in einer abstrakten Klasse eine Template Methode hinzugefügt, die Ablauf implementiert. Anschliessende Hook-Methoden dienen dann zur Spezialisierung (Erweiterung) des Standard-Ablaufs.

![[Pasted image 20240606221807.png]]
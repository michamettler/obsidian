#softwareengineering #sem4 #architecture
## Adapter
Adapter-Klasse zwischen zwei inkompatiblen Klassen zwischenschalten.
![[Pasted image 20240606214538.png#invert]]
## Simple Factory
Klasse für Erzeugen eines Objekts schreiben, das häufig genutzt wird.
![[Pasted image 20240606214726.png#invert]]
## Singleton
Klasse, von der nur eine Instanz benötigt wird, mittels einer statischen Methode (mit `return` des Objekts) erstellen.
Achtung, globale Sichtbarkeit wird heute als kritisch betrachtet.

```java
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

## Dependency Injecton
Referenz von Klasse auf anderes Objekt mit Interface wird von aussen (Injector) gesetzt.
Ersetzt das Factory Pattern. Wird bspw. in Java Spring eingesetzt und ist besonders hilfreich für das Schreiben von Unit Tests. ist Singleton und Factory vorzuziehen.
![[Pasted image 20240606214220.png#invert]]
## Proxy
Objekt, das nicht oder noch nicht im selben Adressraum verfügbar ist, wird mittels Stellvertreter-Objekts ersetzt. Proxy leitet alles an das richtige Objekt weiter. Wird oft für Caching verwendet.

Arten
- Remote Proxy: Stv. für Objekt in anderem Adressraum und übernimmt Kommunikation.
- Virtual Proxy: Verzögert Erzeugen des richtigen Objekts auf das erste Mal, dass dieses benutzt wird.
- Protection Proxy: kontrolliert Zugriff auf richtiges Objekt.
![[Pasted image 20240606214256.png#invert]]
## Chain of Responsibility
Um für ein Objekt mit mehreren Handlern herauszufinden, welches der richtige ist, werden Handler in verketteter Linie aneinander geschaltet. Jeder Handler entscheidet, ob er Anfrage bearbeiten will. Möglich, dass niemand die Anfrage behandelt.
![[Pasted image 20240606214332.png#invert]]
## Decorator
Um Objekt (nicht ganze Klasse) mit zusätzlichen Verantwortlichkeiten zu versehen, wird Decorater mit identischen Schnittstellen vorgeschaltet. Decorator kann Methodenaufrufe selber bearbeiten oder weiterleiten.
![[Pasted image 20240606214104.png#invert]]
## Observer
Interface informiert Objekt über Änderungen eines anderen Objekts.
![[Pasted image 20240606214832.png#invert]]
## Strategy
Algorithmus wird in eine eigene Klasse mit nur einer Methode verschoben, um ihn einfach auszutauschen. Interface stellt sicher, dass Algorithmus-Klassen implementiert und einheitlich aufgerufen werden.
![[Pasted image 20240606214958.png#invert]]
## Composite
Wenn eine Menge von Objekten dasselbe Interface haben, kann ein Composite definiert werden, welches dasselbe Interface definiert und Methoden an darin enthaltene Objekte weiterleitet (Hierarchie).
![[Pasted image 20240606215559.png#invert]]
## State
Um Zustände eines Objekts zu steuern, wird ein eigenes Zustandsobjekt generiert, in welchem die zustandsspezifischen Methoden enthalten sind. Zustandsobjekte implementieren wiederum ein Zustandsinterface.
![[Pasted image 20240606215653.png#invert]]
## Visitor
Klassenhierarchie wird mit einer Visitor-Infrastruktur erweitert, um zusätzliche Verantwortlichkeiten zu realisieren. Stellt allerdings Widerspruch zum Information Expert dar.
![[Pasted image 20240606215842.png#invert]]
## Facade
Um die Kom­pli­ziert­heit eines Systems zu minimieren, welches eine vereinfachte Schnittstelle zum Subsystem anbietet und die meisten Anwendungen abdeckt. Kapselt (im Gegensatz zu Facade) nicht komplett ab. Beispiel wäre ein Framework.
![[Pasted image 20240606220653.png#invert]]
## Abstract Factory
Erweiterung der Factory um abstrakte Produkte zu generieren. Hat für jedes Objekt eine eigene Create-Methode. Die konkrete Factory wird dann davon abgeleitet, um das konkrete Objekt zu erzeugen.
![[Pasted image 20240606220932.png#invert]]
## Factory Method
Creator eines abstrahierten Objekts mit abstrakter Methode erweitern, dass die Spezialisierung korrekt returned. Konkrete Creator Klasse erzeugt dass die konkrete Subklasse des abstrakten Objekts.
![[Pasted image 20240606221155.png#invert]]
## Command
Um Aktionen für späteren Gebrauch zu speichern (inkl. allfälliger Priorisierung und Protokollierung) wird Interface definiert, das nur Auslösung dieser Aktion erlaubt. Implementation des Interfaces überschreiben Methoden zur Auslösung der Aktion, was bedeutet, dass Methode auf einem anderen Objekt aufgerufen wird. Parameter dieser Methode werden in Aktion zwischengespeichert.
![[Pasted image 20240606221620.png#invert]]
## Template Method
Um Ablauf in gewissen Punkten anpassen zu können, wird in einer abstrakten Klasse eine Template Methode hinzugefügt, die Ablauf implementiert. Anschliessende Hook-Methoden dienen dann zur Spezialisierung (Erweiterung) des Standard-Ablaufs.
![[Pasted image 20240606221807.png#invert]]
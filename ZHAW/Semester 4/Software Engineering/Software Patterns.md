#sem4 #softwareengineering #architecture

## Softwarepatterns (GRASP)
Allgemein, an Verantwortlichkeiten denken (RDD). Diese werden durch Attribute und Methoden implementiert. Kann auf jeder Ebene des Designs angewendet werden.

> [!NOTE] Title
> Ein Prinzip ist ein Grundsatz oder Postulat, das zu gutem OO-Design führen soll.

> [!NOTE] Title
> Pattern ist bekanntes Problem-Lösungspaar, das in neuen Kontexten angewendet werden kann.

### Information Expert
Verantwortlichkeit einer Klasse zuweisen, die erforderliche Informationen verfügt um diese zu erfüllen.
![[Pasted image 20240606200606.png#invert]]
### Creator
Klasse A Verantwortlichkeit zuweisen, Klasse B zu erstellen.
![[Pasted image 20240606200805.png#invert]]
### Controller
Welches Objekt jenseits der UI-Schicht empfängt und koordiniert Systemoperation => Controller Klasse.
- Fassaden Controller
	- Root-Objekt, übergeordnetes System
- Use Case Controller
	- Pro Use Case Szenario künstliche Klasse, in der Systemoperation abläuft
![[Pasted image 20240606200950.png#invert]]
### Low Coupling / High Cohesion
Geringe Abhängigkeiten zwischen Objekten (Low Coupling) und wohldefinierte Aufgaben pro Objekt (High Cohesion)
### Polymorphismus
Typabhängiges Verhalten mit polymorphen Operationen einer Klasse zuweisen mittels Abstraktion.
![[Pasted image 20240606201149.png#invert]]
### Pure Fabrication
Künstliche Hilfsklasse um bspw. bei Information Expert High Cohesion und/oder Low Coupling sicherzustellen.
![[Pasted image 20240606201307.png#invert]]
### Indirection
Verantwortlichkeiten zwischengestelltem Objekt zuweisen, das zwischen anderen Komponenten oder Diensten vermittelt.
![[Pasted image 20240606201451.png#invert]]
### Protected Variations
Instabilitäten mittels stabiler Interfaces entkapseln.
![[Pasted image 20240606201652.png#invert]]

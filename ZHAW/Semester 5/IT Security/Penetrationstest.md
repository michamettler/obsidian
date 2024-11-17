#itsecurity #sem5

## Überblick
![[Pasted image 20241115121946.png#invert]]
## Projektablauf
![[Pasted image 20241115122324.png#invert]]
### Technische Durchführen
![[Pasted image 20241115123213.png#invert]]
___
## Angriffe
### XSS
- XSS = Cross-Site Scripting
- Eigentlich: Script Injection
- Name kommt daher, dass man damit Cross-Site interaktive Inhalte ausführen kann (Verhindern aus Same Origin Policy)
- Drei Varianten
	- Stored/Persistent
	- Reflected
	- DOM Mutational
#### Beispiel
![[Pasted image 20241115125918.png#invert]]
#### Schutz
- **nicht über Input-Validation** (ändert Standard)
- Whitelist (positive Input Spezifizierung)
- Output Encoding & Escaping (bspw. `\`)
### SQL-Injection
Mit SQL Befehlen Daten aus anderen Tabellen abziehen (bspw. mit SQL-Map)
#### Beispiel
![[Pasted image 20241115130746.png#invert]]
#### Folgen
- Daten abziehen
- Command Execution
- Code Execution (**!**)
#### Schutz
- Parametrisierung (Prepared Statement)
	- Aufteilen von Code und Parameter
### IDOR
ID vorhersehbar (Pseudo-Zufall, Sequenz)
#### Beispiel
![[Pasted image 20241115131658.png#invert]]
#### Schutz
- UUID benutzen
- Zugriffsschutz (Authenticate & Authorization)
## Defensive
- Principle of Least Privilege
- Zero Trust & Need to know/need access
- Trennung Daten und Kontrollstrukturen
- Segmentierung/Blast Radius Reduction
	- Brandschutztür
- Kerckhoffsches Prinzip
- Reduktion
	- Komplexität
	- Abhängigkeit
	- Angriffsfläche
- Secure in Depth (mehrdimensional) **by Design** (Single Point of Control, Security Middleware etc.) & Programming (mehrere Checkpoints, Regex, etc.) **by Default**
- Automatisierung Pipelines & DevSecOps
- Escaping & Encoding bei Daten von aussen

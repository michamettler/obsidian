#softwareengineering #sem4 #architecture
## Patterns
![[Pasted image 20240606182957.png#invert]]
### Layered Pattern
- Zerlegung Applikation in Schichten
- je weiter unten, desto allgemeiner
- zuoberst das UI
- Kopplung nur von oben nach unten, nie umgekehrt
- ![[Pasted image 20240606183047.png#invert]]
### Client-Server
- ein Server und mehrere Clients
- Request/Response
- ![[Pasted image 20240606183107.png#invert]]
### Master-Slave
- Master verteilt Aufgaben auf Slaves
- Slaves senden Ergebnis zu Master
- ![[Pasted image 20240606183144.png#invert]]
### Pipe-Filter
- Datenströmen (RxJs, Observables)
- Jeder Prozessschritt durch Operator abstrahieren
- ![[Pasted image 20240606183158.png#invert]]
### Broker
- Verteilte Systeme koordinieren
- Broker für Kommunikation zwischen Client und Subsystemen zuständig
- ![[Pasted image 20240606183400.png#invert]]
### Event-Bus
- EventSource publizieren Meldungen für Kanal
- EventListeners Melden sich für Events an & werden informiert, sobald Meldungen auf Kanal
- ![[Pasted image 20240606183413.png#invert]]
### Model View Controller (MVC)
![[Pasted image 20240606183430.png#invert]]
## Clean Architecture
![[Pasted image 20240606185144.png#invert]]
- Unabhängigkeit von Framework
- Business Rules unabhängig von UI, DB und Web Server (Infra)
- Domänenlogik keine Abhängigkeit zu externen Code (Stored Procedures)
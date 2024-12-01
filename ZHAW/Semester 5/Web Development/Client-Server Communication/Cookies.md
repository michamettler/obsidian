#webdevelopment/client-server #sem5 #webdevelopment/javascript 

- HTTP als zustandsloses Protokoll konzipiert
- Cookies: Speichern von Informationen auf dem Client
- RFC 2965: HTTP State Management Mechanism
- Response: `Set-Cookie`-Header, Request: `Cookie`-Header
- Zugriff mit JavaScript möglich (ausser `HttpOnly` ist gesetzt)
![[Pasted image 20241129133928.png#invert]]
## Sessions
- Cookies auf dem Client leicht manipulierbar
- Session: Client-spezifische Daten auf dem Server speichern
- Identifikation des Clients über Session-ID (Cookie o.a.)
- Gefahr: Session-ID gerät in falsche Hände (Session-Hijacking)
![[Pasted image 20241129134004.png#invert]]

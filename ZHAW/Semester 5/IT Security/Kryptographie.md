#itsecurity #sem5
## Kryptographie

Betrifft Confidentiality und Cryptology bzgl Zielen der IT Security [[Overview]].
### Ziele der Kryptographie

 - **Confidentiality**: Nur berechtigte Personen können eine Nachricht lesen. Unberechtigte Personen können die Nachricht zwar sehen, sie aber nicht entziffern, da die Nachricht für sie nur aus einer zufälligen Zeichenfolge zu bestehen scheint.
- **Integrity**: Eine Nachricht wird vom Empfänger so empfangen, wie sie vom Sender geschickt wurde. Das heisst, eine unberechtigte Person könnte zwar eine Nachricht abfangen, verändern, und dem Empfänger zustellen. Dieser würde dann aber merken, dass die Nachricht nicht der ursprünglichen Nachricht entspricht und sie daher verwerfen.
- **Authenticity**: Der Empfänger kann sicher sein, dass eine Nachricht auch wirklich von der Person stammt, von welcher die Nachricht zu kommen scheint. Das heisst, er kann überprüfen, ob der angegebene Absender auch dem tatsächlichen Absender entspricht.
- **Non-Repudiation**: Wenn eine Person eine Nachricht bekommen hat, kann diese Person nicht abstreiten, dass sie die Nachricht erhalten hat. Das heisst, es kann bewiesen werden, dass sie die Nachricht erhalten hat.
- **Freshness**: Alle erhaltenen Nachrichten sind aktuell. Das heisst, ein Attacker könnte zwar eine Nachricht zurückbehalten und später senden, oder eine abgefangene Nachricht duplizieren und zu einem späteren Zeitpunkt noch einmal senden, aber dies würde vom Empfänger bemerkt.
![[Pasted image 20241006161346.png#invert]]
### Work Factor der Kryptographie

$Work Factor$ = Durchschnittliche Anzahl Versuche, bis richtiger Schlüssel gefunden wird (mit einer Brute Force Attacke).

Hängt von folgenden Faktoren ab:
- Verschlüsselungsalgorithmus
- Schlüssellänge
- Zufälligkeit des Schlüssel

| Work Factor | Durchschnittliche Zeit (Sekunden) | Durchschnittliche Zeit (Jahre) |
| ----------- | --------------------------------- | ------------------------------ |
| $2^{64}$    | $1.8*10^{-2}$                     |                                |
| $2^{96}$    | $7.9*10^{7}$                      | 2.5                            |
| $2^{128}$   | $3.4*10^{17}$                     | $1.1*10^{10}$                  |
| $2^{256}$   | $1.2*10^{56}$                     | $3.7*10^{48}$                  |
Wie von aus dieser Tabelle ersichtlich, können Algorithmen mit einem Work Faktor von mindestens $2^{128}$ als sicher betrachtet werden.
Den Work Faktor kann man auch in _bits_ darstellen.  
Ein Work Faktor von $2^{n}$ entspricht einem Work Faktor von _n bits_.
## Hash Funktionen
![[Pasted image 20241006161324.png#invert]]
### Work Factor
Für eine sichere Hash Funktion sollte der Work Faktor mindestens 128 bit betragen.

| Funktion | Hash Länge      | Work Factor     |
| -------- | --------------- | --------------- |
| MD5      | 128 bit         | 64 bit          |
| SHA-1    | 160 bit         | 80 bit          |
| SHA-2    | 224 - 512 bit   | 112 bis 256 bit |
| SHA-3    | 225 bis 512 bit | 112 bis 256 bit |
Die Tabelle zeigt, dass sowohl MD5 als auch SHA-1 heute nicht mehr als sicher eingestuft werden können. Beide SAH-2 und SHA-3 gelten bei einer Hashlänge von mindestens 256 bits als sicher.
## Secret Key Algorithmen
Sowohl für die Verschlüsselung E(k) als auch für die Entschlüsselung D(k) wird derselbe Schlüssel k verwendet. Der Schlüssel k muss über einen sicheren Kanal vorher zwischen Sender und Empfänger ausgetauscht werden. Dies kann zum Beispiel bei einem persönlichen Treffen stattfinden, oder wie wir im nächsten Kapitel sehen werden mit Hilfe der Public Key Kryptographie.
![[Pasted image 20241006161633.png#invert]]
![[Pasted image 20241006161910.png#invert]]
### Initialisierungsvektor
Im Deutschen kommt beispielsweise der Buchstabe "e" viel häufiger vor, als der Buchstabe "x".
Um diese Attacke zu verunmöglichen wird ein zufälliger Wert gebraucht, der für jeden verschlüsselten Block anders aussieht. Diesem zufälligen Wert sagen wir Initialisierungsvektor. Der Initialisierungsvektor (IV) hat folgende Eigenschaften:

- Er muss für jeden Block, welcher mit demselben Schlüssel verschlüsselt wird, unterschiedlich sein.
- Er muss Sender und Empfänger bekannt sein.
- Er muss nicht geheim sein (da nach wie vor auch der Schlüssel gebraucht wird, um die Nachricht zu entschlüsseln).
![[Pasted image 20241006161308.png#invert]]
### Work Factor
Zur Berechnung des Work Factors für zufällige Schlüssel kann die Anzahl bits im verwendeten Schlüssel verwendet werden

**Allgemeine Formel für den Work Factor für einen zufälligen Schlüssel der Länge n bits**  
$$WorkFactor=(2^n+1)/2$$
Dies kann approximiert werden zu :

**Approximierte Formel für den Work Factor für einen zufälligen Schlüssel der Länge n bits**  
$$Work Factor = 2^{n-1}$$
**Approximierte Formel für den Work Factor für einen zufälligen Schlüssel der Länge n bits, wo n > 128bits** 
$$Work Factor = 2^n$$
**Work Factor in bits**
Um die Notation zu vereinfachen, kann man den Work Faktor auch in bits angeben. Ein Work Faktor von 2n2n entspricht einem Work Faktor von $n$ bits.
### Authenticated Encryption
Eine Verschlüsselung einzelner Blöcke mittels Secret Key Kryptographie stellt lediglich die Vertraulichkeit (Confidentiality) der Daten sicher. Sollen ausserdem auch Authentizität und Integrität sichergestellt werden, müssen sogenannte Message Authentication Codes (MAC) eingefügt werden. Wird Verschlüsselung und Message Authentication in einem Algorithmus zusammengefasst, wird dies als _Authenticated Encryption (AE)_ bezeichnet. Wird zusätzlich noch die Möglichkeit geboten Daten nur zu authentisieren, aber nicht zu Verschlüsseln, nennt man dies _Authenticated Encryption with Associated Data (AEAD)._ Dies ist heute der Standard. Für die Payload einer Nachricht wird die Confidentiality per Verschlüsselung sichergestellt und die Integrität der gesamten Nachricht (Payload und Header) wir per MAC sichergestellt.
#### Algorithmen
![[Pasted image 20241006161958.png#invert]]
#### AES Modes
![[Pasted image 20241006162023.png#invert]]
#### AES Implementierung
```python
import sys
import numpy as np
from PIL import Image
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
from Crypto.Random import get_random_bytes

# Define the mode and key length
mode = 'png'  # or 'gif'
key_length = 16  # AES key must be either 16, 24, or 32 bytes long

# Load and convert the image
if mode == 'png':
    img = Image.open("./Lab03/tux.png").convert('RGBA')
else:
    img = Image.open("./Lab03/tux.gif").convert('P')

# Shape array (flatten & padding)
img.load()
data = np.asarray(img, dtype="uint8")
data_flat = data.flatten()
data_bytes = data_flat.tobytes()
data_padded = pad(data_bytes, AES.block_size)

# Encryption
key = get_random_bytes(key_length)
iv = get_random_bytes(AES.block_size) # only used for cbc & gcm

# choose mode of operation

# cipher = AES.new(key, AES.MODE_CBC, iv)
cipher = AES.new(key, AES.MODE_GCM, iv)
# cipher = AES.new(key, AES.MODE_ECB)

encrypted_data = cipher.encrypt(data_padded)

# discard extra bytes & reshape array (deflatten & unpadding)
encrypted_data = encrypted_data[:len(data_bytes)]
encrypted_data_flat = np.frombuffer(encrypted_data, dtype="uint8")
encrypted_data = encrypted_data_flat.reshape(data.shape)

# Case distinction (save image)
if mode == 'png':
    encrypted_img = Image.fromarray(encrypted_data, 'RGBA')
    encrypted_img.save("./Lab03/encrypted_tux.png")
else:
    encrypted_img = Image.fromarray(encrypted_data, 'P')
    encrypted_img.save("./Lab03/encrypted_tux.gif")

print("Encryption complete. Encrypted image saved.")
```
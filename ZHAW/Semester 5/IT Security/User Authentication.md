#itsecurity #sem5 

## Access Control
![[Pasted image 20241122150233.png#invert]]
## Authentication
Find out if given party is who they claim to be.
![[Pasted image 20241122150308.png#invert]]
### Basic Problem
Passwords aren't enough.
### Hashing
![[Pasted image 20241122150941.png#invert]]
#### Precompiled dictionary attacks
- Attacker can still try many different passwords, compute the hash, and check if it matches any hash in the password file
- He'll typically not just try random passwords, but test them according to a strategy, because users tend to pick simple passwords
- Even better, the attacker has to do the work of computing hashes of likely passwords once
![[Pasted image 20241122152620.png#invert]]

### Salting
This can be achieved by not hashing the passwords directly, but by adding a random value to the password before hashing it
- This random value is called **salt** and should be large, e.g. 64 – 128 bits
- The **salt** is stored in the password file along with the hashed password
- Because the attacker cannot predict the salt values in the password file, he cannot prepare for the attack by performing pre-computations
![[Pasted image 20241122152736.png#invert]]
### Peppering
Pepper stored separately (physically) for pepper, but does the same like salting (additional layer).
![[Pasted image 20241122152806.png#invert]]
### Work Factor revisited
[[Kryptographie]]
![[Pasted image 20241122153102.png#invert]]
### Key Stretching
Increasing the computing effort for the attacker is possible by increasing the complexity to compute the password hash • E.g. key stretching: Apply the hash-function multiple times using (some) of the output of the previous round as input to the next round.
### Bycript
Specialized Password-Hashing Function (make hashing longer).
#### Argon2
- Argon2i: there seem to be "attacks" that, if successful, invalidate some of the guarantees w.r.t. memory and time complexity
- Argon2d: no attacks known
- Argon2id: no attacks known
## Multi-Factor Authentication
- Lure victim with a phishing e-mail to the fake banking website
- In the background, directly interact with the real banking website to authenticate with the credentials of the victim
![[Pasted image 20241122153905.png#invert]]
### MFA Fatigue
![[Pasted image 20241122153932.png#invert]]
#### Countermeasure (Number in Office 365)
Normal case: The user sees the number on the screen and transfers it to the authenticator
Attack: The user does not see the number and therefore cannot transfer it and the attacker is not logged in
### Attacks
While mobile phone-based approaches are very convenient, they introduce new security risks compared to individual hardware tokens
- One risk is that if someone steals your (unlocked) mobile phone, then he possesses all 2 nd authentication factors for which the device is used
- Another risk are attacks against mobile phones which allow an attacker to get control over the 2nd authentication factor
## Password-less Authentication
Password-less authentication is based on the cryptographic methods public key cryptography and digital certificates (eg. Windows Hello, Apple Face ID).
![[Pasted image 20241122154130.png#invert]]
### With Public Key Cryptography
![[Pasted image 20241122154211.png#invert]]
#### Registration Flow
![[Pasted image 20241122154317.png#invert]]
![[Pasted image 20241122154332.png#invert]]

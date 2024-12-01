#sem5  #itsecurity 

## Direct User Authentication
- User contacts a host / server and sends it the credentials
- Host / server has all information to authenticate the user
- Example: local or remote login on a server
![[Pasted image 20241129122635.png#invert]]
## Indirect User Authentication
- User contacts a host / server and sends it the credentials
- Host / server does not directly authenticate the user
- To authenticate the user, an additional authentication server is used
- Examples: RADIUS, NTLM, Kerberos, Shibboleth, SAML, OpenID Connect
![[Pasted image 20241129122652.png#invert]]
## Single Sign On (SSO)
- Use one identity (one login) for several applications
- For example login with google, facebook, etc.
- Benefits
	- Comfort for user (does not have to remember several passwords)
	- Since no credentials are stored with applications, they also cannot be stolen
- Drawbacks
	- If credentials are stolen, they can be used for many applications
	- If the central authentication system breaks, users cannot log into any application
	- Central authentication systems knows all activities of the user
![[Pasted image 20241129122845.png#invert]]
### Implementation Possibilities
- can be combined
![[Pasted image 20241129123039.png#invert]]
## OAuth2
- Framework for authorization (not authentication)
- Goal: Allow authorization via APIs without sharing passwords
![[Pasted image 20241129123627.png#invert]]
![[Pasted image 20241129123659.png#invert]]
### OpenId
- based on [[#OAuth2]]
- single login for different sites
- removes need for managing passwords in applications
- google, microsoft, amazon, etc.
#### Terminology
![[Pasted image 20241129123853.png#invert]]
#### Connect Protocol
(nicht so PR)
![[Pasted image 20241129124102.png#invert]]
### Security Assertion Markup Language (SAML)
- Provides Single Sign On (SSO) for web applications
- Used for Browser based applications • No support for mobile devices
- No support for API access • Very flexible protocol • Assertions written in XML
- Can exchange anything that can be represented in XML (as long as sender and receiver know how to parse it)
#### Terminology
![[Pasted image 20241129124500.png#invert]]
#### Differences SAML to OpenID
##### OpenID Connect
- Light weight JWT
- Supports web, mobile and API
- Encryption based on HTTPS connection
- Easier to implement
- Newer, still evolving protocol
- Only asserts identity (no permissions)
- **rather for social**
- **User can choose which attributes (claims) to give to the relying party**
##### SAML
- **rather for corporate**
- Heavy weight XML
- Supports web applications
- Encryption is part of SAML
- More difficult to implement
- Older, established standard (2005)
- Allows for permissions to be transferred from IdP to SP
- **Implementation decides which attributes are given to relying party**
### Kerberos
- User authentication in IP networks
- Use of secret key (no public key) cryptography
- only inside one company
#### Terminology
![[Pasted image 20241129124829.png#invert]]
#### View
![[Pasted image 20241129124850.png#invert]]
#### In Practice
![[Pasted image 20241129124913.png#invert]]
#### Example
#####  getting a ticket-granting ticket (TGT)
![[Pasted image 20241129124944.png#invert]]
##### requesting a ticket to access Server Sam
![[Pasted image 20241129125015.png#invert]]
##### accessing Server Sam
![[Pasted image 20241129125042.png#invert]]
#### Security Analysis
**Kerberos version 5 is considered to be secure**
- No passwords are transmitted in the clear
- Timestamps prevent replay attacks and enable mutual authentication
- At the end, user and server share a key to protect the communication
- But: the users' master keys are still derived from their password  offline attacks possible if passwords are weak

**Kerberos requires a reasonably synchronized time among the participants**
- Because replay attacks are detected based on timestamps
- In practice, timestamps of the clients are accepted during a certain time window around the time of the servers (e.g., +/- 1 minute)
- In addition, received messages must be stored on the server while their timestamps are still valid to detect replayed messages
#### Authentication across realms
![[Pasted image 20241129125213.png#invert]]
### Shibboleth
- Shibboleth is a system for federated identity management
- Federated identity management: Identity information is managed and used across multiple security domains
- Every user has one credential (e.g., username / password) that is stored and managed by his home security domain
	- E.g., by the ZHAW for ZHAW students
- Authentication always happens in the home security domain, which issues a token to access a service in another security domain
- The token does not necessarily have to contain the user's identity
- SWITCH
#### Terminology
- **Organizations**: institutions that are participating in a federation, e.g., companies, universities,...
- **Users**: participating persons, each one is assigned to an organization
- **Service providers (SP)**: services provided by organizations to users
- **Identity providers (IdP)**: maintain credentials and attributes of users of an organization
	- Create tokens to access a SP
- **Discovery service**: used to determine a user's home organization (IdP)
- The protocol is based on HTTPS and [[#Security Assertion Markup Language (SAML)]] (Security Assertion Markup Language)
![[Pasted image 20241129131215.png#invert]]
#### Example
![[Pasted image 20241129131343.png#invert]]
#### Security Analysis
 - In general, Shibboleth is considered secure, provided that HTTPS is used on all communication links
 - Shibboleth has several similarities to Kerberos across realms:
	 - Authentication is done by the organization where the user is at home: IdP (Identity Provider) ≡ Authentication Service
	 - Access to the resource is protected by the organization of the service: Service Provider ≡ Ticket-Granting Service / Server
	 - Tokens are provided by the home organization and interpreted by the organization of the service: Assertion & Attribute Statements ≡ Tickets
	 - Trust between IdP's and service providers ≡ Trust between KDCs
 - But Shibboleth is based on different technologies than Kerberos: HTTPS, SAML / own Kerberos protocol
	 - And Shibboleth uses public key cryptography
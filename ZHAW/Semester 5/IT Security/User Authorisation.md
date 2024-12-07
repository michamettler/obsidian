#itsecurity #sem5 

**What is an authorized [[User Authentication]] allowed to do?** => **Business** decides
## Building Blocks
![[Pasted image 20241206190451.png#invert]]

## Access Control Model
![[Pasted image 20241206191319.png#invert]]
### Discretionary Access Control (DAC)
- The control of access is based on the discretion of the owner of an object.
- The owner of the object (e.g., a file) controls which subjects (user, computer, group,…) can have access to it and to what degree
- The owner of an object is typically the user who created the object
- In practice, [[#Access Control List (ACL)]] and Capabilities are therefore the preferred methods to capture permissions
![[Pasted image 20241206190751.png#invert]]
![[Pasted image 20241206190805.png#invert]]
#### Access Control List (ACL)
- implementation of [[#Discretionary Access Control (DAC)]]
- An ACL is associated with an object with entries of permissions per subject (user, group etc.)
	- Permissions are stored in the meta-information for the object
	- Example: The read permission flag for the group CRM is true
- ACLs are used by virtually all current OS: Windows, Linux, Mac OS, Android
![[Pasted image 20241206191221.png#invert]]
![[Pasted image 20241206191338.png#invert]]
##### ACL on Linux
![[Pasted image 20241206202736.png#invert]]
![[Pasted image 20241206202650.png#invert]]
##### Problems
- While ACLs are often used and well understood, there are some situations where it's difficult to determine the permissions
- has to be programmatically tracked
![[Pasted image 20241206203506.png#invert]]
#### Capabilities
- Capabilities are another approach to implement DAC
- A capability is an unforgeable token (ticket) owned by a subject that contains the permissions for specific objects
- Unforgeability is achieved, e.g., by protecting them with cryptographic mechanisms, e.g., with digital signatures or MACs
- The reason why capabilities are a DAC-variant is because capabilities can usually be delegated to others
##### Solving confused deputy with capabilities
- Capabilities also make it possible to grant a program minimal rights
![[Pasted image 20241206203542.png#invert]]
![[Pasted image 20241206203613.png#invert]]
### Mandatory Access Control (MAC)
- Access control is mandated by the system: A system-wide policy determines who is allowed to do what on the system
	- Individual user cannot alter this (in contrast to DAC)
	- The policy is configured by a (security) policy administrator
- Typically only used for critical parts of the systems
- In operating systems, MAC is usually used in combination with DAC
- Based on Integrity Levels (IL) assigned to processes and objects
	- - Installer
	- System (OS processes)
	- High (administrators)
	- Medium (non-administrators)
	- Low (temporary Internet files)
	- Untrusted (logged on anonymously)
- Processes usually inherit the integrity level of the process that spawned it
![[Pasted image 20241206204718.png#invert]]
### Role-Based Access Control (RBAC)
- DAC and MAC are rather technical access control models
- Furthermore, in the business world, its more natural to define access rights for users depending on things such as job functions, project team membership, department
- In a RBAC system, access control decisions are based on the role(s) a user has within an organization
- A role defines a set of transactions allowed for its members
- One solution to overcome the «static aspect» of roles was combining RBAC with ABAC (ABAC can be used as a standalone mechanism)
![[Pasted image 20241206204810.png#invert]]
#### Example Jakarta
![[Pasted image 20241206210640.png]]
## Access Management process
![[Pasted image 20241206190703.png#invert]]

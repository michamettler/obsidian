#itsecurity #sem5 
![[Pasted image 20241006163700.png]]
## Certificate Types
A certificate is a signed statement by a trusted third party that a certain public key belongs to a certain name. It is a means to authenticate a public key. It is **not** a means to authenticate a communication partner.
![[Pasted image 20241006163519.png]]
## Certificate Chains
Public Key Infrastructure (PKI): In order to authenticate the subject (domain in cert), one needs to authenticate the public key of the issuer (the CA) => chain. The root CA's certificate can be verified by the public key that is in that very cert (**self-signed**/**root-certs**). Those root certs are being preinstalled in the browser.
![[Pasted image 20241006162407.png]]
Intermediate Certificates are used to minimize the risk in case the root certificate has been attacked.
### X.509 Certificate
![[Pasted image 20241006164124.png]]
## Certificate Transparency
Logs of certificates for transparency.
![[Pasted image 20241006162450.png]]
## Certificate Revocation
If the private key of Alice has been stolen, the corresponding certificate has to be revoked. However, she (the subject) can't change their own certificate, so the issuer has to do it.
### Certificate Revocation List (CRL)
This is a list by the Certificate Authority (CA) of all private keys that has been stolen. Every client has to obtain CRL from CA.
![[Pasted image 20241006162734.png]]
#### Limitations
- **time window** between revoking cert and finding on list
- CRLs only get larger
- can't remove cert from CRL (even when expired)
- many cert go into CRL in case of security breach
- => getting smaller
### Alternative 1: Online Certificate Status Protocol (OCSP)
![[Pasted image 20241006163036.png]]
- Privacy Issues
- Single Point of Failure
- most implement soft fail (if OCSP response is not received in time, its valid)
- can be used in **Must-Saple**, meaning every TLS handshake requires an OCSP response (=> **hard fail**), which results in transition period
### Alternative 2: Browser-Summarized CRLs
Preinstalled CRLs on browser which is being updated automatically for famous sites.
## Workflow Summarized
![[Pasted image 20241006164311.png]]
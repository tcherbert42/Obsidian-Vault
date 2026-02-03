# Windows Part 2 - [[Kerberos|kerberos]]

# [[Kerberos|kerberos]]
1. Sends an AS-REQ, a request with a secret key from the user's password
2. If valid, the ticket is returned in a AS-REP message. This is the user's identity encrypted with the Kerberos accounts password
3. If the user attempt to access a resource, the client looks for a Service Principle Name and will present its ticket to Kerberos in a TGS-REQ to verify they are legit
4. Kerberos returns the Ticket Granting Service Ticket in a TGS-REP

## Kerberoasting / ASREProasting


# Delegation (server will access another service as a user or service account )
Delegation allows servers to act behalf of others to another service
Ex: User authenticates to front-end webserver
	- Webserver needs to authenticate to the back-end as an authenticated user

## Constrained Delegation (server can only access certain services)
- Constrained delegation allows restriction of what services the server can act to.
- Allows for request for a ticket of another user with its own ticket
	- First find where you can delegate to
	- Dump or request a ticket with asktgt for the principle
	- Rubeus S4U to request a usable ticket
		``` Rubeus s4u /impersonateuser: /msdsspn:<service> /user: /ticket: /nowrap ```
	- Use the ticket for a new logon session
		``` Rubeus createnetonly /Program:C:\Windows\System32\cmd.exe /domain: /username: /password: /ticket: ```
		- Then use the token of the newly created process with C/2


### Alternate Service Name (changing the service - has to be one of the allowed services if under constrained delegation)
- All service tickets are encrypted with the same key, if they are running under system.
- SPN information of the ticket is not encrypted, so we can modify it
	- This is "by design"
- Rubeus /altservice can be used to change the service 
	``` Rubeus s4u /impersonateuser: /msdsspn:cifs/win2016d-10 /altservice:ldap /user: /ticket: /nowrap ```
	- Then use the token
- This would then allow for DCSync attack

# Domain Replication
- Organization may have multiple domain controllers for redundancy and load balance.
- Those Domain Controllers must sync data to each other to have up-to-date, consistent information
	- This is done using Directory Replication Service protocol


# DCSync Attack
- If we can compromise a domain account with the **"Replicating Directory Changes" /all** permissions, then we can gain domain hashes for accounts such as krbtgt. 
- [[Mimikatz|mimikatz]]
	``` lsadump::dcsync /user:<user> /domain:<domain> ```

# Ticket Persistence
## Silver Tickets
- Forged service ticket signed with RC4/AES
- Short/Medium form of persistence
	- Thirty-day password reset.
- If we can dump Kerberos keys for a computer account, forge a silver ticket for the cifs(kinda like smb) service, and use that ticket to maintain access to the system. 

Rubeus.exe silver 

## Golden Tickets
- Tickets signed with the domain krbtgt account.
- Golden tickets can impersonate any user, to any service, on any machine in the domain.
- Long-term persistence
	- Krbtgt account password is not changed automatically
- If we can dcsync from the domain admin, then we can forge a golden ticket to import for full domain access. 

Rubeus.exe golden 

## Diamond Tickets
- Diamond Tickets also allow us to access any service as any user. 
	- Remember golden tickets are created offline with krbtgt hash of domain 
	- It is theoretically possible then for golden tickets to be detected because there is a TGT request without a AS request. 
- A Diamond Ticket is a modified legit TGT issued by a [[Domain Controller|domain controller]](DC). 
	- This is achieved by
		- Requesting a TGT
		- Decrypting with domain's krbtgt hash
		- Modifying desired fields 
		- Re-encrypting 

### Diamond Ticket Steps
``` Rubeus.exe diamond /tgtdelg /ticketuser: /ticketuserid: groups:512 /krbkey: ```
- tgtdelg : Uses Kerberos GSS-API to obtain useable TGT for current user without needing any creds
- Ticketuser: username of user to impersonate
- Ticketuserid: domain RID of user
- Groups: desired group RID
	- 512 is domain admin
- Krbkey: krbtgt AES256 hash

# Group Policy Abuse

## Modify Existing [[Group Policy Object|GPO]]s (Group Policy Objects)
- We can look for CreateChild, WriteProperty, or GenericWrite for groups we have access to.
- Tools such as SharpGPOAbuse can be used to create startup scripts network shares for computer sunder GPOs we have access to

## Linking [[GPO]]s
- If we can gain "Create groupPolicyContainer objects" privileges over principles, we can create new GPOs on them.

# AD Certificate Services (ADCS)
- Allows you to build public key infrastructure
	- Digital Certificates, public key cryptography, and Digital signature capabilities
	- Often used for VPNs, Internet Protocol Security (IPSec), and SSL/TLS
- This can be used for authentication through certificate keys with computer, user, or device accounts on the network

## Certify 
- Certify is the main tool used for enumerating and abusing misconfiguration in AD CS. 
	- Certify.exe cas
		- Finds Root and subordinate certificate provides for the domain
	- Certify.exe find /vulnerable
		- Enumerates for excessive privileges 

### Enrollment Rights abuse
- Enrollment rights define who can request a certificate from the certificate template
- If the template has **ENROLLE-SUPPLIES_SUBJECT**, it can be requested for any user
	- If we are within the enrollment rights, we can request a certificate for any user
	``` Certify.exe request /<cert server> /template: /altname:<user> ```

# Domain Trusts
What is a trust?
- Trust relationships allow users in one domain to authenticate and access resources in another domain.
- Trusts can be bidirectional, or one-way
	- Trusted domain is allowing access to resources in the trusting domain
	- One-way trusts can be labeled as inbound and outbound depending on perspective

## One-way Inbound
- If the trust is inbound from our perspective, principles in our domain can access the foreign domain
- (Inbound means inbound trust, meaning your are being trusted.)
- Using powerview, we can enumerate groups that have users outside its domain
	- These users can be used o exploit the trust and interact with the foreign domain.
	- Rubeus can get a target user TGT, request a referral ticket, and request tickets in the target domain
	- Referral tickets are used to move across domains. 

## One-way Outbound
(we are trusting someone else to access our resources)
- This type of trust is where your domain is trusting another
- This can still be exploited with a domain user by abusing a shared cred for the trust. 
	- Both domains have a shared password for the trust which we can dump to abuse the trust. 
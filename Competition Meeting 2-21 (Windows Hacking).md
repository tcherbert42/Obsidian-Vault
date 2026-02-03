# Windows Hacking

##### Agenda
- Recon
- Priv Esc
- Persistence
Introduction into Domain (AD)
- Recon
- Kerberos

### Host Recon
- WinPeas.exe
	- Sometimes too verbose, does not have colors like LinPeas (just use sharpup)
- SharpUp
	- More granular checks
	- Service Enumeration, hijackable paths, autoruns, embedded passwords in Group Policy (Vulnerable services and get beacon)
- Get-ServiceAcl.psl
	- Prints out the service rights we have 

## Privilege Escalation
- Service paths with spaces and no quotes 
Why does this matter?
- Windows interprets spaces as a terminator
C:\Program Files\Vulnerable Services\Service
- C:\Program.exe
- C:\Program Files\Vulnerable.exe
- C:\Program Files\Vulnerable Services\Service.exe 

##### Service Permissions
If we find we have permissions to modify a service path from SharpUp and Get-ServiceACL.ps1, we can modify it to our own path
```run sc config <servicename> binPath=""```

If we find a service binary that we can modify, we can replace the binary with ours 
```cp <payload> <servicepath>```

# Persistence Overview (not necessarily important for lab)
Common persistence mechanisms
- Services
- Registry Keys
- Scheduled Tasks
- Startup Folder
Maintaining persistence
- Password Filters

### Common Persistence Mechanisms
Services
Scheduled Tasks
Startup Folder
Run key in Registry
- Any executable path here will be executed on system startup if under system, 

## Persistence - Registry Keys (common)
Debugger values
- Debugger values can be added to any binary, and we can replace them with a command prompt
- In this example, adding "Debugger" lets us open an admin terminal on the login screen 

##### Password Filter DLL Uses
Credential Harvesting 
- DLL could be configured to log/harvest passwords when changed
Keyword enforcing
- May set password filter to require a certain keyword, or that a password must be a specific phrase

# ACTIVE DIRECTORY

## ADPeas
- Active Directory spinoff of the PEAS Suite
- Color Coded
- Basically just a powershell script
- Returns configs for accounts
- Caught everything they needed for compromise at CPTC

##### Other Recon Options
- PowerView
	- Importable PowerShell tool for queries
	- Good for finding where users can login (through RemoteDesktop, etc)
- SharpView
	- C# version of PowerView
	- C# executable workaround if you cant use PowerView
- ADSearch
	- Custom LDAP searches
	- More difficult to use

# LDAP
###### same kinda thing as kerberos but less secure
- Protocol used for server communication, storing object data, and authenticating users. (it is a schema)
- How do users authenticate?
	- Client sends bind request along with username and password
	- Server checks client's credentials against LDAP Database
	- User is authenticated

### Pass-the-Hash
Attacker will often dump user hashes and credentials
Hashes can be passed to a computer to authenticate and laterally move across networks
- Mimikats
	- ```sekurlsa::pth /user: /domain: /ntlm: /run:cmd```
- Evil-WinRM

# Kerberos
###### More secure authentication method (TGS)
1. Sends a [[AS-REQ]], a request with a secret key from the user's password
2. If valid, the ticket is returned in a [[AS-REP]] message. This is the user's identity encrypted with the Kerberos accounts password
3. If the user attempt to access a resource, the client look for a Service Principle Name and will present its ticket to Kerberos in a [[TGS-REQ]] to verify they are legit 
4. Kerberos returns the **Ticket Granting Service Ticket** in a [[TGS-REP]]

###### ASREP - Roasting and Kerberoasting 

## ASREP-Roasting
"Do not require Kerberos preauthentication"
This allows you to request a AS-REP without authenticating first and passwords can be cracked offline
```Rubeus.exe asreproast /user: /nowrap```

## Kerberoasting
Post-compromise attack on service accounts
- Attackers can request Ticket Granting Tickets running under domain accounts and crack them offline, since TGS are encrypted with secret from password of the account
Rebeus
``` Rubeus.exe kerberoast /simple /nowrap```

Have to use a TGT to get a TGS to then use a service. TGS (ticket granting ticket) is just for authentication, and AS_REP can be cracked cause contains user password. Once you have TGT, you can then request TGS (ticket granting service) to allow you to request a service from a server. Using AS

## Delegation
Delegation allows users or machines to act behalf of others to another service
EX: User authenticates to front-end webserver
- Webserver needs to authenticate to the back-end as an authenticated user

### Unconstrained Delegation
When configured kerberos issues TGT along with service ticket, so no repeated authentication prompts. 
- There are no limits when requesting access to services. 
- TGTs are cached

#### Unconstrained Delegation Abuse
- Use ADPeas to look for Unconstrained Delegation and PWN the box
- Rebeus Triage for domain admin tickets (use rebeus to get domain admin tickets)
- Leverage ticket for logon session
	``` Rubeus createnetonly /program:cmd.exe /domain: /username: /password:Fake (use whatever password) /ticket: ```
- Use Mimikatz to abuse the created process



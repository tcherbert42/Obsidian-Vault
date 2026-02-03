
# Windows Hacking
- NTFS - has advantages over fat16/fat32
- Permissions
System32
- Contains OS system environment variables

### System Configuration
msconfig
- Tabs: General, boot
###### Computer Management
compmgmt.msc
- system tool, Storage, Applcations
## Know Your System 
System Information
- msinfo32
Resource Monitor -  resmon

##### Registry Editor
Regedit
- Editing stuff directly on cpu (assembly?)
- Supercedes all other windows settings (end all be all)

### Active Directory
- Permissions 
- Domain Controller
- Group Policy Objects (GPOs)
- Organizational Units (OUs)

## Security Groups
- Domain ADmins
- Server Operators
- Backup Operatorss
- ACcount Operators
- Domain Users
- Domain Computers

### AD Authentication
LDAP
- Lightweight directory acess protocol
- Functions - Authentication, query
Kerberos
- Facilitates mutual authentication
- Advanced and more secure
- Ticket granting system using shared key cryptography
- Key distribution 

### Exploits
Sticky Keys Exploit
- Gateway to start priv esc.
- Get to windows recovery mode and use troubleshoot option
- Companies don't upgrade cuz it costs $
Eternal Blue Exploit
- made by NSA
- Patch happened in 2017 but didnt quite get fixed until 2019
- Takes advantage of the Server Message Block (SMBv1)

## Password Spraying
- Common targets: enterprise networks, cloud services, web applications, VPNs, and email systems
- Only 5 - 10 to one account to avoid lockout
- Different than Password stuffing

### Phishing with AD Bypass
- Middleman attack but acting like a server
- Token or Session hijacking 

# Priv esc with sticky keys
- Troubleshoot, CMD prompt, C:, System32, 

### WinPEAS
- Same as linPEAS, and adPEAS
- winPEAS.exe
- use winPEAS.exe quit verbose for better formatted output

## Hacking AD
High Level
- Abuse of authentication methods
- LDAP
- Kerberos
Looking for users with Domain Action Privileges
- Users that can sync can dump everything
If you can create objects 

### Auth Abuse
LDAP
- Recon
- Pass the Hash
- Password Cracking
Kerberos
- Pass the ticket
- Exploiting account configuration
	- Kerberoasting - tickets are encrypted with user's password, if you have password you can crack encryption on the ticket
	- ASERP Roasting - same as kerberoasting 
	- Delegations


### Directory Services Continued - Module 5

## Groups and Organizational Units
- Implement a least-privilege policy - only give users the permissions necessary to perform their jobs. 
- Periodically review group memberships and OU structures for any inaccuracies or redundancies. 

## Role-Based Access Control (RBAC)
- **Principles and Benefits**
	- RBAC assigns permissions based on roles within the organization rather than assigning permissions to specific users. 
	- It simplifies the management and auditing of access controls and can be highly effective in large, complex organizations
- **Implementation Strategies**
	- Start with a thorough analysis of roles within the organization and the permissions each role requires. 
	- Implement role hierarchies where senior roles inherit permissions from junior roles.
	- Test thoroughly before deployment and perform regular audits after that. 

## Access Control Lists (ACLs)
- ACLs are lists of permissions attached to an object within the directory. They specify which users or system processes are granted access to the object, and what operations are allowed. 
- For example, an ACL might specify that users in the "HR" group can read and write to a "Personnel Records" folder, while users in the "Finance" group can only read the folder. 

# Authentication and Authorization

## [[SSO, single sign-on|Single Sign-On]] (SSO)
- **Definition and Benefits**
	- [[SSO, single sign-on|Single Sign-On]] allows a user to authenticate once and gain access to multiple systems without being required to log in again for each application. 
	- Benefits include improved user experience, reduced password fatigue, and centralized management of authentication, which can make monitoring and auditing easier. 
- **Risks and Countermeasures**
	- **Risks**: If an attacker gains access to the SSO system, they can potentially access all linked applications. Phishing attacks may also become more effective. 
	- **Countermeasures**: Use strong encryption, regular monitoring, and employ [[Multi-Factor Authentication]] ([[Multi-Factor Authentication|MFA]]) for added security. 
## [[Multi-Factor Authentication]] (MFA)
- **Types of Authentication Factors**
	- **Something You Know**: Passwords, PINs, etc. 
	- **Something You Have**: Smart cards, security tokens, mobile devices, etc. 
	- **Something You Are**: Biometrics like fingerprints, iris scans, etc. 
- **Implementation Considerations**
	- Ensure that the [[MFA]] system is user-friendly to encourage adoption. 
	- Choose the right combination of factors based on the sensitivity of the data being protected. 
	- Be aware of the scalability and how easily new users can be onboarded. 

### Authorization Mechanisms within Directory Services
- **Policy Enforcement**
	- Authorization policies dictate what authenticated users are allowed to do. These policies can be enforced at different layers such as application level, network level, or directly within the directory service. 
	- Enforcement could be done through Access Control Lists (ACLs), Role-Based Access Control (RBAC), or Attribute-Based Access Control (ABAC).
- **Privilege Levels**
	- Privilege levels are used to categorize users based on the extent of access they should have within the system. 
	- Common levels include Administrator, Power User, Standard User, and Guest, each with its own set of permissions. 
	- It's crucial to follow the principle of least privilege-granting only the permissions necessary for users to complete their tasks. 
## Secure LDAP (LDAPS)
- **How it Differs from LDAP**
	- [[LDAPS]] is essentially [[LDAP]] over [[Secure Sockets Layer|SSL]] (Secure Sockets Layer) or TLS (Transport Layer Security). While LDAP transmits data in plaintext, LDAPS encrypts the data, making it more secure. 
	- In LDAP, the default port is 389, while for LDAPS, the default port is 636
- **Implementation Best Practices**
	- Always use certificates from a trusted Certificate Authority (CA).
	- Implement strong ciphers and disable weak ones to ensure robust encryption. 
	- Regularly update the SSL/TLS libraries to the latest versions to stay secure against known vulnerabilities. 


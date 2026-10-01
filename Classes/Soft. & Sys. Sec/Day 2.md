________
09-01-2026 | 08:02
Status: #school 
Tags: #SoftwareSystemsSecurity

### Usable Security - Design Principle
Ex: Allowing fingerprints, facial recognition, patterns to unlock rather than typing and memorizing complicated passwords. 
- Informed privacy settings to allow informed decision by users

**What about SSO (Singe-Sign on)?
- Do not need to repeat credentials
- User (attempt access App X) -> redirects to IDP(identity provider) -> (authenticated at IDP) -> Token issued -> Token send to App X -> Grant Access
- Security: Centralized control, easier MFA enforcement, better audit logging. 
- Risks:
	- Large blast radius (multiple applications)
	- Identity Provider outage
	- Misconfig: incorrect redirects, token validation, or application permissions can enable authorized access






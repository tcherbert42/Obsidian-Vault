# Web Hacking
# DNS
- Domain Name System
	- DNS Recursor
		- Server for receiving requests from client machine ( google servers )
	- Root Server
		- Points to a more specific location
	- Top Level Server
		- Resolves the ".com" portion
	- Authoritative Server
		- Final stop; returns the requested IP to the Recursor 
# HTTP
- Hypertext Transfer Protocol
- HTTPS = Secure
	- Uses TLS and SSL encryption
- Application layer
- Requests

# Web APIs 
- Application Programming Interface
- Abstraction of lower-level code
	- has its own syntax
- Browser APIs
	- Built into most browsers using JavaScript
- Third-Party APIs
	- Code must be found elsewhere
	- Larger learning curve
	- Ex. Google Maps API, Facebook Graph API

## CMS 
- Content Management System
- Simplistic website designing 
	- No need for coding or writing your own HTML files
- Ex. WordPress, Presta Shop, Wix, SquareSpace

# Web Enumeration
Wappalyzer
- Tool to identify the technology stack behind a website
- Can be used at its website or as a browser extension
- Useful in understanding what a website was built with - may contain vulnerabilities 

## OWASP Top 10
- List of most critical security risks to web applications
- Expecting a 2025 update, actually
- Enumeration can help identify technologies/configurations linked to these vulnerabilities

# Directory Busting
- Lots of different tools for this
	- Feroxbuster, DirBuster, GoBuster
- Using brute force to discover unlinked pages on an application
- Must have a word list to use: SecLists is a good one
- Warning: doing this to random websites can be considered malicious because you are repeatedly requesting the application

# Subdomain + Vhost Enumeration
- Important to enumerate subdomains because vulnerabilities may have been patched in the top domain, but not in subdomains
- Similar to directory busting, but may use a different command (depending on the tool used)
```  gobuster dns -d example.com -w <wordlist>```

- Virtual hosts are different websites on the same machine
- Same general structure as the dir command in gobuster, but a little more complex
``` gobuster vhost -u "http://0.0.0.0" --domain example.com -w <wordlist> ```

# Injection Probing
- Poking at the application to determine if its vulnerable to various injection attacks
	- SQL injection, command injection, cross-site scripting, etc.
- Injecting different inputs into parameters, URLs, etc. to see how the app responds. (can be automated)
- Can use BurpSuite to inject various payloads 

## BurpSuite
- Target
	- Select and modify scope
	- View past request
- Proxy 
	- Intercept and manage requests
- Repeater 
	- Hand modify and send requests
	- Grouping for race conditions
- Intruder 
	- Send (a few) requests rapidly
- Browser
	- (or foxy proxy)

# Authentication Attacks

## Sessions
- Why don't we just keep logging in?
- Session Lifecycle
	- Creation
	- Tracking
	- Expiration
	- Termination
- Session Management
	- Cookie Based
	- Token Based
		- JWT (javascript web token)
	- Crazy developer nonsense
- Cookie-Based Session Management
	- Set-Cookie Request Header
	- Auto sent with requests
	- Client side vulnerable
	- Domain Specific
	- Browser storage
- Token-Based session management
	- Javascript Web Tokens
	- Manually sent with requests
	- Challenges CSRF
	- Local Storage

### JWT Structure
- Header 
	- Algorithm
	- JWT
- Payload
	- Your data here
- Signature
	- Option to use None here 
"." used to separate Header, Payload, and Signature. Signature comes after the second "."

# Hacking Session Tokens
Finding Insecure Session management:
- Unencrypted/unobfuscated cookies
- Headers: HttpOnly, Creation/Expiry time
- Termination Process
- Local storage data

JWT Vulnerabilities
- Lack of Signing algorithm verification (None)
- Crackable/Compromised key

# Injection Attacks
Command Injection
- Leveraging direct calls to the server's console
- Types
	- Result Based
	- Blind
		- File vs. Time
- Filter Evasion 
- Inline
- Shell Operations
	- Eg: & whoami

# SQL Injection
- Structured Query Language (SQL)
- Types
	- In band
		- Union vs Error based
	- Out of band
	- Inferential 
		- Boolean vs Time Based
- Where can I find it
	- Input fields
	- Login portals
- Filter Evasion
	- Character Encoding 
		- URL
		- Hex
		- Unicode
- Components
	- Normal input
	- SQL commands 
	- Escape characteristics
- Objectives 
	- Authentication Bypass
	- Information Exposure
	- Malicious interference
	- Data destruction 

# NoSql Injection
NoSql
- The generic term for Database solutions using anything other than SQL
- Most common: MongoDB
Pros
- Extra Features
- Different Protections
Cons
- Complications/Complexities
- Identification

# SSTI and CSTI
- Server-side Template Injection
- Client-side Template Injection
- Differences:
	- Server vs. Client
- Fuzzing
	``` ${{<%[%'"}}% ```
- GitHub repos for syntax 
	- Input fields

# File Inclusion
Local File Inclusion
- Path Traversal
- Find "hidden files"
Remote File Inclusion
- http://ipaddress/
- SSRF (Internal IPs)
Path Traversal
- Traversal String ../
- Absolute Path /etc
Filter Evasion
- Dir breakouts
- Obfuscation
Others
- PHP Wrappers

# Server-Side Request Forgery (SSRF)
Server making requests to a user variable locations?
- You mat be able to use SSRF!
- Using Web Servers as primitive pivot points
- Resource Exposure
- URL Parameters
- Source code modification

# XSS (Cross Site Scripting)
- Stored
	- Scripts are stored on server
	- Executed when loaded 
	- i.e. comments on a website, blogposts, etc
- Reflected
	- Input immediately returned b web application 
	- Not stored on the server
	- Bad links
- Dom-Based
	- Dump, old, and stupid. Don't worry abt it
- Exfiltration 
	- Web requests to listener
	- Other black magic


# Module 3 - OS Essentials
Continuing after Active Directory/Directory Services

##### PAM - Pluggable Authentication Modules (Linux)
- a mechanism to integrate multiple low-level authentication schemes into a high-level application programming interface.
- There are third party ways to integrate Linux into active directory services, but Microsoft does not like open-source. 

### Remote Access
- ##### SSH - Secure Shell
	- A cryptographic network protocol for operating network services securely over an unsecured network, most notably remote login and command-line execution. 
	- Huge advantage to SSH is secure!
- ##### RDP - Remote Desktop Protocol
	- A very useful tool where safe to use
	- GUI based
	- The bane of existence for security professionals
- ##### VNC - Virtual Network Computing
	- Remote Frame Buffer protocol (RFB)
	- Open-source parallel to RDP
- ##### VPN - Virtual Private Network
	- Creates a secure connection between two networks using strong encryption
	- Makes multiple boxes look like they are on the same LAN through the magic of encryption

### Monitoring and Logging
- ##### SNMP - Simple Network Management Protocol
	- Internet Standard protocol for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behaviour. 
- ##### Syslog - Standard message logging system for Linux and other UNIX systems
	- A standard for message logging allowing separation of the software that generates messages, the system that stores them, and the software that reports and analyzes them.
	- Taking in logs from everything besides Windows
	- Logs reside here
- ##### Event Logs - Windows equivalent of Syslog

### Security Services
##### Firewalls
- IPtables (Linux)
- Windows Firewall
- PFSense
##### SSL/TLS - secure communications platform
##### IDS/IPS 
- Intrusion Detection Systems
- Intrusion Prevention Systems

### Virtualization Services
- ##### Type 1 - bare metal
	- Microsoft Hyper-V
	- VMware ESXi
	- Citrix XenServer
- ##### Type 2 - requires operating system host
	- KVM (Linux)
	- Oracle VirtualBox

## Web Services
##### Apache HTTP Server (Apache)
- One of the oldest and most widely used web servers. It offers high flexibility, extensive module support, and a strong community. Apache uses a process-driven model but can be configured to use a threaded model.
##### Nginx
- Known for its high performance and low resource usage, Nginx often serves as a reverse proxy, HTTP cache, or load balancer in addition to being a web server. 
##### Microsoft Internet Information Services (IIS)
- Integrated with the Windows OS, IIS is commonly used for serving ASP.NET applications but also supports PHP and other web technologies. It is highly optimized for the Windows environment. 
##### Tomcat
- Apache Tomcat is often used as an application server for serving java-based web applications but can also act as a standalone web server.

### Database Services - SQL
##### MySQL 
- One of the most popular open-source relational database management systems, MySQL is well-known for its speed and reliability. 
##### PostgreSQL 
- A powerful, open-source object-relational database system that extends the SQL language. 
##### Microsoft SQL Server
- A relational database server developed by Microsoft, SQL Server is known for its robustness and extensive feature set. 
##### Oracle Database
- A multi-model database management system produced and marketed by Oracle Corporation.
##### SQLite
- A C-Language library that implements a small, fast, self-contained, high-reliability SQL database engine. 

### Database Services - NoSQL
##### MongoDB 
- A popular NoSQL database that uses a document-oriented data model.

#####  Cassandra
- A highly scalable NoSQL database designed for handling large amounts of data scross many commodity servers.

##### Couchbase
- A NoSQL database that offers high-performance, flexible data models, and easy salability.

#####  Neo4j 
- A graph database that offers high-performance, flexible data models, and easy scalability. 

## Messaging Services - Windows


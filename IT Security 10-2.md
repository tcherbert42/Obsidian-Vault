### Windows Tools Continued
[[sysinternals suite|Sysinternals Suite]]:
- Provided by Microsoft, it's a collection of utilities for managing, diagnosing, troubleshooting, and monitoring Windows sytems. While not open source, it is free to use.
[[osquery|OSQuery]]:

## Linux Tools
[[lynis|Lynis]]:
- An open-source security auditing tool used to elevate the security defenses of Linux and UNIX-based systems. 
[[openscap|OpenScap]]:
- An auditing tool that utilizes the Security Content Automation Protocol (SCAP) to provide automated configuration and vulnerability scanning. 
[[osquery|OSQuery]]:
- This tool can also be used on Linux systems to query the system state for various security metrics. 
[[rkhunter|RKhunter]]: (Rootkit Hunter):
- Searches systems for known and unknown rootkits, backdoors, and other vulnerabilities. 
[[clamav|ClamAV]]:
- An open-source antivirus engine for detecting trojans, viruses, and other malicious software. 
Auditd:
- The Linux Auditing System can capture system events such as file accesses, system calls, and user activities to enable system monitoring and security analysis. 
[[fail2ban|Fail2Ban]]:
- A log-parsing tool that protects against brute-force attacks and can update firewall rules to reject suspicious IP addresses. 
[[chkrootkit|Chkrootkit]]:
[[tiger|Tiger]]:

# Cross Platform Tools
[[Nmap]]:
- Often used to discover hosts and services on a network, Nmap can also be used to detect security risks.
[[Wireshark]]:
- While primarily a network protocol analyzer, Wireshark can also be used to identify malicious activity on a network. 
[[Inspec]]:
- An open-source testing framework that allows you to specify compliance, security, and other policy requirements in an easy-to-read language. 

## Cross Platform Tools - Configuration
Although not security tools per se, these tools can be used to enforce security configurations across various systems. 
- **[[ansible|Ansible]]** is an open-source automation tool primarily used for software provisioning, configuration management, and application deployment. Written in Python, it uses a simple, human-readable language (YAML) for defining automation tasks. [[ansible|Ansible]] does not require agents to be installed on target systems, relying instead on SSH for executing tasks, making it relatively easy to set up and use. 
- [[saltstack|SaltStack]] (Salt), commonly known simply as Salt, is an open-source configuration management and remote execution tool. It uses a master-minion architecture and is designed to handle larger infrastructures with high levels of complexity and scalability. It is known for its high-speed data collection and task execution capabilities. SaltStack uses YAML to define states and can execute shell commands across multiple systems in parallel.
- [[terraform|Terraform]] is an open-source infrastructure-as-code tool developed by  HashiCorp. It is designed to build, change, and version control cloud  infrastructure efficiently. Terraform uses its own domain-specific  language (DSL) called HashiCorp Configuration Language (HCL) to  define infrastructure resources in a declarative manner. Terraform is particularly strong at provisioning and managing cloud infrastructure  resources and supports multiple cloud providers like AWS, Azure, and Google Cloud.
- [[puppet|Puppet]] is an open-source configuration management tool that automates the provisioning and management of infrastructure. It uses a master-agent architecture and a declarative, domain-specific language for defining the desired state of resources. Puppet then ensures that the defined state is enforced on target systems. It is widely used in large enterprises and supports both Linux and Windows systems.

# Directory Services 
Identity and Access Management - **Module 5**
10-02-2025

**Identity management** ([[IAM, IdAM|IdM]]), also known as **identity and access management** (**IAM** or **IdAM**), is a framework of policies and technologies to ensure that the right users (that are part of the ecosystem connected to or within an enterprise) have the appropriate access to technology resources.

**Identity management** (**ID management**) – or **identity and access management** (**IAM**) – is the organizational and technical processes for first registering and authorizing access rights in the configuration phase, and then in the operation phase for identifying, authenticating and controlling individuals or groups of people to have access to applications, systems or networks based on previously authorized access rights. 

## **IAM** - Functions
1. The **pure identity** function: Creation, management and deletion of identities without regard to access or entitlements; 
2. The **user access** (log-on) function: For example, a [[smart card]] and its associated data used by a customer to log on to a service or services (a traditional view);
3. The **service** function: A system that delivers personalized, role-based, online, on-demand, multimedia (content), presence-based services to users and their devices. 
4. **Identity Federation**: A system that relies on [[federated identity]] to authenticate a user without knowing their password.
	 - This is what allows you to sign in to Epic Games with gmail or apple account!
	 - Like when you only sign in to tech express and then automatically signed in to iLearn, Outllook, or Yujamedia as well.
5. **Audit** function: Monitor bottlenecks, malfunctions, and suspect behavior. 

## **IAM** - Capabilities
- **Authentication**: Verification that an entity is who/what it claims to be using a password, biometrics such as a fingerprint, or distinctive behavior such as a gesture pattern on a touchscreen.
- **Authorization**: Managing authorization information that defines what operations an entity can perform in the context of a specific application. For example, one user might be authorized to enter a sales order, while a different user is authorized to approve the credit request for that order.
- **Roles**: Roles are groups of operations and/or other roles. Users are granted roles often related to a particular job or job function. Roles are granted authorizations, effectively authorizing all users which have been granted the role. For example, a user administrator role might be authorized to reset a user's password, while a system administrator role might have the ability to assign a user to a specific server. 
- **Delegation**: Delegation allows local administrators or supervisors to perform system modifications without a global administrator or for one user to allow another to perform actions on their behalf. For example, a user could delegate the right to manage office- related information.
- **Interchange**: The [[SAML protocol]] is a prominent means used to exchange identity information between two identity domains. [[OpenID Connect]] is another such protocol
	- For example, when we connect our Amazon account to our Twitch account and the separate page is opened that says "give amazon access to twitch account {insert permission}"

### **IAM** - Centralized vs. Decentralized
##### **IAM** - Centralized - Advantages
1. **Single Point of Management**: All identity and access management tasks are consolidated, making it easier to manage user identities and permissions.
2. **Consistency and Standardization**: Enforces uniform security policies and procedures across the organization. 
3. **Ease of Auditing**: A centralized system facilitates easier logging and monitoring, which is crucial for compliance with regulations like GDPR, HIPAA, etc. 
4. **Reduced Complexity**: Having one system reduces the learning curve and the chances of misconfiguration. 
5. **Cost Efficiency**: Lower total cost of ownership as you maintain fewer systems. 

###### **IAM** - Centralized - Disadvantages
1. **Single Point of Failure**: If the centralized IAM system goes down or is compromised, it can affect the entire organization. 
2. **Scalability Challenges**: As the organization grows, the centralized system may require significant upgrades or redesign. 
3. **Potential for Bottlenecks**: High volumes of authentication and authorization requests may lead to delays.
4. **Less Flexibility**: Difficult to tailor specific IAM solutions for individual departments or business units. 

##### **IAM** - Decentralized - Advantages
1. **Local Control**: Departments or business units have the flexibility to implement IAM policies that are most relevant to them. 
2. **Scalability**: Easier to scale the organization horizontally. New departments can have their IAM solutions without burdening the central system. 
3. **High Availability**: Failure in one part of the decentralized IAM infrastructure is less likely to disrupt the entire organization. 
4. **Faster Implementation**: Smaller, department-level solutions can often be implemented more quickly than a single, large centralized system. 
###### **IAM** - Decentralized - Disadvantages 
- **Inconsistency**: Different departments may have different levels of security, leading to a fragmented security posture. 
- **Higher Costs**: The total cost of ownership could be higher due to the maintenance of multiple systems. 
- **Complex Management**: Requires coordinated efforts to manage and update multiple systems. 
- **Difficult Auditing**: Compliance verification is more complicated as logs and records are spread across various systems. 


## Directory Service Fundamentals - History
- 

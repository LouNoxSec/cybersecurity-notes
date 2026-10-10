# 🛡️ Cybersecurity Fundamentals

## 📘 Overview

This document summarizes the cybersecurity concepts, principles, tools, technologies, programming languages, and analysis environments introduced during my initial hands-on learning through TryHackMe and other training resources.

The goal is to build a structured reference, reinforce fundamental concepts, and identify topics that require further practice.

These notes represent an ongoing learning process, not a claim of mastery.

## 🧠 Core Cybersecurity Concepts

### 🔐 The CIA Triad

The CIA triad is a fundamental model used to describe the three main objectives of information security.

- **Confidentiality:** Ensures that information is accessible only to authorized users.  
  *Example:* Encrypting sensitive files and restricting access through permissions.

- **Integrity:** Ensures that information remains accurate and is not modified without authorization.  
  *Example:* Using cryptographic hashes to detect unexpected file modifications.

- **Availability:** Ensures that systems and information remain accessible when needed.  
  *Example:* Using backups, redundancy, and protection against denial-of-service attacks.

### 🪪 Authentication, Authorization, and Accounting (AAA)

AAA is a framework for managing and tracking access to systems and resources.

- **Authentication:** Verifies who a user or system is.
- **Authorization:** Determines what an authenticated user or system is allowed to do.
- **Accounting:** Records activities and resource usage for monitoring and auditing.

📋 *Example:* A user logs in with multifactor authentication, receives access only to permitted resources, and their activity is recorded in logs.

### 🔑 Identification, Authentication, and Authorization

These concepts describe different stages of access control.

- **Identification:** A user claims an identity, for example by entering a username.
- **Authentication:** The system verifies the claimed identity.
- **Authorization:** The system determines which resources the user can access.

⚠️ **Important:** Being authenticated does not automatically mean having permission to access every resource.

### 🔒 Least Privilege

The principle of least privilege means granting users, applications, and systems only the permissions necessary to perform their tasks.

📋 *Example:* A standard user should not need domain administrator privileges to read a document.

### 🛡️ Defense in Depth

Defense in depth uses multiple layers of security controls so that the failure of one control does not automatically compromise the entire system.

📋 *Example:* Combining firewalls, endpoint protection, multifactor authentication, network segmentation, and centralized logging.

### ⚠️ Threats, Vulnerabilities, Exploits, and Risk

These terms describe related but different security concepts.

- **Threat:** Something capable of causing harm, such as a malicious actor or a destructive event.
- **Vulnerability:** A weakness that could be exploited.
- **Exploit:** A technique or piece of code used to take advantage of a vulnerability.
- **Risk:** The potential for loss or harm, considering the likelihood and impact of an event.

📋 *Example:* An unpatched server contains a vulnerability. An attacker may use an exploit to compromise it, creating risks such as data theft or service disruption.

### 🚧 Security Controls

Security controls are measures used to reduce security risks. They can be classified by their purpose and function.

**By purpose:**
- **Preventive:** Attempt to stop an incident before it occurs.
- **Detective:** Identify or alert on suspicious activity.
- **Corrective:** Help restore systems or correct problems after an incident.
- **Deterrent:** Discourage unauthorized or harmful actions.
- **Compensating:** Provide an alternative when a preferred control cannot be implemented.

📋 *Examples:* A firewall can be preventive, an IDS can be detective, and restoring from a backup can be corrective.

### 🔐 Encryption, Hashing, and Encoding

These techniques transform data for different purposes and should not be confused.

- **Encryption:** Protects confidentiality by transforming data so that it can be recovered with the appropriate decryption key.
- **Hashing:** Produces a fixed-length digest used for purposes such as integrity verification. Secure password storage uses specialized password-hashing methods.
- **Encoding:** Changes the representation of data so that it can be stored or transmitted in a particular format. It does not inherently provide confidentiality.

📋 *Examples:* AES is an encryption algorithm, SHA-256 is a cryptographic hash function, and Base64 is an encoding scheme.

### 🗝️ Access Control

Access control determines who or what can access resources and which actions are permitted.

Common models include:

- **DAC (Discretionary Access Control):** Resource owners can determine access permissions.
- **MAC (Mandatory Access Control):** Access is governed by centrally defined policies, often using security labels.
- **RBAC (Role-Based Access Control):** Permissions are assigned to roles.
- **ABAC (Attribute-Based Access Control):** Access decisions use attributes such as user identity, resource, action, or environmental conditions.

### 🛡️ The Principle of Zero Trust

Zero Trust is a security approach based on the principle that access should not be granted solely because a user or device is inside a trusted network.

Key ideas include:
- Verify access requests explicitly.
- Apply least-privilege access.
- Assess and monitor access continuously where appropriate.

Zero Trust is an architectural approach, not a single product or tool.

### 🚨 Incident Response

Incident response is the structured process of handling suspected or confirmed security incidents.

Common phases include:
- **Preparation:** Establish procedures, tools, and responsibilities.
- **Detection and analysis:** Identify suspicious activity and determine its significance.
- **Containment:** Limit the incident's impact.
- **Eradication:** Remove the threat and its underlying cause.
- **Recovery:** Restore normal operations safely.
- **Lessons learned:** Review the incident and improve defenses.

Organizations may use different frameworks and phase names, but the overall goal is to manage incidents effectively and reduce future risk.

### 🔎 Indicators of Compromise (IOCs)

Indicators of Compromise are observable artifacts that may suggest malicious activity.

Examples include:
- Suspicious IP addresses or domain names
- File hashes associated with known malware
- Unusual processes or persistence mechanisms
- Unexpected authentication events

⚠️ **Important:** An IOC is a clue, not necessarily proof of compromise. Findings should be evaluated in context and corroborated with additional evidence.

### 🎯 Vulnerability Assessment and Penetration Testing

These activities have related but different objectives.

- **Vulnerability assessment:** Identifies and evaluates potential security weaknesses.
- **Penetration testing:** Uses authorized, controlled techniques to validate whether weaknesses can be exploited and assess their potential impact.

Both require a clearly defined scope and appropriate authorization.

### 🎭 Social Engineering

Social engineering manipulates people into revealing information, granting access, or performing actions that may compromise security.

Common examples include:
- **Phishing:** Fraudulent messages designed to deceive recipients.
- **Pretexting:** Using a fabricated scenario to gain trust or obtain information.
- **Impersonation:** Pretending to be a trusted person or organization.

Security awareness, verification procedures, and multifactor authentication can help reduce the risk.

## 🧰 Cybersecurity Tools

### 📡 Network Traffic Analysis — Wireshark

🎯 **Purpose:** Capture and inspect network packets to understand communications and investigate potential network issues or suspicious activity.

🧠 **Key concepts:**
- Packet capture and protocol analysis
- Source and destination IP addresses
- TCP and UDP communications
- Display filters
- DNS queries and TCP handshakes

📚 **Further study:** Learn to filter traffic efficiently, recognize normal communication patterns, and investigate unusual network activity.

### 💻 Command-Line Packet Analysis — tcpdump

🎯 **Purpose:** Capture and analyze network traffic directly from the command line.

🧠 **Key concepts:**
- Selecting a network interface
- Filtering traffic by host, port, or protocol
- Saving packet captures to PCAP files
- Reading packet captures
- Understanding capture filters

📚 **Further study:** Practice basic capture and filtering commands, then inspect saved captures with Wireshark.

### 🔎 Network Reconnaissance — Nmap

🎯 **Purpose:** Discover hosts, identify open ports, and gather information about network services.

🧠 **Key concepts:**
- Host discovery
- TCP and UDP port scanning
- Service and version detection
- Network mapping
- Interpreting scan results

⚠️ **Important:** An open port indicates an accessible service, not necessarily a vulnerability.

📚 **Further study:** Understand common scan options, service detection, and authorized scanning practices.

### 🔑 Password Auditing — John the Ripper

🎯 **Purpose:** Test password strength by attempting to recover passwords from password hashes.

🧠 **Key concepts:**
- Password hashes
- Dictionary attacks
- Wordlists
- Hash formats
- Password complexity and storage

⚠️ **Important:** A hash is not the same as a plaintext password. Results depend on the hash format, password strength, and available resources.

📚 **Further study:** Learn to identify hash formats and understand secure password storage practices.

### 🧨 Exploitation Framework — Metasploit

🎯 **Purpose:** Support authorized security testing through modules used to investigate and validate vulnerabilities, including exploitation when appropriate.

🧠 **Key concepts:**
- Modules and exploits
- Auxiliary modules
- Payloads
- Target configuration
- Sessions and post-exploitation modules

⚠️ **Important:** A successful exploit depends on factors such as the target configuration, vulnerability, payload, and network connectivity.

📚 **Further study:** Understand the role of each module type and practice only in authorized lab environments.

### 🌐 Web Development and Security — JavaScript

🎯 **Purpose:** A programming language widely used to implement interactive behavior in web browsers and, in other environments, server-side applications.

🧠 **Key concepts:**
- Client-side versus server-side code
- Variables, functions, and objects
- DOM manipulation
- User input and event handling
- Client-side validation

🛡️ **Security relevance:** Client-side controls can be modified or bypassed. Security-critical validation and access control must also be enforced server-side.

📚 **Further study:** Understand how JavaScript interacts with HTML, HTTP requests, and web application security.

### 🗄️ Database Language and Security — SQL

🎯 **Purpose:** Query and manipulate data in relational databases.

🧠 **Key concepts:**
- SELECT queries
- INSERT, UPDATE, and DELETE operations
- Tables, columns, and records
- WHERE conditions
- Database permissions and parameterized queries

🛡️ **Security relevance:** SQL injection can occur when an application incorporates untrusted input into database queries unsafely.

📚 **Further study:** Learn basic queries, understand how SQL injection works in authorized labs, and study prepared statements and least-privilege database access.

### 🕸️ Web Application Testing — Burp Suite

🎯 **Purpose:** Inspect and test HTTP/S communications between a browser and a web application.

🧠 **Key concepts:**
- HTTP requests and responses
- Proxying and intercepting traffic
- Repeater for manually testing requests
- Request parameters, cookies, and headers
- Web application behavior

📚 **Further study:** Practice inspecting requests and responses, then investigate common web vulnerabilities in authorized labs.

### 🔐 Network Authentication Testing — Hydra

🎯 **Purpose:** Test authentication security by attempting multiple login combinations against supported network services.

🧠 **Key concepts:**
- Authentication protocols and services
- Username and password lists
- Login attempts and responses
- Account lockout and rate limiting
- Strong passwords and multifactor authentication

⚠️ **Security note:** Use authentication-testing tools only against systems for which explicit authorization has been granted. Uncontrolled attempts can disrupt services or lock accounts.

📚 **Further study:** Understand how weak credentials and inadequate authentication protections create risk, and how defenders can detect repeated login failures.

### 🧭 Web Content Discovery — Gobuster

🎯 **Purpose:** Discover potentially accessible directories, files, DNS subdomains, or virtual hosts, depending on the selected mode.

🧠 **Key concepts:**
- Wordlists
- Directory and file discovery
- HTTP response codes
- DNS enumeration
- Interpreting discovered paths

⚠️ **Important:** A discovered path or subdomain is a lead for further investigation, not proof of a vulnerability.

📚 **Further study:** Learn the different modes and how to interpret results without assuming every response is meaningful.

### 🛠️ SQL Injection Testing — sqlmap

🎯 **Purpose:** Automate the detection and testing of SQL injection vulnerabilities in web applications.

🧠 **Key concepts:**
- HTTP parameters and requests
- SQL injection indicators
- Supported database types
- Testing options and output interpretation
- The importance of manual validation

⚠️ **Important:** Automated results need careful interpretation. Use sqlmap only against authorized targets and controlled lab environments.

📚 **Further study:** Understand the underlying SQL injection concepts before relying on automated testing, and learn how parameterized queries help prevent these vulnerabilities.

### 📊 Security Monitoring — Logs and SIEM

🎯 **Purpose:** Collect, centralize, correlate, and analyze security-relevant events to identify suspicious activity and support investigations.

🧠 **Key concepts:**
- System, application, and authentication logs
- Event timestamps and source information
- Event correlation
- Alerts and detection rules
- Security incident triage

📚 **Further study:** Learn to identify relevant events, distinguish normal behavior from suspicious patterns, and investigate alerts using supporting evidence.

### 🚨 Intrusion Detection — IDS and Snort

🎯 **Purpose:** An Intrusion Detection System (IDS) monitors network or system activity to identify suspicious behavior. Snort is a tool that can perform network intrusion detection and traffic analysis.

🧠 **Key concepts:**
- Network-based intrusion detection
- Rules and signatures
- Packet inspection
- Alerts and false positives
- IDS versus IPS

⚠️ **Important:** An IDS typically detects and alerts; an IPS can also take action to block or prevent traffic, depending on its configuration.

📚 **Further study:** Understand how Snort rules work, inspect alerts, and learn the limitations of signature-based detection.

### 🧪 Data Analysis and Transformation — CyberChef

🎯 **Purpose:** Transform, decode, encode, and analyze data using configurable operations called recipes.

🧠 **Key concepts:**
- Base64 decoding
- URL decoding
- Hexadecimal conversion
- Data extraction and transformation
- Chaining operations into recipes

⚠️ **Important:** Encoding is not encryption. Encoded data is not necessarily confidential.

Avoid submitting sensitive or confidential data to online tools unless the environment and data-handling policy explicitly allow it.

📚 **Further study:** Practice recognizing common data formats and combining operations to investigate unfamiliar strings or artifacts.

### 🦠 Malware Analysis — capa

🎯 **Purpose:** Identify capabilities that may be present in executable files by analyzing patterns associated with known behaviors.

🧠 **Key concepts:**
- Static analysis
- Capability identification
- Rules and behavioral indicators
- Recognizing potentially suspicious functionality
- Interpreting analysis results

⚠️ **Important:** capa findings indicate capabilities suggested by the analysis; they do not, on their own, prove that a file is malicious.

📚 **Further study:** Learn how to interpret reports and combine capability findings with other evidence during malware analysis.

### 🐧 Malware Analysis Environment — REMnux

🎯 **Purpose:** A Linux-based toolkit and environment designed to support malware analysis, reverse engineering, and digital forensics.

🧠 **Key concepts:**
- Malware investigation utilities
- Static and dynamic analysis workflows
- File and artifact examination
- Network artifact analysis
- Safe analysis practices

📚 **Further study:** Become familiar with the available tools and learn how to examine suspicious files and artifacts in an isolated environment.

### 🪟 Malware Analysis Environment — FLARE-VM

🎯 **Purpose:** A Windows-based environment that provides a collection of tools for malware analysis, reverse engineering, and digital forensics.

🧠 **Key concepts:**
- Windows-based analysis tools
- Static and dynamic malware analysis
- Debugging and reverse engineering
- Examining executable files
- Isolated lab environments

⚠️ **Important:** Suspicious files must be handled carefully. Use appropriate isolation and lab safety measures to reduce the risk of accidental execution or system compromise.

📚 **Further study:** Explore the tools included in the environment and understand when Windows-based analysis is useful alongside Linux-based tools such as REMnux.

# Cybersecurity Fundamentals

## Overview

This document summarizes the cybersecurity tools, technologies, programming languages, and analysis environments introduced during my initial hands-on learning through TryHackMe and other training resources.

The goal is to build a structured reference, reinforce fundamental concepts, and identify topics that require further practice.

These notes represent an ongoing learning process, not a claim of mastery.

## 1. Network Traffic Analysis — Wireshark

**Purpose:** Capture and inspect network packets to understand communications and investigate potential network issues or suspicious activity.

**Key concepts:**
- Packet capture and protocol analysis
- Source and destination IP addresses
- TCP and UDP communications
- Display filters
- DNS queries and TCP handshakes

**Further study:** Learn to filter traffic efficiently, recognize normal communication patterns, and investigate unusual network activity.

## 2. Command-Line Packet Analysis — tcpdump

**Purpose:** Capture and analyze network traffic directly from the command line.

**Key concepts:**
- Selecting a network interface
- Filtering traffic by host, port, or protocol
- Saving packet captures to PCAP files
- Reading packet captures
- Understanding capture filters

**Further study:** Practice basic capture and filtering commands, then inspect saved captures with Wireshark.

## 3. Network Reconnaissance — Nmap

**Purpose:** Discover hosts, identify open ports, and gather information about network services.

**Key concepts:**
- Host discovery
- TCP and UDP port scanning
- Service and version detection
- Network mapping
- Interpreting scan results

**Important:** An open port indicates an accessible service, not necessarily a vulnerability.

**Further study:** Understand common scan options, service detection, and authorized scanning practices.

## 4. Password Auditing — John the Ripper

**Purpose:** Test password strength by attempting to recover passwords from password hashes.

**Key concepts:**
- Password hashes
- Dictionary attacks
- Wordlists
- Hash formats
- Password complexity and storage

**Important:** A hash is not the same as a plaintext password. Results depend on the hash format, password strength, and available resources.

**Further study:** Learn to identify hash formats and understand secure password storage practices.

## 5. Exploitation Framework — Metasploit

**Purpose:** Support authorized security testing through modules used to investigate and validate vulnerabilities, including exploitation when appropriate.

**Key concepts:**
- Modules and exploits
- Auxiliary modules
- Payloads
- Target configuration
- Sessions and post-exploitation modules

**Important:** A successful exploit depends on factors such as the target configuration, vulnerability, payload, and network connectivity.

**Further study:** Understand the role of each module type and practice only in authorized lab environments.

## 6. Web Development and Security — JavaScript

**Purpose:** A programming language widely used to implement interactive behavior in web browsers and, in other environments, server-side applications.

**Key concepts:**
- Client-side versus server-side code
- Variables, functions, and objects
- DOM manipulation
- User input and event handling
- Client-side validation

**Security relevance:** Client-side controls can be modified or bypassed. Security-critical validation and access control must also be enforced server-side.

**Further study:** Understand how JavaScript interacts with HTML, HTTP requests, and web application security.

## 7. Database Language and Security — SQL

**Purpose:** Query and manipulate data in relational databases.

**Key concepts:**
- SELECT queries
- INSERT, UPDATE, and DELETE operations
- Tables, columns, and records
- WHERE conditions
- Database permissions and parameterized queries

**Security relevance:** SQL injection can occur when an application incorporates untrusted input into database queries unsafely.

**Further study:** Learn basic queries, understand how SQL injection works in authorized labs, and study prepared statements and least-privilege database access.

## 8. Web Application Testing — Burp Suite

**Purpose:** Inspect and test HTTP/S communications between a browser and a web application.

**Key concepts:**
- HTTP requests and responses
- Proxying and intercepting traffic
- Repeater for manually testing requests
- Request parameters, cookies, and headers
- Web application behavior

**Further study:** Practice inspecting requests and responses, then investigate common web vulnerabilities in authorized labs.

## 9. Network Authentication Testing — Hydra

**Purpose:** Test authentication security by attempting multiple login combinations against supported network services.

**Key concepts:**
- Authentication protocols and services
- Username and password lists
- Login attempts and responses
- Account lockout and rate limiting
- Strong passwords and multifactor authentication

**Security note:** Use authentication-testing tools only against systems for which explicit authorization has been granted. Uncontrolled attempts can disrupt services or lock accounts.

**Further study:** Understand how weak credentials and inadequate authentication protections create risk, and how defenders can detect repeated login failures.

## 10. Web Content Discovery — Gobuster

**Purpose:** Discover potentially accessible directories, files, DNS subdomains, or virtual hosts, depending on the selected mode.

**Key concepts:**
- Wordlists
- Directory and file discovery
- HTTP response codes
- DNS enumeration
- Interpreting discovered paths

**Important:** A discovered path or subdomain is a lead for further investigation, not proof of a vulnerability.

**Further study:** Learn the different modes and how to interpret results without assuming every response is meaningful.

## 11. SQL Injection Testing — sqlmap

**Purpose:** Automate the detection and testing of SQL injection vulnerabilities in web applications.

**Key concepts:**
- HTTP parameters and requests
- SQL injection indicators
- Supported database types
- Testing options and output interpretation
- The importance of manual validation

**Important:** Automated results need careful interpretation. Use sqlmap only against authorized targets and controlled lab environments.

**Further study:** Understand the underlying SQL injection concepts before relying on automated testing, and learn how parameterized queries help prevent these vulnerabilities.

## 12. Security Monitoring — Logs and SIEM

**Purpose:** Collect, centralize, correlate, and analyze security-relevant events to identify suspicious activity and support investigations.

**Key concepts:**
- System, application, and authentication logs
- Event timestamps and source information
- Event correlation
- Alerts and detection rules
- Security incident triage

**Further study:** Learn to identify relevant events, distinguish normal behavior from suspicious patterns, and investigate alerts using supporting evidence.

## 13. Intrusion Detection — IDS and Snort

**Purpose:** An Intrusion Detection System (IDS) monitors network or system activity to identify suspicious behavior. Snort is a tool that can perform network intrusion detection and traffic analysis.

**Key concepts:**
- Network-based intrusion detection
- Rules and signatures
- Packet inspection
- Alerts and false positives
- IDS versus IPS

**Important:** An IDS typically detects and alerts; an IPS can also take action to block or prevent traffic, depending on its configuration.

**Further study:** Understand how Snort rules work, inspect alerts, and learn the limitations of signature-based detection.

## 14. Data Analysis and Transformation — CyberChef

**Purpose:** Transform, decode, encode, and analyze data using configurable operations called recipes.

**Key concepts:**
- Base64 decoding
- URL decoding
- Hexadecimal conversion
- Data extraction and transformation
- Chaining operations into recipes

**Important:** Encoding is not encryption. Encoded data is not necessarily confidential.

Avoid submitting sensitive or confidential data to online tools unless the environment and data-handling policy explicitly allow it.

**Further study:** Practice recognizing common data formats and combining operations to investigate unfamiliar strings or artifacts.

## 15. Malware Analysis — capa

**Purpose:** Identify capabilities that may be present in executable files by analyzing patterns associated with known behaviors.

**Key concepts:**
- Static analysis
- Capability identification
- Rules and behavioral indicators
- Recognizing potentially suspicious functionality
- Interpreting analysis results

**Important:** capa findings indicate capabilities suggested by the analysis; they do not, on their own, prove that a file is malicious.

**Further study:** Learn how to interpret reports and combine capability findings with other evidence during malware analysis.

## 16. Malware Analysis Environment — REMnux

**Purpose:** A Linux-based toolkit and environment designed to support malware analysis, reverse engineering, and digital forensics.

**Key concepts:**
- Malware investigation utilities
- Static and dynamic analysis workflows
- File and artifact examination
- Network artifact analysis
- Safe analysis practices

**Further study:** Become familiar with the available tools and learn how to examine suspicious files and artifacts in an isolated environment.

## 17. Malware Analysis Environment — FLARE-VM

**Purpose:** A Windows-based environment that provides a collection of tools for malware analysis, reverse engineering, and digital forensics.

**Key concepts:**
- Windows-based analysis tools
- Static and dynamic malware analysis
- Debugging and reverse engineering
- Examining executable files
- Isolated lab environments

**Important:** Suspicious files must be handled carefully. Use appropriate isolation and lab safety measures to reduce the risk of accidental execution or system compromise.

**Further study:** Explore the tools included in the environment and understand when Windows-based analysis is useful alongside Linux-based tools such as REMnux.

## 18. Core Concepts to Revisit

- **Reconnaissance:** Gather information about authorized targets before further testing.
- **Network analysis:** Inspect packets and protocols to understand communications.
- **Authentication security:** Identify weak credentials and inadequate protections.
- **Web application security:** Understand requests, responses, input validation, and common vulnerabilities.
- **Detection and monitoring:** Use logs, SIEM platforms, and IDS alerts to investigate suspicious activity.
- **Malware analysis:** Examine files and artifacts to understand their potential capabilities and behavior.
- **Evidence-based conclusions:** Validate findings instead of assuming that every scan result or alert proves a security issue.


## 19. Planned Improvements

As my skills develop, I intend to:
- Add practical examples and explanations of selected commands.
- Create dedicated pages for individual tools and technologies.
- Document lessons learned from authorized labs.
- Include references to official documentation.
- Record common mistakes and troubleshooting techniques.
- Add sanitized screenshots or sample outputs where useful.
- Develop detailed lab write-ups for selected portfolio projects.
- Review and update these notes as my understanding improves.

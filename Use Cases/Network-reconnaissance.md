# 🛡️ Network Reconnaissance

## 📘 Overview

**Network Reconnaissance** is the process of gathering information about a network, its hosts, exposed services, and potential entry points.

It is often an early phase of a penetration test or security assessment. The goal is to understand the target environment before deciding which systems or services require further investigation.

Reconnaissance can be performed using passive techniques, which gather information without directly probing the target, or active techniques, which send traffic to discover hosts and services.

## 🎯 Objective

- Discover hosts that are reachable within an authorized network scope.
- Identify open ports and exposed services.
- Determine which protocols and service versions are in use.
- Identify potentially unnecessary or unexpected network exposure.
- Map the attack surface for a security assessment.
- Gather evidence to prioritize further investigation.
- Document findings in a clear and reproducible way.

## 🧠 Key Concepts

- **Reconnaissance:** Collecting information about a target before deeper investigation or testing.
- **Passive reconnaissance:** Gathering information without directly probing the target systems, for example by reviewing public documentation or existing records.
- **Active reconnaissance:** Sending traffic to a target to discover hosts, ports, services, or other characteristics.
- **Host discovery:** Identifying systems that appear reachable on a network.
- **Port scanning:** Checking ports to determine their observed state.
- **Open port:** A port on which a service is listening and accepting connections.
- **Closed port:** A port that is reachable, but no service is listening on it.
- **Filtered port:** A scanner cannot reliably determine whether a port is open or closed, often because a firewall or other network control interferes with the probes.
- **Service detection:** Identifying the application or service associated with an open port.
- **Version detection:** Attempting to identify the version of a detected service.
- **Attack surface:** The systems, services, applications, and interfaces that could potentially be targeted.
- **Enumeration:** Collecting more detailed information about discovered services, resources, or accounts.
- **False positive / false negative:** A system or service may be incorrectly identified or missed due to network conditions, filtering, or scanner limitations.
- **Scope:** The systems and addresses explicitly authorized for assessment.

## 🛠️ Tools Used

- **Nmap:** Discovers hosts, scans ports, and attempts to identify services and versions.
- **Gobuster:** Enumerates web directories, files, virtual hosts, or DNS names using wordlists, depending on the selected mode.
- **Wireshark:** Inspects the packets generated during reconnaissance and helps explain network responses.
- **tcpdump:** Captures traffic from the command line for later inspection.
- **CyberChef:** Helps decode or transform collected text and data when required.

Nmap is the primary tool in this workflow. Gobuster is useful when a discovered web service needs further authorized enumeration. Wireshark and tcpdump help analyze the traffic and responses.

## 🔎 Workflow

### Define the scope

Identify the IP addresses, hostnames, and network ranges that are authorized for testing.

Confirm any restrictions, such as prohibited ports, rate limits, or systems that must not be scanned.

### Discover reachable hosts

Use an appropriate discovery method to identify systems that appear reachable.

Example:

`nmap -sn 192.168.1.0/24`

This performs host discovery across the specified subnet without conducting a conventional port scan.

A host may still be online even if it does not respond to the discovery probes, so discovery results are not always complete.

### Scan ports

Scan the authorized target to identify accessible TCP ports.

Example:

`nmap -sS 192.168.1.10`

This performs a TCP SYN scan. It generally requires appropriate privileges and may not work as expected on every operating system or network.

For a basic TCP connect scan, another option is:

`nmap -sT 192.168.1.10`

### Identify services and versions

Once open ports have been identified, attempt to determine which services are running.

Example:

`nmap -sV 192.168.1.10`

Service detection probes the discovered ports to identify the applications and potentially their versions.

### Review the exposure

Compare the discovered services with the expected configuration.

For example, an organization may expect a server to expose HTTPS but discover an additional remote administration service.

An unexpected service is a reason to investigate, not automatically proof of a vulnerability.

### Enumerate web resources when relevant

If an authorized target exposes a web server, Gobuster can help discover paths that are not linked from the main page.

Example:

`gobuster dir -u http://192.168.1.10 -w /path/to/wordlist.txt`

This attempts to discover web paths using the specified wordlist. Replace the target and wordlist path with values appropriate for the authorized lab.

### Document the findings

Record the target, scan options, date and time, discovered hosts, port states, services, and observations.

Identify uncertainties and recommend further investigation where evidence is incomplete.

## 📋 Practical Examples

### Example 1 — Mapping a small network

An analyst is authorized to assess a laboratory subnet.

They perform host discovery, identify reachable systems, and then scan the relevant hosts for open ports.

**Goal:** Build an initial inventory of reachable systems and exposed services.

### Example 2 — Finding an unexpected service

A server is expected to provide HTTPS on TCP port 443.

Nmap also reports another open port associated with a remote administration service.

The analyst checks the service identity, confirms whether the exposure is expected, and consults the system owner before recommending changes.

**Goal:** Identify and validate unnecessary or unexpected exposure.

### Example 3 — Enumerating a web server

An authorized assessment identifies a web server.

The analyst uses Gobuster with an appropriate wordlist to discover additional paths, then manually reviews relevant results to determine whether they expose sensitive or unintended resources.

**Goal:** Understand the application's accessible attack surface without assuming that every discovered path is vulnerable.

### Example 4 — Understanding an ambiguous scan result

Nmap reports a port as filtered.

The analyst reviews the scan context and, if authorized, examines packet responses with Wireshark or tcpdump.

A firewall, packet filtering, routing behavior, or lack of a response may explain the result.

**Goal:** Understand the limits of the scan rather than treating filtered as equivalent to closed.

## ⚠️ Important

- Only scan systems and networks for which you have explicit authorization.
- Active reconnaissance generates network traffic and may trigger security alerts.
- A scan can miss hosts or services because of firewalls, routing, rate limiting, or the selected scan options.
- An open port does not automatically mean that a service is vulnerable.
- Service-version detection is an estimate and may not identify the exact software version correctly.
- An unfamiliar service should be investigated in context before being classified as a security issue.
- Gobuster results may include false positives caused by wildcard responses, generic error pages, or application routing behavior.
- Start with the least intrusive method that meets the assessment objective, and follow the agreed scope and testing rules.
- Keep records of scan options and timestamps so findings can be reproduced and compared.

## 📚 References

- Nmap official documentation: https://nmap.org/book/man.html
- Nmap reference guide: https://nmap.org/book/man-briefoptions.html
- Gobuster GitHub repository: https://github.com/OJ/gobuster
- Wireshark documentation: https://www.wireshark.org/docs/
- tcpdump manual: https://www.tcpdump.org/manpages/tcpdump.1.html

## 🔗 Related Repository Files

- `nmap.md`
- `gobuster.md`
- `wireshark.md`
- `tcpdump.md`
- `network-traffic-analysis.md`

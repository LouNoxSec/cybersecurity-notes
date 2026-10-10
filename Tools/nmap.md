# 🛡️ Nmap

## 📘 Overview

Nmap (Network Mapper) is an open-source network discovery and security auditing tool. It is used to identify hosts, discover open ports, detect services, and gather information about network systems.

## 🎯 Purpose

- Discover hosts on a network.
- Identify open, closed, and filtered ports.
- Detect running services and their versions.
- Identify potential attack surfaces.
- Support network troubleshooting and authorized security assessments.

## 🧠 Key Concepts

- **Host discovery:** Determines which systems appear reachable on a network.
- **Port scanning:** Checks the state of ports on a target host.
- **Service detection:** Attempts to identify the service listening on a port.
- **OS detection:** Estimates the target operating system using network responses.
- **Open port:** A service is listening and accepting connections.
- **Closed port:** The host responds, but no service is listening.
- **Filtered port:** A firewall or other filtering mechanism prevents Nmap from determining whether the port is open.
- **Target:** The host, IP address, or network being scanned.
- **NSE (Nmap Scripting Engine):** Extends Nmap with scripts for discovery, detection, and other assessment tasks.

## 💻 Commands / Operations

**Scan a single host**

`nmap 192.168.1.10`

Performs a default scan against the specified host.

**Scan the local machine**

`nmap 127.0.0.1`

Scans the loopback address of the machine running Nmap.

**Discover hosts on a subnet**

`nmap -sn 192.168.1.0/24`

Performs host discovery without a port scan. The results depend on network conditions and discovery methods.

**Scan specific ports**

`nmap -p 22,80,443 192.168.1.10`

Checks the specified ports, commonly associated with SSH, HTTP, and HTTPS.

**Scan a range of ports**

`nmap -p 1-1000 192.168.1.10`

Scans ports 1 through 1000.

**Scan all TCP ports**

`nmap -p- 192.168.1.10`

Scans all 65,535 TCP ports.

**Detect service versions**

`nmap -sV 192.168.1.10`

Attempts to identify the services and versions running on discovered ports.

**Detect the operating system**

`sudo nmap -O 192.168.1.10`

Attempts to identify the target operating system. Results are estimates and may require suitable privileges and network responses.

**Perform a TCP SYN scan**

`sudo nmap -sS 192.168.1.10`

Uses TCP SYN probing. This scan commonly requires elevated privileges.

**Save scan results to a text file**

`nmap -oN scan-results.txt 192.168.1.10`

Saves the output in normal text format.

## 📋 Practical Examples

**Example 1 — Identify exposed services**

Run `nmap -sV 192.168.1.10` against an authorized lab host.

If ports 22 and 80 are open, investigate whether SSH and a web service are expected on that system.

**Example 2 — Investigate an unexpected port**

Run `nmap -p 8080 -sV 192.168.1.10`.

If port 8080 is open, determine which service is listening and whether it should be accessible.

**Example 3 — Map a lab subnet**

Run `nmap -sn 192.168.1.0/24`.

Review the discovered hosts and compare them with the expected devices in the lab.

## 🔎 Investigation

When reviewing scan results, ask:

- Which hosts appear reachable?
- Which ports are open, closed, or filtered?
- Which services and versions have been identified?
- Are any unnecessary services exposed?
- Could a detected service version be affected by a known vulnerability?
- Are firewall rules behaving as expected?

A discovered service can help identify a potential risk, but additional verification is needed before concluding that a vulnerability exists.

## ⚠️ Important

- Only scan systems and networks for which you have explicit authorization.
- Nmap results depend on routing, firewalls, packet filtering, and target availability.
- A host that appears down may still be active but blocking discovery probes.
- An open port does not automatically mean that the service is vulnerable.
- Service and OS detection provide estimates, not guaranteed identification.
- Aggressive scans and scripts may generate significant traffic or affect fragile systems.
- Use the least intrusive scan appropriate for the investigation.

## 📚 References

- Official website: https://nmap.org/
- Official reference guide: https://nmap.org/book/man.html
- Nmap Scripting Engine: https://nmap.org/book/nse.html

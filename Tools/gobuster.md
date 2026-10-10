# 🛡️ Gobuster

## 📘 Overview

Gobuster is an open-source command-line tool used for discovering hidden resources on web servers and identifying certain types of infrastructure exposed through network services.

It is commonly used during authorized web application assessments and capture-the-flag (CTF) exercises.

## 🎯 Purpose

- Discover directories and files that are not linked from a website.
- Identify hidden web application endpoints.
- Discover virtual hosts configured on a web server.
- Enumerate DNS subdomains in supported modes.
- Identify potential areas requiring further investigation.

## 🧠 Key Concepts

- **Enumeration:** Systematically discovering resources and services.
- **Directory enumeration:** Searching for directories and paths on a web server.
- **Wordlist:** A list of candidate names used during discovery.
- **HTTP status code:** Indicates the result of an HTTP request.
- **Virtual host (vhost):** A hostname served by a web server, potentially sharing an IP address with other sites.
- **Subdomain:** A domain beneath another domain, such as `dev.example.com`.
- **False positive:** A result that appears meaningful but does not correspond to a real resource.
- **Gobuster mode:** Determines the type of enumeration performed, such as directory, DNS, or virtual-host discovery.

## 💻 Commands / Operations

Gobuster is a command-line tool. Its syntax depends on the mode being used.

**Display help**

`gobuster --help`

Displays the available modes and general options.

**Display help for directory enumeration**

`gobuster dir --help`

Displays options available for directory and file discovery.

**Directory and file enumeration**

`gobuster dir -u http://TARGET -w /path/to/wordlist.txt`

Tests candidate paths from the wordlist against the specified web server. Replace `TARGET` and the wordlist path with values appropriate for an authorized lab.

**Specify file extensions**

`gobuster dir -u http://TARGET -w /path/to/wordlist.txt -x php,html,txt`

Tests candidate paths with the specified extensions as well.

**Virtual-host enumeration**

`gobuster vhost -u http://TARGET -w /path/to/vhosts.txt`

Tests candidate hostnames against the specified web server.

**DNS subdomain enumeration**

`gobuster dns -d example.com -w /path/to/subdomains.txt`

Tests candidate subdomains against the specified domain. Use only domains within your authorized assessment scope.

## 📋 Practical Examples

**Example 1 — Discover hidden directories**

A web server exposes a homepage but provides few visible links.

Gobuster tests candidate paths and may discover resources such as `/admin` or `/backup`. Each result must be checked to determine whether the resource actually exists and is accessible.

**Example 2 — Investigate HTTP responses**

A candidate path returns status code `403 Forbidden`.

This may indicate that access is restricted, but it does not prove that the resource exists in every server configuration. Compare the response with known valid and invalid paths.

**Example 3 — Discover virtual hosts**

A lab server hosts several websites on the same IP address.

Virtual-host enumeration can reveal additional hostnames that are not obvious from the main website.

## 🔎 Investigation

When reviewing Gobuster results, examine:

- Discovered paths and hostnames.
- HTTP response codes.
- Response sizes and redirects.
- Differences between valid and invalid paths.
- Whether resources expose sensitive information.
- Whether discovered endpoints require authentication.
- Whether the results are genuine resources or false positives.

**Useful investigation question:** Does the discovered resource expose functionality or information that should not be publicly accessible?

## ⚠️ Important

- Gobuster discovers potential resources; it does not automatically prove that they are vulnerable.
- A `200 OK` response does not guarantee that a valid resource exists, as some applications return the same page for unknown paths.
- A `403 Forbidden` response may indicate access restrictions rather than a vulnerability.
- Wordlist quality strongly affects the results.
- Large wordlists can generate significant traffic and trigger security monitoring.
- Follow the defined scope and obtain explicit authorization before enumerating websites, domains, or virtual hosts.
- Do not access, modify, or download sensitive resources without permission.

## 📚 References

- Official GitHub repository: https://github.com/OJ/gobuster
- Kali Linux tool documentation: https://www.kali.org/tools/gobuster/

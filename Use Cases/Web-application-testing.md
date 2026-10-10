# 🛡️ Web Application Testing

## 📘 Overview

**Web Application Testing** is the process of evaluating a web application's security by examining its behavior, inputs, authentication mechanisms, access controls, and interactions with the server.

Security professionals perform authorized tests to identify weaknesses such as injection vulnerabilities, broken access controls, insecure session management, and unintended information disclosure.

Testing can be performed manually, with automated tools, or through a combination of both.

The objective is not simply to find vulnerabilities, but to understand their impact, validate the evidence, and recommend appropriate remediation.

## 🎯 Objective

- Understand how a web application communicates with its server.
- Inspect HTTP requests and responses.
- Identify exposed resources and unexpected application behavior.
- Test input handling and potential injection vulnerabilities.
- Evaluate authentication, sessions, and access controls.
- Validate findings while minimizing impact on the application.
- Document vulnerabilities and recommend remediation.

## 🧠 Key Concepts

- **Client-server architecture:** The browser sends requests to a server, which returns responses.
- **HTTP:** The protocol used to exchange requests and responses between clients and web servers.
- **HTTPS:** HTTP protected by TLS encryption during transport.
- **Request:** A message sent by a client, containing elements such as a method, URL, headers, and potentially a body.
- **Response:** A server's reply, including a status code, headers, and potentially a body.
- **HTTP methods:** Methods such as GET, POST, PUT, and DELETE describe the intended operation.
- **Status code:** A number indicating the outcome or nature of an HTTP response, such as 200, 403, or 404.
- **Cookie:** Data stored by a browser and sent with applicable requests; cookies are often used for session management.
- **Session:** A mechanism for maintaining state across multiple requests.
- **Authentication:** Verifying a user's identity.
- **Authorization:** Determining what an authenticated user is allowed to access or do.
- **Input validation:** Checking that user-supplied data meets expected requirements.
- **SQL injection (SQLi):** A vulnerability in which untrusted input affects the structure of a database query.
- **Cross-site scripting (XSS):** A vulnerability that allows attacker-controlled script content to execute in a victim's browser.
- **Broken access control:** A weakness that allows users to perform actions or access resources beyond their permissions.
- **Directory and content enumeration:** Discovering web paths or resources that may not be directly linked from the application's interface.
- **False positive:** A reported issue that is not a genuine vulnerability in the tested context.
- **Scope:** The applications, accounts, endpoints, and testing techniques explicitly authorized for assessment.

## 🛠️ Tools Used

- **Burp Suite:** Intercepts and inspects HTTP requests and responses, supports manual testing, and helps investigate application behavior.
- **Gobuster:** Enumerates web directories, files, or virtual hosts using wordlists.
- **sqlmap:** Automates the detection and testing of SQL injection vulnerabilities.
- **JavaScript:** Helps analysts understand client-side application behavior and identify how browser-side code handles data.
- **SQL:** Helps analysts understand database queries and the conditions that can lead to SQL injection.
- **Wireshark:** Can help inspect network-level communication, although HTTPS payloads are generally encrypted unless suitable decryption is available.

Each tool has a distinct role. Burp Suite is useful for observing and modifying requests, Gobuster discovers paths, and sqlmap focuses on SQL injection testing. JavaScript and SQL knowledge help explain what is happening behind the interface.

## 🔎 Workflow

### Define the scope

Identify the target application, permitted endpoints, test accounts, and allowed techniques.

Confirm whether automated scanning, authenticated testing, and potentially disruptive tests are permitted.

### Map the application

Browse the application normally and identify:

- Main pages and endpoints.
- Login and logout functions.
- Forms and user-controlled inputs.
- URL parameters and API requests.
- Features involving files, search, or database-backed content.
- Different roles and permission levels.

Burp Suite can help capture and organize the requests generated during this process.

### Inspect HTTP requests and responses

Use Burp Suite Proxy and HTTP history to examine requests and their corresponding responses.

Review the request method, path, headers, parameters, cookies, response status, and returned content.

Compare requests from different roles or application states to understand how the application behaves.

### Enumerate accessible resources

If authorized and relevant, use Gobuster to identify additional paths.

Example:

`gobuster dir -u https://app.example.test -w /path/to/wordlist.txt`

This tests paths from the supplied wordlist against the specified application. Replace the example hostname and wordlist path with those provided by the authorized lab.

Review the results manually. A discovered path is not necessarily sensitive or vulnerable.

### Test input handling

Identify inputs that influence server-side operations, including search fields, URL parameters, and form submissions.

Determine whether the application validates inputs correctly and whether unexpected input changes the response.

Use safe test values and controlled cases first. Avoid destructive payloads or actions unless they are explicitly authorized.

### Investigate potential SQL injection

If evidence suggests that user input may influence a database query, investigate the behavior carefully.

sqlmap can assist with authorized SQL injection testing against a defined target.

Example help command:

`sqlmap -h`

This displays available options. Target-specific commands should be selected according to the lab instructions and the scope of authorization.

### Evaluate access controls

Where test accounts with different roles are provided, compare what each account can access and modify.

Check whether the server enforces permissions rather than relying only on hidden buttons or client-side JavaScript.

Do not access real users' data or change sensitive records during testing.

### Validate and document findings

For each suspected issue, record the affected endpoint, relevant request and response, expected behavior, observed behavior, impact, and reproducible evidence.

Recommend remediation and retest the issue after a fix is applied.

## 📋 Practical Examples

### Example 1 — Inspecting a login request

An analyst signs in using a designated test account and observes the HTTP request in Burp Suite.

They inspect the request method, submitted fields, cookies, and response behavior.

**Goal:** Understand the authentication flow and identify areas that require further authorized testing.

### Example 2 — Discovering an unlinked resource

Gobuster identifies a path that is not linked from the application's main page.

The analyst opens the path using an authorized test account and determines whether it is a legitimate public resource, an administrative endpoint, or an improperly exposed page.

**Goal:** Determine whether the resource is intended to be accessible and whether access controls are correctly enforced.

### Example 3 — Investigating possible SQL injection

A search parameter produces noticeably different application responses when safe test inputs are changed.

The analyst captures the requests in Burp Suite and evaluates whether the behavior is consistent with an input-handling issue.

If permitted by the assessment scope, sqlmap can help validate whether the parameter is vulnerable to SQL injection.

**Goal:** Confirm the issue with minimal impact and collect evidence sufficient for a report.

### Example 4 — Testing access control

Two authorized test accounts have different permissions.

The analyst compares their requests to determine whether a lower-privileged account can access a resource reserved for a higher-privileged role.

**Goal:** Identify broken access control while avoiding unauthorized access to real users' information.

### Example 5 — Understanding client-side validation

A form rejects an invalid value in the browser.

The analyst examines the JavaScript and sends a controlled test request to determine whether the server independently validates the same requirement.

**Goal:** Verify that security controls are enforced server-side rather than relying exclusively on browser-side checks.

## ⚠️ Important

- Perform testing only on applications and systems for which you have explicit authorization.
- HTTPS encrypts traffic in transit, but an authorized interception proxy can inspect traffic when the test environment and browser are configured to trust its certificate. Never bypass certificate protections on systems you do not control.
- Client-side validation is useful for usability but cannot replace server-side validation.
- A hidden URL or an inaccessible interface element is not a substitute for proper authorization checks.
- Automated tools can generate substantial traffic and may alter data or affect application availability.
- sqlmap should only be used against targets and techniques explicitly permitted by the test scope.
- A tool's output is evidence to evaluate, not automatic proof of a vulnerability.
- Minimize access to sensitive data, avoid destructive operations, and preserve reproducible evidence.
- Follow responsible disclosure and the organization's reporting requirements.

## 📚 References

- OWASP Web Security Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
- OWASP Top 10: https://owasp.org/www-project-top-ten/
- PortSwigger Web Security Academy: https://portswigger.net/web-security
- Burp Suite documentation: https://portswigger.net/burp/documentation
- Gobuster GitHub repository: https://github.com/OJ/gobuster
- sqlmap official documentation: https://github.com/sqlmapproject/sqlmap/wiki
- MDN Web Docs — HTTP: https://developer.mozilla.org/en-US/docs/Web/HTTP
- MDN Web Docs — JavaScript: https://developer.mozilla.org/en-US/docs/Web/JavaScript

## 🔗 Related Repository Files

- `burp-suite.md`
- `gobuster.md`
- `sqlmap.md`
- `network-reconnaissance.md`
- `network-traffic-analysis.md`
- `cyberchef.md`

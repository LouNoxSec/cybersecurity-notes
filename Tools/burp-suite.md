# 🛡️ Burp Suite

## 📘 Overview

Burp Suite is a web application security testing platform developed by PortSwigger. It allows security professionals to intercept, inspect, modify, and replay HTTP and HTTPS requests to assess web application security.

It is commonly used during web penetration tests and vulnerability assessments.

## 🎯 Purpose

- Inspect communication between a browser and a web server.
- Analyze HTTP requests and responses.
- Identify potential web application vulnerabilities.
- Test how applications handle user input, sessions, and authentication.
- Investigate application behavior during authorized security assessments.

## 🧠 Key Concepts

- **Proxy:** Intercepts and displays traffic between the browser and the web server.
- **HTTP request:** A message sent by a client to a server.
- **HTTP response:** The server's reply to a request.
- **Repeater:** Allows requests to be modified and resent manually.
- **Intruder:** Automates customized request attacks and input testing.
- **Scanner:** In supported editions, automatically checks for certain vulnerabilities.
- **Target scope:** Defines the hosts and URLs included in an assessment.
- **Parameter:** A value supplied to an application, often through a URL, form, or request body.
- **Cookie:** Data used by a browser to maintain state, including session information.
- **HTTPS interception:** Requires Burp's certificate to be trusted by the test browser when inspecting encrypted traffic.

## 💻 Commands / Operations

Burp Suite is primarily a graphical application, so most operations are performed through its interface rather than terminal commands.

**Configure the browser**

Configure the browser to send web traffic through Burp's proxy listener. A common local configuration uses `127.0.0.1:8080`, provided Burp is listening on that address and port.

**Intercept a request**

Open the Proxy section and enable interception. Generate a request from the configured browser and inspect it before forwarding it.

**Forward a request**

Use the Forward action to allow an intercepted request or response to continue through the proxy.

**Send a request to Repeater**

Send a captured request to Repeater to modify its parameters, headers, or body and resend it manually.

**Review HTTP history**

Use the HTTP history to examine previously captured requests and responses.

**Define the target scope**

Configure the authorized hosts and URLs in the target scope to focus testing on the intended application.

## 📋 Practical Examples

**Example 1 — Inspect a login request**

Submit a login form in the configured browser and inspect the intercepted HTTP request.

Identify the request method, URL, headers, cookies, and submitted parameters. Avoid recording real passwords or other sensitive values in notes.

**Example 2 — Investigate a parameter**

Send a request to Repeater and change a harmless test parameter in an authorized lab.

Compare the responses to understand how the application processes the input and whether server-side validation is applied.

**Example 3 — Inspect session handling**

Review the cookies and session-related headers returned by the application.

Check whether session identifiers change appropriately during authentication and whether sensitive pages require an authenticated session.

## 🔎 Investigation

When testing a web application, examine:

- Request methods, URLs, headers, and parameters.
- HTTP response status codes and response bodies.
- Authentication and session management.
- Input validation and output encoding.
- Access controls and authorization checks.
- Unexpected differences between requests and responses.
- Whether sensitive information is exposed.

**Useful investigation question:** Does the server correctly validate the request and enforce authentication and authorization, even when the client modifies the input?

## ⚠️ Important

- Burp Suite is a testing platform; findings must be validated before being reported as vulnerabilities.
- HTTPS interception requires appropriate browser and certificate configuration.
- Restrict testing to explicitly authorized applications and defined scope.
- Automated scanning and Intruder attacks can generate substantial traffic or affect application availability.
- Never test destructive payloads against production systems without explicit authorization and appropriate safeguards.
- Do not include real credentials, session tokens, or personal data in public reports or repositories.
- Burp Suite Community Edition and Professional Edition have different capabilities; some automated scanning features require a paid edition.

## 📚 References

- Official website: https://portswigger.net/burp
- Official documentation: https://portswigger.net/burp/documentation
- Web Security Academy: https://portswigger.net/web-security

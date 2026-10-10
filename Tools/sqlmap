# 🛡️ sqlmap

## 📘 Overview

sqlmap is an open-source command-line tool used to detect and assess SQL injection vulnerabilities in web applications that interact with databases.

It automates parts of the testing process and can help identify database technologies and potential injection points.

## 🎯 Purpose

- Detect potential SQL injection vulnerabilities.
- Assess how web applications handle user-controlled input.
- Identify database management systems in authorized assessments.
- Validate security weaknesses in controlled lab environments.
- Support the investigation and remediation of SQL injection risks.

## 🧠 Key Concepts

- **SQL (Structured Query Language):** A language used to query and manage relational databases.
- **SQL injection (SQLi):** A vulnerability in which untrusted input changes the intended meaning of a database query.
- **Injection point:** An input location that may influence a database query.
- **Parameter:** A value submitted through a URL, form, cookie, or HTTP request.
- **DBMS:** Database Management System, such as MySQL, PostgreSQL, Microsoft SQL Server, or Oracle Database.
- **Boolean-based blind SQLi:** Infers information from differences between true and false query conditions.
- **Time-based blind SQLi:** Infers information from differences in response timing.
- **Error-based SQLi:** Uses database error messages to identify or investigate an injection.
- **Prepared statement:** A database query mechanism that separates SQL instructions from supplied parameter values.
- **False positive:** A test result that appears to indicate a vulnerability but requires further verification.

## 💻 Commands / Operations

sqlmap is a command-line tool. Its options depend on the version installed and the testing scenario.

**Display help**

`sqlmap -h`

Displays the main command-line options.

**Display extended help**

`sqlmap -hh`

Displays additional options and configuration details.

**Check the installed version**

`sqlmap --version`

Displays the installed version.

**Test a lab URL**

`sqlmap -u "http://TARGET/item.php?id=1" --batch`

Tests the specified URL for potential SQL injection using the available default checks and answers routine prompts automatically. Replace the URL with an authorized lab target.

**Inspect an HTTP request from a lab**

`sqlmap -r request.txt --batch`

Loads an HTTP request saved in a file and tests it. This is useful when a request contains parameters, cookies, or headers not represented in a simple URL.

## 📋 Practical Examples

**Example 1 — Investigate a URL parameter**

A lab application uses a URL such as `http://TARGET/item.php?id=1`.

The tester investigates whether the `id` parameter is handled safely by the application and whether it can influence the database query unexpectedly.

**Example 2 — Investigate an authenticated request**

A lab application requires a session cookie to access a page.

The tester saves an authorized test request to a file and uses the request-based workflow to assess the relevant input.

**Example 3 — Recommend remediation**

A test confirms that user input can alter the structure of a SQL query.

The recommended fix is to use parameterized queries or prepared statements, apply least-privilege database permissions, and avoid exposing detailed database errors to users.

## 🔎 Investigation

When reviewing a potential SQL injection finding, examine:

- The input parameter associated with the result.
- Whether the behavior is reproducible.
- The database technology, if reliably identified.
- Whether the application returns informative database errors.
- Whether response content or timing changes consistently.
- The sensitivity of data accessible through the affected query.
- The server-side query construction and input-handling practices.

**Useful investigation question:** Can untrusted input alter the intended SQL query, and what database operations could consequently be affected?

## ⚠️ Important

- sqlmap automates testing but does not guarantee that every reported result is a real vulnerability.
- Some checks can generate many requests, affect application performance, or trigger security monitoring.
- Automated testing may be disruptive, especially when data-changing operations are involved.
- Do not use data extraction, modification, deletion, or operating-system interaction features against systems without explicit authorization.
- Use dedicated training environments and test databases for hands-on practice.
- The primary remediation is to use parameterized queries or prepared statements rather than concatenating untrusted input into SQL statements.
- Apply least-privilege permissions to database accounts and handle errors securely.

## 📚 References

- Official GitHub repository: https://github.com/sqlmapproject/sqlmap
- Official wiki: https://github.com/sqlmapproject/sqlmap/wiki
- OWASP SQL Injection Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

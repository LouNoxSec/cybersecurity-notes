# 🛡️ Hydra

## 📘 Overview

Hydra, also known as THC Hydra, is an open-source password auditing tool designed to test authentication services by attempting logins using supplied usernames and password candidates.

It supports multiple network protocols and is commonly used in authorized penetration tests to assess the strength of authentication mechanisms.

## 🎯 Purpose

- Audit the security of network authentication services.
- Identify weak or easily guessed passwords.
- Assess password policies and account protections.
- Understand the risks of online password-guessing attacks.
- Test authentication controls in authorized lab environments.

## 🧠 Key Concepts

- **Authentication:** The process of verifying a user's identity.
- **Username:** An identifier associated with an account.
- **Password list:** A collection of candidate passwords used during an audit.
- **Dictionary attack:** Attempts authentication using candidate passwords from a wordlist.
- **Brute-force attack:** Systematically tests possible password combinations.
- **Online attack:** Tests credentials directly against a live authentication service.
- **Account lockout:** A control that temporarily blocks authentication after repeated failures.
- **Rate limiting:** Restricts how frequently authentication attempts can be made.
- **MFA (Multi-Factor Authentication):** Requires additional proof of identity beyond a password.
- **Authentication protocol:** The mechanism used to authenticate a user, such as SSH or FTP.

## 💻 Commands / Operations

Hydra is a command-line tool. Its syntax and supported options depend on the installed version and the target service.

**Display help**

`hydra -h`

Displays the available options and supported services.

**Display the installed version**

`hydra -U <service>`

Displays usage information for a specified supported service module.

**Understand the general syntax**

`hydra [options] <target> <service>`

The options specify authorized test parameters, while the target and service identify the system and authentication protocol being assessed.

**Review service-specific options**

`hydra -U ssh`

Displays usage information for Hydra's SSH module, where supported by the installed version.

## 📋 Practical Examples

**Example 1 — Assess password strength**

During an authorized assessment, a security tester reviews whether a service is protected against common password-guessing attempts.

The tester uses an approved test account and a controlled set of candidate passwords.

**Example 2 — Evaluate account protections**

A tester checks whether repeated failed logins trigger rate limiting, account lockout, monitoring alerts, or other defensive controls.

**Example 3 — Document authentication weaknesses**

If weak credentials are identified in an authorized lab, the tester records the affected service, the observed behavior, the risk, and recommended remediation.

## 🔎 Investigation

When assessing an authentication service, examine:

- Whether weak or default credentials are accepted.
- Whether repeated login failures are monitored.
- Whether rate limiting and account lockout are configured appropriately.
- Whether multi-factor authentication is enabled where appropriate.
- Whether authentication attempts generate useful security logs.
- Whether the service uses secure transport.
- Whether exposed authentication services are necessary.

**Useful investigation question:** How effectively does the service resist repeated password-guessing attempts, and can its defensive controls detect or limit them?

## ⚠️ Important

- Hydra tests authentication against a live service; it does not crack a password hash offline.
- Online password guessing can trigger account lockouts, generate alerts, or disrupt services.
- Results can be affected by network errors, service behavior, authentication configuration, and account protections.
- A successful login does not necessarily prove that the password policy is broadly insecure; findings require context.
- Use only accounts, systems, and services for which you have explicit authorization.
- Prefer dedicated lab accounts and low-impact testing parameters.
- Never use Hydra to attempt unauthorized access to real accounts or third-party systems.

## 📚 References

- THC Hydra repository: https://github.com/vanhauser-thc/thc-hydra
- Kali Linux tool documentation: https://www.kali.org/tools/hydra/

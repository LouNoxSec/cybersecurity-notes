# 🛡️ John the Ripper

## 📘 Overview

John the Ripper is an open-source password security auditing tool used to test password strength by attempting to recover passwords from password hashes.

It supports multiple hash formats and password-cracking techniques.

## 🎯 Purpose

- Audit password strength.
- Identify weak or easily guessed passwords.
- Understand password hashing and password security.
- Test password policies in authorized security assessments.
- Demonstrate the risks associated with weak passwords.

## 🧠 Key Concepts

- **Plaintext password:** The original, readable password.
- **Hash:** The output of a one-way function applied to data, such as a password.
- **Password cracking:** Attempting to recover a password by testing candidate values.
- **Wordlist:** A file containing candidate passwords.
- **Dictionary attack:** Tests candidate passwords from a wordlist.
- **Brute-force attack:** Systematically tests possible character combinations.
- **Password hash format:** The algorithm or format used to represent a password hash.
- **Salt:** A random value added during password hashing to make identical passwords produce different hashes.
- **Hash verification:** Checks whether a candidate password produces a result matching the stored hash.

## 💻 Commands / Operations

**Display version and build information**

`john --list=build-info`

Displays information about the installed build.

**Audit a hash file**

`john hashes.txt`

Attempts to recover passwords from hashes stored in `hashes.txt` using John the Ripper's default cracking mode.

**Use a wordlist**

`john --wordlist=wordlist.txt hashes.txt`

Tests candidate passwords from the specified wordlist.

**Display recovered passwords**

`john --show hashes.txt`

Displays passwords recovered from the hash file, where supported.

**List supported hash formats**

`john --list=formats`

Displays the formats supported by the installed build.

**Specify a hash format**

`john --format=<FORMAT> hashes.txt`

Uses the specified format when processing the hashes. The format must match the actual hash type and be supported by the installed version.

## 📋 Practical Examples

**Example 1 — Audit password strength**

An authorized auditor receives a file containing password hashes and runs John the Ripper against it.

If weak passwords are recovered quickly, this indicates that the organization's password practices may need improvement.

**Example 2 — Test a wordlist**

The auditor uses a wordlist containing common passwords and variations.

John tests these candidates against the supplied hashes. Passwords that match can be identified as weak or predictable.

**Example 3 — Understand password storage**

Two users may have the same password but different stored hashes if the system uses unique salts.

This is one reason password storage design matters when assessing resistance to offline cracking.

## 🔎 Investigation

When conducting an authorized password audit, examine:

- Whether passwords are weak or predictable.
- Whether common passwords are being reused.
- Which hashing algorithm and parameters are used.
- Whether unique salts are implemented correctly.
- How quickly candidate passwords can be tested.
- Whether password policies and multi-factor authentication reduce the overall risk.

**Useful investigation question:** Could an attacker who obtains the stored password hashes recover weak passwords within a realistic amount of time?

## ⚠️ Important

- A hash is not the original password; cracking attempts to find a matching candidate.
- Successful recovery depends on password strength, hash format, algorithm, configuration, and available computing resources.
- Strong, unique passwords and appropriately configured password hashing make recovery more difficult.
- Password hashing algorithms designed for password storage, such as Argon2id, scrypt, bcrypt, and appropriately configured PBKDF2, help resist offline cracking.
- A failed cracking attempt does not prove that a password is strong.
- Only test password hashes you are explicitly authorized to audit.
- Password hashes and recovered passwords must be handled as sensitive information.

## 📚 References

- Official website: https://www.openwall.com/john/
- Official documentation: https://www.openwall.com/john/doc/

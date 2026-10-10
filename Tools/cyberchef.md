# 🛡️ CyberChef

## 📘 Overview

**CyberChef** is a free, web-based tool developed by GCHQ that helps analysts transform, decode, encode, parse, and analyze data.

It provides a visual interface where users combine operations into a sequence called a **recipe**. It is useful for cybersecurity investigations, digital forensics, malware analysis, and general data processing.

CyberChef is often described as the *Cyber Swiss Army Knife* because it supports a wide variety of operations without requiring users to write code.

## 🎯 Purpose

- Decode encoded data, such as Base64 or URL encoding.
- Convert data between different formats.
- Extract readable strings from suspicious data.
- Parse and transform logs or other text.
- Calculate file hashes for identification and integrity checks.
- Inspect and manipulate data during malware or incident investigations.
- Quickly test transformations that would otherwise require scripts or command-line tools.

## 🧠 Key Concepts

- **Recipe:** A sequence of operations applied to input data.
- **Operation:** An individual transformation, such as Base64 decoding, hashing, or string extraction.
- **Input:** The original text, data, or file being analyzed.
- **Output:** The result produced by the recipe.
- **Encoding:** A way of representing data in a different format. Encoding is not necessarily encryption.
- **Decoding:** Reversing an encoding to recover the represented data.
- **Encryption:** Protecting information using a cryptographic method and a key.
- **Hashing:** Producing a fixed-length digest used for tasks such as integrity verification and file identification. A cryptographic hash is not intended to be reversed.
- **Regular expression (regex):** A pattern used to search for or extract text matching specified rules.
- **Magic bytes / file signature:** Bytes that can help identify a file's format.
- **IOC (Indicator of Compromise):** An indicator associated with potentially malicious activity, such as a suspicious domain, IP address, or file hash.

## 💻 Commands / Operations

CyberChef is primarily a graphical tool rather than a command-line utility. Users select operations, configure their options, and arrange them into a recipe.

Common operations include:

- **From Base64:** Decodes Base64-encoded data.
- **To Base64:** Encodes data into Base64.
- **URL Decode:** Decodes URL-encoded text.
- **URL Encode:** Encodes characters for use in URLs.
- **Hex to Bytes / From Hex:** Converts hexadecimal representations into byte data.
- **To Hex:** Represents data as hexadecimal.
- **Extract strings:** Extracts readable text from binary data.
- **Regular expression:** Searches for or extracts patterns from text.
- **SHA-256:** Calculates a SHA-256 hash of the input.
- **Entropy:** Estimates the randomness of data, which can help identify data that may be compressed, encrypted, or otherwise high-entropy.
- **Magic:** Examines file signatures to help identify a likely file type.
- **Gzip / Gunzip:** Compresses or decompresses data using the Gzip format.

Operation names and available options can vary by version.

## 📋 Practical Examples

**Example 1 — Decode Base64 data**

An analyst finds the following string in a suspicious log:

`SGVsbG8gV29ybGQ=`

They paste it into CyberChef and apply **From Base64**.

The decoded output is `Hello World`.

This demonstrates how encoded content can conceal readable text without encrypting it.

**Example 2 — Investigate a suspicious URL**

An analyst encounters a URL containing encoded characters.

They apply **URL Decode** to reveal the underlying text and inspect its parameters for suspicious values or unexpected destinations.

**Example 3 — Calculate a file hash**

An analyst loads a file and applies **SHA-256**.

The resulting hash can be compared with a known hash from a trusted source or threat intelligence database. A matching hash can help identify a file, although the context and reliability of the reference must still be considered.

**Example 4 — Inspect suspicious text or binary data**

An analyst receives a file or a block of hexadecimal data.

They use **Extract strings**, **From Hex**, or **Magic** to identify readable content, interpret bytes, and gather clues about the data's structure.

**Example 5 — Build a multi-step recipe**

An analyst receives Base64-encoded, URL-encoded text.

They can chain decoding operations in the appropriate order, inspecting the output after each step to understand how the original data was transformed.

## 🔎 Investigation

When analyzing suspicious data with CyberChef:

- **Preserve the original:** Keep an untouched copy of the source data or file.
- **Identify the format:** Determine whether the data appears to be Base64, hexadecimal, URL-encoded, compressed, or another format.
- **Choose the right operation:** Encoding, compression, encryption, and hashing are different processes.
- **Build the recipe carefully:** Apply transformations in a logical order and inspect intermediate outputs.
- **Look for indicators:** Search the results for IP addresses, domains, URLs, file paths, commands, or other suspicious strings.
- **Verify findings:** Compare extracted indicators with trusted sources and corroborate them using other analysis tools.
- **Document the process:** Record the operations used and the relevant results so the analysis can be reproduced.

## ⚠️ Important

- **Encoding is not encryption.** Base64 and hexadecimal representations do not provide confidentiality.
- **Hashing is not decoding.** A hash cannot normally be reversed to recover the original file or message.
- **High entropy does not prove maliciousness.** Compression and legitimate encrypted data can also have high entropy.
- **Decoded content may still be dangerous.** Treat extracted commands, scripts, URLs, and files as untrusted.
- **Do not execute suspicious content simply because CyberChef has decoded it.**
- **Be careful with sensitive data.** Prefer a trusted local instance when handling confidential logs, credentials, malware samples, or proprietary information.
- **CyberChef complements other tools.** It helps transform and inspect data, but it does not replace a full malware-analysis environment, network analyzer, or SIEM.

## 📚 References

- CyberChef official website: https://gchq.github.io/CyberChef/
- CyberChef GitHub repository: https://github.com/gchq/CyberChef
- GCHQ GitHub organization: https://github.com/gchq

# 🛡️ capa

## 📘 Overview

**capa** is an open-source tool developed by Mandiant FLARE that identifies capabilities in executable files, especially Windows PE files, by analyzing their features and matching them against a set of detection rules.

It helps malware analysts understand what a program may be capable of doing without having to manually reverse-engineer every function.

For example, capa may identify capabilities related to network communication, process injection, persistence, file manipulation, or cryptographic operations.

**Important:** capa identifies capabilities suggested by the file's code and behavior patterns. It does not automatically prove that a capability was executed or that the file is malicious.

## 🎯 Purpose

- Quickly triage suspicious executable files.
- Identify potentially malicious capabilities.
- Support malware analysis and reverse engineering.
- Help analysts understand unfamiliar binaries.
- Provide leads for deeper investigation with tools such as Ghidra or a debugger.
- Generate structured reports describing detected capabilities.

## 🧠 Key Concepts

- **Binary:** A file containing executable code or other data in machine-readable form.
- **PE (Portable Executable):** The executable file format commonly used by Windows programs, including `.exe` and `.dll` files.
- **Static analysis:** Examining a file without running it.
- **Dynamic analysis:** Observing a program while it executes in a controlled environment.
- **Capability:** An action or behavior that a program may be able to perform, such as creating a service or communicating over a network.
- **Rule:** A detection definition used by capa to identify patterns associated with a capability.
- **Rule match:** Evidence that the analyzed file matches the patterns described by a rule.
- **Triage:** An initial assessment used to prioritize files for further investigation.
- **False positive:** A detected capability that does not accurately represent relevant behavior in the context being investigated.
- **False negative:** A capability that is present but not detected by the available rules or analysis.
- **Reverse engineering:** Examining a program to understand its internal structure and functionality.

## 💻 Commands / Operations

capa is a command-line tool. Exact options may vary by release and installation method.

**Display help**

`capa -h`

Shows available command-line options.

**Analyze a file**

`capa suspicious.exe`

Analyzes the executable and reports capabilities identified by capa's rules.

**Analyze a file with verbose output**

`capa -v suspicious.exe`

Requests more detailed output to help understand the analysis results.

**Generate a JSON report**

`capa -j suspicious.exe`

Produces JSON-formatted results, useful for automation or further processing when supported by the installed version.

**Specify a rule directory**

`capa -r /path/to/rules suspicious.exe`

Uses the specified directory for capa rules. The path must point to a compatible rules directory.

**Analyze a file using a format-specific backend**

capa supports different analysis backends and file formats depending on the release and configuration. Consult the installed version's help and official documentation before selecting advanced options.

## 📋 Practical Examples

**Example 1 — Initial malware triage**

An analyst receives an unknown Windows executable.

They run capa and find capabilities associated with network communication and process injection.

These results help prioritize the file for further investigation, but they do not prove that the program performed either action during execution.

**Example 2 — Investigating persistence**

capa identifies a capability associated with modifying Windows Registry settings.

The analyst investigates whether the program may use Registry changes to maintain persistence and validates the finding using additional static or dynamic analysis.

**Example 3 — Comparing suspicious files**

Two executables are analyzed with the same capa rules.

Their reports reveal overlapping capabilities, which can help an analyst identify similarities. Similar capabilities alone do not establish that the files belong to the same malware family.

**Example 4 — Supporting reverse engineering**

capa reports a capability related to process injection.

The analyst uses a reverse-engineering tool, such as Ghidra, to examine the relevant code and determine how the capability may be implemented.

## 🔎 Investigation

When using capa during malware analysis:

- **Identify the file:** Record its name, type, size, and cryptographic hash.
- **Check compatibility:** Confirm that the file format and analysis backend are supported.
- **Run capa:** Analyze the file using an appropriate version of the tool and rules.
- **Review the results:** Examine detected capabilities and the rules that matched.
- **Prioritize findings:** Focus on capabilities relevant to the investigation, such as persistence, process injection, credential access, or network communication.
- **Validate the evidence:** Use static analysis, dynamic analysis, or reverse engineering to confirm what the program actually does.
- **Document the findings:** Preserve the report, tool version, rule version, and file hash to support reproducibility.

## ⚠️ Important

- capa is primarily a **capability-identification and triage tool**, not a complete malware-analysis solution.
- A detected capability does not necessarily mean that the behavior occurred during execution.
- The absence of a detected capability does not prove that the program is harmless.
- Results depend on file compatibility, analysis methods, rule coverage, and the quality of the available evidence.
- Static analysis can miss behavior that is obfuscated, dynamically resolved, or otherwise difficult to detect.
- Do not run unknown executables on your normal workstation. Use an appropriately isolated malware-analysis environment for dynamic analysis.
- Keep capa and its rules updated when possible, and consult the documentation for the version you are using.

## 📚 References

- capa official GitHub repository: https://github.com/mandiant/capa
- capa documentation: https://mandiant.github.io/capa/
- FLARE-VM: https://github.com/mandiant/flare-vm
- Ghidra reverse-engineering framework: https://github.com/NationalSecurityAgency/ghidra
